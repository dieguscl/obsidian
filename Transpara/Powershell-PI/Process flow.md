
## On each data source server

- Set up PI extractor to send data to tStore. It will be done using [this file]([Corning - Google Drive](https://drive.google.com/drive/folders/1xhzI7CLvjt0WEYpWBFp4ZKYL193s3rt7) (.zip) extracted roughly on this path `C:\Program Files\Transpara\extractors\Aveva-PIRDA` 
- Edit `extractor-pirda.exe` config file to point to the right tStore, and have the adequate metric name
- List all matching metrics according to the tag filter (maybe save to a file for later inspection)
- Start a service to begin extracting data
- Make sure it is correctly extracting (?)

## On the server with the server manager

- Add a tStore interface for each tStore instance being used