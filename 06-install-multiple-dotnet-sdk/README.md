# Multiple .NET SDKs and Runtimes Installation

As a beginner in Microsoft ecosystem, especially under Linux, I found a little bit difficult to get everything works as expected. Last week, I tried to get [WebSharper](https://websharper.com/) up and run but turns out I can not get it worked. I probably will write about this later. The solution is pretty simple: I need to have .NET SDK - LTS version (3.1.x) while I only have *Current* version (5.x.x).

So yes, I have to intall more than one SDKs and Runtimes. How to do that? `dotnet` command - AFAIK - can not be used to do that. The answer is [dotnet-install scripts](https://dotnet.microsoft.com/download/dotnet/scripts) - available for Windows and for `Bash` shell. Using this install script, I can install more than one SDK and Runtimes. Here's how.

## Install LTS Version First

* The argument `--install-dir` is used to let installer knows the installation directory.
* The argument -c LTS means that we will install latest version from LTS channel

```
$ dotnet-install.sh --install-dir ~/software/dotnet-dev-tools/dotnet-all -c LTS
dotnet-install: Note that the intended use of this script is for Continuous Integration (CI) scenarios, where:
dotnet-install: - The SDK needs to be installed without user interaction and without admin rights.
dotnet-install: - The SDK installation doesn't need to persist across multiple CI runs.
dotnet-install: To set up a development environment or to run apps, use installers rather than this script. Visit https://dotnet.microsoft.com/download to get the installer.

dotnet-install: Downloading primary link https://dotnetcli.azureedge.net/dotnet/Sdk/3.1.412/dotnet-sdk-3.1.412-linux-x64.tar.gz
dotnet-install: Extracting zip from https://dotnetcli.azureedge.net/dotnet/Sdk/3.1.412/dotnet-sdk-3.1.412-linux-x64.tar.gz
dotnet-install: Adding to current process PATH: `/home/bpdp/software/dotnet-dev-tools/dotnet-all`. Note: This change will be visible only when sourcing script.
dotnet-install: Note that the script does not resolve dependencies during installation.
dotnet-install: To check the list of dependencies, go to https://docs.microsoft.com/dotnet/core/install, select your operating system and check the "Dependencies" section.
dotnet-install: Installation finished successfully.
$
```

## Install Current Version

Install current version at the same directory location

```
$ dotnet-install.sh --install-dir ~/software/dotnet-dev-tools/dotnet-all -c Current
dotnet-install: Note that the intended use of this script is for Continuous Integration (CI) scenarios, where:
dotnet-install: - The SDK needs to be installed without user interaction and without admin rights.
dotnet-install: - The SDK installation doesn't need to persist across multiple CI runs.
dotnet-install: To set up a development environment or to run apps, use installers rather than this script. Visit https://dotnet.microsoft.com/download to get the installer.

dotnet-install: Downloading primary link https://dotnetcli.azureedge.net/dotnet/Sdk/5.0.400/dotnet-sdk-5.0.400-linux-x64.tar.gz
dotnet-install: Extracting zip from https://dotnetcli.azureedge.net/dotnet/Sdk/5.0.400/dotnet-sdk-5.0.400-linux-x64.tar.gz
dotnet-install: Adding to current process PATH: `/home/bpdp/software/dotnet-dev-tools/dotnet-all`. Note: This change will be visible only when sourcing script.
dotnet-install: Note that the script does not resolve dependencies during installation.
dotnet-install: To check the list of dependencies, go to https://docs.microsoft.com/dotnet/core/install, select your operating system and check the "Dependencies" section.
dotnet-install: Installation finished successfully.
$
```

## Installation Check

Now, when we use --info as `dotnet` CLI argument, we will have those 2 SDKs and 2 Runtimes already installed:

```
$ dotnet --info
.NET SDK (reflecting any global.json):
 Version:   5.0.400
 Commit:    d61950f9bf

Runtime Environment:
 OS Name:     devuan
 OS Version:  4
 OS Platform: Linux
 RID:         linux-x64
 Base Path:   /home/bpdp/software/dotnet-dev-tools/dotnet-all/sdk/5.0.400/

Host (useful for support):
  Version: 5.0.9
  Commit:  208e377a53

.NET SDKs installed:
  3.1.412 [/home/bpdp/software/dotnet-dev-tools/dotnet-all/sdk]
  5.0.400 [/home/bpdp/software/dotnet-dev-tools/dotnet-all/sdk]

.NET runtimes installed:
  Microsoft.AspNetCore.App 3.1.18 [/home/bpdp/software/dotnet-dev-tools/dotnet-all/shared/Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 5.0.9 [/home/bpdp/software/dotnet-dev-tools/dotnet-all/shared/Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 3.1.18 [/home/bpdp/software/dotnet-dev-tools/dotnet-all/shared/Microsoft.NETCore.App]
  Microsoft.NETCore.App 5.0.9 [/home/bpdp/software/dotnet-dev-tools/dotnet-all/shared/Microsoft.NETCore.App]

To install additional .NET runtimes or SDKs:
  https://aka.ms/dotnet-download
$
```

Now, we can use `LTS` and `Current` version altogether. Enjoy!

