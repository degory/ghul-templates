# ghūl 'dotnet new' templates

[![CI/CD](https://img.shields.io/github/workflow/status/degory/ghul-templates/CICD)](https://github.com/degory/ghul-templates/actions?query=workflow%3ACICD)
[![NuGet version (ghul.templates)](https://img.shields.io/nuget/v/ghul.templates.svg)](https://www.nuget.org/packages/ghul.templates/)
[![Release](https://img.shields.io/github/v/release/degory/ghul-templates?label=release)](https://github.com/degory/ghul-templates/releases)
[![Release Date](https://img.shields.io/github/release-date/degory/ghul-templates)](https://github.com/degory/ghul-templates/releases) 
[![Issues](https://img.shields.io/github/issues/degory/ghul-templates)](https://github.com/degory/ghul-templates/issues) 
[![License](https://img.shields.io/github/license/degory/ghul-templates)](https://github.com/degory/ghul-templates/blob/main/LICENSE)
[![ghūl](https://img.shields.io/badge/gh%C5%ABl-100%25!-information)](https://ghul.dev)

These are ['dotnet new' templates](https://docs.microsoft.com/en-us/dotnet/core/tools/custom-templates) for quick-starting a .NET 8.0 console application or class library project written in the [ghūl programming language](https://ghul.dev).

Note that these templates do not include things like GitHub Actions workflows, development container config, Dependabot config, unit tests, etc. For a GitHub repository template that does include all those things, see the [ghūl repository template](https://github.com/degory/ghul-repository-template) repo.

## Quick start

```
$ dotnet new --install ghul.templates
The following template packages will be installed:
   ghul.templates

Success: ghul.templates::0.0.12 installed the following templates:
Template Name               Short Name     Language  Tags   
--------------------------  -------------  --------  -------
ghūl class library package  ghul-classlib  ghūl      Console
ghūl console application    ghul-console   ghūl      Console

$ mkdir my-console-project
$ cd my-console-project
$ dotnet new ghul-console
The template "ghūl console application" was created successfully.

$ dotnet run
Hello world!
```

## Prerequisites

These templates create skeleton ghūl programming language projects that can be built on any host that supports the [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

You'll need to either install the [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0), or use a container that includes it like the [ghūl development image](https://hub.docker.com/r/ghul/devcontainer/tags) or a recent Microsoft .NET SDK image

## Recommended

- [Visual Studio Code](https://code.visualstudio.com/)
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

## Installing the templates

The templates are distributed as a NuGet package containing two .NET templates. Before you can use them, you need to install the template package:

```
$ dotnet new --install ghul.templates
```

## Instantiating the templates

Start by creating a new folder for your project and `cd` into it
```
$ mkdir example
$ cd example
```

Then use `dotnet new` to initialize a new instance of either template in your project folder:
```
$ dotnet new ghul-console
```
Or

```
$ dotnet new ghul-classlib
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

## Building your ghūl application or package

ghūl applications are standard .NET applications using familiar MSBuild projects and .NET SDK commands such as `dotnet build` and `dotnet pack`.

### Building your project

Just use the normal dotnet commands:

```
$ dotnet build
```
```
$ dotnet pack
```

And, for the console application template:
```
$ dotnet run
```

## the ghūl compiler tool

The ghūl compiler is [packaged](https://www.nuget.org/packages/ghul.compiler/) as a [.NET tool](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools) and can be installed either locally or globally.

### Local tool install

These templates include a local tool manifest in the `.config` folder which includes the compiler. This means the compiler tool will be restored automatically when you build your application, however you can also restore it manually with:

```
$ dotnet tool restore
```

To run the compiler local tool directly from the command line, use:

```
$ dotnet tool run ghul-compiler
ghūl v0.2.154
```

### Global tool install

If you prefer to install the compiler globally, you can run:

```
$ dotnet tool install --global ghul.compiler
```

This will install the compiler globally allowing you to run it from any folder with
```
$ ghul-compiler
```
Note: if you do install the compiler globally, you will also need to change the `GhulCompiler` property in your `.ghulproj` file to reference it:

```
    <GhulCompiler>ghul-compiler</GhulCompiler>
```

