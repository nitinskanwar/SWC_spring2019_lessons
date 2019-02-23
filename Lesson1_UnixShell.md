# SWC_Spring2019: Feb23-24

## Lesson1: Linux Shell: Part 1
Instructor: Ayda

- [x] Make `SWC_spring2019` folder on you desktop
- [x] Download Data.zip:
https://raw.githubusercontent.com/utacarpentries/2019-02-23-UTA/gh-pages/data/Data.zip
- [x] Unzip and add `Data` folder to `SWC_spring2019` folder


### 1. Why learn Linux?
+ Most widely used OS in research and technology
+ Open-source: free to get, free to use, free to modify.
+ Availability: Linux VM, Linux servers/clusters (UTA, TACC)
+ CLI (command line interface) and GUI (graphical user interface) are available


### 2. Bash as shell program to interact with Linux OS

+ Bash is one of shell programs that can be used to interact with Linux OS. It is a program that runs other programs and it is also a programming language itself.
+ Bash is available on Unix/Linux/mac machines by default through Terminal. On Windows, bash is available through GitBash that you installed earlier. Both applications provide command-line interface (CLI) and will be referred in our lessons as "terminal" or "terminal window".

Let’s get familiar with the terminal first: prompt, commands, output. Open your terminal - you will see text with `$` as the last character. The text displays your username, name of the computer and your location. The system is waiting for your commands after `$` sign.
```
# who am I? Try
$ whoami
```
When the user types a command and then presses the enter (or return) key, the computer reads it, executes it, and prints its output. This is known as Read-Evaluate-Print loop of CLI. For example, here you ask to print a message with 'echo' command. Try:

```
$ echo "Welcome to our workshop"
```
`echo` command is read, executed and the output is printed. Only commands known to bash will be executed. Try:
```
$ stop this session 
```
You will see `command not found` message. This means that Bash does not recognize this command.


Here is the list of the commands we will use in the first half of the lesson. Not too many, but when used effectively, do simplify and speed up your work enormously!

``` shell
$ echo       # print
$ whoami     # prints username
$ pwd        # print working directory path
$ cd         # change directory
$ mkdir      # make directory
$ touch      # create empty file
$ cat        # view file/concatinate files
$ mv         # move/rename file
$ cp         # copy file
$ rm         # delete file
``` 

You can get an idea about the functionality of bash commands from [this Bash commands cheat sheet](https://learncodethehardway.org/unix/bash_cheat_sheet.pdf)


### 2a. Bash: navigate through your file system
Know who you are and where you are! Let’s talk about file system (folders and files) and how to find your way around …
Note: when you see `#` in the code below, it serves as a comment to explain the code, not a command. Commands that you should try are typed after `$` sign 

And if I were to ask you where are you? Minimize your terminal for a second. You are back in your familiar GUI environment. Where are you? What folders are immediately available to you? Desktop folders? Open the terminal. Can you navigate to desktop using CLI?

```
# where am I? Try
$ pwd  
```
`pwd` command prints your current location (or path to working directory) in the computer. The path you see now should display the path to your home directory. You can check this by typing `echo $HOME`

Let's talk more about the output of `pwd`.

**File system**: root, working, current, parent directories… 

![](http://i1.wp.com/mycodinglab.com/wp-content/uploads/2014/01/Linux-File-System-Mycodinglab.jpg)


File systems have a hierarchial structure. In a hierarchical file system, the folders and files are displayed in groups, which allows the user to see only the files they’re interested in seeing. For example, in the picture above, the root folder contains folders named `bin`, `etc`, `home`, *etc.* Each of these folders could have hundreds of their own files, but unless they are opened the files are not displayed.

In GUI the user views the contents of each folder by double-clicking the folder.

With command-line user interface , the  folders (also known as directories) are listed as text.


Let's see how you would list the files inside directory using command-line interface:

```
# list files
$ ls

# use flags to show different details: Try
$ ls -F
```

`-F` indicates file type — Adds a symbol to the end of each listing:
`/` to indicate a directory; 
`@` to indicate a symbolic link to another file;   
`*` to indicate an executable file

There are special help pages (manuals) that explain what every command does and what options (flags) can be used with it. To access these pages, use `man` command
```
$ man ls
# or
$ ls --help
```
The output provides full documentation for a command, everything you need to know is there!

Other useful options of `ls` command are:
```
# Option -a (all) — Lists all files in the
#directory, including hidden files (.filename).
$ ls -a

#Option -l (long) — Lists details about contents,
#including permissions (modes), owner, group,
#size, creation date, whether the file is a link
#to somewhere else on the system and where its link points.
$ ls -l
```
So far, you were looking at the contents of your home directory. Let's see the contents of the Desktop directory

```
$ ls -F Desktop  
```
If you do not have `Desktop` directory, it will give you an error...


#### **Challenge 1**

Remember, we made `SWC_spring2019` folder in the beginning of workshop and moved our `Data` folder there. Can you now list files in `SWC_spring2019` directory from your current directory?

#### **Solution:** 
```
ls -F Desktop/SWC_spring2019/
```
####

In the exercise above, you viewed files in `SWC_spring2019`  directory while in home directory. But you can change the directory and move directly into `SWC_spring2019`  directory.

```
$ cd Desktop
$ pwd

$ cd SWC_spring2019
$ pwd

# you could have done it in one step: 
$ cd Desktop/SWC_spring2019

$ ls -F
```
So, `cd` lets you change directories into daughter subdirectories. What if you need to go back?

```
$ cd Desktop     
#does not work, cd gets you into 
#directories within current directory only

# But try this:
$ cd ..          #works!

# Why? List all files in `SWC_spring2019` folder 
$ ls -F -a
```
`..` is a special directory name meaning “the directory containing this one”, or the parent of the current directory and `.` means “the current working directory”.


But `cd` without any arguments takes you ... where?
```
$ cd

$ pwd
```

**Relative vs Absolute Paths**

Navigation with `cd ..` is an example of the relative path - you indicate where you want to go relative to the location you are currently in. in contrast, when you give an absolute path to the folder or file, you will end up there no matter what your current location within file system is.

```
$ pwd  #specifies absolute path to current directory
```
Notice the format of the absolute path: it starts with forward slash indicate the root directory with every subsequent forward slash separating folders that you go through to get the final folder or file


Other shortcuts:
```
$ cd ~ #takes you home
$ cd - #takes you BACK one directory, NOT UP!!!
```

#### **Challenge 2**
Make a diagram of our directory structure (~/Desktop/SWC_spring2019/Data/) and practice navigation commands.

a) Find out where you currently are
b) Go to `Data` folder, what is there? 
c) Go back where you came from (with `cd -` command)
d) Go one directory up
e) Try relative and absolute paths
f) Get comfortable navigating across file system


### 2b. Bash: make new files and directories
Now that you know how to navigate your file system and list files that are already there, let’s see how we can create new folders and files.
You can create, delete, move, copy, rename files and directories using linux commands.

```
#Navigate to `SWC_spring2019` folder
$ cd 
$ cd Desktop/SWC_spring2019

#check you are in the correct place
$ pwd

#create new directory for this lesson
$ mkdir unix_shell

#check
$ ls

#go into Linux directory
$ cd unix_shell

#now lets make two more directories here
$ mkdir India
$ mkdir Japan

#now check to see if you have these
#two directories in the folder
$ ls 

#create file
$ touch MyFirstFile.txt   # creates empty file

#view file
$ cat MyFirstFile.txt 

#Or create and open MyFirstFile.txt
#if you have Sublime Text as test editor
$ subl MyFirstFile.txt

#if you are on mac working with default text editor
$ open MyFirstFile.txt 


```
Open `MyFirstFile.txt` in text editor
Type:
```
"This is Software Carpentry Workshop"
```
Save and close it.

Now let's open the file in Bash:

```
$ cat MyFirstFile.txt
```
You should see the line `This is Software Carpentry Workshop` in the terminal


Now lets try to rename, move, copy and delete files
```
# move/rename file
# general syntax: mv $source $destination
$ mv MyFirstFile.txt MyFirstScript.sh

# Now try to move (but do not rename)
# MyFirstScript.sh to Japan folder
# remember, you are currently in `unix_shell`

$ mv MyFirstScript.sh Japan/

# Copy file from `Japan` to `unix_shell`
# General cp syntax: cp $source $destination
$ cp Japan/MyFirstScript.sh .
# remember `.` means working directory
# 
#Now lets navigate to folder ‘India’
$ cd India/

#Now copy the file ‘MyFirstScript.sh’ to India
cp ../MyFirstScript.sh .

# Delete file !!! CANNOT BE UNDONE
# clean up `India`
$ rm MyFirstScript.sh  

# now lets clean up `unix_shell`
#go back to unix_shell
$ cd ..

#try to delete folders India and Japan
rm -r India Japan
#deletes the folders India and Japan

```

#### **Challenge 3**

Next we will work with files from the `Data` folder that you moved to `SWC_spring2019` folder in the beginning of this workshop. Please move `Data` folder to `unix_shell` folder. We will keep all the files for Linux lesson in the `unix_shell` folder from now on. Make sure you understand the directory structure of `SWC_spring2019` before we continue.

**Solution**

```
cp -r Data unix-shell

# SWC_spring2019 directory structure
SWC_spring2019
  -> Data/
  -> unix_shell/
        -> Data/

```

-------- coffee break ---------------

## Linux part 2: Working with text files

Instructor: Farah
            

#### Learning objectives:

- linux tools to manipulate text files
- working with multiple files
- shell scripts



### 2c. Bash: manipulate text files

Here is the list of the commands we will use in this second half of the lesson.

```
$ wc         #word count
$ head/tail  #display start/end of file
$ cut        #extract fields(columns) of interest from file
$ sort       #sort file
$ uniq       #select uniq lines only
$ grep       #select rows based on content
```
Let's start with looking at some real data.
You copied`Data` folder into `unix-shell` before the break. Let's see what is in `Data` folder.

How will you do this?
Start from `SWC_spring2019` folder.
```
$ cd unix_shell

# view folder contents:
$ ls 

# go to Data
$ cd Data

# What is here? 
$ ls Data
```
Here we have a file, `gapminder.txt` and a folder, `ByCountry`. We will be working with one of the files in `ByCountry` folder and return to `gapminder.txt` later.

```
$ cd ByCountry
$ ls
```
Looks like we have some information about different countries here. Let's explore `Uruguay.txt`
```
$ cat Uruguay.txt
# note: use tab completion feature by typing the beginning of the text file name and then `tab`
```
What information do we have here? This file is short and you can examine it by eye. But in case the file is long, you want to be able to examine datasets like that with Linux commands. 
Let's copy`Uruguay.txt` to `unix_shell` folder and then play with the dataset.

```
#how would you copy to unix_shell?
$ cp Uruguay.txt ../../

# change directory to unix_shell
$ cd ../../
```
Some questions you might want to ask about this file:

- What is in the file?
- How big is this file?
- What is the highest life expectancy?


Q1: what is in the file?
```
$ cat Uruguay.txt
$ less Uruguay.txt
$ head -n Uruguay.txt
$ tail -n Uruguay.txt
```
Q2: how big is your file?
```
#how big is your file `wc` outputs lines, words, bytes
$ wc Uruguay.txt  
$ wc -l Uruguay.txt
```
Q3: What is the highest life expectancy? We need more than one step here! We need to extract numerical values in the 4th column,sort them numerically and record the max value to file.
```
#remove the header
# Use 'grep' to select lines that contain the word 'Uruguay'
$ grep 'Uruguay' Uruguay.txt >Uruguay_noH.txt

#or you can select lines that DO NOT contain the word 'country' that our header starts with
grep -v 'country' Uruguay.txt > Uruguay_noH.txt

# get 4th column
# Use 'cut' to select column
$ cut -f4 Uruguay_noH.txt > Uruguay_LE.txt

#sort output numerically and write to new file
$ sort -n Uruguay_LE.txt > Uruguay_LE_sorted.txt

#finally get the last line with max value
$ tail -n 1 Uruguay_LE_sorted.txt > Uruguay_LE_max.txt
```
Notice that to get max life expectancy in this dataset we created three intermediate files that we do not really need... One way to avoid generating such files is to string different commands together. This is known as ‘piping’

**Pipes**

Now let’s see how we can string commands together.
We use `|` symbol to pass the output of one command as an input to the next command. 
Our question 3 can be answered with one line of code without creating unnecessary intermediate files!
```
$ grep 'Uruguay' Uruguay.txt | cut -f4 | sort -n |tail -n1 > Uruguay_LE_max2.txt
```
#### **Challenge 4**
Use pipes to find the year with the highest life expectancy in `Sweden.txt` Record the year to `Sweden_YearWithMaxLE.txt`
First, copy `Sweden.txt` to `unix-shell`:
`cp Data/ByCountry/Sweden.txt .`
Hints: 1) to select multiple columns, use `cut -fcol1,col2` For example, to select columns 2 and 3, use `cut -f2,3` 2) to sort by column 2, use `sort -k2`

**Solution**
```
$ grep 'Sweden' Sweden.txt | cut -f3,4 |sort -n -k2|tail -n1|cut -f1 >Sweden_YearWithMaxLE.txt
```

### 2d. Working with multiple files

There are two ways we can work with multiple files at the same : 
- using wildcards
- using loops 

**Wild cards**
If we want to apply a command to a group of files , we can use `*` wildcard:
`*` substitutes for any 0 or more characters

```
$ cd Data/ByCountry

#list all .txt files
$ ls *.txt

#count lines in all .txt files that start with 'G
$ wc -l G*.txt
```

**Loops**

First, let's talk about variables in bash.

Varible name: myName; value assigned to it: Your Name
```
#try this
$ myName=Joe  #variable assignment
$ echo Joe  
$ echo myName

# need `$` to get the value of the variable
$ echo $myName 
```

General syntax of for loop in Bash:

```
for VARIABLE in file1 file2 file3
do
	command $VARIABLE
done
```
You can write it as one line:
```
$ for VARIABLE in file1 file2 file3; do command $VARIABLE; done
```

When the shell sees the keyword for, it knows to repeat a commands between `do` and `done` once for each item in a list that follows `in` keyword. Each time the loop runs (called an iteration), an item in the list is assigned in sequence to the variable, and the commands inside the loop are executed, before moving on to the next item in the list. Inside the loop, we get the value of the variable by putting `$` in front of it. 

Here is an example:
```
$ for file in Zambia.txt Zimbabwe.txt; do echo $file;done

# OR using wildcard:

$ for file in Z*.txt; do head -n3 $file; done

#file here is a variable; its value is Zambia.txt
#when loop executes the first time(first iteration)and Zimbabwe.txt
#when loop executes the second time(second iteration)

```
#### **Challenge 5**

1. Compare the output of the two for loops below.
Can you explain why the outputs are different?
```
$ for datafile in G*.txt;do ls G*.txt;done
$ for datafile in G*.txt;do ls $datafile;done
```
2. Write a for loop that outputs the highest life expectancy with a corresponding year and contry name for every file that starts with `U` and contains `a`


**Solution**
```
 $ for file in U*a*; do cut -f1,3,4 $file|sort -nk3|tail -n1 ;done
 
# And if you want to write output to file
$ for file in U*a*; do cut -f1,3,4 $file|sort -nk3|tail -n1 >> Highest_LE.txt;done
 ```
***Note:***
Notice that you are using the append symbol >> here to save the output to a file before 'done'. This file will be created after the loop runs for the first time, and then for each reiteration, the outputs will be appended to this file.

Instead, you could also use
```
$ for file in U*a*; do cut -f1,3,4 $file|sort -nk3|tail -n1; done > Highest_LE.txt
```
In this case, the final output is saved to the file once the loop is completed. 


### 2e. Bash: writing shell scripts

So far, we used very few commands to work with files. You can probably type them up every time you need to look up some information about the file. But as your analysis becomes more complex, you would want to save your commands to a file. This will allow you to reuse/modify them later. A file that contains a series of commands in the order to be executed is known as **shell scipt**.

Before we start writing shell scripts, let's move back to `unix_shell` directory:
```
cd ../../
```
Let's write the commands we used to find the highest life expectancy to text file. We will look at Mexico this time.
Open your text editor, add the following lines:
```
#!/bin/bash  #path to bash shell that will execute this file

#notice path to data file - why?
cut -f1,3,4 Data/ByCountry/Mexico.txt|sort -nk3|tail -n1 > HighestLE_Mexico.txt
```
Save file as `MyScript1.sh`. To run file, type:

```
#./ indicates that you are running script from working directory
$ ./MyScript1.sh
```

Check your working directory. You should have HigestLE_Mexico.txt with the expected output.
```
$cat HighestLE_Mexico.txt
```
So, here it is, your first shell script!
You can add as many command as you want in your text file (script file) -everything is kept in one place and can be reused and modified if needed. 

Let's improve it a little.

- Add description of what script does.
  #this scripts outputs the highest life expectancy
- Add usage statement: 
#usage: ./MyScript.sh

What else?
Could you reuse it with a different input file?
To make it usable with any file(not just Mexico) we need to inroduce a variable for a part of the code that we want to change frequently. For example, if we want to run this code with a different file, we want a variable instead of hard-wired filename. So, let's change `Mexico.txt` to `input` and assign the value`Mexico.txt` to it. We can also define `output` variable and assign `HighestLE.txt`  Save as `MyScript2.sh`

```
#!/bin/bash

#Description
#get the highest life expectancy across years

#usage: ./MyScript2.sh

#define input variable
input=Data/ByCountry/Mexico.txt
output=HighestLE2.txt

#command
cut -f1,3,4 $input|sort -nk3|tail -n1 > $output
```
Run:
```
./MyScript2.sh
```
Why is this better?
What would be even better? 
Ideally, we do not want to change the contents of the script at all, but we do want to be able to reuse it with different input files. It would be nice if we could provide input file at the command line so we could run our script like this:
```
./MyScript input > output
```
Let's see how to that.

#### Passing command-line arguments to shell scripts

Here is `MyScript3.sh`
```
#!/bin/bash

#Description
#get the highest life expectancy across years

#usage: ./MyScript.sh input > output  #notice new usage - we are redirecting output to file here

# $1 is a special variable that accepts value from the command line
input=$1  # $1 has value of the first command-line argument

#command
cut -f1,3,4 $input|sort -nk3|tail -n1 
```

Run it: 
```
./MyScript3.sh Data/ByCountry/Mexico.txt > HighestLE3.txt
```
No we can run this script on any file from `ByCountry` directory without changing anything inside the script itself!

#### **Challenge 6**

1. Use`for loop` to run `MyScript3.sh` on every file that ends with `s`. You output will record the highest life expectancy with corresponding year and contry name for every file in your list. 
Hint: use `>>` instead of `>` to append new content to file.

2. Modify `MyScript3.sh` to output the highest value for any of the measures in a file (not just life expectancy)
Hint: you need to introduce additional command-line argument that specifies the column number you are interested in.


**Solution**

1. `for loop`
```
$ for file in Data/ByCountry/*s.txt;do ./MyScript3.sh $file >> HighestLE_loop.txt;done
```
2. Modified `MyScript3.sh` saved as `MyScript4.sh`
```
#!/bin/bash

#Description
#get the highest value of a column

#usage: ./MyScript.sh input column > output  #notice new usage - we are redirecting output to file here

# $1 is a special variable that accepts value from the command line
input=$1  # $1 has value of the first command-line argument
colNum=$2  # $2 holds the value of the column number you want to analyze

#command
cut -f1,3,$colNum $input|sort -nk$colNum|tail -n1 
```

Run it: 
```
# input here is Mexico.txt, but any country should work
./MyScript4.sh Data/ByCountry/Mexico.txt 6> Highest_gdp.txt

# or if you want population
./MyScript4.sh Data/ByCountry/Mexico.txt 5> Highest_pop.txt
```


!!! You have seen how we can write and run shell scripts from the command line. But remember that the shell is the environment for running any scripts/programs. We can just as easily run Python or R scripts from the command line or inside Bash`for loop` construct.
You can also run Python scripts inside shell scrips! Such combination of Linux commands with Python(or R) scripts can be very effective. 
In the next lesson you will learn about Python scripts and see how to run them from the command line. :+1: 
