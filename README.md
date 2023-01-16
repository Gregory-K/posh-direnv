# posh-direnv

This is a fork of [posh-direnv](https://github.com/direnv/direnv), an environment switcher for the PowerShell. It can load and unload environment variables depending on the current directory, just like [direnv](https://direnv.net/).

There is nothing special here, a quick fix for the latest code to work again and manual-install instructions in order to address [issue 5](https://github.com/takekazuomi/posh-direnv/issues/5). Target audience is the author's, friends', and the occasional random visitor's use.


## Branches

**'dev'** (current):  
A tiny fix for the 'master' to work error-free and expose all the functions listed bellow (## Use).  
*(tested on Windows 10 WindowsPowerShell & PowerShell 7)*

**fix-homepath**:  
'master' with the environment variable fix.

**'master'**:  
Synced carbon copy of the original [posh-direnv](https://github.com/direnv/direnv).  
*(sync is not automated, always check the original repo for any advancements)*


## Install

- Download Code as a [zip file](https://github.com/Gregory-K/posh-direnv/archive/refs/heads/dev.zip)  
  OR  
  Clone the repo and checkout branch 'dev'
- Copy `posh-direnv` folder to
  - Legacy Windows Powershell:  
    `~\Documents\WindowsPowerShell\Modules\`
  - PowerShell 7:  
    `~\Documents\PowerShell\Modules\`
- Auto-load it on every pwsh window:
  - Add the line `Import-Module -Name posh-direnv` to  
    your user-profile PowerShell init script  
    - Legacy Windows Powershell:  
      `~\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`
    - PowerShell 7:  
      `~\Documents\PowerShell\Microsoft.PowerShell_profile.ps1`
- OR manually import/enable it on occassion (maybe that's your case):
  - Enter the command `Import-Module ...` or
  - use a command alias, function in this case, in your pwsh init script,  
    e.g. for 'psenv' > `function psenv { Import-Module -Name posh-direnv }`, or
  - call a psenv.ps1 script in path ...


## Use

See bellow > # Official README > ### Usage

Available Functions to explore

```sh
Set-DirEnvRc
Edit-DirEnvRc
New-DirEnvRc
Initialize-AllowList
Compare-DirEnvRc
Approve-DirEnvRc
Deny-DirEnvRc
Repair-DirEnvAuth
```


---



# Official README


## posh-direnv

Inspired by direnv

<https://github.com/direnv/direnv>

posh-direnv is an environment switcher for the PowerShell. It executes
".psdirenv" in the current directory. You can easily set unique
environment variables for each directory.

### How to install

You can install from PowerShell Gallery.
[posh-direnv](https://www.powershellgallery.com/packages/posh-direnv)

```ps
$ Install-Module -Name posh-direnv
```

### Usage

```ps
$ mkdir work
$ cd work
$ Edit-DirEnvRc
```

Since notepad starts up, edit .psdirenv. When you exit the editor
.psdirenv is authorised and applied if the file was modified.

```ps
$ cat .\.psenvrc
Write-Host "Hello posh-direnv"
$Host.UI.RawUI.WindowTitle="posh-direnv"
```

Activate the new powershell and check its operation. If you move to a
directory with .psdirenv, it will be displayed as below and the console
title will be changed.

```ps
$ cd work
psenvdir: loading work/.psenvrc
Hello posh-direnv
psenvdir: export
```

Once you exit the directory tree and move again the environment changes
will be reversed and reapplied if you reenter the directory.

If you edit the .psenvrc file yourself or move it between directories
you must authorise it before it will be applied.

```ps
$ cd work
psenvdir: work/.psenvrc not in allow list
$ Approve-DirEnvRc
psenvdir: loading work/.psenvrc
Hello posh-direnv
psenvdir: export
```

You can unauthorise a .psenvrc file by calling Deny-DirEnvRc and cleanup
the authorised list in the event directories are deleted before being
denied by calling Repair-DirEnvAuth.
