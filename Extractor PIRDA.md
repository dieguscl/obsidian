This PIRDA extractor is designed to extract data from a PI database tStore for more efficient and faster reading of the data when requested on-demand by VisualKPI, multiplying the speed compared to not having tStore as an intermediary.

It works by installing and configuring a service on a Windows Server machine that will poll the data and put it constantly into tStore.

# Installation

Installing the service is simple, run the executable file of the extractor as follows
```cmd
./extractor-pirda.exe install
```

If it is desired to personalize the installation in any way, run the `--help` command to see the options available
```
./extractor-pirda.exe --help
```