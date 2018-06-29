# LatestLangVersion
Upgrade all your projects to the latest C# version, the lazy way.

PM:
```powershell
Get-Project -All | Install-Package LatestLangVersion
```

dotnet cli (using PowerShell):
```powershell
Get-ChildItem *.csproj -Recurse | ForEach-Object { dotnet add $_ package LatestLangVersion }
```

# What is this?
C# 7 is the first release where Microsoft started doing minor releases (7.1, 7.2, 7.3). Okay great, so what do you have to do to get them? 

Actually you probably already have them installed. So Why can't you use new C# features? That's because the default build behavior is to use C# 7.0 (the latest major version). Minor releases are [opt-in](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version#edit-the-csproj-file).

# How does this thing work then?
When you install this package into a project, a little chunk of MSBuild stuff is added to your project.
```xml
<PropertyGroup>
  <LangVersion>latest</LangVersion>
</PropertyGroup>
```

This is the opt-in part that lets you use whatever latest C# version you have installed.

When you uninstall this package from a project, the project will revert to using the default version.

# Why should I use this?
Because you can use the NuGet package manager UI in Visual Studio to quickly upgrade a large solution.

# Why should I use this instead of Directory.build.props?
Because directory-wide build.props don't offer the same control over which projects get upgraded or not.
