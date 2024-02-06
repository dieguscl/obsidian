A CSV Is going to be used to describe all the PI servers that are going to be extracted from
- [[CSV Contents]]
This is a general look of the process that the powershell script is going to be doing
- [[Process flow]]
Now a more specific way to look at it, to start developing the script 
- [[Process flow (specific)]]

I got the following to work, I just put in a CSV the configs that I had previously put in, with my single local PI data source:
```csv
pi_server,af_server_name,af_database_name,log_only,tstore_endpoint,tstore_username,tstore_password,metric_name,backfill_start,backfill_end
"WIN-HD6ET0BPF08","WIN-HD6ET0BPF08","Test",0,"http://172.30.145.98:10001","tstoredev@transpara.com","tStoreDev!22","Fish","2024-01-01","2024-02-01"
```

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
    $extractorName = "Aveva-PIRDA" # Customize this per row if needed
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
        }
    }
    
    # Save the modified configuration file
    $configXml.Save($configFilePath)
    
    # Start the extractor service by running the executable
    Start-Process -FilePath $executableFilePath
    
    # Output a confirmation message
    Write-Host "Configuration for '$extractorName' has been updated and the service started."
}

```