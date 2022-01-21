# How to run dotnet with profile using CLI

To run a dotnet app on a specific profile first verify `launchSettings.json` file has the proper profile there specified. 

E.g.
```json
 "PROFILE_NAME": {
      "commandName": "Project",
      "launchBrowser": true,
      "launchUrl": "healthz",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      },
      "applicationUrl": "http://localhost:5000"
    }
```

Then run the following.

```
dotnet run --launch-profile "PROFILE_NAME"
```