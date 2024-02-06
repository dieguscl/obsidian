```powershell
# Path to the CSV file
$csvPath = "C:\Users\Administrator\Downloads\data_sources.csv"
# Path to the downloaded .zip file (assumed to be the same for all)
$zipPath = "C:\Users\Administrator\Downloads\Aveva-PIRDA.zip"
# Base destination directory
$baseDestination = "C:\Program Files\Transpara\extractors"

# Read the CSV file
$dataSources = Import-Csv -Path $csvPath

foreach ($dataSource in $dataSources) {
    $extractorName = $dataSource.extractor_name
    $destination = Join-Path -Path $baseDestination -ChildPath $extractorName
    
    # Ensure the destination directory exists
    if (-not (Test-Path -Path $destination)) {
        New-Item -Path $destination -ItemType Directory | Out-Null
    }
    
    # Unzip the file to the destination directory
    Expand-Archive -LiteralPath $zipPath -DestinationPath $baseDestination -Force
    
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
    
    # Start the extractor service by running the executable
    Start-Process -FilePath $executableFilePath
    # To install a service
    # Start-Process -FilePath $executableFilePath -ArgumentList "/install"

	# Install the service (if not already installed) and start it 
	# Check if service is installed (simplified check, might need enhancement) 
	$serviceInstalled = Get-Service -Name $serviceName -ErrorAction SilentlyContinue 
	if (-null -eq $serviceInstalled) { 
	# Install the service 
	Start-Process -FilePath $serviceExecutablePath -ArgumentList "install --servicename:$serviceName --autostart -instance:$extractorName --localsystem start" -Wait 
	} 
	# Start the service 
	Start-Process -FilePath $serviceExecutablePath -ArgumentList "start -servicename:$serviceName" -Wait
    
    # Output a confirmation message
    Write-Host "Configuration for '$extractorName' has been updated and the service started."
}
```