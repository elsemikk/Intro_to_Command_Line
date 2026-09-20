# Intro to the Command Line for Bioinformatics 
# Workshop

# Day 1: Navigating the command line

## Anatomy of the Command Line

### broad overview and terms  
Most of the time when using computers, we are using a **graphical user interface** (GUI), something that lets us point our mouse and click on buttons or browse through menus. A more direct way of communicating with the computer is through the **command line**, where you type lines of text containing commands for the computer. To use the command line, you need a program called a **shell** to interpret your commands, and the most popular shell used in bioinformatics (and more widely) is **bash**. Bash is used with Linux and UNIX operating systems, and also comes installed on macs. To use the shell, you need an application referred to as a **terminal**. The terminal is the application you open and interact with, the command line is where you type your commands, and the shell (bash) is the program that interprets your commands and tells your operating system what to do.  

Here, we will go over the basics of working on the command line and writing simple bash code. This requires you to have access to a terminal program with bash. Accessing that varies depending on your operating system. In practice, most bioinformatics work is done on a server accessed remotely, rather than done locally on a laptop.   

*Linux* if you are on Linux, you should already have an application called Terminal, which can be opened from your applications, or with `ctrl + alt + t`.
*Mac* if you are on Mac, you should have an application called Terminal. It is often located in your `Applications/Utilities` subfolder; [this page](https://support.apple.com/en-ca/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) from Apple explains more about how to open it on different MacOs versions if you are having trouble locating it. Note that the default shell that comes with newer macs is not bash, it is zsh - it is extremely similar, so the code in this tutorial will work the same, but if you do more complicated things you may notice a difference.  
*Windows* Windows doesn't come with bash, so you will need to install it. One popular option is [git bash](https://gitforwindows.org/). Alternatively, you can `ssh` into a server if you have access to one.  

# Directories and paths  

Before we get started, lets go over a couple more pieces of computer jargon - **directories** and **paths**. A directory is more-or-less the more technical term for a folder. All files on a computer are located within a directory, and directories are organized in a nested hierarchy. The deepest level of the nested hierarchy is called the **root** (eg, `C:\` on Windows or `/` on Linux), and other directories branch off from the root. The list of nested directories from the root to a given file is called the file's **path**.  

# Running commands - basic navigation commands  

To run a command, type or paste the command into the command line, and then hit enter.  

Here we will go over some of the most-commonly used commands: commands for getting around on the command line.  
`pwd` - print current working directory  
`ls` - lists the contents of your current working directory  
`mkdir $name_of_directory` - makes a new directory  
`cd $name_of_directory` - change to a new working directory  
`rmdir $name_of_directory` - remove (delete) an empty directory 
`man $name_of_command` - open the manual for a command (then press "q" to quit the manual)  

First, find out where you are in your computer's filesystem using the `pwd` command ("print working directory"). This will print text as output in the next line of your terminal. This printed output text is called "standard output". The standard output of `pwd` will be the full path from the root of your computer's filesystem to your current working directory. When you run commands, your working directory is the default place where your computer will look for input files, and is the default place where output files appear.  

To find out what is in your working directory, type `ls` into your command prompt, then hit "enter". The text that pops up in your terminal (the "standard output" of `ls`) is a list of all the files in your current working directory.  

Next, let's move around the filesystem. We can do this using the `cd` ("change directory") command. To use it, type `cd` followed by a space, then the name/path of the directory you want to move to. If the directory you want to move to is in your current working directory, you can just give the name of the directory. If it is somewhere else, you will have to specify the path to that directory. Let's move into the directory for this tutorial. If you downloaded the tutorial folder manually, you will need to know where on your computer it ended up.  

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
* Commands are very sensitive to the presence of spaces. If you have a space in the name of a file/directory, it can cause huge headaches as bash will see the space-separated chunks as separate things, not parts of the same name. If you must deal with files/directories with spaces in the name, enclose the name in quotes (eg "Name of file").  
* Different types of quotes are interpreted differently. Single and double quotes mean different things, and critically, curly quotes will cause errors. Spot the difference: `" vs ' vs “ vs ‘`. When you are writing code, make sure you are using a *plain text editor* or code editor instead of a *rich text editor* that will make your quotes curly. Plain text editors include [Visual Studio Code](https://code.visualstudio.com/) and [Sublime Text](https://www.sublimetext.com/). Examples of rich text editors (avoid!) include Microsoft Word and Google Docs.  
* Unlike an interactive text editor, you can't use your mouse to click to move the text cursor. If you made a typo and need to go back, you have to use your arrow keys to move the cursor backwards. (Exception: Macs often let you point-and-click to move your cursor - just hold down the `option` key when you click.  
* Time saver: in many systems, you can press ctrl+a to jump your cursor to the start of the line, and then ctrl+e to jump back to the end of the line. Saves some time if you made a typo way at the beginning of the line!  
* to get help with a command or remind yourself of its flags, you can use the `man` command to open the command's manual page. For example, to open the manual for `mkdir`, do `man mkdir`. To exit the manual and return to the command line, type `q` to quit.  

## Flags  
An important aspect of running commands on the command line is setting flags. These are settings that can alter the behaviour of the command you are running. They are usually single letters or short words, that are placed after a command (separated by a space), like this: `command -a -b -c --flag_d`. That command has four flags: `-a`, `-b`, `-c`, and `--flag_d`. Flags are attached to dashes - generally a single dash for single-letter flags or two dashes for flags that are words. If a flag is a word, it cannot have a space in it (instead, underscores `_` can be used). Often, there will be two synonymous flags you can choose between that do the same thing, a single-letter option for brevity, or a short-word option you can use to make it easier to remember what it does when you go back and read your code in the future.  

The other thing we have been given some commands is/are argument(s). These are also settings that alter the action of the command you are running or the flag you set - they are often the name of input files or output files, or parameters that you need to change/specify for the program you are running. These are distinguished from flags because they are not preceded by dashes. Sometimes arguments are required (eg, `mkdir` would not have anything to do if you didn't tell it the name of the directory it should make), and sometimes they are not required (eg, `ls` defaults to listing your current working directory if you don't give it any arguments).  

Let's add some flags to `ls`. If we just run `ls`, it will tell us the contents of our current working directory. If we add  the flag `-l` and run `ls -l`, it will now give us a more lengthy summary of our files, including handy information like the size of our files, which user owns them, and date/time when they were last modified. Let's now add another flag, `-h`: `ls -l -h` or `ls -lh` (for single-letter flags, you can either give each flag their own dash, or smoosh them together behind the same dash, whatever style looks best to you). `-h` stands for "human-readable", and will convert the file sizes from number of bytes to abbreviations (K for Kilobyte, M for Megabyte, etc).   

# Looking at files

Now we will look at some important commands for reading and manipulating files:  
`cat` - read a file (or text input on the command line) and print the contents  
`less` - look at a file on the command line (without printing anything). Press `q` when done looking. 
`head` - print only the first lines of a file  
`tail` - print only the last lines of a file  
`wc` - count the number of lines/words/characters  
`cut` - print only specific column(s) from a file  
`sort` - sort input  
`uniq` - remove repeated lines (if they are adjacent)  
`paste` - merge files horizontally (paste columns together line-by-line)  

The first command we will look at is `cat`, which stands for "concatenate". This is a handy and frequently-used command that reads contents of a file and prints them out. The most simple way to run it is `cat $Name_of_file`. Let's try it:  
`cat ABBABABA1.txt`  
That will print the contents of ABBABABA1.txt.  
`cat` can also take multiple files as input and concatenate them together in the order they are listed. For example:  
`cat ABBABABA1.txt ABBABABA2.txt`  
That will print the contents of ABBABABA1.txt and then the contents of ABBABABA2.txt.  
Often, we need to save this output, rather than just printing it to the command line. We can redirect it to a file using the `>` symbol to point to a file where the output should be printed. This could be just the file name (in which case it will appear in your current working directory), or it could also include a path to save it in a different directory. Warning! Redirecting output using `>` will overwrite the contents of the file if it already exists, without any warnings. There are many sad stories of people losing their work by accidentally overwriting files using `>`. When a file is overwritten in that way, it is called "clobbering".  
Let's use `cat` to combine two files together and save the results.  
`mkdir -p processed_data`  
`cat ABBABABA1.txt ABBABABA2.txt > processed_data/ABBABABA_concatenated.txt`
Oops! We missed ABBABABA3.txt. We could add it by running `cat ABBABABA1.txt ABBABABA2.txt ABBABABA3.txt > processed_data/ABBABABA_concatenated.txt`, which would erase and remake processed_data/ABBABABA_concatenated.txt, an annoying solution. Instead, we can concatenate ABBABABA3.txt to the end of processed_data/ABBABABA_concatenated.txt without overwriting it, by using `>>` instead of `>`, like this:  
`cat ABBABABA3.txt >> processed_data/ABBABABA_concatenated.txt`   

Now let's take a look at `processed_data/ABBABABA_concatenated.txt`. However, this is a big file, it would not be convenient to run `cat processed_data/ABBABABA_concatenated.txt` and have all that text print to our command line. Instead, let's use another handy command: `less`, which lets us scroll through files without printing them out.   

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
By default, they print 10 lines. We can change this using the `-n` (AKA `--lines`) flag. For example `head -n 5 processed_data/ABBABABA_concatenated.txt` prints only the first 5 lines while `tail -n 5 processed_data/ABBABABA_concatenated.txt` prints only the last 5 lines. You can also `-` or `+` symbols to remove only the first/last n lines without knowing exact what line number they are. Try comparing the results of these:    
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
* `stdin`: "standard input" - input data that is either read from a file (using `<`), typed from the keyboard, or passed to a command using a pipe `|`.
* `stdout`: "standard output" - output that is produced by a command. By default this is printed to the terminal, but it can also be directed to be saved to a file (using `>` or `>>`) or piped to another command using `|`.
* `stderr`: "standard error" - another stream of output that is produced by a command; usually error messages or extra info that is not needed in the main output, like status updates. By default it is printed to the command line, and will not be redirected with `|` or `>` or `>>`. To save it to a file, use `2>` or `2>>`. To make it go to the same place as standard output, use `2>&1`. To make it not be printed, use `2>/dev/null`.

Let's find out how many samples are in our dataset. Scroll back to look at the file `processed_data/ABBABABA_concatenated.txt`. This file contains sample names in column 2. These samples might be repeated multiple times. To find out how many samples we have, we should see how many unique sample IDs occur in column 2. We can do that using the `cut`, `sort`, `uniq`, and `wc` commands. (There are of course fancier ways we could code it in other languages, but let's build a pipeline with just bash basics).  

First, let's isolate column 2. `cut` grabs the columns that we specify, and we can use the `-f` flag to tell it which fields (column numbers) to select. By default, `cut` expects columns to be tab-delimited, otherwise we would need to tell it what delimits out columns using the `-d` flag.  
Let's check that it works! To avoid printing out the whole long file, let's just grab the first 5 lines and pass those to `cut` as a test. Try these:  
`head processed_data/ABBABABA_concatenated.txt | cut -f 2`
`head processed_data/ABBABABA_concatenated.txt | cut -f 2-4 #we can ask for a range of columns`
`head processed_data/ABBABABA_concatenated.txt | cut -f 2-4,6 #we can also use commas to list columns`
`head processed_data/ABBABABA_concatenated.txt | cut -f 1 -d "3" #we can ask it to use anything we want as the column delimiter`

So far, `cut -f 2` does what we want, selecting the column containing our sample names. Now, let's remove any duplicates. We can do this using the `uniq` command, which deduplicates any repeated lines to keep only one copy of each. However, `uniq` only compares adjacent lines, so repeated lines have to be right after to each other to be detected. We can ensure this will be the case by using the `sort` command to sort the lines. This will sort lines alphanumerically - if we wanted to, we could change that behaviour (for example `--ignore-case` to treat upper and lower case characters the same, `-n` AKA `--numeric-sort` to sort numerically, or `-r` AKA `--reverse` to reverse the sort). If we hadn't already isolated the column we wanted, we could also specify which field(s) to sort by using `-k` AKA `--key` to specify the column numbers. By default, `sort` uses whitespace as a column delimiter, but we can change that using `-t`.    
`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort`  
`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort -r #reverse order`  
`head processed_data/ABBABABA_concatenated.txt | sort -k 2 #sort on column 2`  
Especially compare how it treats numbers with different settings:  
`head processed_data/ABBABABA_concatenated.txt | cut -f 8 | sort #sort alphanumerically by default`  
`head processed_data/ABBABABA_concatenated.txt | cut -f 8 | sort -n #sort numerically`  

Can you decipher what this is doing?  
`head processed_data/ABBABABA_concatenated.txt | cut -f 8 | sort -t "." -k 2 -n `  
Answer: It is sorting by the numbers after the decimals, numerically (It is using the "." as the column delimiter).  

`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort` is doing what we want. We can then send it to `uniq` to deduplicate the list. Another nice thing `uniq` can do is to count how many times each line was repeated using the `-c` flag.
`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq`
`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq -c #counts the number of times each sample occured`

`head processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq` is doing what we want. Lastly, we just need to count how many samples are in this de-duplicated list. We can do that using `wc -l`. Let's commit this time and run it on the whole file, instead of running `head` first.
`cut -f 2 processed_data/ABBABABA_concatenated.txt | sort | uniq | wc -l`  
There we have it, the number of samples in the file.  
Oh, but wait! You may have noticed earlier that one of the lines in the file was the header, not an actual sample! Our number is therefore one too high. We could just subtract this in our heads, but what if we forget about the header the next time we run this code? Let's get rid of it. There are two easy ways to do this - we could use `tail` to cut it off, or we could use pattern matching to exclude it. We have already learned about `tail`, so try building a pipeline incorporating `tail` to remove the header from our count.
Solution:
`tail -n +2 processed_data/ABBABABA_concatenated.txt | cut -f 2 | sort | uniq | wc -l`  
or
`cut -f 2 processed_data/ABBABABA_concatenated.txt | tail -n +2 | sort | uniq | wc -l`  
(we can put tail before or after `cut`, but we can't put it after `sort`, since we don't necessarily know ahead of time where it will end up after sorting. 

One last basic file editing piece for our toolkit is `paste`. The `paste` command can take multiple files/inputs and merge them horizontally as columns, separated by tabs (by default).  

Let's pretend that our SampleID data was in a different file than the rest of our data. We can make set up this scenario like this:  
`cut -f 2 ABBABABA.txt > toy_SampleID`  
`cut -f 1,3- ABBABABA.txt > toy_OtherColumns`  
In this scenario, we could put them together like this: `paste toy_SampleID toy_OtherColumns > toy_MergedColumns`  
Check if it worked: `head toy_MergedColumns`  
Note that `paste` will paste them together in the order you specify.  
When using `paste`, make sure you are very confident that all of your lines are in the same order! Paste will not warn you if your files are sorted differently or differ in length.  

## redirecting standard error
Redirecting stderr is similar to redirecting stdout, but the code is slightly different so that you can redirect stderr and stdout to separate places. By default, stderr gets printed to the command line, and if you redirect the stdout, stderr will continue to get printed to the command line. To redirect stderr, instead of using `>` or `>>`, use `2>` or `2>>`. (the inputs and outputs are assigned "file descriptors": "2" is stderr, while "1" is stdout and "0" is stdin). For example: `command --settings input_file > output.txt 2> errors.log` will send stdout and stderr to separate files. This is handy for saving error messages to a log so that you can refer to them later if needed.  

If you want the stderr to instead be printed alongside stdout in the same file (with the lines interspersed as they are generated), you can use `2>&1` which means "send stderr to the same place as stdout". For example: `command --settings input_file > output.txt 2>&1` will send both stdin and stdout to the same place. This can be handy when both stdout and stderr are log messages that you want to save to a single log file, or if you want to be able to send error messages through a pipe to be processed by the next command.  

We can also use another trick to make error messages go away entirely - we can redirect the standard error to a place called `/dev/null`. This is a special file which acts like a "black hole" in the computer. It is an empty file, and any data that gets sent to it is immediately discarded. Redirecting our error messages to `/dev/null` gets rid of them so they never get printed. This can be handy when you need to loop through 2000 files with commands that produce a lot of stderr messages and you don't want all that text flying at you on the command line.  

# making a file from scratch
cat
echo
nano
printf


# Day 2 materials
(in progress)

# efficiency commands
time, htop, df, screen, history, ssh, scp

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
`Thing_to_echo="This is a sentence with spaces in it"
echo $Thing_to_echo`

Variables can be a little finicky at times. If a variable contains any whitespace or special characters, it can cause unexpected things to happen when the code is run. To stop that from happening, it is good practice to wrap the variable in double quotes, like this: `head -n "$num_lines" ABBABABA.txt` or `echo "$Thing_to_echo"`. If there were no unexpected characters in your variable, the double quotes won't do anything (except make your code look a little more sparkly), but getting into the habit of using double quotes may eventually save you some headache.  

# PATH variable
Bash includes some special variables that are set automatically - environmental variables. Most of them handle background things that you won't need to alter, but one environmental variable that you may occasionally need to interact with is `$PATH`. `$PATH` is a list of paths which tells bash where it should look for executables (code) when running commands. For example, when running `ls`, bash scrolls through the directories listed by $PATH until it finds the code for the `ls` program. Built-in commands (like `ls`, `cd`, etc) have their code in standard locations that are already included in `$PATH`. To run other commands (eg., programs you download or scripts you write), you will either need to place them into a directory that is in PATH, or specify the whole path to the executable when you run it, or add its directory to PATH so that bash can find it.

You can find out what directories are included in your `PATH` by running `echo $PATH`. This will give a list of paths separated by `:` colons. 
If you want to be able to run a program in a different directory without specifying the full path when you run it, or if a program you are running needs to be able to run dependencies, you can add a new path to your PATH variable by redefining PATH variable with your new path separated by the rest of the paths by a ":".  
For example, let's imagine we want to add `/home/scripts` to our $PATH. We can do that like this:  
`PATH="$PATH:/home/scripts"`  
This has the effect of appending `:/home/scripts` to the existing PATH variable. Bash will now search through `/home/scripts` after searching through the other paths that were already in PATH. If you want bash to search the new path *before* searching other paths (bash will use the first copy that it finds), you can instead prepend your new path to the PATH variable, like this:  
`PATH="/home/scripts:$PATH"`  



* which

# for loops, while loops, if statements
* syntax for loops and if statements
* brace expansion
* cat samples.txt | while read sample ; do (...) ; done
* if statements checking if a file exists before doing a command
* seq

# gnu Parallel
* cat samples.txt | parallel (...)

# awk
(in progress)
* using awk for simple one-liners

# file permissions
When sharing files between users or when writing your own scripts, one concept that you may encounter is **permissions**. Permissions control who can view or edit a file, and whether a file can be executed as code. Those three actions are controlled separately, and are as follows:  
* Read: a user can open and view the contents of a file.
* Write: a user can edit the file.
* Execute: a user can run the file as code.

By default, most files that you create will have read and write permissions for you, but will not have execute permissions. That is a safety measure that stops you from accidentally running a random (or malicious) file as code. If you try to run something that does not have execute permissions, you will get the error message `Permission denied`. That means that before you can run a newly-written script, you need to tell bash that you do in fact intend for the file to be executable. This is done with the `chmod` function. `chmod` can change the owners and permissions of a file that you own. 

If you want to add executable permissions to a file, you use `+x` with `chmod`, for example, `chmod +x script.py`. After doing that, you should be able to run your code. One thing to be aware of is that sometimes, drives can be set up such that nothing on the drive can be executed no matter the permissions you set. If that is the case, the owner of the server should have informed you of where you can place executable files so that they can run.  

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
`alias nia="ssh elsemikk@niagara.scinet.utoronto.ca"`: this allowed me to `ssh` into the niagara cluster without having to type the whole address.  

All those aliases have the form `alias name_of_alias="command that you want to make an alias for"`.

Try writing or picking a bash alias that would be useful to you. You can add this to your account's `~/.bash_aliases` file any way that you like to edit a text file, for example, using `cat` or `nano`. Once you have added an alias, it won't take effect right away, because bash won't have read your alias file. You will need to close your session and open a new session, at which point bash will read your alias file.    
To edit the file with `cat`, run `cat >> ~/.bash_aliases`, then type or paste what you would like added, hit "enter" to add a line break, then type `ctrl+d` when you are done.  
To edit the file with `nano`, run `nano ~/.bash_aliases`, paste or type the alias you want to add, then exit nano with ctrl+x. It will ask you if you want to save you changes; type `y` if you do.  

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
2) `grep "^rubrocapilla\t.*\tmentalis" ABBABABA.txt
3) `sed "s/rubrocapilla/PLACEHOLDER/g; s/erythrocephala/rubrocapilla/g; s/PLACEHOLDER/erythrocephala/g" ABBABABA.txt`. 
4) `cut -f 2 ABBABABA.txt | sed "s/Ceratopipra_/Ceratopipra@/g; s/_.*$//g; s/@/_/g; s/SampleID/Species_name/g" > temp_SpeciesNames
cut -f 1-3 ABBABABA.txt | paste - temp_SpeciesNames > temp_FourColumns
cut -f 4- ABBABABA.txt | paste temp_FourColumns - > `  
Note - some of those are a bit clunky and could be done much more elegantly using other tools, a different language, or more advanced syntax - this was just meant to illustrate that you can do quite a bit with only some very basic commands/syntax.  


