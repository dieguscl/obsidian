```powershell
# Read the CSV file
$dataSources = Import-Csv -Path $csvPath

# Set the base path for Aveva-PIRDA correctly
$baseAvevaPIRDAPath = Resolve-Path ".."

# Navigate to Aveva-PIRDA directory
Set-Location -Path $baseAvevaPIRDAPath

# Define the source directory path relative to the script's location
$sourceDirectory = ".\"

# Define the directory to exclude from copying
$excludeDirectory = "pi_bulk"

# Loop through each dataSource to configure and copy necessary files
foreach ($dataSource in $dataSources) {
    $extractorName = $dataSource.extractor_name
    $destination = Join-Path -Path $baseDestination -ChildPath $extractorName

    # Check if the service is installed and running
    $service = Get-Service -Name $extractorName -ErrorAction SilentlyContinue

    # Just copy files when service is not installed already
    # TODO: maybe this approach needs improvement
    if ($service -eq $null) {
        # Ensure the destination directory exists
        if (-not (Test-Path -Path $destination)) {
            New-Item -Path $destination -ItemType Directory | Out-Null
        }
        # Copy all items from the source directory to the destination, excluding the specified directory
        Get-ChildItem -Path $sourceDirectory -Recurse | Where-Object {
            # Exclude the directory itself and its contents
            $_.FullName -notlike "*\$excludeDirectory\*"
        } | ForEach-Object {
            # Construct the relative path to maintain the structure without the base directory name
            $relativePath = $_.FullName.Substring((Resolve-Path $sourceDirectory).Path.Length)
            $targetPath = Join-Path -Path $destination -ChildPath $relativePath
            # If item is a file, copy it to the destination
            if (-not $_.PSIsContainer) {
                $targetDir = Split-Path -Path $targetPath -Parent
                # Ensure the target directory exists
                if (-not (Test-Path -Path $targetDir)) {
                    New-Item -Path $targetDir -ItemType Directory -Force | Out-Null
                }
                Copy-Item -Path $_.FullName -Destination $targetPath -Force
            }

        }

    }

    # Path to the config file and the extractor executable within the extracted folder
    $configFilePath = Join-Path -Path $destination -ChildPath "extractor-pirda.exe.config"
    $executableFilePath = Join-Path -Path $destination -ChildPath "extractor-pirda.exe"
    # Load the XML configuration file
    [xml]$configXml = Get-Content $configFilePath

    # Iterate through each 'add' element within 'appSettings'
    foreach ($node in $configXml.configuration.appSettings.add) {
        switch ($node.key) {
            "pi_server" { $node.SetAttribute('value', $dataSource.pi_server) }
            "af_server_name" { $node.SetAttribute('value', $dataSource.af_server_name) }
            "af_database_name" { $node.SetAttribute('value', $dataSource.af_database_name) }
            "log_only" { $node.SetAttribute('value', $dataSource.log_only) }
            "tstore_endpoint" { $node.SetAttribute('value', $dataSource.tstore_endpoint) }
            "tstore_username" { $node.SetAttribute('value', $dataSource.tstore_username) }
            "tstore_password" { $node.SetAttribute('value', $dataSource.tstore_password) }
            "metric_name" { $node.SetAttribute('value', $dataSource.metric_name) }
            "tag_filter" { $node.SetAttribute('value', $dataSource.tag_filter) }
            "tag_filter_enabled" { $node.SetAttribute('value', '1') }
        }
    }

    # Save the modified configuration file
    $configXml.Save($configFilePath)

    # Check if service is installed
    $serviceInstalled = Get-Service -Name $extractorName -ErrorAction SilentlyContinue

    if ($serviceInstalled -ne $null) {
        # Service is already installed, stop the service to apply changes
        Write-Host "Service '$extractorName' is already installed. Stopping service to apply changes."
        Start-Process -FilePath $executableFilePath -ArgumentList "stop -servicename:$extractorName" -Wait
        Start-Process -FilePath $executableFilePath -ArgumentList "start -servicename:$extractorName" -Wait
        Write-Host "Service '$extractorName' has been restarted with the new configuration."
    } else {
        # Service is not installed, proceed with installation
        $displayName = "Transpara PIRDA Data Extractor ($extractorName)"
        Start-Process -FilePath $executableFilePath -ArgumentList "install -servicename $extractorName -displayname `"$displayName`" --autostart" -Wait
        # Start the service after installation
        Start-Process -FilePath $executableFilePath -ArgumentList "start -servicename:$extractorName" -Wait
        Write-Host "Service '$extractorName' has been installed and started."
    }
}
```