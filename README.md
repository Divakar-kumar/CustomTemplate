# Create .NET Core Project Template

This repo contains a sample showing how to create a .net core template that can be used either by the
dotnet command line (`dotnet new`) or Visual Studio & Visual Studio for Mac. For more info see [.NET CLI Templates in Visual Studio
](https://devblogs.microsoft.com/dotnet/net-cli-templates-in-visual-studio/).

The samples are in the `src/content` folder.

## Getting started creating templates

To get started creating templates, take a look at the following resources.
 - [How to create .NET Core Project Template](https://divakarkumar.azurewebsites.net/2021/05/14/create-net-core-project-template/)
 - [Custom templates for dotnet new
](https://docs.microsoft.com/en-us/dotnet/core/tools/custom-templates)
 - [Sources for asp.net core templates](https://github.com/dotnet/aspnetcore/tree/master/src/ProjectTemplates)
 
### `sourceName`

In the `template.json` file you should have a `sourceName` property declared. The `sourceName` property is special, and should always be declared. When a project is created, either through the command line or Visual Studio, the project will be given a name. For example, when creating a project with `dotnet new` you can pass in the `-n|--name` parameter. In Visual Studio during New Project the user will be prompted to provide a project name.
The value provided by the user for project name will replace the string declared in `sourceName`. This is typically
used to replace the `namespace` declaration in generated files.

```json
{
  "sourceName": "MyCommand",
}
```

For a full example of `sourceName` see [src/Content/MyCommand/.template.config/template.json](template.json)

### `defaultName`

When a project is created in Visual Studio, the screen that the user provides the project name will always be
pre-populated. If `defaultName` is declared in the `template.json`, that value will be used as the default name
for the project. Otherwise `Project1` is always used.
When users create projects from the command line with `dotnet new` if the `-n|--name` parameter is not passed in, the `defaultName` value will be used.

```json
{
  "defaultName": "MyCommandTool",
}
```

For a full example of `sourceName` see [src/Content/MyCommand/.template.config/template.json](template.json)

### `classifications`

In Visual Studio when creating a new project there is an `All Project Types` dropdown that can be used to filter
the list of templates shown. You should declare the relevant values from that dropdown in the `classifications`
property of the `template.json`. Here are some of the values that you can use.

 - Cloud
 - Console
 - Desktop
 - Games
 - IoT
 - Library
 - Mobile
 - Service
 - Web

Here is an example of the declaration.

```json
{
  "classifications": ["Console"],
}
```

Note: in the current preview the Visual Studio New Project Dialog will add all classifications from installed 
templates into the `All Project Types` dropdown. That behavior is likely to change, custom classifications
will not be listed. You should select the values that you see in Visual Studio (without any additional tempaltes installed) so that the user can filter.

### Language and type

In the `template.json` you should define the `language` and `type` for the template in the `tags` property. For
example

```json
"tags": {
  "language": "C#",
  "type":"project"
},
```

***If the `type` property is not declared, the template will not be shown in the Visual Studio New Project Dialog***
