---
title: "Bash cheat sheet"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---


## Useful Unix Commands
* **cd *dir*** -- used to change directory *directory to change to*
* **pwd** -- print the current working directory
* **ls *dir*** -- list all contents (i.e. files and sub-directories) within the directory. the -a flag is used to see invisible dot files (.) such as .git. *dir* a directory can be added if you would like to list files in a directory different to you working directory
* **echo** -- displays (i.e. will print out in terminal) a text/string passed into the command line as an argument
* **touch *dir*** -- Creates a new empty file. _dir/file name_ the name of the directory and new file name. 
* **cp _source_ _destination_** -- Create a copy of a file and save it to another directory. _source_ is where the file currently is and _destination_ is where it will be copied to.
* **scp _local dir/file name_ _remote host name dir/file name_** -- securely copy a file or directory to a remote computer. _local dir/file name_ the directory and file name to be moved. _remote host name dir/file name_ the remote hosts domain directory and file name while it will be moved to.
* **sftp** secure file transfer program
* **mv _source_ _destination_** -- Move a file to another directory, the file will not be in the _source_ directory after this command is run. _source_ is where the file currently is and _destination_ is where it will be moved to.
* **rm _dir/file name_** -- Remove a file. _dir/file name_ add the directory path and file name to be removed. This cannot be undone - it will get completely deleted from your computer.
* **rmdir _dir_** -- Remove a directory. _dir_ add the directory path to be removed. This cannot be undone - it will get completely deleted from your computer.
* **cat** -- read files sequentially and write them to a single standard output
* **exit** -- type exit then ENTER into terminal to exit the HPC 


## Common Shortcuts  
**Home Directory** -- the tilda symbol "~" represents your home directory, e.g. /homeN/XX/jcXXYYY  
**Current Directory** -- a single full-stop "." represents your current working directory, e.g. same directory returned by `pwd`  
**Parent Directory** -- a double full-stop ".." represents the *parent* of your current working directory  
**Root Directory** -- on it's own, a single forwardslash "/" represents the root directory, e.g. the bottom of the directory *tree*  
**New Directory** -- between two words, a forwardslash "/" represents a new directory, e.g. in this situation "/homeN/XX/" the directory "XX" is contained within the directory "homeN"  
**Up & Down Arrows** -- use these keys to navigate through your command history  
**Tab Key** -- performs *autocompletion* of commands, directory paths & file paths  
**Escape Character** -- a single backslash "\" is used to 'escape' special characters, such as spaces, ampersands & apostrophes  
**Environment Variables** -- when you open your shell, a number of pre-saved variables, so called 'environment' variables are set for you. You can view them all by executing the command `printenv`, and access individual variables by prefacing their name with a "$", e.g. $USER or $HOSTNAME.  
**Wildcards** -- the asterisk symbol "*" can be used to represent a string of characters of non-zero length; most commonly you can integrate an '\*' into other commands to create search patterns.  For example, `ls *zip` will display all files and directories that end with "zip", regardless of the leading characters. 
> **Skip to beginning of command** --  Click control+A to move the cursor from the end of the command to the begining
{: .callout}



## Grabbing files from the internet

For downloading files directly from the Linux command line, there are two utilities that immediately come to mind:
 wget and cURL. 
They share a lot of features and can easily get many of the same tasks accomplished. Though they share similar features they aren't exactly the same. These programs fit slightly different roles and use cases, and do have traits that make each better for certain situations.

wget is simple and straightforward. It’s meant for quick downloads, and it’s excellent at it. wget is a single self-contained program. 

The syntax is relatively straightforward: `wget https://some/link/to/a/file.tar.gz`

wget has the ability to download recursively. For example, wget allows you to download everything on a page or all of the files in an FTP directory at once.

You can include both wget and cURL in your Bash scripts to automatically interact with online content and retrieve what you need.

cURL is a multi-tool which support a wide range of protocols including HTTP, HTTPS, FTP in both directions, LDAP and even Samba shares. You can actually use cURL to send and retrieve email. cURL has some nifty security features providing support of the SSL/TLS libraries, use of proxies using SOCKS, etc. cURL also supports gzip compression to send large amounts of data more easily.

The syntax is as straightforward: `curl https://some/link/to/a/file.tar.gz`

You can think of cURL like a stripped-down command line web browser. It supports just about every protocol you can think of and can access and interact with nearly all online content. The only is that a browser renders the responses that it receives, and cURL doesn’t.

> ## Downloading the Drosophila genome
> The *Drosophila melanogaster* reference genome is located at the following website:
> [http://metazoa.ensembl.org/Drosophila_melanogaster/Info/Index](http://metazoa.ensembl.org/Drosophila_melanogaster/Info/Index).
> Download it to the cluster with `wget`.
>
> Some additional details:
>
> * You want to go get the genome through the "Download DNA Sequence" link
> * We are interested in the `Drosophila_melanogaster.BDGP6.dna.toplevel.fa.gz` file.
{: .challenge}

> ## Working with compressed files, using unzip and gunzip
> 
> The file we just downloaded is gzipped (has the `.gz` 
> extension).
>You can uncompress it with `gunzip filename.gz`.
>
## Download internet files using the CLI

To download files from the internet, 
the absolute best tool is `wget`.
The syntax is relatively straightforwards: `wget https://some/link/to/a/file.tar.gz`

>File decompression reference:
>
>* **.tar.gz** - `tar -xzvf archive-name.tar.gz`
>* **.tar.bz2** - `tar -xjvf archive-name.tar.bz2`
>* **.zip** - `unzip archive-name.zip`
>* **.rar** - `unrar archive-name.rar`
>* **.7z** - `7z x archive-name.7z`
>
>However, sometimes we will want to compress files 
>ourselves to make file transfers easier.
>The larger the file, the longer it will take to 
>transfer. 
>Moreover, we can compress a whole bunch of little 
>files into one big file to make it easier
>on us (no one likes transferring 70000) little files!
>
>The two compression commands we'll probably want to 
>remember are the following:
>
>* Compress a single file with Gzip - `gzip filename`
>* Compress a lot of files/folders with Gzip - `tar -czvf archive-name.tar.gz folder1 file2 folder3 etc`
> 
{: .callout}
