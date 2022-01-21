# Thread pool exhaustion in dotnet

todo: introduction to thread pool exhaustion link

- [dotNet Video - Diagnosing thread pool exhaustion issues in .NET core apps](https://www.youtube.com/watch?v=isK8Cel3HP0)

On this video, Mike Rousos show some dotnet CLI tools that are good to investigate possible thread pools exhaustion problems on net core apps.

Mainly he used `dotnet-counters` tool in order to get details about the dotnet projet.

Then after that he analised the results where he noticed that the Thread Pool was increasing in a way that is not normal, and sequentially.

*Ideally the Thread pool should be steady, which shows that the application is being able to re use the same thread pools and serving all requests/process properly"



Todo: more details on the tool `dotnet-counters`
Todo: more details about `thread pools`