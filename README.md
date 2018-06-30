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

# About
C# 7 is the first C# release where Microsoft started doing minor releases (7.1, 7.2, 7.3). However all new projects are still configured to use C# 7.0 (the latest major version).

_Okay how do I get them?_ 

Well you probably already have them installed.

_Then why can't I use new C# features in my code?_

Minor releases are [opt-in](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version#edit-the-csproj-file).

_How does this thing work then?_

When you install this package into a project, a little chunk of MSBuild stuff is added to your project.
```xml
<PropertyGroup>
  <LangVersion>latest</LangVersion>
</PropertyGroup>
```

This is the opt-in part that lets you use whatever latest C# version you have installed. When you uninstall this package from a project, the project will revert to using the default version.

_Why should I use this?_

Because you can use the NuGet package manager UI in Visual Studio to quickly upgrade a large solution.

_Why should I use this instead of Directory.build.props?_

Because directory-wide build.props don't offer the same control over which projects get upgraded or not.
