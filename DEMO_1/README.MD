# .NET Core Setup and HelloWorld #

- Download .NET Core SDK from [Official Site](https://www.microsoft.com/net/core)
- Or Using Docker Directly. [Official Site - Docker](https://www.microsoft.com/net/core#dockercmd)

## CMD ##

## ASP.NET Core 1.0.0 CLI ##

Display SDK version:

    dotnet --version

Display runtime version:

    dotnet

List Templates:

    dotnet new --help

### Hello World! ###

    mkdir app
    cd app

    dotnet new console
    dotnet restore
    dotnet run

### Hi, GCP Guru! ###

Go to app > Program.cs and modify:

```csharp
using System;

namespace app
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hi, GCP Guru!");
        }
    }
}

```

Execute :

    dotnet run