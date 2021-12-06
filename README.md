# How to get started with WSL2

## Install WSL2

If you have the latest updates of your OS, installation of WSL2 is a one-liner command (in PowerShell):

```
wsl --install
```

This will automatically install `wsl2` and Ubuntu. [@see](https://docs.microsoft.com/en-us/windows/wsl/install#install)

Now reboot.

## Configuring Ubuntu

Type "Ubuntu" in your start menu and launch the distro. It may take some time for the first inititialization. When the prompt will appear, type username and password. Welcome to linux.

Close Ubuntu and type "Microsoft store" in start menu. Search for "Windows terminal" and install. Open Windows terminal, click down arrow near the plus sign and select Ubuntu. Now it's time to update your system. By default, when you open any linux distro inside your terminal, your current working directory is windows user documents and settings. Don't try to work under it, as you will use NTFS zone of your file system which is several times slower then linux EXT one. First of all change current working directory to your linux HOME:

```
cd ~
```

Then issue the command:

```
sudo apt update && sudo apt upgrade
```

Install curl and wget:

```
sudo apt install curl wget
```

Install zsh (convenient shell):

```
sudo apt install zsh
```

and Oh-My-ZSH goodies [@see](https://ohmyz.sh/#install):

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### NodeJS

Install NodeJS via `nvm` (node version manager) [@see](https://github.com/nvm-sh/nvm):

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

then install the latest stable nodejs version:

```
nvm install --lts
```

Install yarn:

```
npm i -g yarn
```

### Docker

[Install Docker](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository). Install dependencies:

```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Add GPG key:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Setup Docker repository:

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Install docker

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

To run Docker, issue:

```
sudo service docker start
```

Test:

```
sudo docker run hello-world
```

### VsCode

Install official extension called "Remote - WSL" [@see](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)

> Open any folder in the Windows Subsystem for Linux (WSL) and take advantage of Visual Studio Code's full feature set.

### Docker autocompletion via Oh-My-Zsh

[@see](https://docs.docker.com/compose/completion/#zsh)

Type `code ~/.zshrc` to open shell configuration file in VsCode (yes, you can open any file or folder directly in VsCode from your linux shell). Find the line with plugins and modify it like `plugins=(... docker docker-compose)`.

Reload shell:

```
exec zsh
```

## How to start your work

Generate SSH-keypair for your repository and add it to linux ssh-agent:


- [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Azure](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops)
- [BitBucket](https://support.atlassian.com/bitbucket-cloud/docs/set-up-an-ssh-key/)

Create projects folder in your linux home directory:

```
cd ~
md Projects
cd Projects

git clone <your project repository name>
cd <your project repository folder>

code .
```

Then follow instructions from project readme.