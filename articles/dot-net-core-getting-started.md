Getting started with .NET Core
=========================

[In the previous article](https://radu.microsoft.pub.ro/dot-net-core-introduction/), we saw what is .NET Core and what can we build with it. In this article, we will install .NET Core and start with some basic examples using the command line and Visual Studio Code.

> This tutorial can be done using Windows, Linux or macOS..

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


Installing Visual Studio Code
-----------------------------------

We saw how to create, build and run applications from the command line, now it is time to move to a complete code editor that has IntelliSense and debugging built in - [Visual Studio Code](https://code.visualstudio.com/).

> [Install Visual Studio code from here](https://code.visualstudio.com/) 

In order to get IntelliSense working, you need to install the C# extension for Visual Studio Code that also installs [OmniSharp](omnisharp.net/) for IntelliSense.

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/vs-code-extensions.JPG)

After it installs, enable it and restart VS Code. At this point, we can open the folder with the earlier project in VS Code.

> You can do this in the command line by using `code .`


Running in Visual Studio Code
-------------------------------------

In order to enable debugging and running the code from VS Code, a prompt is shown asking to add the configuration files.

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/vs-code-assets.JPG)


> This will add a `.vscode` folder in the solution root with two `.json` files - `tasks.json` and `launch.json`


We can run the application by going to the Debug pane (or by pressing Ctrl(Cmd)+Shift+D) and press the run button (or F5).

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/vs-code-run.jpg)

If everything goes well, you should be able to see the output in the debug console.

Debugging in Visual Studio Code
---------------------------------------

We saw how to run the application, not let's add a method that adds two integers.

```
using System;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            int a = 7, b = 12;

            Console.WriteLine(Add(a, b));
        }

        public static int Add(int a, int b)
        {
            int sum = a + b;
            return sum;
        }
    }
}
```

If we add a breakpoint at the `return sum` line and we run the application, we get the following output:

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/vs-code-breakpoint.jpg)

The execution stopped at the line with the breakpoint and we can see the state of our program at this point.


Adding classes and navigating through code
-----------------------------------------------------

We are now going to add some classes to our console application and [create an inheritance structure based on a simplified version of this project](https://github.com/microsoft-dx/csharp-fundamentals/tree/master/CSharpFundamentals/csharp06%20-%20Inheritance).
> The project also contains documentation with step-by-step explanations and all concepts detailed.

> [This repository contains all necessary materials required to learn C#](https://github.com/microsoft-dx/csharp-fundamentals).


Let's add the following files: `Animal.cs`, `Dog.cs` with the following code:

```
using System;

public class Animal
    {
        public string Color { get; set; }

        public void Eat(string food)
        {
            Console.WriteLine("{0} animal eating {1}", Color, food);
        }

        public Animal()
        {
        }

        public Animal(string color)
        {
            Color = color;
        }
    }
```

```
using System;

public class Animal
    {
        public string Color { get; set; }

        public void Eat(string food)
        {
            Console.WriteLine("{0} animal eating {1}", Color, food);
        }

        public Animal()
        {
        }

        public Animal(string color)
        {
            Color = color;
        }
    }
```

> You can go to the definition of code elements by pressing F12.
>
> [For a complete list of Visual Studio Key Bindings see this page](https://code.visualstudio.com/docs/customization/keybindings).

And add the following as the `Main` method:

```
        public static void Main(string[] args)
        {
            Animal animal = new Animal("green");
            animal.Eat("food");

            Dog dog = new Dog("blue", "bichon"); 
            dog.Eat("bones"); 
            dog.Bark(); 

            var animals = new Animal[]
            {
                animal,
                dog        
            };

            foreach(var a in animals)
                a.Eat("food for animals");
        }
```

After running the application, you get the expected output. 

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/vs-code-animals-run.JPG)

You can also debug the application by adding breakpoints and using the stack trace and variable watch.

You can also run the application from the command line using the `dotnet run` command. Depending on the command line used, you will get something very close to the following image:

![](https://raw.githubusercontent.com/radu-matei/blog-content/master/media/dot-net-getting-started/command-line-animals.JPG)
