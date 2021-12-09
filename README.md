# ghūl 'dotnet new' templates

[![CI/CD](https://img.shields.io/github/workflow/status/degory/ghul-templates/CICD)](https://github.com/degory/ghul-templates/actions?query=workflow%3ACICD)
[![Version](https://img.shields.io/github/v/release/degory/ghul-templates?label=version)](https://github.com/degory/ghul-templates/releases)
[![Release Date](https://img.shields.io/github/release-date/degory/ghul-templates)](https://github.com/degory/ghul-templates/releases) 
[![Issues](https://img.shields.io/github/issues/degory/ghul-templates)](https://github.com/degory/ghul-templates/issues) 
[![License](https://img.shields.io/github/license/degory/ghul-templates)](https://github.com/degory/ghul-templates/blob/main/LICENSE)
[![ghūl](https://img.shields.io/badge/gh%C5%ABl-100%25!-information)](https://ghul.io)

These are ['dotnet new' templates](https://docs.microsoft.com/en-us/dotnet/core/tools/custom-templates) for quick-starting a console application or class library .NET 6.0 project written in the [ghūl programming language](https://ghul.io).

Note that these templates do not include things like GitHub Actions workflows, development container config, Dependabot config, unit tests, etc. For a GitHub repository template that does include all those things, see the [ghūl repository template](https://github.com/degory/ghul-repository-template) repo.

## Quick start

```
$ dotnet new --install ghul.templates
$ mkdir my-console-project
$ cd my-console-project
$ dotnet new ghul-console
The template "ghūl console application" was created successfully.
$ dotnet run
Hello world!
```

## Prerequisites

These template create a skeleton ghūl programming language projects that can be built on any host that supports the [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)

You'll need to install the [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0) or use a container that includes it such as the [ghūl development image](https://hub.docker.com/r/ghul/devcontainer/tags) or a recent Microsoft .NET SDK image

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

In Visual Studio Code, run the build task (`<ctrl>` + `<shift>` + `B`), which is set up to run `dotnet build` or `dotnet pack`