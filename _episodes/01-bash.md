---
title: "Connect to the HPC"
teaching: 10
exercises: 5
questions:
- "How do I connect to an HPC system?"
objectives:
- "Be able to connect to a remote HPC system"

keypoints:
- "We connect to remote servers, like HPC's, using the command line interface"
- "SSH is a secure protocl for connecting to remote servers"
- "To connect to a server, you need it's address, an open port, and your user ID"
---
## IMPORTANT

If you are using the Griffith Wireless network you must be logged in with Griffith's VPN to use the HPC. More information about downloading and using <a href="https://intranet.secure.griffith.edu.au/computing/remote-access/virtual-private-network" target="_blank">Griffith's VPN</a>

## Opening the command line interface (CLI)

The first thing you will need to do is move your data and scripts from your computer (this can also be another storage device such as external hard drive or <a href="https://www.griffith.edu.au/digital-solutions/research-storage" target="_blank">research space</a>) to the HPC. Connecting to a HPC system is most often done with a tool known as "ssh" (**S**ecure **SH**ell) which is accessed through the computers CLI. Linux and Mac users will find the "Terminal" CLI already installed on their computers.  

Windows users will need to install a Terminal emulator, we suggest using MobaXterm (CLI) or PuTTY (GUI). If you haven't done so, please download the free version of <a href="https://mobaxterm.mobatek.net/download.html" target="_blank">MobaXterm</a> or the appropriate version of puTTy for your <a href="https://the.earth.li/~sgtatham/putty/latest/w32/putty.exe" target="_blank">32bit</a> or <a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank">64bit</a> OS.

> ## 32 bit or 64 bit OS?
> Visit this <a href="https://support.wdc.com/knowledgebase/answer.aspx?ID=9405" target="_blank">link</a> for instructions on determining if your Windows 7,8 or 10 is 32 or 64 bit.
{: .callout}

## Connecting with ssh
The `ssh` command allows us to connect to UNIX computers remotely, and use them as if they were our own.
The general syntax of the connection command follows the format `ssh yoursNumber@some.remote.server.address`

* **some.remote.server.address** The web address of the server to connect to. Griffith has multiple HPC's that can be used, each with a unique address.


Additional parameters may also be necessary:

* **Port Number** The specific port used to connect to the server
* **User ID** Your user ID on the HPC system  

<span style="color:white">blankline</span>
   
> ## What's my User Name?
> Your user name is your Griffith sNumber.  Wherever you see **"sNumber"**, be sure to replace it with your Griffith sNumber.
{: .callout}

## Using ssh to connect to the HPC

Open terminal, and input the following command.

~~~
ssh gc-prd-hpclogin1.rcs.griffith.edu.au
~~~
{: .bash}

If you've never connected to this particular server before you'll encounter a message similar to this:

~~~
The authenticity of host 'gc-prd-hpclogin1.rcs.griffith.edu.au (10.250.250.3)' can't be established.
ECDSA key fingerprint is SHA256:VlHJK1c0osj32r0jFi5nSy2hZI6u1vymneqvK3D1dyI.
Are you sure you want to continue connecting (yes/no)?
~~~
{: .bash}

This is your computer warning you that you're about to connect to another computer, type \"yes\" to proceed.  This will add the HPC to your \"known hosts\", and you shouldn't see the message again the future.

~~~
generating ssh file /export/home/sNumber/.ssh/id_rsa ...
Generating public/private rsa key pair.
Your identification has been saved in /export/home/sNumber/.ssh/id_rsa.
Your public key has been saved in /export/home/sNumber/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:ozMjBGsgSjGwHKsTVLyQYszPAJp4poR+mAhXeAIh1qA sNumber@gc-prd-hpclogin1
The key's randomart image is:
+---[RSA 2048]----+
|@X*o.            |
|@XB+.            |
|E=Xo.            |
|XBo*             |
|*+o..   S        |
| o..   . .       |
|    . =          |
|     . +         |
|                 |
+----[SHA256]-----+
adding id to ssh file /export/home/sNumber/.ssh/authorized_keys
~~~~
{: .bash}

You should now be prompted to input the password which corresponds to your Griffith sNumber. Type it in carefully (no characters will appear on the screen), then press ENTER.

~~~
sNumber@gc-prd-hpclogin1.rcs.griffith.edu.au's password: 
~~~
{: .bash}

If you entered your password appropriately, congratulations, you're now connected to the HPC!  

<span style="color:white">blankline</span>

> ## The Command Prompt
> The command prompt is the symbol or series of characters which precedes each shell command, and lets the user know the shell is ready to receive commands.  For example, when you initially login to the HPC you command prompt should resemble `-bash-4.1`. If your command prompt changes to `>`, the shell is expecting further input. Use the key-binding CTRL+C to escape shell commands, returning your prompt from `>` to `-bash-4.1`.  
>
> Let's all change our command prompts to something more useful, input the command `PS1='\W\n $ '`. Our command prompt is now our current working directory followed by a \"$\".
{: .callout}

## Using putty as a ssh emulator to connect to the HPC 

![putty1](../files/putty1.jpg)

To install putty ssh client on windows, download the software from:

Click here to download <a href="https://the.earth.li/~sgtatham/putty/latest/w32/putty-0.73-installer.msi" target="_blank">puTTy 32bit</a>
Click here to download <a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.73-installer.msi" target="_blank">puTTy 64bit</a>

Once putty is installed, start putty
Start ==> All Programs ==> puTTy ==> puTTy

Configure the cluster login node as follows:

Open ssh on the left pane and click on X11 and enable X11 forwarding:

![putty2](../files/putty2.jpg)

Click on Tunnels on the left pane and Enter:

source ports : 5901
Destination: localhost:5901
Click Add button

![putty3](../files/putty3.jpg)

Click on Sessions on the left pane and Enter for host name: gowonda.rcs.griffith.edu.au
And for saved session type: gowonda

![putty4](../files/putty4.jpg)

Double click or select Open to connect to gowonda

![putty5](../files/putty5.jpg)

If you have enabled X11 port forwarding and enabled a local Xming X11 Windows server, type "xclock" and a clock should pop up on your desktop.

![putty6](../files/putty6.jpg)


## Connecting with a "Key"

That was pretty awesome, but I really disdain having to type my password in all the time.  There exists an alternative method of authentication for remote servers known as "key-pairs".  Using this method, we can **securely** connect to other computers without explicitly providing our user ID and password every time.  Without going into a great deal of detail, key-pairs function much like a traditional lock & key.

### Generating a Key Pair

These commands should be run on your Terminal i.e. sNumber@PC12345-OSX:~$ , not the HPC i.e. [sNumber@gc-prd-hpclogin1 ~]$  Let's start by using the `ssh-keygen` command to make our key pair.  But first, let's make sure we're in the right directory.

Now let's create our keys using the `ssh-keygen` command:

~~~
ssh-keygen -t rsa -b 2048 -f ~/.ssh/HPC
~~~
{: .bash}

You'll now be prompted to input a password for your key, leave it blank by pressing ENTER.

~~~
ssh-keygen -t rsa -b 2048 -f ~/.ssh/HPC
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
~~~
{: .bash}

Confirm your password as blank by pressing ENTER again

~~~
ssh-keygen -t rsa -b 2048 -f ~/.ssh/HPC
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again:  
~~~
{: .bash}

You've now created a pair of keys!  The private key will be called HPC, the public key will be called HPC.pub. They should be located in your .ssh directory.

~~~
ssh-keygen -t rsa -b 2048 -f ~/.ssh/HPC
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/sNumber/.ssh/HPC.
Your public key has been saved in /Users/sNumber/.ssh/HPC.pub.
The key fingerprint is:
SHA256:tEyXvo+HZgnIrnxSiZYyZ5ymw4lsLDTc9mBX/JgwQxw sNumber@PC040706-OSX
The key's randomart image is:

+---[RSA 2048]----+
|    . ==*oo.     |
| . . + =o+oo     |
|  o . oo+o= .    |
| . . .oo o..     |
|  ..o=.oS        |
|  .o+o*..        |
|. +o.... .       |
| +.o    . +      |
|++.    ..=E.     |
+----[SHA256]-----+
~~~
{: .bash}

### Move Your Key to the HPC

In order to use your keys to connect to the HPC, you'll need to first place it in a special file in your HPC home account called \"authorized_keys\". The easiest way to do this is simply with copy and paste.  Locate the **public** key with your GUI finder, open it with a text editor, and copy the entire contents. Return now to your Terminal which is logged-in to the HPC and input the following command. 

~~~
echo "[Paste Contents of Key Here]" >> ~/.ssh/authorized_keys
~~~
{: .bash}

We've succesfully (and securely) moved our public key to the HPC, now let's add it to the 'authorized_keys' file.  

Once this is done, logout of the HPC.  Then in your computer's Terminal enter the following command:

~~~
ssh sNumber@gc-prd-hpclogin1.rcs.griffith.edu.au -i ~/.ssh/HPC
~~~
{: .bash}

The `-i` flag tells SSH to use our key to login, and no password is needed.

For an even smoother connecting experience, open a text editor, create a blank file called 'config' in your .ssh directory.  Once you've done this, type the following parameters into your config file:

~~~
Host hpc
	HostName gc-prd-hpclogin1.rcs.griffith.edu.au
	User jcXXYYYY
	Port 8822
	IdentityFile ~/.ssh/HPC
~~~
{: .bash}

Now you can connect to the HPC by simply opening your Terminal and typing the command:
~~~
ssh hpc
~~~
{: .bash}