# Dependency injection with dotnet

Dependency injection exists to facilitate the development process and also the testing process.

In dotnet it is available the following DI scopes


- `Transient` - Transient lifetime services are created each time they're requested from the service container.
    - In apps that process requests, transient services are disposed at the end of the request.

- `Scoped` - For web applications, a scoped lifetime indicates that services are created once per client request (connection).
    - In apps that process requests, scoped services are disposed at the end of the request.

    - When using Entity Framework Core, the AddDbContext extension method registers DbContext types with a scoped lifetime by default.

    - Do not resolve a scoped service from a singleton and be careful not to do so indirectly, for example, through a transient service. It may cause the service to have incorrect state when processing subsequent requests. It's fine to:

        - Resolve a singleton service from a scoped or transient service.
        - Resolve a scoped service from another scoped or transient service.
    - By default, in the development environment, resolving a service from another service with a longer lifetime throws an exception.



- `Singleton` - one instance per application lifetime


References

- https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection
- https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection#service-lifetimes