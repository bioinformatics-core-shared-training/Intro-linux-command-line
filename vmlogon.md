### How to log onto the courses Virtual machine from your Mac or Windows computer

1.



## Important Note

This lesson covers how to log into, and out of, an virtual machine instance.

## Background to the Virtual Machine

To save time, your instructor launched a remote computer (instance) for you prior
to the workshop, and connected it to our lesson data. 

To access the pre-configured workshop data, you'll need to use our log-in credentials (user name and password). These
credentials will be supplied by your instructor.

But first, you need a place to log *into*! To find the instance that's attached to that data,
you'll need something called an IP address. Your instructor should have given this to you
at the beginning of the workshop.

An IP address is essentially the numerical version of a web address like www.amazon.com

## Connection Protocols

We will use a protocol called Secure Shell (SSH) that, as the name implies, provides you
with a secure way to use a [shell](http://swcarpentry.github.io/shell-novice). In our case,
the shell will be running on a remote machine. This protocol is available for every
operating system, but sometimes requires additional software.

## Logging onto a virtual machine

#### Connecting using Windows PC

*Prerequisites*: You must have an SSH client. There are several free options but you should have installed [PuTTY.exe](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) at the begining of the workshop, and we're going to continue using that.


1. Open PuTTY
2. Paste in the 'Host Name (or IP address)' section the IP address provided by your instructor (or the IP address of an instance you have provisioned yourself)

    *Keep the default selection 'SSH' and Port (22)*

    ![](../fig/putty_screenshot_1.png)

2. Click 'Open' 
    
    You will be presented with a security warning

    ![](../fig/putty_screenshot_2.png)

3. Select 'Yes' to continue to connect
3. In the final step, you will be asked to provide a login and password
    
    **Note:** When typing your password, it is common in Unix/Linux not see any asterisks (e.g. `****) or moving cursors. Just continue typing

    ![](../fig/putty_screenshot_3.png)

You should now be connected!


#### Connecting using Mac/Linux

Mac and Linux operating systems will already have terminals installed. 

1. Open the terminal

    Simply search for 'Terminal' and/or look for the terminal icon

    ![terminal icon](../fig/terminal.png)

2. Type the following command substituting `ip_address` by the IP address your instructor will provide (or the IP address of an instance you have provisioned yourself)

    ~~~
    $ ssh dcuser@ip_address
    ~~~
    {: .bash}

    *Be sure to pay attention to capitalization and spaces*

3. You will receive a security message that looks something like the message below

    ~~~
    The authenticity of host 'ec2-52-91-14-206.compute-1.amazonaws.com (52.91.14.206)' can't be established.
    ECDSA key fingerprint is SHA256:S2mMV8mCThjJHm0sUmK2iOE5DBqs8HiJr6pL3x/XxkI.
    Are you sure you want to continue connecting (yes/no)?
    ~~~
    {: .bash}

4. Type `yes` to proceed
5. In the final step, you will be asked to provide a login and password
    
    **Note:** When typing your password, it is common in Unix/Linux not see any asterisks (e.g. `****`) or moving cursors. Just continue typing.

You should now be connected!


## Logging off a virtual machine

Logging off your instance is a lot like logging out of your local computer: it stops any processes
that are currently running, but doesn't shut the computer off. 

To log off, use the `exit` command in the same terminal you connected with. This will close the connection, and your terminal will go back to showing your local computer:

~~~
dcuser@ip-172-31-62-209 $ exit

Amandas-MacBook-Pro-3 $
~~~
{: .bash}

## Logging back in

Internet connections can be slow or unstable. If you're just browsing the internet, that means you have
reload pages, or wait for pictures to load. When you're working in cloud, that means you'll sometimes
be suddenly disconnected from your instance when you weren't expecting it. Even on the best internet
connections, your signal will occasionally drop, so it's good to know the above SSH steps, and be able
to log into our VM without looking up the instructions each time.

In the next section, we'll also show you some programs that you can use to keep your processes going
even if your connection drops. But for now, just practice logging on and off a few times.
