- Download [.zip file](https://drive.google.com/drive/folders/1xhzI7CLvjt0WEYpWBFp4ZKYL193s3rt7) with all the contents needed for extractor (for the first version, download beforehand and pass its location as an argument)
- Unzip it and put it here `C:\Program Files\Transpara\extractors\Aveva-PIRDA` 
- Edit `extractor-pirda.exe` config file to point to the right tStore, and have the adequate metric name. The fields that are going to be edited are the following:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <add key="pi_server" value="WIN-HD6ET0BPF08" />
    <add key="pi_username" value="" />
    <add key="pi_password" value="" />
    <add key="af_server_name" value="WIN-HD6ET0BPF08" />
    ...
```

| key name | value |
| ---- | ---- |
| pi_server | address for the PI server |
| af_server_name | name of the AF server |
| af_database_name |  |
| log_only | `0` if ready to send data |
| tstore_endpoint | reachable address for tstore `example: http://172.30.145.98:10001` |
| tstore_username | tstoredev@transpara.com |
| tstore_password | tStoreDev!22 |
- start the service with the `extractor-pirda` file