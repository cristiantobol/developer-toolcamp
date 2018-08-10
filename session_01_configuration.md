# Session 1: Configuring laptops and Software Installation

* [IDE Installation](#ide)  
* [VSCode Extensions](#extensions)  
* [Installing VSCode extensions](#installextensions)
* [About Node.js](#node)
* [About Node Package Manager (NPM)](#npm)
* [Installing Node.js](#installingnode)
* [What is git?](#git)
* [Installing git?](#installinggit)
* [Configuring Git for IBM GitHub Enterprise](#ibmgit)
* [Further reading](#further)

## Session Objective
This session will cover the following:

* IDE installation and extensions
* Node.js installation
* NPM Installation
* Git installation
* Configuring IBM Github Enterprise


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

Installing an extension is point and click easy.
Locate the extension that you require on the vscode marketplace.
Click install and follow the instructions.

Some recommended extensions:

GitHub - Integrates github and its workflows into vscode
https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-github

Git Blame - See git blame information in the status bar.
https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame

<a name="node"></a>
## About Node.js
*“As an asynchronous event driven JavaScript runtime, Node is designed to build scalable network applications.”*

In essence, Node is a JavaScript server implementation, allowing backend services to be coded in vanilla JavaScript, allowing for fully featured scalable webn applications to be developed totally in JavaScript.  We will cover Node.js in more detail in a later session. 

<a name="npm"></a>
## About Node Package Manager (NPM)

*“npm makes it easy for JavaScript developers to share and reuse code, and makes it easy to update the code that you’re sharing, so you can build amazing things.”*

NMP is bundled with the Node installation.

<a name="installingnode"></a>
Installing Node.js

Visit the Node website to download and install the version appropriate to your IDE.
https://nodejs.org/en/download/

<a name="git"></a>
## What is Git?

*“Git is a mature, actively maintained open source project originally developed in 2005 by Linus Torvalds, the famous creator of the Linux operating system kernel. A staggering number of software projects rely on Git for version control, including commercial projects as well as open source.”*
**Atlassian.com**

<a name="installinggit"></a>
## Installing Git
1. Download and install the latest version of Git
https://git-scm.com/downloads

1. Set your username in Git
https://help.github.com/articles/setting-your-username-in-git

1. Set your commit email address in Git
https://help.github.com/articles/setting-your-commit-email-address-in-git

<a name="ibmgit"></a>
## Configuring Git for IBM GitHub Enterprise
Generating ssh keys:
https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

Adding the ssh keys to your IBM GitHub Enterprise account
1. Login to your IBM Github Enterpise account at https://github.ibm.com/
2. Follow the instructions to add a new ssh key, making sure to substitute any mention of github.com with github.ibm.com.
https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

<a name="further"></a>
## Further reading
[VSCode](https://code.visualstudio.com/download)  
[VSCode Market for Extensions](https://marketplace.visualstudio.com/VSCode)
[What is Git?](https://www.atlassian.com/git/tutorials/what-is-git)
[What is Node.js?](https://www.oreilly.com/ideas/what-is-node)