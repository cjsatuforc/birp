Big Iron Recon & Pwnage (BIRP)
==============================
by @singe

Overview
--------

BIRP is a tool that will assist in the security assessment of mainframe applications served over TN3270. Much like what BURP and other web application proxies do for web application assessments, BIRP aims to do the same for TN3270 application assessments. And, much like with web applications, being able to see and modify fields that the application developer assumed were neither visible nor modifiable allows security assumptions be bypassed.

In particular, BIRP provides two capabilities for the aspiring TN3270 hacker. The first is that it shows all the data returned by the application in the screen. This includes hidden fields. The second is that it allows fields marked as "protected" aka "non modifiable" to be modified. Depending on how the application has been developed, this can allow application functionality to be modified.

Running
-------

./birp.py -h will give you startup help if you want to get running.

All you need is to specify a target with -t . Target specification can include a port with a : after the IP e.g. 10.10.10.10:1023. If no port is specified it will default to :23 as per x3270 default behaviour.

You can use -l to load a previously saved history file into the history. You must always specify a target and cannot just view history yet unfortunately.

Check the pre-requisites below for installing. Unfortunately, this will only run in Unix environments at the moment, no Windows support.

Functionality
-------------

Currently, BIRP has a fairly limited set of functionality. These are:

* Interactive Mode

Interactive mode is the heart of BIRPs functionality. It will pass keypresses and other commands from BIRP to x3270 and allow the analyst to interact with the application as they would if they were using x3270 directly. However, it will also display the marked up "hacker view" of each screen returned, as well as record "transactions" and store it in the proxy history for later analysis and inspection.

In interactive mode hitting Ctrl-h will print a help screen, Ctrl-k will display a color key, and ESC will exit back to the menu.

* View History

This will display the history of all transactions BIRP recorded, and allow them to be inspected. Specifically it provides access to the screen submitted, the fields that were modified in that screen (i.e. the data submitted) and the response.

For each screen, only the first row is displayed as context, but the full screen can be printed if you view the transaction.

Also, you can drop into python and examine the screen object directly.

* Save History

You can save your history to a file, and load it again later with the -l switch on the command line. You need to save it to a unique filename.

Pre-requisites:
---------------

* Python libraries: py3270, colorama, IPython
These can be installed with pip or easy_install

* Hacked x3270 client
The patch is included. You can download the source at http://x3270.bgp.nu/download.html then cd to the x3270 directory once extracted, and patch -p1 < x3270-hack.patch
You can use an unmodified client, but then you will not be able to edit protected fields.

By dominic () sensepost.com (@singe)
