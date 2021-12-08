# ghūl console application template

This is a ['dotnet new' template](https://docs.microsoft.com/en-us/dotnet/core/tools/custom-templates) for quick-starting a .NET 6.0 console application project written in the [ghūl programming language](https://ghul.io).

Note that this template does not include things like GitHub Actions workflows, development container config, Dependabot config, unit tests, etc. For a GitHub repository template that does include all those things, see the [ghūl repository template](https://github.com/degory/ghul-repository-template) repo.

## CI/CD status

 [![CI/CD](https://github.com/degory/ghul-console-template/workflows/CI/CD/badge.svg?branch=main)](https://github.com/degory/ghul-application-template/actions?query=workflow%3ACI%2FCD)

## Package

[ghul.templates](https://www.nuget.org/packages/ghul.templates/)

## Prerequisites

This template will create a skeleton ghūl application that can be built on any host that supports the [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0), including any of:
- GitHub [Codespaces](https://github.com/features/codespaces)
- Windows 10
- Windows 10 with [Docker Desktop](https://www.docker.com/products/docker-desktop) and either the [ghūl development container](https://hub.docker.com/r/ghul/devcontainer/tags) or another image that includes the .NET 6.0 SDK
- Windows 10 with [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install-win10)  
- Linux with
- Linux with Docker and [ghūl development container](https://hub.docker.com/r/ghul/devcontainer/tags) or another image that includes the .NET 6.0 SDK

You'll need to install the [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0) or, for the Docker options, make sure you're using an image that includes it (try the [ghūl development image](https://hub.docker.com/r/ghul/devcontainer/tags) or the Microsoft .NET SDK image)

## Recommended

- Visual Studio Code
- The [ghūl language Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=degory.ghul), which will give you rich language support including:
  - syntax highlighting
  - error highlighting as you type
  - code snippets
  - symbol information on hover
  - intelligent code completion
  - function signature help
  - find uses
  - go to/peek definition
  - go to symbol in file
  - go to symbol in workspace

## Installing the template

The template is distributed as a NuGet package containing a .NET template. Before you can use it, you need to install the template package:

```
$ dotnet new --install ghul.templates
```

## Instantiating the template

Start by creating a new folder for your project and `cd` into it
```
$ mkdir example
$ cd example
```

Then use `dotnet new` to initialize a new instance of this template in your project folder:
```
$ dotnet new ghul-console
```

This will create a `.ghulproj` MSBuild project file, a `.ghul` source file and some other supporting files:
```
$ find

./src
./src/example.ghul
./src/README.md
./README.md
./.config
./.config/dotnet-tools.json
./.vscode
./.vscode/tasks.json
./example.ghulproj
```

## Building the template application  

ghūl applications are standard .NET applications using familiar MSBuild projects and .NET SDK commands such as `dotnet build` and `dotnet pack`. However, before these commands will work, you do need to install the [ghūl compiler](https://www.nuget.org/packages/ghul.compiler/)

### Installing the ghūl compiler

(If you're developing in a container using the [ghūl development Docker image](https://hub.docker.com/r/ghul/devcontainer/tags) then you can skip this step)

The ghūl compiler [is packaged](https://www.nuget.org/packages/ghul.compiler/) as a [.NET tool](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools) and can be installed either locally or globally.

#### Local tool install

This template includes a local tool manifest in the `.config` folder which includes the compiler, so you can install the compiler locally simply by restoring local tools:

```
$ dotnet tool restore
```

Note: if you're using Visual Studio Code and the ghūl extension, the  extension will do this for you automatically when you open the project folder

#### Global tool install

If you prefer to install the compiler globally, you can run:

```
$ dotnet tool install --global ghul.compiler
```

Note: if you do install the compiler globally, you will also need to change the `GhulCompiler` property in your `.ghulproj` file to reference it:

```
    <GhulCompiler>ghul-compiler</GhulCompiler>
```

### Building and running the application

Just use the normal dotnet commands:

```
$ dotnet build
```
```
$ dotnet pack
```
```
$ dotnet run
```

etc. etc.

In Visual Studio Code, run the default build task (`<ctrl>` + `<shift>` + `B` and select `build`) is set up to run `dotnet build`