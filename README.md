# Setup guide for Windows scripting enviroment
## Chocolatery - Package manager for Windows
>Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

**Install WSL (if on latest Windows 10 2021+)**
>wsl.exe --install

**If not on this version:**<br>
>dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
>dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

**Download Linux kernal package:**<br>
>https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi<br>

**Set WSL to version two:**<br>
>wsl --set-default-version 2

**Install Windows Terminal**
>choco install microsoft-windows-terminal -y

**Install Ubuntu in WSL**
>choco install wsl-ubuntu-2004 -y

**Install PowerShell Core alongside with PowerShell (5.1)**
>choco install PowerShell-core -y

**Install VSCODE**
>choco install vscode -y

**Install GIT**
>choco install git -y

## VSCode and Git setup
> --- NEED TO BE UPDATED ---

**Generate ssh keys if you do not have any - Must use passphrase!**
>ssh-keygen -t ed25519 -f $env:USERPROFILE\.ssh\id_ed25519 -C $env:USERNAME@$env:USERDNSDOMAIN

**We should avoid using RSA SSH-keys but if you must have one, make it 4096 bits:**
>ssh-keygen -t rsa -b 4096 -f $env:USERPROFILE\.ssh\id_rsa -C $env:USERNAME@$env:USERDNSDOMAIN


**Alias to show git history in a pretty way ("git hist")**

>git config --global alias.hist "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"


## Setup SSH-agent keys so you dont have to type password all the time when using VSCODE and PowerShell:
>Get-Service ssh-agent | Set-Service -StartupType Automatic<br>
>start-service ssh-agent<br>

**Add private key to ssh-agent:**
>ssh-add $env:USERPROFILE/.ssh/id_ed25519

**Make sure Windows native is using OpenSSH from Windows/system32 folder:**
>Get-Command ssh | Select-Object Source<br>

**Change from Git's SSH to Windows native (OpenSSH) :<br>**
>[Environment]::SetEnvironmentVariable("GIT_SSH", "$((Get-Command ssh).Source)", [System.EnvironmentVariableTarget]::User)