# C# RuleSet

Custom RuleSet to enforce coding standards for C# projects. Requires Visual Studio 2015+.

## Usage

Download the `SfwStyleCop.ruleset` file and place it in the same folder as your `.sln` solution file.

For each `.csproj` in the solution you wish to apply the rules to, first install the `StyleCop.Analyzers` NuGet package. Install from the NuGet Package Manager in Visual Studio, or by using the command line:

```
Install-Package StyleCop.Analyzers
```

Next, open the `.csproj` file in an editor, find the top most `<PropertyGroup>` element, without the `Condition` attribute, and add the following element within it:

```
<CodeAnalysisRuleSet>..\SfwStyleCop.ruleset</CodeAnalysisRuleSet>
```

If your `.csproj` files are in folders below the solution file then this path is correct, otherwise update the path to point to the `.ruleset` file. If you do not have a `<PropertyGroup>` element, such as for a .NET Core project, you can add one in.

NOTE: It is possible to add the `.ruleset` to the `.csproj` from Visual Studio, but not at a top level which applies to all build configurations, so this is the preferred method.

For example, your `.csproj` file should contain something like this:

```
<PropertyGroup>
  <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
  <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
  <ProjectGuid>{...}</ProjectGuid>
  <OutputType>Exe</OutputType>
  <RootNamespace>MyApp</RootNamespace>
  <AssemblyName>MyApp</AssemblyName>
  <TargetFrameworkVersion>v4.5.2</TargetFrameworkVersion>
  <FileAlignment>512</FileAlignment>
  <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>
  <CodeAnalysisRuleSet>..\SfwStyleCop.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

Now when you build your solution any violations will be reported as errors. Most have fixes which can be applied by pressing **Ctrl + .** and selecting them from the Quick Actions menu.