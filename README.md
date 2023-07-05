> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [github.com](https://github.com/ScoopInstaller/Install)

> PowerShell execution policy is required to be one of: Unrestricted, RemoteSigned or ByPass to execute......

## [](#installation)Installation

### [](#prerequisites)Prerequisites

-   [PowerShell](https://aka.ms/powershell) latest version or [Windows PowerShell 5.1](https://aka.ms/wmf5download)

PowerShell execution policy is required to be one of: `Unrestricted`, `RemoteSigned` or `ByPass` to execute the installer. For example:

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### [](#typical-installation)Typical Installation

Run this command from a **non-admin** PowerShell to install scoop with default configuration, scoop will be install to `C:\Users\<YOUR USERNAME>\scoop`.

```
irm get.scoop.sh | iex
# You can use proxies if you have network trouble in accessing GitHub, e.g.
irm get.scoop.sh -Proxy 'http://<ip:port>' | iex
```

### [](#advanced-installation)Advanced Installation

If you want to have an advanced installation, you can download the installer and manually execute it with parameters.

```
irm get.scoop.sh -outfile 'install.ps1'
```

To see all configurable parameters of the installer.

For example, you could install scoop to a custom directory, configure scoop to install global programs to a custom directory, and bypass system proxy during installation.

```
.\install.ps1 -ScoopDir 'D:\Applications\Scoop' -ScoopGlobalDir 'F:\GlobalScoopApps' -NoProxy
```

Or you can use the legacy method to configure custom directory by setting Environment Variables. (**Not Recommended**)

```
$env:SCOOP='D:\Applications\Scoop'
$env:SCOOP_GLOBAL='F:\GlobalScoopApps'
[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')
irm get.scoop.sh | iex
```

#### [](#for-admin)For Admin

Installation under the administrator console has been disabled by default for security considerations. If you know what you are doing and want to install Scoop as administrator. Please download the installer and manually execute it with the `-RunAsAdmin` parameter in an elevated console. Here is the example:

```
irm get.scoop.sh -outfile 'install.ps1'
.\install.ps1 -RunAsAdmin [-OtherParameters ...]
# I don't care about other parameters and want a one-line command
iex "& {$(irm get.scoop.sh)} -RunAsAdmin"
```

### [](#silent-installation)Silent Installation

You can redirect all outputs to Out-Null or a log file to silence the installer. And you can use `$LASTEXITCODE` to check the installation result, it will be `0` when the installation success.

```
# Omit outputs
.\install.ps1 [-Parameters ...] | Out-Null
# Or collect logs
.\install.ps1 [-Parameters ...] > install.log
# Get result
$LASTEXITCODE
```
