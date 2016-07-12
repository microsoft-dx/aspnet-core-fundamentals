Getting started with .NET Core
=========================

[In the previous article](https://radu.microsoft.pub.ro/dot-net-core-introduction/), we saw what is .NET Core and what can we build with it. In this article, we will install .NET Core and start with some basic examples using the command line and Visual Studio Code.

Installing .NET Core
------------------------

Wether your OS is Windows, Linux or macOS, you can [go to this page and follow the instructions](https://www.microsoft.com/net/core) for getting .NET Core on your machine.

When the installation is complete, you should be able to open a command line interface (CMD, PowerShell for Windows, Terminal for Linux and macOS) and check if the installation was successful by executing the following command: [`dotnet`](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet).

![dotnet PowerShell](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/dotnet-powershell.JPG)
> Output for the [`dotnet`](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet) command in PowerShell. The output is similar for Linux and macOS.

At this point, you have successfully installed .NET Core and you can start building applications.

Building a .NET Core application using the command line interface
-------------------------------------------------------------------------------

In Windows PowerShell or the Linux / macOS Terminal, let's create a new directory. I will call it `dot-net-tutorial` and navigate to it and create a new console application here using the [`dotnet new`](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-new) command.

    mkdir dot-net-tutorial
    cd dot-net-tutorial
    dotnet new

This is how it should look like after executing these commands.
![enter image description here](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/dotnet-powershell-new.JPG)

Notice how we got two files after creating the project

- `Program.cs`- C# file containing the entry point in the console application - the `Main` method

```
using System;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}

```
      
This is a basic `Hello World` example in C# and you can [find more information about everything in the code in this article](https://radu.microsoft.pub.ro/csharp-fundamentals-01/).
        
    
- `project.json` - JSON file that contains all necessary dependencies and the frameworks for the application to run, including .NET frameworks and NuGet packages.
```
{
  "version": "1.0.0-*",
  "buildOptions": {
    "debugType": "portable",
    "emitEntryPoint": true
  },
  "dependencies": {},
  "frameworks": {
    "netcoreapp1.0": {
      "dependencies": {
        "Microsoft.NETCore.App": {
          "type": "platform",
          "version": "1.0.0"
        }
      },
      "imports": "dnxcore50"
    }
  }
}
```

> In a future release, the `project` file will return to a `.csproj` extension in order to maitain compatibility with all Visual Studio and Xamarin projects. 

Calling [`dotnet restore`](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-restore)  will restore all dependencies of the application.

```
dotnet restore
```

> [`dotnet restore`](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-restore) calls into NuGet to restore the tree of dependencies. NuGet analyzes the `project.json` file, downloads the dependencies stated in the file (or grabs them from a cache on your machine), and writes the `project.lock.json` file. The `project.lock.json` file is necessary to be able to compile and run.

> The `project.lock.json` file is a persisted and complete set of the graph of NuGet dependencies and other information describing an app. This file is read by other tools, such as dotnet build and dotnet run, enabling them to process the source code with a correct set of NuGet dependencies and binding resolutions.

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/dotnet-restore.JPG)

At this point, we can run the application and see if the output is the expected one using the [`dotnet run`](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-run) command.

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/dotnet-run.JPG)

This is how you create, build and run a basic .NET Core application using the command line.