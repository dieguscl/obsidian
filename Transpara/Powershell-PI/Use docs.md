## Prerequisites
Before proceeding, ensure you meet the following requirements:
- **Configured PI Interface**: Your environment should already have a PI interface set up and operational.
- **Administrative Access**: You need the capability to open a PowerShell session with administrator privileges.
- **Execution Policy**: Your PowerShell execution policy must be configured to allow script execution, ensuring you can run scripts as needed.
## Installation process
1. Download the `.zip` file and extract it anywhere
2. Go to the `AutomationScripts` folder and edit the `data_sources.csv` file according to the data sources that are desired to be extracted from. Here are the most used columns to modify the settings of the data extractor
### Data Extractor Configuration
Configure your data extractor by editing the `data_sources.csv` file with these settings:

| Setting | Description |
|---------|-------------|
| `extractor_name` | Identifier for the extractor's folder. |
| `metric_name` | Label for metrics in the tStore table. |
| `tstore_endpoint` | URL/path to the tStore service. |
| `pi_server` | Hostname/IP of the PI Server. |
| `af_server_name` | Name of the AF server. |
| `af_database_name` | Name of the AF database. |
| `tstore_username` | Username for tStore access.  tstoredev@transpara.com |
| `tstore_password` | Password for tStore access. tStoreDev!22 |
| `tag_filter` | Regex or template to filter source tags. |
| `tag_filter_enabled` | Enable (`1`) or disable (`0`) tag filter. |
> NOTE: If it is desired comment out row, put a `#` at the start of it

If it is wanted to modify any other configurations from the `extractor.exe.config`, add a column to the `data_source.csv` based on the configuration that is going to be modified. Example:

To modify the `af_username` setting in the `extractor.exe.config` file, which appears as follows:
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    ...
    <add key="af_username" value="" />
    ...
```
You should add a new column to your `data_sources.csv` file, naming it `af_username`. In this column, specify the desired username value for each data source row. This method enables dynamic configuration of the extractor based on the CSV inputs, ensuring that any changes or additions to settings can be handled efficiently without altering the script.

3. After modifying `data_source.csv`, the next step is to run the `pi_bulk_install.ps1`. This should create a folder for each configured data source under `C:\Program Files\Transpara\extractors\<extractor_name>` and start a service for each extractor as well
4. Make sure data is correctly writing to tStore. A metric for each `metric_name`  on `data_sources.csv` should be created

## Uninstall Process

1. Make sure to close any programs that could be using the files under the `C:\Program Files\Transpara\extractors` 
2. Ensure that the `data_sources.csv` file was the same one used for the installation process, run the
3. Then run the `pi_bulk_uninstall.ps1` file under the `AutomationScripts` folder that was used for installing in the first place.

