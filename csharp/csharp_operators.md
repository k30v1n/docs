# Csharp Operators

## Nullable checks
Access variables that can be nullable is something common on any programing language. In C# it is possible to perform a couple of checks. 

For example to tell the compiler to `trust me this is not null` we should use the [!(null-forgiving) operator](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-forgiving)
```csharp
var foo = Entity!.DoSomething();
```

But if we really dont known if something is null we can use the Nullable Values
```csharp
int? foo = null;
string bark = string.Empty;

bark = foo.ToString(); // NullPointerException

bark = foo?.ToString(); // assign null, but without throwing error
```

Other option is to use coalesce operators, such as `??=` [reference](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator). Which will assign the left variable according to the right variable in case of the left is NULL. 
```csharp
List<int> numbers = null;
int? a = null;

(numbers ??= new List<int>()).Add(5);
Console.WriteLine(string.Join(" ", numbers));  // output: 5

numbers.Add(a ??= 0);
Console.WriteLine(string.Join(" ", numbers));  // output: 5 0
Console.WriteLine(a);  // output: 0
```

Or, just the coalesce operation without assignment by using only the `??` [reference](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator)
```csharp 
private static void Display<T>(T a, T backup)
{
    Console.WriteLine(a ?? backup);
}
```