# Session 1: Configuring laptops and Software Installation

* [IDE Installation](#ide)  
* [VSCode Extensions](#extensions)  
* [Installing VSCode extensions](#installextensions)
* [About Node.js](#node)
* [About Node Package Manager (NPM)](#npm)
* [Installing Node.js](#installingnode)
* [What is git?](#git)
* [Installing git?](#installinggit)
* [Installing the stand-alone IBM Cloud CLI](#ibmcloud)
* [Verify IBM Cloud installation](#verifyibmcloud)
* [Installing Homebrew](#homebrew)
* [Installing Zsh](#zsh)
* [Verify Zsh installation](#verifyzsh)
* [Install MongoDb](#install-mongo)
* [Installing Docker](#docker)
* [Verify Docker Installation](#verifydocker)
* [Further reading](#further)

## Session Objective
This session will cover the following:

* IDE installation and extensions
* Node.js installation
* NPM installation
* Git installation
* IBM Cloud CLI installation
* Homebrew installation
* Zsh installation


<a name="ide"></a>
## IDE Installation
**VSCode** is the IDE that we recommend using for Front End Development (FED).

* Free and open source tool that is approved for installation.
* Extensible with a massive amount of plugins.
* Can’t find the plugin you need? Write your own!
* Integrated with Git

To download and install, visit the following link and follow the instructions for your operating system: https://code.visualstudio.com/download

<a name="extensions"></a>
## VSCode Extensions
There are a vast array of extensions available on the VSCode website:

https://marketplace.visualstudio.com/VSCode

<a name="installextensions"></a>
## Installing VSCode extensions

* Installing an extension is point and click easy.
* Locate the extension that you require on the vscode marketplace.
* Click install and follow the instructions.

Some recommended extensions:

**GitHub** - [Integrates github and its workflows into vscode](https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-github)

**Git Blame** - [See git blame information in the status bar](https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame)

<a name="node"></a>
## About Node.js
> As an asynchronous event driven JavaScript runtime, Node is designed to build scalable network applications.

In essence, Node is a JavaScript server implementation, allowing backend services to be coded in vanilla JavaScript, allowing for fully featured scalable web applications to be developed totally in JavaScript.  We will cover Node.js in more detail in a later session. 

<a name="npm"></a>
## About Node Package Manager (NPM)

> npm makes it easy for JavaScript developers to share and reuse code, and makes it easy to update the code that you’re sharing, so you can build amazing things.

NMP is bundled with the Node installation.

<a name="installingnode"></a>
Installing Node.js

Visit the Node website to download and install the version appropriate to your IDE.
https://nodejs.org/en/download/

<a name="git"></a>
## What is Git?

> it is a mature, actively maintained open source project originally developed in 2005 by Linus Torvalds, the famous creator of the Linux operating system kernel. A staggering number of software projects rely on Git for version control, including commercial projects as well as open source.
**Atlassian.com**

<a name="installinggit"></a>
## Installing Git
1. Download and install the latest version of Git
https://git-scm.com/downloads

<a name="ibmcloud"></a>
## Installing the stand-alone IBM Cloud CLI

1. To install the IBM Cloud CLI for MacOS, visit the following page, select the installer appropriate for your OS and follow the instructions:
https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use

<a name="verifyibmcloud"></a>
## Verify the Installation

### N.B. Windows users should skip this step

1. In the terminal, enter the following command:
```
$ bluemix --help
```
<a name="homebrew"></a>
## Install Homebrew

> Homebrew installs the stuff you need that Apple didn’t.

1. In a terminal, paste the following command:
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. Visit the Homebrew website for further details:
https://brew.sh/

<a name="zsh"></a>
## Install Zsh

### N.B. Windows users should skip this step

Zsh is a command shell which add extra features to your regular terminal shell.

1. Try `$ zsh --version` before installing Zsh from Homebrew. 

2. To install from brew, type the following command:
```
$ brew install zsh zsh-completions
```

<a name="verifyzsh"></a>
## Verify Zsh Installation

### N.B. Windows users should skip this step

1. Verify Zsh installation by running zsh --version. Expected result: zsh 5.1.1 or more recent.
2. Make it your default shell: 
```
$ chsh -s  /bin/zsh
```
3. Log out and login back again to use your new default shell.
4. Test that it worked with `$ echo $SHELL`. Expected result: `/bin/zsh` or similar.

<a name="install-mongo"></a>
## Install MongoDB
> MongoDB is a document database with the scalability and flexibility that you want with the querying and indexing that you need.

> MongoDB stores data in flexible, JSON-like documents, meaning fields can vary from document to document and data structure can be changed over time.

### MAC Users should install Mongo with Homebrew using the following instructions:
We'll use [home brew](https://brew.sh/) to install mongo.

Check if MongoDB is installed by running:
```
$ mongo --version
```

If MongoDB is not installed run the following:
```
$ brew install mongodb
```

### Windows users should install Mongo using the following instructions:
1. Download the .msi package from the Mongo website and save to a memorable location e.g. Downloads folder: https://www.mongodb.com/download-center?initial=true#community

1. Locate the .msi file downloaded in step 1.  Double click the .msi file and follow the on screen instructions to install Mongo.

* Mongo is self contained and has no requirement on other system resources.  You could install it in any folder you wish.

1. Make the directory that will be used for the Mongo data.  In a command prompt, type the following:
```
$ md \data\db
```

1. To specify an alternate path for data files:
```
$ "C:\Program Files\MongoDB\Server\3.2\bin\mongod.exe" --dbpath "d:\test\mongo db data"
```

1. To start MongoDB, run mongod.exe.

<a name="docker"></a>
## Install Docker
Visit the Docker website and select the platform according to whether you have a MAC or Windows PC. https://docs.docker.com/install/#supported-platforms

Download the installer and follow the instructions on the Docker website to complete the installation.

<a name="verifydocker"></a>
## Verify the Docker Installation
In a terminal, type the following command to check that docker is installed correctly:
```
$ docker --version
```

<a name="further"></a>
## Further reading
[The VSCode website](https://code.visualstudio.com/download)  
[VSCode Market for Extensions](https://marketplace.visualstudio.com/VSCode)  
[What is Git?](https://www.atlassian.com/git/tutorials/what-is-git)  
[What is Node.js?](https://www.oreilly.com/ideas/what-is-node)  
[What is Zsh?](https://ohmyz.sh/)   
[What is Homebrew?](https://brew.sh/)  
[MongoDb Docs](https://docs.mongodb.com/)  
