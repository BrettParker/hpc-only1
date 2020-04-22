---
title: "Transferring Files"
teaching: 30
exercises: 10
questions:
- "How do I upload/download files to the HPC cluster?"
objectives:
- "Be able to tranfer files to and from a HPC cluster."
keypoints:
- "`wget` downloads a file from the internet."
- "`sftp`/`scp` transfer files to and from your computer."
- "You can use an SFTP client like FileZilla to transfer files through a GUI."
---

Now we have everything we need to run our analysis, but before we can run anything on the HPC we need to copy our data and scripts across. This is something that people very frequently struggle with.
We'll cover several methods of doing this from the command line interface (CLI),
then cover how to do this using the graphical user interface (GUI, i.e. a point and click program) program FileZilla, 
which is much more straightforwards.

## File storage on the HPC
On the HPC you will have a home directory with 50gb of allocated space. The directory path is **/exports/home/sNumber**
You will also have a work space avaliable at **/scratch**. This directory is for reading and writing data associated with the submitted job. Data is deleted from the scratch directory after 1 week. The data that you generate on the HPC is not backed up, so you should save it somewhere else such as on <a href="https://www.griffith.edu.au/digital-solutions/research-storage" target="_blank">research space</a>


## Transferring single files and folders with scp

To copy a single file to or from the cluster, we can use `scp`.
The syntax can be a little complex for new users, 
but we'll break it down here:

To transfer *to* another computer:
```
scp /path/to/local/file.txt yourUsername@remote.computer.address:/path/to/remote/computer
```
{: .bash}

To download *from* another computer:
```
scp yourUsername@remote.computer.address:/path/on/remote/computer/file.txt /path/to/local/copy
```
{: .bash}

Note that we can simplify doing this by shortening our paths.
On the remote computer, everything after the `:` is relative to our home directory.
We can simply just add a `:` and leave it at that if we don't care where the file goes.

```
scp local-file.txt yourUsername@remote.computer.address:
```
{: .bash}

To recursively copy a directory, we just add the `-r` (recursive) flag:

```
scp -r some-local-folder/ yourUsername@remote.computer.address:target-directory/
```
{: .bash}

## Transferring files interactively with sftp

`scp` is useful, but what if we don't know the exact location of what we want to transfer?
Or perhaps we're simply not sure which files we want to tranfer yet.
`sftp` is an interactive way of downloading and uploading files.
To connect to a cluster, we use the command `sftp yoursNumber@remote.server.address`.
This will start what appears to be a bash shell (though our prompt says `sftp>`).
However we only have access to a limited number of commands.

We can see which commands are available with `help`:
```
help
```
{: .bash}
```
Available commands:
bye                                Quit sftp
cd path                            Change remote directory to 'path'
chgrp grp path                     Change group of file 'path' to 'grp'
chmod mode path                    Change permissions of file 'path' to 'mode'
chown own path                     Change owner of file 'path' to 'own'
df [-hi] [path]                    Display statistics for current directory or
                                   filesystem containing 'path'
exit                               Quit sftp
get [-afPpRr] remote [local]       Download file
reget [-fPpRr] remote [local]      Resume download file
reput [-fPpRr] [local] remote      Resume upload file
help                               Display this help text
lcd path                           Change local directory to 'path'
lls [ls-options [path]]            Display local directory listing
lmkdir path                        Create local directory
ln [-s] oldpath newpath            Link remote file (-s for symlink)
lpwd                               Print local working directory
ls [-1afhlnrSt] [path]             Display remote directory listing

# omitted further output for brevity
```
{: .output}

Notice the presence of multiple commands that make mention of local and remote.
We are actually connected to two computers at once (with two working directories!).

To show our remote working directory:
```
pwd
```
{: .bash}
```
Remote working directory: /global/home/yourUsername
```
{: .output}

To show our local working directory, we add an `l` in front of the command:

```
lpwd
```
{: .bash}
```
Local working directory: /home/jeff/Documents/teaching/hpc-intro
```
{: .output}

The same pattern follows for all other commands:

* `ls` shows the contents of our remote directory, while `lls` shows our local directory contents.
* `cd` changes the remote directory, `lcd` changes the local one.

To upload a file, we type `put some-file.txt` (tab-completion works here).

```
put config.toml
```
{: .bash}
```
Uploading config.toml to /global/home/yourUsername/config.toml
config.toml                                   100%  713     2.4KB/s   00:00 
```
{: .output}

To download a file we type `get some-file.txt`:

```
get config.toml
```
{: .bash}
```
Fetching /global/home/yourUsername/config.toml to config.toml
/global/home/yourUsername/config.toml                               100%  713     9.3KB/s   00:00 
```
{: .output}

And we can recursively put/get files by just adding `-r`.
Note that the directory needs to be present beforehand.

```
mkdir content
put -r content/
```
{: .bash}
```
Uploading content/ to /global/home/yourUsername/content
Entering content/
content/scheduler.md              100%   11KB  21.4KB/s   00:00    
content/index.md                  100% 1051     7.2KB/s   00:00    
content/transferring-files.md     100% 6117    36.6KB/s   00:00    
content/.transferring-files.md.sw 100%   24KB  28.4KB/s   00:00    
content/cluster.md                100% 5542    35.0KB/s   00:00    
content/modules.md                100%   17KB 158.0KB/s   00:00    
content/resources.md              100% 1115    29.9KB/s   00:00    
```
{: .output}

To quit, we type `exit` or `bye`. 

## Transferring files to the HPC with WinSCP

WinSCP is a cross-platform client for securly downloading and uploading files to and from a remote computer. Files can be moved using ftp, ftps, scp, sftp, WebDAV or S3 file transfer protocols.

<a href="https://winscp.net/download/WinSCP-5.15.9-Setup.exe" target="_blank">Download</a> and install the WinSCP client.

After installation, Click on:
Start -> All Programs -> WinSCP --> WinSCP
Click on "new"

![winscp1](../files/winscp1.jpg)

For the hostname, type: "gowonda.rcs.griffith.edu.au"
User name: yoursNumber e.g. s1234567
Password: Leave it blank for now

Leave everything else as it is.

Click on login button
If it is the first time you are logging into this server, it will prompt you to agree to add the ssh keys into local cache. (Click YES).

Next it will prompt for password.

![winscp2](../files/winscp2.jpg)

If the login is successful, it will provide a window with two panes.
The left hand pane is the local file system (your local drive) and the right hand pane is the remote file system on the rcsxfer machine.
(Click yes to login).

![winscp3](../files/winscp3.jpg)

Simply click on the drop down window to navigate to other folders on the local drive.

![winscp4](../files/winscp4.jpg)

To transfer files, simply drag and drop the files between the two panes.


> ## Transferring files
> Using one of the above methods, try transferring files to and from the cluster.
> Which method do you like the best?
{: .challenge}

> ## Working with Windows
> When you transfer files to from a Windows system to a Unix system 
> (Mac, Linux, BSD, Solaris, etc.) problems can occur.
> Windows encodes its files slightly different than Unix,
> and adds an extra character to every line.
> 
> On a Unix system, every line in a file ends with a `\n` (newline).
> On Windows, every line in a file ends with a `\r\n` (carriage return + newline).
> This causes problems sometimes.
> 
> Though most modern programming languages and software handles this correctly,
> in some rare instances, you may run into an issue.
> The solution is to convert a file from Windows to Unix encoding with the `dos2unix` command.
> 
> You can identify if a file has Windows line endings with `cat -A filename`.
> A file with Windows line endings will have `^M$` at the end of every line.
> A file with Unix line endings will have `$` at the end of a line.
> 
> To convert the file, just run `dos2unix filename`.
> (Conversely, to convert back to Windows format, you can run `unix2dos filename`.)
{: .callout}

> ## A note on ports
> All file tranfers using the above methods use encrypted communication over port 22.
> This is the same port used by SSH.
> In fact, all file transfers using these methods occur through an SSH connection.
> If you can connect via SSH over the normal port, you will be able to transfer files.
> If your cluster uses a non-standard port, you'll need to change the port for sftp/scp 
> as well.
{: .callout}
