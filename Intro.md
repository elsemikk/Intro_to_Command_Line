# Intro to bash for bioinformatics - getting started on the command line  
by Else Mikkelsen, Bioinformatics postdoc at the Biodiversity Research Centre, University of British Columbia  
Last updated: September 2026  

Welcome! This workshop is designed to provide an entry into using the command line and building pipelines in bash. It is designed to start from the beginning and require no prior experience on the command line, while  providing enough tips and tricks to remain useful to users with an intermediate level of experience.  

**This workshop is currently a work-in-progress - some sections have not yet been written**

# Day 1: Navigating the command line  

## Anatomy of the Command Line  

### broad overview and terms  
Most of the time when using computers, we are using a **graphical user interface** (GUI), something that lets us point our mouse and click on buttons or browse through menus. A more direct way of communicating with the computer is through the **command line**, where you type lines of text containing commands for the computer. To use the command line, you need a program called a **shell** to interpret your commands, and the most popular shell used in bioinformatics (and more widely) is **bash**. Bash is used with Linux and UNIX operating systems, and also comes installed on macs. To use the shell, you need an application referred to as a **terminal**. The terminal is the application you open and interact with, the command line is where you type your commands, and the shell (bash) is the program that interprets your commands and tells your operating system what to do.  

Here, we will go over the basics of working on the command line and writing simple bash code. This requires you to have access to a terminal program with bash. Accessing that varies depending on your operating system. In practice, most bioinformatics work is done on a server accessed remotely, rather than done locally on a laptop. In this workshop, we will be working on a Linux server - the instructions will have been emailed to you ahead of time, and we will spend the first few minutes making sure you are logged in.   

Here are general instructions for getting into a terminal:  
*Linux* if you are on Linux, you should already have an application called Terminal, which can be opened from your applications, or with `ctrl + alt + t`.  
*Mac* if you are on Mac, you should have an application called Terminal. It is often located in your `Applications/Utilities` subfolder; [this page](https://support.apple.com/en-ca/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) from Apple explains more about how to open it on different MacOs versions if you are having trouble locating it. Note that the default shell that comes with newer macs is not bash, it is zsh - it is extremely similar, so almost all of the code in this tutorial will work the same, but if you do more complicated things you may notice a difference.  
*Windows* Windows doesn't come with bash, so you will need to install it yourself. One popular option is [git bash](https://gitforwindows.org/). Alternatively, you can just `ssh` into a server if you have access to one.  

Once you have your Terminal open, you will a screen with some text on it that should look something like this:  

<img width="1019" height="644" alt="image" src="https://github.com/user-attachments/assets/80226990-1bd3-4b14-b8f4-39223d0228c5" />

The colours may be different - those can be customized - but it should look similar. On the bottom line, it will show you username and IP address of server name separated by "@", then a ":" symbol, then the directory you are in (usually a "~" symbol when you first start up - explained below), and finally a "$" symbol. Next to the `$` is the command prompt where you type/paste commands.  

# Directories and paths  

Before we get started, lets go over a couple more pieces of computer jargon - **directories** and **paths**. A directory is more-or-less the more technical term for a folder. All files on a computer are located within a directory, and directories are organized in a nested hierarchy. The top-most level of the nested hierarchy is called the **root** (eg, `C:\` on Windows or `/` on Linux), and other directories branch off from the root. The list of nested directories from the root to a given file is called the file's **path**. For example, the path to the Downloads directory on my laptop is `/Users/else/Downloads` (`Downloads` is nested within my `else` directory, which is nested within my `Users` directory, which is nested within my root directory (`/`).  

One special path is your home directory. This can be represented with the shortcut `~` (the "tilde"), and is usually the directory that you start out in when opening a new terminal.  

# Running commands - basic navigation commands  

To run a command, type or paste the command into the command line, and then hit enter.  

Here we will go over some of the most-commonly used commands: commands for getting around on the command line.  
* `pwd` - print current working directory  
* `ls` - lists the contents of your current working directory  
* `mkdir $name_of_directory` - makes a new directory  
* `cd $name_of_directory` - change to a new working directory  
* `rmdir $name_of_directory` - remove (delete) an empty directory 
* `man $name_of_command` - open the manual for a command (then press "q" to quit the manual)

(in the above list, the variables starting with $ are placeholders I wrote which you will replace when writing your command - don't include those `$` symbols)

First, find out where you are in your computer's filesystem using the `pwd` command ("print working directory"). This will print text as output in the next line of your terminal. This printed output text is called "standard output". The standard output of `pwd` will be the full path from the root of your computer's filesystem to your current working directory. When you run commands, your working directory is the default place where your computer will look for input files, and is the default place where output files appear.  

To find out what is in your working directory, type `ls` into your command prompt, then hit "enter". The text that pops up in your terminal (the "standard output" of `ls`) is a list of all the files in your current working directory.  

Next, let's move around the filesystem. We can do this using the `cd` ("change directory") command. To use it, type `cd` followed by a space, then the name/path of the directory you want to move to. If the directory you want to move to is in your current working directory, you can just give the name of the directory. If it is somewhere else, you will have to specify the path to that directory. Let's move into the directory for this tutorial. If you downloaded the tutorial folder manually, you will need to know where on your computer it ended up.  

`cd Intro_2_command_line`  

Now that we are in the tutorial directory, let's start by making a new directory. We can make a directory using the `mkdir` command: just type `mkdir` followed by a space, then the name of the new directory. For example, run:  
`mkdir test`  
If you now run `ls`, you will see a new directory named `test`. Let's enter this directory:  
`cd test`  
If you run `ls`, you should see nothing - we are just in an empty directory that we just created. Let's go back up. There are a few ways we can do this. We could specify the whole path to the folder above us. Alternatively, we could use a handy shorthand. In bash, a single dot `.` stands for your current working directory. If you run `cd .` nothing will happen - you will change directories to the directory you are already in. Two dots `..` stands for the directory just above your working directory. Run:  
`cd ..`  
That should bring you back up to the directory we were just in. You can stack these together, for example `cd ../../..` to go up three levels. You can also use them to navigate to other folders relative to your working directory. For example `cd ../raw_data` to go up one level and then down into a directory called `raw_data`.  
One last `cd` trick: You can use `cd -` as shorthand to go back to your previous working directory, a handy shortcut if you find yourself constantly needing to move back and forth between two directories.  

At this point, make sure you are back in the main tutorial directory. Let's delete that test folder we just made. You can delete directories using the `rmdir` command. Run it like this:  
`rmdir test`.  
If you run `ls`, you should now see that the test directory is gone. Careful! There is no "undo" on the command line. Luckily, `rmdir` will refuse to delete a directory that is not empty.  

Now let's move on to some slightly more complex commands. Before we do, here are some important general tips for running commands on the command line:  
* Commands are very sensitive to the presence of spaces. If you have a space in the name of a file/directory, it can cause huge headaches as bash will see the space-separated chunks as separate things, not parts of the same name. If you must deal with files/directories with spaces in the name, enclose the name in quotes (eg "Name of file"). As best practice though, don't include spaces in the name of any file or directory - instead_you_can_experiment_with_underscores, or.you.can.try.using.dots, OrYouCanTryWritingInCamelCase.  
* Different types of quotes are interpreted differently. Single and double quotes mean different things, and critically, curly quotes will cause errors. Spot the difference: `" vs ' vs “ vs ‘`. When you are writing code, make sure you are using a *plain text editor* or code editor to use straight quotes instead of a *rich text editor* that will make your quotes curly. Plain text editors include [Visual Studio Code](https://code.visualstudio.com/) and [Sublime Text](https://www.sublimetext.com/). Examples of rich text editors (avoid!) include Microsoft Word and Google Docs.
* Rich text editors will also add invisible characters called "carriage returns". You will not be able to see these in your document, but the command line sure can! These invisible characters break code and cause major headaches; using a plain text editor will avoid that problem.  
* Unlike an interactive text editor, you can't use your mouse to click to move the text cursor. If you made a typo and need to go back, you have to use your arrow keys to move the cursor backwards. (Exception: Macs often let you point-and-click to move your cursor - just hold down the `option` key when you click.  
* Time saver: in many systems, you can press ctrl+a to jump your cursor to the start of the line, and then ctrl+e to jump back to the end of the line. Saves some time if you made a typo way at the beginning of the line!  
* to get help with a command or remind yourself of its flags, you can use the `man` command to open the command's manual page. For example, to open the manual for `mkdir`, do `man mkdir`. To exit the manual and return to the command line, type `q` to quit.  

## Flags  
An important aspect of running commands on the command line is setting flags. These are settings that can alter the behaviour of the command you are running. They are usually single letters or short words, that are placed after a command (separated by a space), like this: `command -a -b -c --flag_d`. That command has four flags: `-a`, `-b`, `-c`, and `--flag_d`. Flags are attached to dashes - generally a single dash for single-letter flags or two dashes for flags that are words. If a flag is a word, it cannot have a space in it (instead, underscores `_` can be used). Often, there will be two synonymous flags you can choose between that do the same thing, a single-letter option for brevity, or a short-word option you can use to make it easier to remember what it does when you go back and read your code in the future.  

The other thing we have given some commands is/are argument(s). These are also settings that alter the action of the command you are running or the flag you set - they are often the name of input files or output files, or parameters that you need to change/specify for the program you are running. These are distinguished from flags because they are not preceded by dashes. Sometimes arguments are required (eg, `mkdir` would not have anything to do if you didn't tell it the name of the directory it should make), and sometimes they are not required (eg, `ls` defaults to listing your current working directory if you don't give it any arguments).  

Let's add some flags to `ls`. If we just run `ls`, it will tell us the contents of our current working directory. If we add  the flag `-l` and run `ls -l`, it will now give us a more lengthy summary of our files, including handy information like the size of our files, which user owns them, and date/time when they were last modified. Let's now add another flag, `-h`: `ls -l -h` or `ls -lh` (for single-letter flags, you can either give each flag their own dash, or smoosh them together behind the same dash, whatever style looks best to you). `-h` stands for "human-readable", and will convert the file sizes from number of bytes to abbreviations (K for Kilobyte, M for Megabyte, etc).   

# Looking at files

Now we will look at some important commands for reading and manipulating files:  
* `cat` - read a file (or text input on the command line) and print the contents
* `cp` - copy a file  
* `mv` - move (and possibly rename) a file  
* `rm` - remove (permanently delete) a file  
* `less` - look at a file on the command line (without printing anything). Press `q` when done looking. 
* `head` - print only the first lines of a file  
* `tail` - print only the last lines of a file  
* `wc` - count the number of lines/words/characters  
* `cut` - print only specific column(s) from a file  
* `sort` - sort input  
* `uniq` - remove repeated lines (if they are adjacent)  
* `paste` - merge files horizontally (paste columns together line-by-line)  

The first command we will look at is `cat`, which stands for "concatenate". This is a handy and frequently-used command that reads contents of a file and prints them out. The most simple way to run it is `cat $Name_of_file`. Let's try it:  
`cat ABBABABA1.txt`  
That will print the contents of the file `ABBABABA1.txt`.  
`cat` can also take multiple files as input and concatenate them together in the order they are listed. For example:  
`cat ABBABABA1.txt ABBABABA2.txt`  
That will print the contents of `ABBABABA1.txt` and then the contents of `ABBABABA2.txt`.  
Often, we need to save this output, rather than just printing it to the command line. We can redirect it to a file using the `>` symbol to point to a file where the output should be printed. This could be just the file name (in which case it will appear in your current working directory), or it could also include a path to save it in a different directory. Warning! Redirecting output using `>` will overwrite the contents of the file if it already exists, without any warnings. There are many sad stories of people losing their work by accidentally overwriting files using `>`. When a file is overwritten in that way, it is called "clobbering".  
Let's use `cat` to combine two files together and save the results.  
```
mkdir -p processed_data 
cat ABBABABA1.txt ABBABABA2.txt > processed_data/ABBABABA_concatenated.txt
```  
Oops! We forgot about `ABBABABA3.txt`. We could add it by running `cat ABBABABA1.txt ABBABABA2.txt ABBABABA3.txt > processed_data/ABBABABA_concatenated.txt`, which would erase and remake `processed_data/ABBABABA_concatenated.txt`, an annoying solution. Instead, we can concatenate `ABBABABA3.txt` to the end of `processed_data/ABBABABA_concatenated.txt` without overwriting it, by using `>>` instead of `>`, like this:  
`cat ABBABABA3.txt >> processed_data/ABBABABA_concatenated.txt`   
`>` and `>>` are special components of bash code. Both are used to redirect output to a file, but `>` starts the file fresh while `>>` appends things to a file without modifying/overwriting any content that may already be there.  

A few more basic actions we often need to do are to copy, move, or delete files. Copying a file is done with `cp`, which makes a duplicate of the file. This duplicate can be in the same or different directory. If it is in the same directory as the original, it needs to have a new name (you can't have two files with the same name in the same directory), but if it is in a different directory it can have the same name as the original.  
Let's make a backup of our new `processed_data/ABBABABA_concatenated.txt` file:  
```
mkdir -p backups
cp processed_data/ABBABABA_concatenated.txt backups/ABBABABA_concatenated_backup.txt
```
When running `cp`, we first give the name/path of the original file we want to copy, and then give the name/path of the duplicate we want to create.  
Let's backup `ABBABABA1.txt` too: `cp ABBABABA1.txt backups/ABBABABA2.txt`.  
Oops! Did you see that typo? We accidentally named our ABBABABA**1** backup ABBABABA**2**! Let's rename it before we confuse our future selves. We can rename files using the `mv` command. `mv` moves a file from one place to another, without leaving a copy of the original behind (unlike `cp`). We can move files from one directory to another, or we can "move" files without changing their directories. When we move files, we can keep their name or change their name. That means that we can edit the name of a file by "moving" it within the same directory to a different name, like this:  
`mv backups/ABBABABA2.txt backups/ABBABABA1.txt`  
To use `mv`, provide the name/path of the file you want to move, followed by the name/path that you want to move it to. Note that if you want to move it to a new directory without changing the name, you can just give the name of the directory without specifying a name for the file, and it will keep its original name. (Careful! Make sure that directory exists, otherwise you will rename your file to the name of the directory you intended it to move to).  
Let's try some more:  
```
cp ABBABABA1.txt backups
mv backups/ABBABABA1.txt backups/blueberry
cp ABBABABA2.txt backups/blueberry
```
Whoops! Look what just happened. We copied a file to a place where there was already a file with that name (`backups/blueberry`). `cp` overwrote that file without any warning. This is another type of file "clobbering" to watch out for, which both `cp` and `mv` can do. If our old version of `backups/blueberry` was an important file, it would be gone - better hope we had a backup!  

Next, we can delete files using `rm`. `rm` removes (permanently deletes) files that we list. For example, we can delete `backups/blueberry` like this: `rm backups/blueberry`. Careful! Here again there is no "undo". By default, bash will not ask whether you are sure, it will go ahead an execute the command, and the file will be gone (this behaviour can be altered using bash aliases explained later). Be very careful when executing `rm` commands - there are some joke or malicious "advice"/memes out there that try to trick new coders into erasing their whole filesystem using `rm`! Directories can be deleted recursively (including all their contents and subdirectories) using `rm -r` - a powerful tool that can be very useful when you need to delete whole directories with thousands of files, but a command that can be catastrophic when used by mistake! Don't experiment with that one until you are very confident about its usage.   

Now let's take a look at `processed_data/ABBABABA_concatenated.txt` that we made previously. However, this is a big file, it would not be convenient to run `cat processed_data/ABBABABA_concatenated.txt` and have all that text print to our command line. Instead, let's use another handy command: `less`, which lets us scroll through files without printing them out.   

Let's try it: `less processed_data/ABBABABA_concatenated.txt`  

Your screen will now show the contents of `processed_data/ABBABABA_concatenated.txt`. From here, you can scroll up and down to look through the file. There are a series of keyboard shortcuts to help navigating when using `less`, for example:  
* press `spacebar` to jump to the next "page"  
* type `G` (uppercase) to go to the end of the file  
* type `g` to go to the start of the file  
* type `/` to search the contents of the file: first type `/`, then what you want to search for, then `enter`. For example, try typing `/Trinidad`  

If you get stuck while typing something, press `ctrl + c` to cancel what you just typed.  
To exit `less` and go back to the command line, type `q` for "quit".  

Another nice way to preview files is using `head` and `tail`. `head` prints only lines from the beginning of a file, while `tail` prints only lines at the end of the file. Try it out:  
`head processed_data/ABBABABA_concatenated.txt`  
`tail processed_data/ABBABABA_concatenated.txt`  
By default, they print 10 lines. We can change this using the `-n` (AKA `--lines`) flag. For example `head -n 5 processed_data/ABBABABA_concatenated.txt` prints only the first 5 lines while `tail -n 5 processed_data/ABBABABA_concatenated.txt` prints only the last 5 lines. You can also use `-` or `+` symbols to remove only the first/last n lines without knowing exact what line number they are. Try comparing the results of these:    
* `head -n 2` AKA `head -n +2`: print the first two lines (start at the beginning and then stop at line 2).  
* `head -n -2`: remove the last 2 lines (start at the beginning and then stop at line -2, ie, 2 lines before the end). Not all versions support using negative line numbers with `head`, in which case you get the error message `head: illegal line count`.  
* `tail -n 2` AKA `tail -n -2`: print the last two lines (start 2 lines before the end and print until the end of the file)  
* `tail -n +2`: remove the first line (start at line 2 and print until the end of the file).  

<img width="361" height="354" alt="image" src="https://github.com/user-attachments/assets/ca0fc1c7-bc67-4e09-a69c-411c89926f4d" />

Another useful piece of info to know about a file is how long it is. We can look at this using the `wc` (word count) command.  
Try running: `wc processed_data/ABBABABA_concatenated.txt`.  
This will show you three pieces of info: the number of lines in the file, the number of words, and the number of bytes. Often all we want to know is the number of lines, which we can specify using the `-l` flag, like this: `wc -l processed_data/ABBABABA_concatenated.txt`.   

## Piping and building pipelines

Often, we want to do many different manipulations to data, and it is a waste of time and storage space to keep saving intermediate files for every single step. The way to avoid this is through pipelines - passing data directly from one command into the next, such that the output of one command is the input for the next. This is not only more convenient, it is often faster, because your computer doesn't have to waste precious milliseconds writing data to the disk and then reading it again, instead keeping the data in its memory when passing between commands. When you have multiple cores available (almost always the case), the computer can also work on both commands at the same time as it goes through the input - much faster when you are dealing with huge bioinformatics datasets.  

To build a pipeline, you use "pipe" symbols (`|`) to separate commands, for example like this: `command_one --settings input_file | command_two --settings | command_three --settings > output_file`. Data passes through the pipes between commands. You can string together as many commands as you would like as long as the commands are able to receive input from "standard input" (stdin) and send output through "standard output" (stdout).  
Let's take a moment to go through that jargon. There are three streams of data on the command line: `stdin`, `stdout`, and `stderr`:   
* `stdin`: "standard input" - input data that is either read from a file (using `<`), typed from the keyboard, or passed to a command using a pipe `|`. Some commands accept `stdin` as input, while others wouldn't know what to do with it. For example, `mkdir` does not do anything with stdin.  
* `stdout`: "standard output" - output that is produced by a command. By default this is printed to the terminal, but it can also be directed to be saved to a file (using `>` or `>>`) or piped to another command using `|`. Many commands produce `stdout`, but some do not - for example, `mkdir` does not produce any stdout (it makes a directory without printing anything)  
* `stderr`: "standard error" - another stream of output that is produced by a command; usually error messages or extra info that is not needed in the main output, like status updates. By default it is printed to the command line, and will not be redirected with `|` or `>` or `>>`. To save it to a file, use `2>` or `2>>`. To make it go to the same place as standard output, use `2>&1`. To make it not be printed, use `2>/dev/null` (explained farther below).  

Let's find out how many samples are in our dataset. Scroll back to look at the file `processed_data/ABBABABA_concatenated.txt`. This file contains sample names in column 2. These samples might be repeated multiple times. To find out how many samples we have, we should see how many unique sample IDs occur in column 2. We can do that using the `cut`, `sort`, `uniq`, and `wc` commands. (There are of course fancier ways we could code it in other languages, but let's build a pipeline with just bash basics).  

First, let's isolate column 2. `cut` grabs the columns that we specify, and we can use the `-f` flag to tell it which fields (column numbers) to select. By default, `cut` expects columns to be tab-delimited, otherwise we would need to tell it what delimits our columns using the `-d` flag.  
Let's check that it works! To avoid printing out the whole long file, let's just grab the first 5 lines and pass those to `cut` as a test. Try these:  
```bash
head processed_data/ABBABABA_concatenated.txt | cut -f 2
head processed_data/ABBABABA_concatenated.txt | cut -f 2-4 #we can ask for a range of columns
head processed_data/ABBABABA_concatenated.txt | cut -f 2-4,6 #we can also use commas to list columns
head processed_data/ABBABABA_concatenated.txt | cut -f 1 -d "3" #we can ask it to use anything we want as the column delimiter
```

So far, `cut -f 2` does what we want, selecting the column containing our sample names. Now, let's remove any duplicates. We can do this using the `uniq` command, which deduplicates any repeated lines to keep only one copy of each. However, `uniq` only compares adjacent lines, so repeated lines have to be right after to each other to be detected. We can ensure this will be the case by using the `sort` command to sort the lines. This will sort lines alphanumerically - if we wanted to, we could change that behaviour (for example `--ignore-case` to treat upper and lower case characters the same, `-n` AKA `--numeric-sort` to sort numerically, or `-r` AKA `--reverse` to reverse the sort). If we hadn't already isolated the column we wanted, we could also specify which field(s) to sort on by using `-k` AKA `--key` to specify the column numbers. By default, `sort` uses whitespace as a column delimiter, which we could change that using `-t`.    
Let's try some out:  
```bash
head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort  
head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort -r #reverse order  
head processed_data/ABBABABA_concatenated.txt | sort -k 2 #sort on column 2
``` 
Especially compare how it treats numbers with different settings:  
```bash
head processed_data/ABBABABA_concatenated.txt | cut -f 8 | sort #sort alphanumerically by default  
head processed_data/ABBABABA_concatenated.txt | cut -f 8 | sort -n #sort numerically  
```

Can you decipher what this is doing?  
`head processed_data/ABBABABA_concatenated.txt | cut -f 8 | sort -t "." -k 2 -n `  
Answer: It is taking column 8 and then sorting it by the numbers after the decimals, numerically (It is using the "." as the column delimiter).  

`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort` is doing what we want. We can then send it to `uniq` to deduplicate the list. Another nice thing `uniq` can do is to count how many times each line was repeated using the `-c` flag (neat but not what we need right now).

```bash
head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq
head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq -c #counts the number of times each sample occured
```

`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq` is doing what we want.  
Lastly, we just need to count how many samples are in this de-duplicated list. We can do that using `wc -l`. Let's commit this time and run it on the whole file, instead of running `head` first.  
`cut -f 2 processed_data/ABBABABA_concatenated.txt | sort | uniq | wc -l`  
There we have it, the number of samples in the file.  
Oh, but wait! You may have noticed earlier that one of the lines in the file was the header, not an actual sample! Our number is therefore one too high. We could just subtract this in our heads, but what if we forget about the header the next time we run this code? Let's get rid of it. There are two easy ways to do this - we could use `tail` to cut it off, or we could use pattern matching to exclude it. We have already learned about `tail`, so try building a pipeline incorporating `tail` to remove the header from our count.  


Solution:  
`tail -n +2 processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq | wc -l`  
or  
`cut -f 2 processed_data/ABBABABA_concatenated.txt | tail -n +2 | sort | uniq | wc -l`  
(we can put tail before or after `cut`, but we can't put it after `sort`, since we don't necessarily know ahead of time where it will end up after sorting.  

One last basic file editing piece for our toolkit is `paste`. The `paste` command can take multiple files/inputs and merge them horizontally as columns, separated by tabs (by default).  

Let's pretend that our SampleID data was in a different file than the rest of our data. We can set up this scenario like this:  
```bash
cut -f 2 ABBABABA.txt > toy_SampleID  
cut -f 1,3- ABBABABA.txt > toy_OtherColumns
```
Now that we are set up in this scenario, let's try putting those files back together. We can use `paste` to do that: `paste toy_SampleID toy_OtherColumns > toy_MergedColumns`  
Check if it worked: `head toy_MergedColumns`  
Note that `paste` will paste them together in the order you specify.  
When using `paste`, make sure you are very confident that all of your lines are in the same order! Paste will not warn you if your files are sorted differently or differ in length.  

## Redirecting standard error
Before we move on, let's talk about standard error (stderr) - this is often error messages, but it can also include useful status updates that we may want to save (programmers can make whatever they want get printed as `stderr`). Redirecting `stderr` is similar to redirecting `stdout`, but the code is slightly different so that you can redirect stderr and stdout to separate places as needed. By default, `stderr` gets printed to the command line, and if you redirect the `stdout`, `stderr` will continue to get printed to the command line. To redirect `stderr`, instead of using `>` or `>>`, use `2>` or `2>>`. (The inputs and outputs are assigned "file descriptors": "2" is stderr, while "1" is stdout and "0" is stdin). For example: `command --settings input_file > output.txt 2> errors.log` will send stdout and stderr to separate files. This is handy for saving error messages to a log so that you can refer to them later if needed.  

If you want the `stderr` to instead be printed alongside `stdout` in the same file (with the lines interspersed as they are generated), you can use `2>&1` which means "send stderr to the same place as stdout". For example: `command --settings input_file > output.txt 2>&1` will send both `stderr` and `stdout` to the same place. This can be handy when both `stdout` and `stderr` are log messages that you want to save to a single log file, or if you want to be able to send error messages through a pipe to be processed by the next command.  

We can also use another trick to make error messages go away entirely - we can redirect the standard error to a place called `/dev/null`. This is a special device which acts like a "black hole" in the computer. It is empty, and any data that gets sent to it is immediately discarded. Redirecting our error messages to `/dev/null` gets rid of them so they never get printed. This can be useful when you need to loop through 2000 files with commands that produce a lot of `stderr` messages and you don't want all that text flying at you on the command line.  

# Making a file from scratch
So far, we have looked at moving around and manipulating files. Now, let's make some files from scratch on the command line. This saves us from needing to switch into a graphical user interface text editor to make a text file (and sometimes you will be working on servers that have no access to graphical user interface text editors at all).  

Four tools useful for building up new text files from scratch include:  
* `cat` - read a file (or text input on the command line) and print the contents
* `echo` - print something 
* `printf` - print something
* `nano` - edit a text file

### cat
We have already used `cat` to print the contents of a file or concatenate files together. We can also use `cat` in a slightly different way - instead of making `cat` open a file to read the contents, we can give cat nothing, like this: `cat`.  
`cat` will then wait infinitely for us to type input. Anything we type (`stdin`) it will print (to `stdout`).  
To end the session with `cat`, type `ctrl+d` for "done".  
That didn't do anything, `cat` just repeated everything we typed back at us. To be more useful, we can redirect the `stdout` to a file, using `>` or `>>`.  
Try this out: `cat > testing_cat.txt`  
Type anything you want, then press `ctrl+d` when you are done. Take a look at the file you made: `less testing_cat.txt` (press `q` to exit `less`).  
A few things of note:  
* use `>` when you want to overwrite any existing content that may exist, use `>>` when you want to append something to the end of a file without overwriting it.
* `cat` interprets your "enter" key as a linebreak (newline character). These are invisible to us but those characters are visible to bash. Make sure to remember a final linebreak on the last line of your file (press "enter" on your last line before exiting with "ctrl+d"), otherwise your last line will have no linebreak character, something that may cause problems if you use that file for anything in bash. (This is something we normally never really have to think about when writing with rich text editors like Microsoft Word).
* there is no backspace after you move to a new line. Once you hit enter and move to the next line, `cat` has already sent that previous line through `stdout` and it has been written to your file.
* if you exit `cat` with ctrl+c ("cancel") instead of ctrl+d ("done"), the line you are currently on will not be written.

A typical use-case for `cat` is creating very short text files that we need as input for other commands, and that are easy to copy-paste or type on the command line. For example, let's create a file listing some species names:  
`cat > Ceratopipra_species.txt`
Copy-paste the contents below into the terminal, hit "enter" once to generate a linebreak if needed, then type ctrl+d to finish.
```
rubrocapilla
chloromeros
erythrocephala
mentalis
cornuta
```
Now check that the file looks ok: `cat Ceratopipra_species.txt` or `less Ceratopipra_species.txt` (press `q` to exit `less`). 

### echo
`echo` is an alternative way to print text to a file. It requires less interaction than `cat`, so is handy in pipelines where you don't want to worry about typos or where you need to make a lot of files. It has the disadvantage of needing to explicitly write out linebreaks, such that you can't just copy-paste multiple lines of text like we did above.  
Let's test it out:  
```
echo "this is a test"
echo test
echo do I need quotation marks
echo "column1 column2" | cut -f 2 -d " "
echo "how many characters are in this sentence" | wc -c
echo "column1\tcolumn2" #in some versions, \t will by default be interpreted as a tab, while in others it is not
echo "Here is a random number: $RANDOM" #we can include variables in echo - these are explained farther below
```
`echo` just repeats whatever we give it and passes that from `stdin` to `stdout`, whether that means printing to our terminal or passing the content through a pipe. We can use that to build text files.  
Let's use `echo` to make a phylogenetic tree file, something that many population genetics programs ask for as input:  
`echo "(cornuta,(mentalis,(erythrocephala,(rubrocapilla,chloromeros))))" > Ceratopipra_phylogeny.nwk`  
Now check that the file looks ok: `cat Ceratopipra_phylogeny.nwk` or `less Ceratopipra_phylogeny.nwk` (press `q` to exit `less`). 
Note that echo automatically adds a newline character to the end of whatever it prints.  

### printf
`printf` is a slightly more standardized way of printing that has more formatting options than `echo`. `echo`, while a very mainstream tool, has the problem of working slightly differently on different versions of bash, so you can't always be sure what its output will be if you are working with text that has any complications like backslash characters. `printf` deals with backslashes and formatting very consistently.  

Try these:  
```
printf "this is a test"
printf test
printf do I need quotation marks #this only prints the word "do" - you do need quotation marks when you have a space you want to print!
printf "column1 column2" | cut -f 2 -d " "
printf "how many characters are in this sentence" | wc -c #one fewer than echo - because echo added a newline character
printf "column1\tcolumn2" #the \t is interpreted as a tab
printf "Here is a random number: $RANDOM" 
```
Those probably look a little wonky - unlike `echo`, `printf` didn't add any newline characters to our output, because we didn't ask it to. Without an invisible newline character, our terminal didn't move to a new line. Newlines are represented by a "\n" (make sure to use a backslash `\` not a forward slash `/`), and we can add "\n" where we want linebreaks to be when using `printf`.  

Let's fix those up a bit by telling `printf` to include linebreaks at the end of our printing:  
```
printf "this is a test\n"
printf test\n #without quotes, the \n didn't get interpreted as a newline character
printf "test\n"
printf "column1 column2" | cut -f 2 -d " "
printf "how many characters are in this sentence" | wc -c #one fewer than echo - because echo added a newline character
printf "column1\tcolumn2\n" #the \t is interpreted as a tab
printf "Here is a random number: $RANDOM\n" 
```
We can use this when building files. For example, let's remake our `Ceratopipra_species.txt` using `printf` instead of `echo`:  
`printf "rubrocapilla\nchloromeros\nerythrocephala\nmentalis\ncornuta\n" > Ceratopipra_species.txt`  
Now check that the file looks ok: `cat Ceratopipra_species.txt` or `less Ceratopipra_species.txt` (press `q` to exit `less`).  

### nano

`nano` is a slightly more fancy command that allows the user to edit text files interactively in the terminal. Let's try it.
Run: `nano nano_test.txt`. This will open the editor with a new blank file, where you can type anything you want, and navigate using the arrow keys (like the command prompt, you can't point-and-click in `nano`).  
To save your progress, type "ctrl+o". It will ask you to confirm/modify the name of the file - press "enter" to confirm.  
To exit `nano`, type "ctrl+x". If you have unsaved changes, it will ask you whether you want to save - type "y" for yes (save) or "n" for no (discard changes).  

Let's try editing a configuration file - many bioinformatics programs use "config files" (or "param files") to set parameters when there are a large number of them, so that you don't need to have long commands with an unwieldy number of flags. Let's take a look at an example config file for the program STRUCTURE: `less config_files/STRUCTURE.params` (press "q" to exit).  
Now, let's imagine we need to make a version of this config file with a different value for the "burnin" - we need to change the text `BURNIN  1000` to `BURNIN  5000`.  
First, make a copy of the file `cp config_files/STRUCTURE.params config_files/STRUCTURE.burnin5000.params`   
Now, edit the file: `nano config_files/STRUCTURE.burnin5000.params`  
Use the arrow keys to navigate to the second-last line, and modify it from `BURNIN  1000` to `BURNIN  5000`. When you are done, type "ctrl+o" to save (press enter to confirm), then ctrl+x to exit.

# Day 2 materials
(in progress)

# efficiency commands
df, screen, history, ssh, scp

# grep and regex
* using grep to grab lines
* using grep -v to exclude lines
* using grep -c to count matching lines
* using simple regex (^, $, escape characters, ., *)
* emphasizing difference between different quote symbols
* [] ranges
* “.” wildcard
* “*” repeats (including zero)
* “^” start of line
* “$” end of line

egrep:
* ”+” repeats (not including zero)
* “?” optional character

# sed
* using sed "s///g" to find-and-replace
* using rename when it is filenames you want to change

# bash variables

Variables are used for storing data. They will be remembered for the rest of your session/script, so you can store a value and then refer to it later. This comes in handy for a few different scenarios, for example:  
* storing a long line of text so you don't have to type it out again or clutter your code or worry about typos (eg, a long filepath)
* allowing code to be reused with different settings/inputs just by editing the variables
* looping through a bunch of samples/files and running the same commands on all of them

To set a variable, you use the syntax `name_of_variable=value_of_variable` (no spaces). For example, `num_lines=3`.  
To use a variable, use the `$` in front of the name of the variable. For example: `head -n $num_lines ABBABABA.txt`. If the variable was assigned a value, that value will now be substituted by bash into the code. Note that unlike many coding languages, you don't have to worry about whether a bash variable is a numeric/character/etc; there are no datatypes.  
If you want to include whitespace in your variable (the value, not the variable name), wrap it in double quotes, otherwise bash will take the first word as the value for the variable and think the rest is supposed to be a new command. For example:  
```
Thing_to_echo="This is a sentence with spaces in it"
echo $Thing_to_echo
```

Variables can be a little finicky at times. If a variable contains any whitespace or special characters, it can cause unexpected things to happen when the code is run. To stop that from happening, it is good practice to wrap the variable in double quotes, like this: `head -n "$num_lines" ABBABABA.txt` or `echo "$Thing_to_echo"`. If there were no unexpected characters in your variable, the double quotes won't do anything (except make your code look a little more sparkly), but getting into the habit of using double quotes may eventually save you some headache.  

# PATH variable
Bash includes some special variables that are set automatically - environmental variables. Most of them handle background things that you won't need to alter, but one environmental variable that you may occasionally need to interact with is `$PATH`. `$PATH` is a list of paths which tells bash where it should look for executables (code) when running commands. For example, when running `ls`, bash scrolls through the directories listed by $PATH until it finds the code for the `ls` program. Basic commands (like `ls`, `grep`, etc) have their code in standard locations that are already included in `$PATH`. To run other commands (eg., programs you download or scripts you write), you will either need to place them into a directory that is in PATH, or specify the whole path to the executable when you run it, or add its directory to PATH so that bash can find it.

You can find out what directories are included in your `$PATH` by running `echo $PATH`. This will spit out the contents of that variable, giving you a list of paths separated by `:` colons. These are the paths where bash searches for programs to run.  
If you want to be able to run a program in a different directory without specifying the full path when you run it, or if a program you are running needs to be able to run dependencies, you can add a new path to your PATH variable by redefining that PATH variable with your new path separated by the rest of the paths by a ":" symbol.  
For example, let's imagine we want to add `/home/scripts` to our $PATH. We can do that like this:  
`PATH=$PATH:/home/scripts`  
This has the effect of appending `:/home/scripts` to the existing PATH variable. Bash will now search through `/home/scripts` after searching through the other paths that were already in PATH. This modification will last until the end of your session - when you close your terminal and start a new session, $PATH will be reset to its original value.  
(there is some subtlety around when you need to include double quotes and when you need to include the command `export`, but you probably won't need to know that unless you are doing more advanced things beyond the scope of this tutorial. It is also possible to make $PATH automatically set itself the way you want so you don't have to do so every time you start a new session - for that you will need to modify your `~/.bash_profile` file, beyond the scope of this tutorial).  

When you start accumulating multiple versions of the same program (eg, updating while keeping old versions for reproducibility of old pipelines, or sharing between users), things can get confusing. If you have multiple versions of the same program visible to bash in your $PATH, bash will use the first one that it finds when going through the list of paths in $PATH. You can check which copy bash is using by using the `which` command, which tells you the full path to a particular program (if bash can find it in $PATH).  
For example, try running `which ls` and `which python` (or how about `which which`!).  

If you want bash to search a new path *before* searching other paths, so that it will use programs in that directory instead of other possible copies, you can instead prepend your new path to the front of the $PATH variable, like this:  
`PATH=/home/scripts:$PATH` (note we have the `:` symbol separating our paths)  
That will now be the first thing that bash searches, the the versions in that directory will take priority over other versions that may be in other directories.  

Note that in practice, you don't necessarily often need to modify $PATH - instead, you can just give bash the full path to the program you are running, so that there will be no confusion in the future over which version was actually run when you look at your code. However, even with that habit you may encounter situations where you need to modify $PATH because a program needs to be able to locate other dependencies when running.  

# day 3 materials (in progress)

# for loops, while loops, if statements  
While often used for only very simple tasks, bash is a full programming language that includes the ability to write loops and evaluate "if" statements. These come in extremely handy in bioinformatics, especially when needing to do repetitive tasks with many samples/genes/etc.  

## loops logic  
If you have programmed in another programming language, you may already be familiar with the logic of loops. Loops allow you to repeat a given task across multiple iterations, possibly doing a slightly different thing in each iteration. Bash has a few different loops (`for`, `while`, `until`, `select`), but here we will focus on the two most useful in bioinformatics: `for` and `while`.  

A `for` loop takes a list of values, and then repeats a chunk of code once for each value in that list. That list could be a list of sample names, gene names, or iteration numbers, for example. This loop is useful when you know the complete list of things/numbers you want to iterate over.  

A `while` loop similarly repeats a chunk of code, but it does so for as long as a condition remains true. That condition could be many different things - a variable holding a certain value, for example. If the condition to exit the loop is never met, the loop will continue infinitely. A nifty use case for while loops in bioinformatics is to hold a list of samples/genes/etc in a text file, and have the loop read through the file, running the loop for every line item in the file, and stopping when it hits the end of the file.  

## for loops syntax
The syntax of a `for` loop goes like this: `for item in item1 item2 item3 ; do SOMETHING ; done`. (note the placement of the `;` symbols, do, and done). SOMETHING can be any command (or multiple commands), and item1/item2/item3 can be a list of any number of words or numbers.

Let's start simple, looping through a short list and just echoing out the name of each thing in our list:  
`for gene in MC1R ND2 COII CYTB ; do echo "analyzing $gene" ; done`  
Note that we could have listed out as many gene names as we want, separated by spaces - bash will keep reading through the list until it hits the ";" symbol.  
That command looped through each of the genes, and executed `echo "analyzing $gene"` for each one. Note that we could name the items in our list anything we want; we could equally have run `for blueberry in MC1R ND2 COII CYTB ; do echo "analyzing $blueberry" ; done`.  

When running loops, we can do more than one command in each loop. To do more than one thing, separate subsequent commands with a `;` symbol.  
Let's add a command to check the length of a fasta file for each gene. A simple way we can do that is to take our fasta file, remove the header (line(s) starting with ">"), delete linebreaks, and then count how many characters are left.   
`for gene in MC1R ND2 COII CYTB ; do echo "analyzing $gene" ; grep -v ">" gene_fastas/"$gene".fa | tr -d "\n" | wc -c ; done` (`tr -d "\n"` deletes the line break character that would otherwise be counted by `wc -c`).  
Now let's add another command to count the number of "A" nucleotides in each gene sequence. We can do that similar to the previous one: take our fasta file, remove the header, delete everything except for the "A"'s, and then count how many characters remain.    
`for gene in MC1R ND2 COII CYTB ; do echo "analyzing $gene" ; grep -v ">" gene_fastas/"$gene".fa | tr -d "\n" | wc -c ; grep -v ">" gene_fastas/"$gene".fa | tr -d -c "A" | wc -c ; done`

We can get more fancy by assigning the lengths and number of A's to variables.

`for gene in MC1R ND2 COII CYTB ; do echo "analyzing $gene" ; length=$(grep -v ">" gene_fastas/"$gene".fa | tr -d "\n" | wc -c) ; num_As=$(grep -v ">" gene_fastas/"$gene".fa | tr -d -c "A" | wc -c) ; echo "length of $gene is $length and number of A's is $num_As" ; done`

More often in bioinformatics, we don't want to be reading data off the terminal, we want it to be saving that data to a file that we can analyze later. Let's do that.
```
echo -e "gene\tlength\tnum_As" > num_As.txt ;
for gene in MC1R ND2 COII CYTB ; do echo "analyzing $gene" ; printf "$gene\t" >> num_As.txt ; grep -v ">" gene_fastas/"$gene".fa | tr -d "\n" | wc -c | tr -d "\n" >> num_As.txt ; printf "\t" >> num_As.txt ; grep -v ">" gene_fastas/"$gene".fa | tr -d -c "A" | wc -c >> num_As.txt; done
```
Notes on the code:  
* we needed to use `echo -e` instead of just `echo` to enable it to interpret `\t` as a tab character, instead of literally printing `\t`. Not all systems have `echo -e`; if it is not available, one could use `printf "gene\tlength\tnum_As\n" instead.     
* we needed to use printf "$gene\t" instead of echo -e "$gene\t" because echo adds a newline (line break) character to the end of what it prints, by default, while printf does not. If we used echo, we would have had to tell echo not to do that, or strip the newline off afterwards.  
* we had to include `tr -d "\n"` a second time after running `wc -c` to count gene length, because `wc` also by default has a newline character at the end of its output. We had to strip this off so that it didn't cause a linebreak in the middle of our line. We didn't strip the newline character off of the last `wc -c` command, because we do want to have a linebreak there, as that is the end of our data entry for that gene.  

Take a look at `num_As.txt` to see the results:  
`cat num_As.txt`  
How does it look? Does it look like the sort of file you could use for downstream analyses/visualizations?

Note this is not the most efficient way to complete this task, but it illustrates how we can accomplish bioinformatics tasks by stringing together simple bash tools.

## brace expansion
Another nifty trick that we can use to upgrade our loops (or other commands) is **brace expansion**. This is a shortcut for generating lists or repetitive text without needing to type everything out. A common use for this trick is to generate a range of numbers by specifying only the first and last number of a series. The syntax of this is to separate the two numbers by two dots (`..`) and surround them in curly brackets (`{}`). You can then insert the braces anywhere you want them to get expanded. Let's try some:  
`echo {1..10}`    
`echo {7..21}`  
A handy time-saver that also eliminates the risk of a hard-to-spot typo.  

[Tip: if you are needing even more functionality that isn't being met with brace expansion (eg, using variables to specify the range of numbers), you could check out the command `seq`.]  

A great use for brace expansion in bioinformatics pipelines is to use them with `for` loops to perform multiple iterations/replicates of a stochastic step.  
For example, let's subsample a list of genes by selecting only 10 random genes from a long list of genes. Perhaps we are running a computationally intensive analysis that can only handle 10 genes, or perhaps we need small samples of random data to build a null distribution to compare to some result (for example to calculate a p-value).  
We can shuffle our list with `sort -R` (sort randomly) and then take the first 10 lines.
`sort -R genes.txt | head -n 10`
(Note: a nice alternative for shuffling lines is the command `shuf`, which comes with many versions of bash, though not on Macs)  

For many cases of subsampling, we need multiple iterations (eg, checking for consistency between replicates or building up a null distribution). We can use a `for` loop with brace expansion to quickly and easily generate as many replicates as we would like.  

`mkdir -p random_genes  
for iteration in {1..10} ; do sort -R genes.txt | head -n 10 > random_genes/random_genes."$iteration".txt ; done`  
That should have made ten files each containing a list of ten random genes - check them out: `ls random_genes`  
Let's look at the first line of each file we just made:  
`for iteration in {1..10} ; do printf "the first gene is: " ; head -n 1 random_genes/random_genes."$iteration".txt ; done`

## nested loops
We can also put loops inside of other loops! This allows us to iterate over multiple things at once. For example, maybe we need to run 10 iterations each for 10 different genes each for 10 samples. Or, perhaps we want to run a program while testing combinations of 3 different settings for one parameter and 2 different settings for another parameter, with 5 replicates per combo.  
Nesting loops is simple; just put a loop in the middle of another loop. Make sure that you include the `do ; done` syntax for each loop. If you make a mistake with the syntax, usually nothing will happen - bash will stay waiting for you to complete typing the loop (press ctrl-c to cancel).   
`for sample in sample1 sample2 sample3 ; do for gene in MC1R ND2 COII CYTB ; do for iteration in {1..3} ; do echo "iteration $iteration for gene $gene of $sample" ; done ; done ; done`  

Note the order - bash loops through the innermost loop before changing the value of the next loop (it goes through all the iterations of sample1 MC1R before moving on to ND2, and completes all the genes of sample1 before moving on to the first iteration of sample2. If we change the order of the loops, it will change the order of the iterations.

`for gene in MC1R ND2 COII CYTB ; do for iteration in {1..3} ; do for sample in sample1 sample2 sample3 ; do echo "iteration $iteration for gene $gene of $sample" ; done ; done ; done`  
Now, it does iteration 1 of MC1R for all samples before moving on to iteration 2.

Let's put nested loops to use. One task we may sometimes have to do in bioinformatics is concatenating DNA sequences stored in separate files. Perhaps we want to make a phylogeny, and need a single DNA sequence alignment with multiple species, but our DNA sequences are scattered across separate files, with each gene sequence of each sample stored in separate files. We could open each file one-at-a-time, copy-pasting the sequences into a new text file, but what if we make a mistake? What if we have hundreds of files and are short on time? What if we realize later that we want to exclude a gene, and need to redo the whole task? To be faster, more reproducible, and avoid typos, we can easily do this on the command line.  
We can first break down what we need to do. For each gene of each species, we need to open the sequence file and grab the DNA sequence. This is usually stored in fasta format, which contains a header (that starts with ">") followed by a line (or lines) of DNA sequence. Then we need to paste this DNA sequence into a new file. We need that new file to contain a fasta header for each sample, and then have a line of DNA sequence with each of our genes back-to-back in the same order. (Let's assume that this is our data, and we already know that our files contain DNA sequence that is homologous and properly aligned across all samples, so we can concatenate the files without worries).  

This loop will be a little more complicated, so let's spell it out in words before writing the loop:  
1) for each sample:
2) make a fasta header entry in the new file (with a linebreak after it)
3) for each gene in that sample:
4) open the gene fasta file for that sample, and remove the fasta header and line breaks
5) paste that DNA sequence into the new file
6) after pasting the last gene, add a linebreak before moving on to the next sample

Now let's put that into bash code:

`for sample in sample1 sample2 sample3 ; do echo ">$sample" >> concatenated_data.fasta ; for gene in MC1R ND2 COII CYTB ; do grep -v ">" "$sample"_"$gene".fasta | tr -d "\n" >> concatenated_data.fasta ; done ; printf "\n" >> concatenated_data.fasta ; done`
Let's take a look: `concatenated_data.fasta`. Ready to open in a sequence alignment viewer or to build a phylogenetic tree with!  

One thing to note: if we were to run the above code twice by accident, it would happily append a second copy of everything to `concatenated_data.fasta` without any easy way for us to realize what happened (perhaps until we get out final result and realize there are twice as many sequences in our tree than expected). When running code that builds files with `>>` like that, we either need to be extra careful not to accidentally run things twice (perhaps running a sanity check like counting sequences before moving on), or build in a fail-safe. For example, a fail-safe could be adding `rm` before the loop to get rid of any existing copies of `concatenated_data.fasta` before continuing (or clobbering it with `>`), or using an `if` statement to check that the file doesn't already exist (described below).  

## while loops

The other handy type of loop is **while loops**. These use very similar `do ... ; done` syntax, but instead of feeding them an explicit list of things to iterate over, they will check whether a condition is met at the start of each iteration, and stop only once that condition is met. A very common usage is to store a list of things to loop through, and loop through the lines of the file with a `while` loop, the exit condition being hitting the end of the file.  

Let's start with a very simple example, with samples.txt containing a list of 3 samples. Take a look: `cat samples.txt`.  
```
sample1
sample2
sample3
```
Let's build a loop using this file:
`cat samples.txt | while read sample ; do echo "Now analyzing $sample" ; done`  
`read` will go through the file line-by-line in each loop iteration, stopping the `while` loop when it hits the end of the file.  
[Note - I have used a slightly less efficient syntax here, using `cat` to read the file. This is technically unnecessary; instead the file can be given to bash through stdin, like this: `while read sample ; do echo "Now analyzing $sample" ; done < samples.txt`. I used the slightly less efficient version as it is a little easier to read. If you were to run a huge number of while loops, it would be better to use the more efficient syntax].  

Note that as in `for` loops, we can name our variable anything we want:  
`cat samples.txt | while read blueberry ; do echo "Now analyzing $blueberry" ; done`  

Let's repeat our gene-concatenating example using `while` loops. First, let's make a file listing all the genes that we want.
First, let's make a list of all the genes we need to concatenate. There are multiple ways we could do this, for example:  
`for gene in MC1R ND2 COII CYTB ; do echo "$gene" >> genes_to_loop.txt ; done` a safe way, but which requires you to type out all the gene names
`ls sample1_*.fasta | grep -v "allgenes" | sed "s/sample1_//g; s/.fasta//g" > genes_to_loop.txt` a hack that technically works, but is vulnerable to breaking if `ls` finds something you weren't expecting.
`grep ">" sample1_allgenes.fasta | sed "s/>//g" > genes_to_loop.txt` a hack that works because we happen to have a file with all the gene names in it, we just needed to extract them from the fasta headers and fix the formatting.  
We could also have written the file ourselves using `nano genes_to_loop.txt` or `cat > genes_to_loop.txt`.  

Now let's write our loop. Recall the `for` loop version was: `for sample in sample1 sample2 sample3 ; do echo ">$sample" >> concatenated_data.fasta ; for gene in MC1R ND2 COII CYTB ; do grep -v ">" "$sample"_"$gene".fasta | tr -d "\n" >> concatenated_data.fasta ; done ; printf "\n" >> concatenated_data.fasta ; done`
Here is the `while` loop version:  
`cat samples.txt | while read sample ; do echo ">$sample" >> concatenated_data.fasta ; cat genes_to_loop.txt | while read gene ; do grep -v ">" "$sample"_"$gene".fasta | tr -d "\n" >> concatenated_data.fasta ; done ; printf "\n" >> concatenated_data.fasta ; done`  
Which syntax do you prefer?  
In general, when you just have a few things to loop through, it makes more sense to write them out as `for` loops. When you have a long list of samples/genes/etc, it can be convenient to store them in a file and use the `while` loop trick instead.  

One thing that you can do with `while read` that you can't do easily with `for` loops is to have `read` parse multiple variables on a line. By default, `read` reads lines as space-separated lists of variables. For example, let's look at `samples_metadata.txt`. 
```
sample1 referenceA
sample2 referenceA
sample3 referenceB
```
`cat samples_metadata.txt | while read sample ; do echo "Now analyzing $sample" ; done` 
We can simply list another variable name, and `read` will interpret the two space-separated words as separate variables.   
`cat samples_metadata.txt | while read sample reference ; do echo "Now analyzing $sample using $reference"; done` 
You can repeat this with as many space-separated variables as you wish. This is handy when you need to loop through different samples/genes/iterations/etc while using slightly different settings for each one, for example:  
* mapping different samples to different reference genomes
* dealing with X/Y or Z/W chromosomes as haploid vs diploid for different samples
* using different sequencing depth filters for different samples
* creating different datasets with different filtering stringencies for different analyses
* testing out several combinations of parameter settings when you don't have computational resources to test every possible combo  

Before moving on, it's important to note that our `while` loops here are working by reading through very basic and cleanly-formatted text files, for which we know the contents and can confidently use knowing there are no unexpected whitespaces in sample names and we didn't use any backslashes in our sample names. Here are some notes for things you may run into:  
* if you need backslashes, use `-r`, otherwise `read` will interpret them as special characters. For example: `cat samples.txt | while read -r sample ; do echo "Now analyzing $sample" ; done`
* if you have multiple variables per line and are using something other than a space to separate them (especially if you have any spaces in your variables), tell bash what the delimiter is using `IFS=` ("internal field separator"). For example, to specify your file is tab-delimited (`\t`), you would run `cat samples.txt | while IFS=$'\t' read sample ; do echo "Now analyzing $sample" ; done`
* if you made the text file using Excel or another rich text editor, delete the invisible "carriage return" line endings from the file by running it through `tr -d '\r'`, otherwise `read` will not parse it properly.

## if statements

One more core piece of bash syntax is the `if` statement. Like other programming languages, `if` statements check whether a condition is true before executing the command. The syntax looks like: `if [ condition ] ; then command ; fi` (substituting "condition" and "command").  

A very common usage in bash is to check whether a file already exists before proceeding. `-e` in an `if` statement condition asks whether a file exists:  

`if [ -e samples.txt ] ; then echo "Yes, samples.txt exists" ; fi`  
`if [ -e abcde.txt ] ; then echo "Yes, abcde.txt exists" ; fi` # this should do nothing, assuming you did not create `abcde.txt`.  

We can also do the opposite - ask whether a file *doesn't* exist. To negate a condition, we can use a `!` symbol, like this:  
`if [ ! -e samples.txt ] ; then echo "No, samples.txt does not exist" ; fi` # this should do nothing, as `samples.txt` should exist.  
`if [ ! -e acde.txt ] ; then echo "No, abcde.txt does not exist" ; fi`   

This can be a handy safety measure to avoid overwriting ("clobbering") an especially valuable file that took a long time to make - when built into an `if` statement, the command will happily exit without overwriting your file if you accidentally paste it into the command line.  
for example: 
`if [ ! -e blueberry.txt ] ; then echo "blueberry" > blueberry.txt ; fi`   
This will only write `blueberry.txt` if it doesn't already exist. That would be handy if `blueberry.txt` took a week to write and we don't want to overwrite it if we ran that command by accident.  

This is also very handy if we aren't sure whether a file already exists, and we only want to make it once. For example, when mapping samples to a reference genome, we might want to check whether the reference genome is already indexed, and only index it if it is not already indexed:  

`cat samples_metadata.txt | while read sample reference ; do if [ ! -e "$reference"_index.txt ] ; then echo "preparing $reference" ; printf "" > "$reference"_index.txt ; fi ; echo "mapping $sample to $reference" ; done` (this is an imaginary example to give you the idea, this command of course isn't actually indexing or mapping anything)  

# gnu Parallel
So far we have looked at using loops to run a potentially large number of repetitive commands. These loops run one iteration at a time, only moving on to the next sample/gene/iteration once the previous has complete. Sometimes this is important, such as when writing things to a file in a particular order. In other cases however, it is a waste of time - when it doesn't matter the order that things are done, we could save potentially weeks of waiting by making our samples/genes/iterations/etc run at the same time instead of one-after-the-other. This is the case when a computer has multiple **cores/threads**. In brief, A computer core (CPU core) is the hardware that actually does the computing. When a computer has multiple cores (as almost any machine you interact with will), it can compute multiple different things at once. The term **threads** is often used interchangeably, a thread is essentially a unit of work that a CPU core can do. Some cores only do 1 thread of work (so the number of threads equals the number of cores), while some cores can "multitask" and work on 2 threads at once (so the number of threads is equal to double the number of cores). 

When we run a single-threaded command (as all of the previous examples were) like a while or for loop, everything is done on only one thread - all the other available threads are sitting idly by. To be more efficient, we could have the other iterations of our loop worked on simultaneously by other threads. This can sometimes add up to enormous time savings! For example, if it takes an hour to map a sample to a reference genome and we have 24 samples to map, running them using a simple while/for loop one-at-a-time would take 24 hours to map all samples. Instead, if we have 24 threads available and map them all at once on different threads, we could have them all done in 1 hour! Using multiple threads at once is called **multithreading** or running things in **parallel**.   

There are many ways we can accomplish that. Many bioinformatics programs have multithreading built in, with the program including a flag asking how many threads we want it to use - handy when we have just one command that we want done faster. When we have *multiple* commands to do at the same time, we could copy-paste them into separate terminals to run at the same time, but that would be inconvenient and annoying. Instead we can use a utility that automatically manages running things in parallel - one popular option is Gnu `parallel`. `parallel` doesn't come with bash, instead it is a separate program that needs to be installed.   

[section about installing gnu parallel - this would have been "homework" from the previous day]

The logic behind setting up a `parallel` run is similar to the `while read` loops - we need a file listing a bunch of values to loop over (samples/genes/iterations/etc), and give that to `parallel` along with the command we want to run, and `parallel` will propagate our values into the command, generating one command for each of them, and then manage those commands by feeding them to any free threads (one command per thread), either using all threads on our computer or sticking to a set number that we tell it to use. If there are more commands than threads, `parallel` will hold the extra commands back, feeding them to a thread as soon as an earlier command finishes and a thread becomes available. 

The syntax looks like this:  

cat samples.txt | parallel echo "processing {}"

In that command, we opened `samples.txt` with `cat` and then sent that list to `parallel` through standard input. `parallel` seems each line as a separate value to iterate over, and generates separate commands for each, dropping them into the `{}` in the command `echo "processing {1}"`. It then runs all of those commands at the same time. 

An alternative syntax looks like this:

parallel echo "processing {}" :::: samples.txt

or this:  

parallel echo "processing {}" ::: sample1 sample2 sample3

In those cases, we give out inputs at the end of the command - if they are listed in a file, we use four colons (`::::`) followed by the filename. If we instead want to write them out, we use three colons (`:::`) followed by a space-separated list. Each of those three syntaxes produces the same result, so it is a matter of convenience or personal preference which you would like to use.  

Let's go back to an earlier task - counting the number of A's in a fasta sequence. Let's count the number of A's in the fasta sequences of ND2 for our three samples in parallel. Before we do that, there are a few more rules to know. When we want to give parallel a longer command that includes special bash characters like `|` or `>`, we need to enclose those characters in single quotes (eg, `'|'`, `'>'`) so that bash will know they belong to the `parallel` command. The easiest way to do this is to just wrap the entire `parallel` command in single quotes as a habit, like this:      
`cat samples.txt | parallel 'echo "processing {}"'` (when we don't need them, those single quotes will just have no effect)  

`cat samples.txt | parallel 'echo "analyzing ND2 from {}" ; num_As=$(grep -v ">" gene_fastas/{}_ND2.fasta | tr -d -c "A" | wc -c) ; echo "The number of As in ND2 of {} is $num_As"'`  

Parallel can also take multiple lists, propagating a command with every pairwise combination of those lists. To do this, specify where each variable should go using `{1}` and `{2}` to specify the first and second variable respectively. These can either be given in separate lists using `:::` or `::::` to feed them in, in which case `{1}` vs `{2}` will depend on the order you list them in, or they can be separate columns in a single file, in which case `{1}` vs `{2}` depends on the order of the columns. Let's try it:  

parallel echo "processing gene {2} from sample {1}" :::: samples.txt :::: genes_to_loop.txt

or

parallel echo "processing gene {2} from sample {1}" ::: sample1 sample2 sample3 ::: MC1R ND2 COII CYTB

If we want to have `parallel` read multiple variables from the same file, the syntax is a little different. Instead of creating all possible combinations of the variables, `parallel` will only use the combinations specified in your file (one per line). For it to interpret columns as separate variables, we will also need to tell `parallel` what the column separator is using the `--colsep` flag.  

Let's create a fast and easy file with 2 columns by pasting our `samples.txt` and `genes_to_loop.txt` files together, keeping only the first three lines, like this `paste samples.txt genes_to_loop.txt | head -n 3`. Then, let's give this to parallel. In this case, the columns are separated by tabs, which we tell parallel using `--colsep "\t"` (if our columns were space separated, we would say `--colsep " "`).   

`paste samples.txt genes_to_loop.txt | head -n 3 | parallel --colsep "\t" echo "processing gene {2} from sample {1}"`
Unlike previous commands which created all possible combos of genes and samples, that only ran the three combos that correspond to the three lines of input that we have `parallel`.  

Let's use this to count the A's in all genes of all samples now.  

`parallel 'echo "analyzing gene {2} from {1}" ; num_As=$(grep -v ">" gene_fastas/{1}_{2}.fasta | tr -d -c "A" | wc -c) ; echo "The number of As in {2} of {1} is $num_As"' ::: sample1 sample2 sample3 ::: MC1R ND2 COII CYTB`  

Just for fun, let's do each of those tasks three times. Let's use brace expansion to generate the list `1 2 3`.

`parallel 'echo "analyzing gene {2} from {1}" ; num_As=$(grep -v ">" gene_fastas/{1}_{2}.fasta | tr -d -c "A" | wc -c) ; echo "The number of As in {2} of {1} in iteration {3} is $num_As"' ::: sample1 sample2 sample3 ::: MC1R ND2 COII CYTB ::: {1..3}`  

The number of tasks that we ask `parallel` to do can get very large, especially when dealing with potentially hundreds of samples or thousands of sequences. Often, the number of commands `parallel` generates can exceed the number of threads that the computer has. By default, `parallel` will use all of them, starting a new command as soon as an earlier one finishes, so that all threads are being used. When running large numbers of commands that take a long time, this can mean that the whole server is occupied for a while, which can be annoying if you want to do a few things on the side while waiting, or if you are sharing the server. It can also be hard on your computer's hardware to have all the CPU cores running with back-to-back commands for a long time with no cooldown. To alleviate that, you can tell `parallel` how many threads to use using the `--jobs` flag. 

For example, if we want to run on a max of 5 threads at a time, we can use `--jobs 5`:  
parallel --jobs 5 echo "processing gene {2} from sample {1}" ::: sample1 sample2 sample3 ::: MC1R ND2 COII CYTB
This can of course make it finish slower if you are letting it use fewer threads than the max possible, but it is often necessary for the sake of other users and our computer's longevity.  

A few more notes:  
* since `parallel` often needs us to wrap our commands in single quotes (`'`), this can become a problem when a command wants us to include quotes. Sometimes we can get around this by using double quotes instead of single quotes (for example, instead of `echo 'test' | sed 's/test/blue berry/g'`, switch to `echo "test" | sed "s/test/blue berry/g"`. Other times when we really need *single* quotes in our commands, we can use the somewhat clunky syntax `'\''` as a drop-in for `'` which will make it through.  
For example, this would fail due to interference of the `'`'s:  
parallel 'echo {} | sed 's/apple/blue berry/g'' ::: apple apple_pie apple_tree  
This works, replacing the `'`'s around the sed command with `'\''`, though the code doesn't look very pretty:  
`parallel 'echo {} | sed '\''s/apple/blue berry/g'\''' ::: apple apple_pie apple_tree`  
A little clunky, and something you don't often have to do, but sometimes comes up with building bioinformatics pipelines.  

As pipelines get complex, gnu parallel commands can be easy to break, and tracking down errors can get difficult. Something that can help enormously when troubleshooting is the `--dry-run` flag, which causes `parallel` to print out a list of all the commands that it would run, without running them. This can let you check that `parallel` is interpreting things the way you intend.  

For example, run `parallel --dry-run 'echo {} | sed 's/apple/blue berry/g'' ::: apple apple_pie apple_tree`  
We can then dissect the code `echo apple | sed s/apple/blue berry/g` and find that it is missing the quotes inside of the `sed` code, even though those were included in our original code. This reveals to us that `parallel` is not seeing those single quotes (bash strips them out before handing that code to `parallel`). Much easier to troubleshoot that trying to figure out why we are getting the error `unescaped newline inside substitute pattern` without seeing how parallel is interpreting our code.  

## time
When evaluating alternate ways of doing things or running long commands, it is often useful to know exactly how long a command took. We can do this using the `time` command. The `time` command can be placed before any command, and once that command is done, it will print out the timing (without otherwise interfering with the command). 

Let's try it:  
time echo "how long does this command take??"  
That will print out three numbers, `real`, `user`, and `sys`. The two we are most concerned with usually are `real` - the actual amount of time the command took (the "wall time") - and `user` time which is more-or-less the amount of CPU time our computer spent doing the command, summed across all threads that were used. When running multithreaded/parallel commands, `user` time can be much higher than `real` time, if the multithreading was done efficiently. (For example, if using 10 threads, `user` time can be a maximum of ~10 times higher than `real` time if done with maximum possible efficiency). 
We may want to collect these times for a few reasons:  
* to evaluate how efficiently our commands are using multiple threads  
* to remind ourselves how long a command took for future planning  
* to compare the speed of alternative methods  
* to brag about how long something took (or how fast our code is)  

Let's use `time` to compare the speed of our `parallel` command, `while` loop, and `for` loop.  

parallel:  
```bash
time parallel 'echo "analyzing gene {2} from {1}" ; num_As=$(grep -v ">" gene_fastas/{1}_{2}.fasta | tr -d -c "A" | wc -c) ; echo "The number of As in {2} of {1} is $num_As"' ::: sample1 sample2 sample3 ::: MC1R ND2 COII CYTB  
```
for loop:  
```bash
time for sample in sample1 sample2 sample3 ; do for gene in MC1R ND2 COII CYTB ; do echo "analyzing gene $gene from $sample" ; num_As=$(grep -v ">" gene_fastas/"$sample"_"$gene".fasta | tr -d -c "A" | wc -c) ; echo "The number of As in "$gene" of "$sample" is $num_As" ; done ; done  
```
while loop:  
```bash
time cat samples.txt | while read sample ; do cat genes_to_loop.txt | while read gene ; do echo "analyzing gene $gene from $sample" ; num_As=$(grep -v ">" gene_fastas/"$sample"_"$gene".fasta | tr -d -c "A" | wc -c) ; echo "The number of As in "$gene" of "$sample" is $num_As" ; done ; done  
```
Which one was fastest? When running a small number of very fast commands, the difference is often negligible (and the overhead time cost of setting up `parallel` can even make it slower than a `for` loop), but when dealing with heavier tasks it can save you weeks of waiting time.  

## htop

When using multiple threads, it is important to know how many threads our computer has, and how many are free. We can monitor this with the command `htop`. Running `htop` will take you to a screen that shows a series of bars at the top, and a list of processes on the lower half. The bars at the top represent each of your computer's threads, and the percentage shown in each bar tells you how much they are being used at the moment. This tells you how many threads you have, and how many are available for you to use.

[image of a htop showing heavy usage]

[image of htop showing minimal usage]

Another bar below the threads shows how much of your computer's memory is being used. If most of the memory is being used, the computer may slow. Many heavy bioinformatics programs let you specify how much memory they are allowed to use, to avoid that risk.  

Beneath that is a list of all the commands that are being run at the moment - this includes commands being run by you through the terminal, and other things that are happening in the computer.  

To exit `htop`, press `q` for "quit".

# awk
(in progress)
* using awk for simple one-liners

# file permissions
When sharing files between users or when writing your own scripts, one concept that you may encounter is **permissions**. Permissions control who can view or edit a file, and whether a file can be executed as code. Those three actions are controlled separately, and are as follows:  
* Read: a user can open and view the contents of a file.
* Write: a user can edit the file.
* Execute: a user can run the file as code.

By default, most files that you create will have read and write permissions for you, but will not have execute permissions. That is a safety measure that stops you from accidentally running a random (or malicious) file as code. If you try to run something that does not have execute permissions, you will get the error message `Permission denied`. That means that before you can run a newly-written script, you need to tell bash that you do in fact intend for the file to be executable. This is done with the `chmod` function. `chmod` can change the owners and permissions of a file that you own. 

If you want to add executable permissions to a file, you use `+x` with `chmod`, for example, `chmod +x script.sh`. After doing that, you should be able to run your code. One thing to be aware of is that sometimes, drives can be set up such that nothing on the drive can be executed no matter the permissions you set. If that is the case, the owner of the server should have informed you of where you can place executable files so that they can run.  

Other permissions are set the same way (`chmod +r` to add read permissions, `chmod +w` to add write permission). Permissions can also be taken away, using `-x`, `-r`, or `-w`.  

The other aspect of permissions is ownership. There are three categories of user from the perspective of a file:  
* owner: the person who owns the file, usually the person who created the file.  
* group: a designated group of users, for example a group of collaborators or a lab team  
* everyone: anyone who is not the owner or in the designated group  
Those three categories can have different permissions: this allows you to do things like make files private, make files readable only to a selected group of collaborators on a shared server, or make it so that a collaborator can read your files without being able to edit them. By default, you have read and write permissions for files you create, but those files have read-only permissions for others (not editable). Those permissions can each be modified separately by `chmod` (and the owner/group can be changed with `chown`). We won't go over those uses here, but if you run into `Permission denied` errors when trying to share files, those are the commands to look at.  

# Aliases
One thing that we can do to make our lives easier on the command line is to assign **aliases** for commands that we run frequently. An alias is a shortcut for longer commands that we don't want to have to type out every time. An alias is similar to saving something as a variable, except that it is used as a shortcut for commands, it is remembered across sessions (which variables can be but aren't by default), and you don't need to use the `$` symbol to invoke them.  
Aliases get stored in a special file called `~/.bash_aliases`. The `.` symbol in front of the filename makes it an invisible file - it doesn't show up when browsing folders in a GUI or when looking at directories using `ls`, but it can be edited just like a normal file, and it appears when using the `-a` flag with `ls` ("a" stands for "all"). This file may not exist if you have never made an alias before, but will be read by bash next time you open a new terminal session after creating the file.  
Aliases can be anything that you would like a shortcut for, here are some examples of ones that I use:  

`alias rm="rm -i"`: this makes it so that every time I run the `rm` command to remove a file, it adds the `-i` ("interactive") option without me needing to remember to type it. This makes `rm` ask me if I am sure before deleting anything, to save me from accidents. When I want to delete hundreds of files at once without being bothered, I can add the `-f` flag to override the `-i` command and force deletion without it asking me about every single file.  
`alias hub="cd ~/Documents/GitHub"`: this is an alias for me to `cd` into my Github folder without me needing to type the whole word or remember where it is. `alias ll="ls -l"`: this is a fairly popular alias, used to save you from typing all 5 digits of `ls -l`, a command that is usually used *a lot*.  
`alias nseq="grep -c '^>'"`: this is a handy command to count the number of entries in a fasta file, something I need to do a lot.  
`alias nvcf="grep -c -v '^#'"`: this one lets me count the number of sites in a VCF file.  
`alias nia="ssh username@IP_address"`: this allowed me to `ssh` into a server without having to type the whole IP address.  

All those aliases have the form `alias name_of_alias="command that you want to make an alias for"`.

Try writing or picking a bash alias that would be useful to you. You can add this to your account's `~/.bash_aliases` file any way that you like to edit a text file, for example, using `cat` or `nano`. Once you have added an alias, it won't take effect right away, because bash won't have read your alias file. You will need to close your session and open a new session, at which point bash will read your alias file.    
To edit the file with `cat`, run `cat >> ~/.bash_aliases`, then type or paste what you would like added, hit "enter" to add a line break, then type `ctrl+d` when you are done.  
To edit the file with `nano`, run `nano ~/.bash_aliases`, paste or type the alias you want to add, then exit nano with ctrl+x. It will ask you if you want to save you changes; type `y` if you do.  

Note: not all systems are set up this way. If your `~/.bash_aliases` is not working, you will likely have to modify another file, `~/.bashrc`, to have a code block that says:
```
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

# installing programs
* git clone
* wget, tar -zxvf
* dealing with compressed files (gzip, gunzip, zless, zcat)

# Practice Problems
1) count how many different populations there are in column P1.
2) count how many samples of *C. rubrocapilla* there are.
3) change all instances of "InambariW" to "Inambari_West"
4) remove sample Ceratopipra_erythrocephala_CN626 from the dataset
5) select the 20 entries with the lowest value of BBAA
6) select the 20 entries with the highest value of ABBA
7) make a new file containing all entries with sample Ceratopipra_chloromeros_FM433680, but don't include the ABBA, BABA, or BBAA columns, and make sure it is sorted by Z score from highest to lowest. (You can do the pipeline in 2 parts).

1) `cut -f 1 | tail -n +2 | sort | uniq | wc -l`  
2) `cut -f 2 | grep "rubrocapilla" | sort | uniq | wc -l`  
3) `sed "s/InambariW/Inambari_West/g"`  
4) `grep -v "Ceratopipra_erythrocephala_CN626"`  
5) `tail -n +2 | sort -n -k 8 -r | head -n 20` OR `tail -n +2 | sort -n -k 8 | tail -n 20`  
6) `tail -n +2 | sort -n -k 9 | head -n 20`  
7) `head -n 1 > new_data.txt ; grep "Ceratopipra_chloromeros_FM433680" | cut -f 1-7 | sort -n -k 5 -r >> new_data.txt' 


## Harder problems:  
(There are fancier ways to do these things much more succinctly, but can you do it using only command/regex/flags from this tutorial?)  
1) split column 2 so that instead of giving the full sample name (eg. Ceratopipra_chloromeros_B106768), it has the species name in one column and the sample number in a different column (eg, Ceratopipra_chloromeros  B106768).  
2) select all the columns where rubrocapilla is in column P1 and mentalis is in column P3  
3) oops, name mixup. Change all instances of rubrocapilla to erythrocephala and all erythrocephala to rubrocapilla.  
4) Add a new column to the file. This new column should contain the name of the species for the sample in column 2, but don't alter the contents of column 2. Place this new column in between column "P3" and column "D". You can use up to 3 lines of code for this.  

Here are my solutions:  
1) `sed "s/SampleID/SpeciesName\tSampleNumber/g; s/Ceratopipra_/Ceratopipra@/g; s/_/\t/g; s/Ceratopipra@/Ceratopipra_/g" ABBABABA.txt`. 
2) `grep "^rubrocapilla\t.*\tmentalis" ABBABABA.txt`
3) `sed "s/rubrocapilla/PLACEHOLDER/g; s/erythrocephala/rubrocapilla/g; s/PLACEHOLDER/erythrocephala/g" ABBABABA.txt`. 
4)
```
cut -f 2 ABBABABA.txt | sed "s/Ceratopipra_/Ceratopipra@/g; s/_.*$//g; s/@/_/g; s/SampleID/Species_name/g" > temp_SpeciesNames
cut -f 1-3 ABBABABA.txt | paste - temp_SpeciesNames > temp_FourColumns
cut -f 4- ABBABABA.txt | paste temp_FourColumns - >
```  
Note - some of those are a bit clunky and could be done much more elegantly using other tools, a different language, or more advanced syntax - this was just meant to illustrate that you can do quite a bit with only some very basic commands/syntax.  


