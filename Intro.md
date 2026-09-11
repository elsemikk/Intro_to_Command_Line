



# Anatomy of the Command Line

# Directories and paths

# Running commands - basic navigation commands

To run a command, type or paste the command into the command prompt, and then hit enter.

Here we will go over some of the most-commonly used commands: commands for getting around on the command line.
`pwd` - print current working directory
`ls` - lists the contents of your current working directory
`mkdir` - makes a new directory
`cd` - change to a new directory

First, find out where you are in your computer's filesystem using the `pwd` command ("print working directory"). This will print text as output in the next line of your console. This printed output text is called "standard output". The standard output of `pwd` will be the full path from the root of your computer's filesystem down to your current working directory. When you run commands, your working directory is the default place where your computer will look for input files, and is the default place where output files appear.  

To find out what is in your working directory, type `ls` into your command prompt, then hit "enter". The text that pops up in your terminal (the "standard output" of `ls`) is a list of all the files in your current working directory. 

Next, let's move around the filesystem. We can do this using the `cd` ("change directory") command. To use it, type `cd` followed by a space, then the name/path of the directory you want to move to. If the directory you want to move to is in your current working directory, you can just give the name of the directory. If it is somewhere else, you will have to specify the path to that directory. Let's move into the directory for this tutorial. If you downloaded the tutorial folder manually, you will need to know where on your computer it ended up. 

Now that we are in the tutorial directory, let's start by making a new directory. We can make a directory using the `mkdir` command: just type `mkdir` followed by a space, then the name of the new directory. For example, run:  
`mkdir test`  
If you now run `ls`, you will see a new directory named `test`. Let's enter this directory:  
`cd test`  


* Commands are very sensitive to the presence of spaces. If you have a space in the name of a file/directory, it can cause huge headaches as bash will see the space-separated chunks as separate things, not parts of the same name. If you must deal with files/directories with spaces in the name, enclose the name in quotes (eg "Name of file").
* Different types of quotes are interpreted differently. Single and double quotes mean different things, and critically, curly quotes will cause errors. Spot the difference: `" vs ' vs “ vs ‘`. When you are writing code, make sure you are using a *plain text editor* or code editor instead of a *rich text editor* that will make your quotes curly. Plain text editors include [Visual Studio Code](https://code.visualstudio.com/) and [Sublime Text](https://www.sublimetext.com/). Examples of rich text editors (avoid!) include Microsoft Word and Google Docs. 
* Unlike an interactive text editor, you can't use your mouse to click to move the text cursor. If you made a typo and need to go back, you have to use your arrow keys to move the cursor backwards.
* Time saver: in many systems, you can press ctrl+a to jump your cursor to the start of the line, and then ctrl+e to jump back to the end of the line. Saves some time if you made a typo way at the beginning of the line!

