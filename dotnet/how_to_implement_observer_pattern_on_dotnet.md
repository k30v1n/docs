# How to implement observer pattern on dotnet

Following this link https://docs.microsoft.com/en-us/dotnet/standard/events/observer-design-pattern

The observer design pattern enables a subscriber to register with and receive notifications from a provider. It is suitable for any scenario that requires push-based notification. The pattern defines a provider (also known as a subject or an observable) and zero, one, or more observers. Observers register with the provider, and whenever a predefined condition, event, or state change occurs, the provider automatically notifies all observers by calling one of their methods. In this method call, the provider can also provide current state information to observers. In .NET, the observer design pattern is applied by implementing the generic `System.IObservable<T>` and `System.IObserver<T>` interfaces. The generic type parameter represents the type that provides notification information.
