



# Anatomy of the Command Line

*Very broad overview and terms*
Most of the time when using computers, we are using a **graphical user interface** (GUI), something that lets us point our mouse and click on buttons or browse through menus. A more direct way of communicating with the computer is through the **command line**, where you type lines of text containing commands for the computer. To use the command line, you need a program called a **shell** to interpret your commands, and the most popular shell used in bioinformatics (and more widely) is **bash**. Bash is used with Linux and UNIX operating systems, and also comes installed on macs. To use the shell, you need an application referred to as a **terminal**. The terminal is the application you open and interact with, the command line is where you type your commands, and the shell (bash) is the program that interprets your commands and tells your operating system what to do. 

Here, we will go over the basics of working on the command line and writing simple bash code. This requires you to have access to a terminal program with bash. Accessing that varies depending on your operating system.

*Linux* if you are on Linux, you should already have an application called Terminal, which can be opened from your applications, or with `ctrl + alt + t`.
*Mac* if you are on Mac, you should have an application called Terminal. It is often located in your `Applications/Utilities` subfolder; [this page](https://support.apple.com/en-ca/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) from Apple explains more about how to open it on different MacOs versions if you are having trouble locating it. Note that the default shell that comes with newer macs is not bash, it is zsh - it is extremely similar, so the code in this tutorial will work the same, but if you do more complicated things you may notice a difference.  
*Windows* Windows doesn't come with bash, so you will need to install it. Two popular options include [git bash](https://gitforwindows.org/) or [Windows Subsystem for Linux (WSL)]. Alternatively, you can `ssh` into a server if you have access to one.  

# Directories and paths

Before we get started, lets go over a couple more pieces of computer jargon - **directories** and **paths**. A directory is essentially the more technical term for a folder. All files on a computer are located within a directory, and directories are organized in a nested hierarchy. The deepest level of the nested hierarchy is called the **root** (eg, `C:\` on Windows or `/` on Linux), and other directories branch off from the root. The list of nested directories from the root to a given file is called the file's **path**.

# Running commands - basic navigation commands

To run a command, type or paste the command into the command line, and then hit enter.

Here we will go over some of the most-commonly used commands: commands for getting around on the command line.  
`pwd` - print current working directory  
`ls` - lists the contents of your current working directory  
`mkdir $name_of_directory` - makes a new directory  
`cd $name_of_directory` - change to a new working directory  
`rmdir $name_of_directory` - remove (delete) an empty directory  

First, find out where you are in your computer's filesystem using the `pwd` command ("print working directory"). This will print text as output in the next line of your console. This printed output text is called "standard output". The standard output of `pwd` will be the full path from the root of your computer's filesystem down to your current working directory. When you run commands, your working directory is the default place where your computer will look for input files, and is the default place where output files appear.  

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
* Unlike an interactive text editor, you can't use your mouse to click to move the text cursor. If you made a typo and need to go back, you have to use your arrow keys to move the cursor backwards.
* Time saver: in many systems, you can press ctrl+a to jump your cursor to the start of the line, and then ctrl+e to jump back to the end of the line. Saves some time if you made a typo way at the beginning of the line!

## Flags
An important aspect of running commands on the command line is setting flags. These are settings that can alter the behaviour of the command you are running. They are usually single letters or short words, that are placed after a command (separated by a space), like this: `command -a -b -c --flag_d`. That command has four flags: `-a`, `-b`, `-c`, and `--flag_d`. Flags are attached to dashes - generally a single dash for single-letter flags or two dashes for flags that are words. If a flag is a word, it cannot have a space in it (instead, underscores `_` are used). Often, there will be two synonymous flags you can choose between that do the same thing, a single-letter option for brevity, or a short-word option you can use to make it easier to remember what it does when you go back and read your code in the future.  
The other thing we have been given some commands is/are argument(s). These are also settings that alter the action of the command you are running or the flag you set - they are often the name of input files or output files, or parameters that you need to change/specify for the program you are running. These are distinguished from flags because they are not preceded by dashes. Sometimes arguments are required (eg, `mkdir` would not have anything to do if you didn't tell it the name of the directory it should make), and sometimes they are not required (eg, `ls` defaults to listing your current working directory if you don't give it any arguments).  

Let's add some flags to `ls`. If we just run `ls`, it will tell us the contents of our current working directory. If we add  the flag `-l` and run `ls -l`, it will now give us a more lengthy summary of our files, including handy information like the size of our files, which user owns them, and date/time when they were last modified. Let's now add another flag, `-h`: `ls -l -h` or `ls -lh` (for single-letter flags, you can either give each flag their own dash, or smoosh them together behind the same dash, whatever style looks best to you). `-h` stands for "human-readable", and will convert the file sizes from number of bytes to abbreviations (K for Kilobyte, M for Megabyte, etc).   


# Looking at files

Now we will look at some important commands for reading and manipulating files:  
`cat` - read a file (or text input on the command line) and print the contents  
`less` - look at a file on the command line (without printing anything). Press ctrl+d when done looking. 
`head` - print only the first lines of a file  
`tail` - print only the last lines of a file  
`cut` - print only specific column(s) from a file  
`sort` - sort input  
`uniq` - remove repeated lines (if they are adjacent)  
`wc` - count the number of lines/words/characters  
`paste` - merge files horizontally (paste columns together line-by-line)  

The first command we will look at is `cat`, which stands for "concatenate". This is a handy and frequently-used command that reads contents of a file and prints them out. The most simple way to run it is `cat $Name_of_file`. Let's try it:  
`cat ABBABABA1.txt`  
That will print the contents of ABBABABA1.txt.  
`cat` can also take multiple files as input and concatenate them together in the order they are listed. For example:  
`cat ABBABABA1.txt ABBABABA2.txt`  
That will print the contents of ABBABABA1.txt and then the contents of ABBABABA2.txt.  
Often, we need to save this output, rather than just printing it to the command line. We can redirect it to a file using the `>` symbol to point to a file where the output should be printed. This could be just the file name (in which case it will appear in your current working directory), or it could also include a path to save it in a different directory. Warning! Redirecting output using `>` will overwrite the contents of the file if it already exists, without any warnings. There are many sad stories of people losing their work by accidentally overwriting files using `>`.  
Let's use `cat` to combine two files together.  
`mkdir -p processed_data`  
`cat ABBABABA1.txt ABBABABA2.txt > processed_data/ABBABABA_concatenated.txt`
Oops! We missed ABBABABA3.txt. We could add it by running `cat ABBABABA1.txt ABBABABA2.txt ABBABABA3.txt > processed_data/ABBABABA_concatenated.txt`, which would erase and remake processed_data/ABBABABA_concatenated.txt, an annoying solution. Instead, we can concatenate ABBABABA3.txt to the end of processed_data/ABBABABA_concatenated.txt without erasing it, by using `>>` instead of `>`, like this:  
`cat ABBABABA3.txt >> processed_data/ABBABABA_concatenated.txt`   

Let's take a look at `processed_data/ABBABABA_concatenated.txt`. However, this is a big file, it would not be convenient to run `cat processed_data/ABBABABA_concatenated.txt` and have all that text print to our command line. Instead, let's use another handy command" `less`, which let's us scroll through files without printing them out.   

Let's try it: `less processed_data/ABBABABA_concatenated.txt`  

Your screen will now show the contents of `processed_data/ABBABABA_concatenated.txt`. From here, you can scroll up and down to look through the file. There are a series of keyboard shortcuts to help navigating, for example:  
* type `spacebar` to jump to the next "page"
* type `G` (uppercase) to go to the end of the file
* type `g` to go to the start of the file
* type `/` to search the contents of the file: type `/`, then what you want to search for, then `enter`. For example, try typing `/Trinidad`  
If you get stuck typing something, press `ctrl + c` to cancel what you just typed.  
To exit `less` and go back to the command line, type `q`.  

Another nice way to preview files is using `head` and `tail`. `head` prints only lines from the beginning of a file, while `tail` prints only lines at the end of the file. Try it out:  
`head processed_data/ABBABABA_concatenated.txt`  
`tail processed_data/ABBABABA_concatenated.txt`  
By default, they print 10 lines. We can change this using the `-n` (AKA `--lines`) flag. For example `head -n 5 processed_data/ABBABABA_concatenated.txt` prints only the first 5 lines while tail -n 5 processed_data/ABBABABA_concatenated.txt prints only the last 5 lines. You can also `-` or `+` symbols to remove only the first/last n lines without knowing exact what line number they are. Try building a command with these:    
* `head -n 2` AKA `head -n +2`: print the first two lines (start at the beginning and then stop at line 2).  
* `head -n -2`: remove the last 2 lines (start at the beginning and then stop at line -2, ie, 2 lines before the end). Not all versions support this usage, in which case you get the error message `head: illegal line count`.  
* `tail -n 2` AKA `tail -n -2`: print the last two lines (start 2 lines before the end and print until the end of the file)  
* `tail -n +2`: remove the first line (start at line 2 and print until the end of the file).  

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

## redirecting standard error
Redirecting stderr is similar to redirecting stdout, but the code is slightly different so that you can redirect stderr and stdout to separate places. By default, stderr gets printed to the command line, and if you redirect the stdout, stderr will continue to get printed to the command line. To redirect stderr, instead of using `>` or `>>`, use `2>` or `2>>`. (the inputs and outputs are assigned "file descriptors": "2" is stderr, while "1" is stdout and "0" is stdin). For example: `command --settings input_file > output.txt 2> errors.log` will send stdout and stderr to separate files. This is handy for saving error messages to a log so that you can refer to them later if needed.  

If you want the stderr to instead be printed alongside stdout in the same file (with the lines interspersed as they are generated), you can use `2>&1` which means "send stderr to the same place as stdout". For example: `command --settings input_file > output.txt 2>&1` will send both stdin and stdout to the same place. This can be handy when both stdout and stderr are log messages that you want to save to a single log file, or if you want to be able to send error messages through a pipe to be processed by the next command.  

We can also use another trick to make error messages go away entirely - we can redirect the standard error to a place called `/dev/null`. This is a special file which acts like a "black hole" in the computer. It is an empty file, and any data that gets sent to it is immediately discarded. Redirecting our error messages to `/dev/null` gets rid of them so they never get printed. This can be handy when you need to loop through 2000 files with commands that produce a lot of stderr messages and you don't want all that text flying at you on the command line.  


Problems:
* count how many different populations there are in column P1.
* count how many samples of *C. rubrocapilla* there are.
* change all instances of "InambariW" to "Inambari_West"
* remove sample Ceratopipra_erythrocephala_CN626 from the dataset
* select the 20 entries with the lowest value of BBAA
* select the 20 entries with the highest value of ABBA
* make a new file containing all entries with sample Ceratopipra_chloromeros_FM433680, but don't include the ABBA, BABA, or BBAA columns, and make sure it is sorted by Z score from highest to lowest. (You can do the pipeline in 2 parts).

`cut -f 1 | tail -n +2 | sort | uniq | wc -l`  
`cut -f 2 | grep "rubrocapilla" | sort | uniq | wc -l`  
`sed "s/InambariW/Inambari_West/g"`  
`grep -v "Ceratopipra_erythrocephala_CN626"`  
`tail -n +2 | sort -n -k 8 -r | head -n 20` OR `tail -n +2 | sort -n -k 8 | tail -n 20`  
`tail -n +2 | sort -n -k 9 | head -n 20`  
`head -n 1 > new_data.txt ; grep "Ceratopipra_chloromeros_FM433680" | cut -f 1-7 | sort -n -k 5 -r >> new_data.txt' 


Harder problems:  
(There are fancier ways to do these things much more succinctly, but can you do it using only command/regex/flags from this tutorial?)  
* split column 2 so that instead of giving the full sample name (eg. Ceratopipra_chloromeros_B106768), it has the species name in one column and the sample number in a different column (eg, Ceratopipra_chloromeros  B106768).  
* select all the columns where rubrocapilla is in column P1 and mentalis is in column P3  
* oops, name mixup. Change all instances of rubrocapilla to erythrocephala and all erythrocephala to rubrocapilla.  
* Add a new column to the file. This new column should contain the name of the species for the sample in column 2, but don't alter the contents of column 2. Place this new column in between column "P3" and column "D". You can use up to 3 lines of code for this.  

Here are my solutions:  
`sed "s/SampleID/SpeciesName\tSampleNumber/g; s/Ceratopipra_/Ceratopipra@/g; s/_/\t/g; s/Ceratopipra@/Ceratopipra_/g" ABBABABA.txt`. 
`grep "^rubrocapilla\t.*\tmentalis" ABBABABA.txt
`sed "s/rubrocapilla/PLACEHOLDER/g; s/erythrocephala/rubrocapilla/g; s/PLACEHOLDER/erythrocephala/g" ABBABABA.txt`. 
`cut -f 2 ABBABABA.txt | sed "s/Ceratopipra_/Ceratopipra@/g; s/_.*$//g; s/@/_/g; s/SampleID/Species_name/g" > temp_SpeciesNames
cut -f 1-3 ABBABABA.txt | paste - temp_SpeciesNames > temp_FourColumns
cut -f 4- ABBABABA.txt | paste temp_FourColumns - | less`  
Note - some of those are a bit clunky and could be done much more elegantly using other tools, a different language, or more advanced syntax - this was just meant to illustrate that you can do quite a bit with only some very basic commands/syntax.  


