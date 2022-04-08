# CLI - dotnet-counters


https://docs.microsoft.com/en-ca/dotnet/core/diagnostics/dotnet-counters?WT.mc_id=dotnet-00000-cephilli

```
dotnet tool install --global dotnet-counters
```

`dotnet-counters` is a performance monitoring tool for ad-hoc health monitoring and first-level performance investigation. It can observe performance counter values that are published via the EventCounter API. For example, you can quickly monitor things like the CPU usage or the rate of exceptions being thrown in your .NET Core application to see if there's anything suspicious before diving into more serious performance investigation using PerfView or dotnet-trace.

## Usage
### Docker
```shell
docker container exec -it 9f6a4a53431b "/bin/bash"

curl -L https://aka.ms/dotnet-counters/linux-x64 -o 

chmod +x ./dotnet-counters

# if necessary - to discover the PID
# apt-get update && apt-get install procps
# ps aux

./dotnet-counters monitor --process-id 1

```

### Local only

dotnet-counters monitor --process-id 92933