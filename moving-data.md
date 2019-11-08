## Moving and Downloading Data

So far, we've worked with data that is pre-loaded on the instance in the cloud. Usually, however,
most analyses begin with moving data onto the instance. Below we'll show you some commands to 
download data onto your instance, or to move data between your computer and the cloud.

### Getting data from the cloud

There are two programs that will download data from a remote server to your local
(or remote) machine: ``wget`` and ``curl``. They were designed to do slightly different
tasks by default, so you'll need to give the programs somewhat different options to get
the same behaviour, but they are mostly interchangeable.

 - ``wget`` is short for "world wide web get", and it's basic function is to *download*
 web pages or data at a web address.

 - ``cURL`` is a pun, it is supposed to be read as "see URL", so its basic function is
 to *display* webpages or data at a web address.

Which one you need to use mostly depends on your operating system, as most computers will
only have one or the other installed by default.

Let's say you want to download some data from Ensembl. We're going to download a very small
tab-delimited file that just tells us what data is available on the Ensembl bacteria server.
Before we can start our download, we need to know whether we're using ``curl`` or ``wget``.

To see which program you have, type:
 
~~~
$ which curl
$ which wget
~~~
{: .bash}

``which`` is a BASH program that looks through everything you have
installed, and tells you what folder it is installed to. If it can't
find the program you asked for, it returns nothing, i.e. gives you no
results.

On Mac OSX, you'll likely get the following output:

~~~
$ which curl
~~~
{: .bash}

~~~
/usr/bin/curl
~~~
{: .output}

~~~
$ which wget
~~~
{: .bash}

~~~
$
~~~
{: .output}

This output means that you have ``curl`` installed, but not ``wget``.

Once you know whether you have ``curl`` or ``wget``, use one of the
following commands to download the file:

~~~
$ cd
$ wget ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
~~~
{: .bash}

or

~~~
$ cd
$ curl -O ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
~~~
{: .bash}

Since we wanted to *download* the file rather than just view it, we used ``wget`` without
any modifiers. With ``curl`` however, we had to use the -O flag, which simultaneously tells ``curl`` to
download the page instead of showing it to us **and** specifies that it should save the
file using the same name it had on the server: species_EnsemblBacteria.txt

It's important to note that both ``curl`` and ``wget`` download to the computer that the
command line belongs to. So, if you are logged into AWS on the command line and execute
the ``curl`` command above in the AWS terminal, the file will be downloaded to your AWS
machine, not your local one.

### Moving files between your laptop and your instance

What if the data you need is on your local computer, but you need to get it *into* the
cloud? There are also several ways to do this, but it's *always* easier
to start the transfer locally. **This means if you're typing into a terminal, the terminal
should not be logged into your instance, it should be showing your local computer. If you're
using a transfer program, it needs to be installed on your local machine, not your instance.**

## Transferring Data Between your Local Machine and the Cloud

These directions are platform specific, so please follow the instructions for your system:

**Please select the platform you wish to use for the exercises: <select id="id_platform" name="platformlist" onchange="change_content_by_platform('id_platform');return false;"><option value="unix" id="id_unix" selected> UNIX </option><option value="win" id="id_win" selected> Windows </option></select>**



<div id="div_unix" style="display:block" markdown="1">

### Uploading Data to your Virtual Machine with scp

`scp` stands for 'secure copy protocol', and is a widely used UNIX tool for moving files
between computers. The simplest way to use `scp` is to run it in your local terminal,
and use it to copy a single file:

~~~
scp <file I want to move> <where I want to move it>
~~~
{: .bash}

Note that you are always running `scp` locally, but that *doesn't* mean that
you can only move files from your local computer. In order to move a file from your local computer to an AWS instance, the command would look like this:

~~~
$ scp <local file> <AWS instance>
~~~
{: .bash}

To move it back to your local computer, you re-order the `to` and `from` fields:

~~~
$ scp <AWS instance> <local file>
~~~
{: .bash}

#### Uploading Data to your Virtual Machine with scp

Open the terminal and use the `scp` command to upload a file (e.g. local_file.txt) to the dcuser home directory:

~~~
$  scp local_file.txt dcuser@ip.address:/home/dcuser/
~~~
{: .bash}

#### Downloading Data from your Virtual Machine with scp

Let's download a text file from our remote machine. You should have a file that contains bad reads called ~/shell_data/scripted_bad_reads.txt.

**Tip:** If you are looking for another (or any really) text file in your home directory to use instead, try:

~~~
$ find ~ -name *.txt
~~~
{: .bash}


Download the bad reads file in ~/shell_data/scripted_bad_reads.txt to your home ~/Download directory using the following command **(make sure you substitute dcuser@ip.address with your remote login credentials)**:

~~~
$ scp dcuser@ip.address:/home/dcuser/shell_data/untrimmed_fastq/scripted_bad_reads.txt ~/Downloads
~~~
{: .bash}

Remember that in both instances, the command is run from your local machine, we've just flipped the order of the to and from parts of the command.
</div>


<div id="div_win" style="display:block" markdown="1">

### Uploading Data to your Virtual Machine with PSCP

If you're using a PC, we recommend you use the *PSCP* program. This program is from the same suite of
tools as the PuTTY program we have been using to connect.

1. If you haven't done so, download pscp from [http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe](http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe)
2. Make sure the *PSCP* program is somewhere you know on your computer. In this case,
your Downloads folder is appropriate.
3. Open the windows [PowerShell](https://en.wikipedia.org/wiki/Windows_PowerShell);
go to your start menu/search enter the term **'cmd'**; you will be able to start the shell
(the shell should start from C:\Users\your-pc-username>).
4. Change to the Downloads directory:

~~~
> cd Downloads
~~~
{: .bash}

5. Locate a file on your computer that you wish to upload (be sure you know the path). Then upload it to your remote machine **(you will need to know your AMI instance address (which starts with ec2), and login credentials)**. You will be prompted to enter a password, and then your upload will begin. **(make sure you substitute 'your-pc-username' for your actual pc username and 'ec2-54-88-126-85.compute-1.amazonaws.com' with your AMI instance address)**

~~~
C:\User\your-pc-username\Downloads> pscp.exe local_file.txt dcuser@ec2-54-88-126-85.compute-1.amazonaws.com:/home/dcuser/
~~~
{: .bash}

### Downloading Data from your Virtual Machine with PSCP

1. Follow the instructions in the Upload section to download (if needed) and access the *PSCP* program (steps 1-3)
2. Download the text file using the following command **(make sure you substitute 'your-pc-username' for your actual pc username and 'ec2-54-88-126-85.compute-1.amazonaws.com' with your AMI instance address)**

~~~
C:\User\your-pc-username\Downloads> pscp.exe dcuser@ec2-54-88-126-85.compute-1.amazonaws.com:/home/dcuser/shell_data/untrimmed_fastq/scripted_bad_reads.txt.

C:\User\your-pc-username\Downloads
~~~
{: .bash}

</div>
