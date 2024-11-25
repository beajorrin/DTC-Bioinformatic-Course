# DTC-Bioinformatic-Course
# Part 1: Introduction to command line
Just like Windows, iOS, and Mac OS, Linux is an operating system (OS). It is in fact, one of the most popular platforms used, particularly in bioinformatics. **Linux** has a number of different versions to suit any type of user. These versions are called distributions (or, 'distros') and nearly every distribution of Linux can be downloaded for free, burned onto disk (or USB thumb drive), and installed (on as many machines as you like). We are using **UBUNTU**, which is a popular Linux distribution. Most bioinformatics tools run on Linux operating systems and/or on Mac OS since this is also a Unix-like operating system. Interacting with and running programs on Unix-like operating systems usually means using the Unix '**command line**' user interface, or '**terminal**'.
Using the **terminal** means interacting with the computer by typing commands, rather than pointing and clicking. A familiarity with the use of the **command line** can be very helpful. Most bioinformatics programs run on the **Unix command line** and follow similar logic and rules, so they can easily be combined together. In this first practical you will learn some of the most commonly used commands, and how to produce a **bash script**. A **bash script** is a series of commands written in a file. These are read and executed by the bash program. The program executes line by line. This saves you time because you do not have to write certain commands again and again (so is a very handy bioinformatics tool to know!).
## 1.1 Find and launch your terminal
The **terminal** can be accessed in different ways on different versions of Linux, but there should be either a menu entry or icon for '**console**' or '**terminal**'. We will be using Ubuntu and a **terminal** can be opened by clicking on activities at the top left of the screen, then typing the first few letters of either '**terminal**', '**command**', '**prompt**', or '**shell**' in the 'Type to search' box. If you want a faster way of bringing up a terminal, you can use the shortcut keys: **Ctrl+Alt+T**.

Open the terminal and you should see a large mostly empty box area, with a space to type at the top.
## 1.2 Creating directories (i.e. folders)
First, let's work out where we are. As said above, the terminal is just another way of interacting with your computer (so like how you can use your mouse and clicking to navigate through your folders.... you can use your terminal to do the same thing).
Click the mouse into the window and type the following command (all in lowercase) then press the **Enter** key to run it:

:pencil2:**code:**
```bash
pwd
```
*Explanation:* pwd is an abbreviation of 'print working directory'. All it does is print out the shell's current working directory. You should see a directory path printed out, something like '**/home/YOUR_USERNAME**'.

:rocket:**Output:**
```bash
/home/bea
```
#
**Now let's create a new directory** (i.e. folder) to work in. Type the following command then press the **Enter** key to run it: 

:pencil2:**code:**
```bash
mkdir intro
```
This should create a new directory (mkdir - '**mk** (make) **dir** (directory)') within the directory you are currently in called '**intro**'. 
#
**Now let's check it is there**. We can list everything contained within our current directory using the **ls** (list).

:pencil2:**code:**
```bash
ls
```
You should see your terminal return the name of the directory you just made (**intro**).

:rocket:**Output:**
```bash
intro
```
#
You can **change directories** using the **cd** (change directory) command. Let's try this:

:pencil2:**code:**
```bash
cd intro
```
We can check we have successfully changed directory by using **pwd** again:

:pencil2:**code:**
```bash
pwd
```
You should see a directory path printed out, which now ends in intro, something like '**/home/YOUR_USERNAME/intro**'.

:rocket:**Output:**
```bash
/home/bea/intro
```
#
If we try using the **ls** (list):

:pencil2:**code:**
```bash
ls
```
You should see your terminal return an empty directory, because you haven't added anything to your intro directory.

:rocket:**Output:**
```bash

```
#
To move back up one directory (i.e. back to '/home/YOUR_USERNAME'), we can use '**cd**':

:pencil2:**code:**
```bash
cd..
```
Using '**cd ..**' makes you move back up one directory. You can use **ls** or **pwd** to check that you are now back in the directory that contains your intro folder, e.g.:

:pencil2:**code:**
```bash
pwd
```

:rocket:**Output:**
```bash
/home/bea
```
The two full stops after **cd** are important, and say to only go back one. If you leave out the two full stops and just use '**cd**', it goes to your 'upper most' directory (i.e. that contains everything). 

You can also use **cd** to specify a directory to move to using the path description as is given by **pwd** (e.g. cd /home/YOUR_USERNAME/intro). Play with 'cd', 'cd..' and 'cd /home/YOUR_USERNAME/intro'

#
Move back into your intro folder:

:pencil2:**code:**
```bash
cd intro
```
Check you are there:

:pencil2:**code:**
```bash
pwd
```
You should see a directory path printed out, which now ends in intro, something like '/home/YOUR_USERNAME/intro'.

:rocket:**Output:**
```bash
/home/bea/intro
```
#
**What about creating multiple directories?**
You can also use **mkdir** to make multiple directories and name them all in one command. Let's try that, creating multiple directories named *dir1* *dir2* and *dir3*:

:pencil2:**code:**
```bash
mkdir dir1 dir2 dir3
```
Confirm they have been created:

:pencil2:**code:**
```bash
ls
```
You should see your terminal return the names of the three new directories you made just now (*dir1*, *dir2*, *dir3*).

:rocket:**Output:**
```bash
dir1 dir2 dir3
```
You can get more information if:

:pencil2:**code:**
```bash
ls -l
```

:rocket:**Output:**
```bash
total 0
drwxr-xr-x 2 bea staff 64 28 Nov 15:25 dir1
drwxr-xr-x 2 bea staff 64 28 Nov 15:25 dir2
drwxr-xr-x 2 bea staff 64 28 Nov 15:25 dir3
```

Notice that mkdir created all the folders in one directory. It did not create *dir3* inside *dir2* inside *dir1*, or any other nested structure. But sometimes it is handy to be able to do exactly that, and **mkdir** does have a way
#
**Create nested directories**

:pencil2:**code:**
```bash
mkdir -p dir4/dir5/dir6
ls
```

:rocket:**Output:**
```bash
dir1 dir2 dir3 dir4
```
This time you will see that only *dir4* has been added to the list, because *dir5* is inside it, and *dir6* is inside *dir5*.
The '**-p**' that we used is called an option or a switch (in this case it means 'create the parent directories too, and do not give an error if the directories already exist'). Options are used to modify the way in which a command operates, allowing a single command to behave in a variety of different ways. Options can take different forms in different commands. You will often see them as single characters preceded by a hyphen (as in this case), or as longer words preceded by two hyphens.

**Navigate in your terminal** [e.g. using 'cd' 'pwd' and 'cd ..'] to enter *dir4* and *dir5* and check the appropriate folders are there.
Make sure you return back to within your intro folder before proceeding, e.g.:

:pencil2:**code:**
```bash
cd /home/your_username/intro
```

:rocket:**Output:**
```bash
/home/beea/intro
```
#
**What happens if you want to create a directory with a space in its name?** Let's try it:

:pencil2:**code:**
```bash
mkdir folder two
ls
```

:rocket:**Output:**
```bash 
folder
two 
```
You should see your terminal has actually returned two new directories, one named 'folder' and one named 'two'. 
If you want to work with spaces in directory or file names, you need to 'escape' them. Escaping is a computing term that refers to using special codes to tell the computer to treat particular characters differently to normal. Try the following:

:pencil2: **Input:**
```bash 
mkdir "folder two"
ls 
```

:rocket:**Output:**
```bash 
folder two 
```
Although the command line can be used to work with files and folders with spaces in their names, the need to escape them with quote marks or backslashes makes things more difficult. You can often tell a person who uses the command line a lot just from their file names: they will tend to stick to letters and numbers, and use underscores ('**_**') or hyphens ('**-**') instead of spaces. Try the following:

:pencil2: **Input:**
```bash 
mkdir "folder_two" 
ls
```
:rocket:**Output:**
```bash 
folder_two 
```

## 1.3 Creating files
A **FASTA** file is a text file that contains sequence data. Each sequence begins with a single-line sequence header, followed by lines of sequence data. The sequence header always starts with a '**>**', followed by a short sequence description header, then the sequence following below on a separate line. Everything beginning with '**>**' is a new sequence. This is a common format for sequence data, and a common input file type for a lot of bioinformatics software (e.g. blast). We are going to use our terminal to create our own example text file in a FASTA format.
To do this, we can use the **vi editor** to create and write our own file.
#
A short introduction to the **vi editor** and how to use it is given below:
The **vi editor** has two modes: **Command** and **Insert**. When you first open a file with **vi**, you are in **Command mode**. **Command mode** means you can use keyboard keys to navigate, delete, copy, paste, and do a number of other tasks--except entering text.
To enter **Insert mode**, press **i**. In **Insert mode**, you can enter text, use the **Enter** key to go to a new line, use the arrow keys to navigate text, and use vi as a free-form text editor. To return to **Command mode**, press the **Esc key** once.

Some useful **vi** shortcuts: 
- **vi**: Open or edit a file.
- **i**: Switch to Insert mode. 
- **Esc**: Switch to Command mode.
- **:w**: Save and continue editing. 
- **:wq** or **ZZ**: Save and quit/exit
- **vi. :q!**: Quit vi and do not save changes.

It is easy to invoke **vi**. At the command line, you type **vi** to create a new file, or to edit an existing one.
#
So, **let's use vi** to create and open a new file named 'example_sequence.fasta'. Type the following command and press Enter:

:pencil2: **Input:**
```bash 
vi example_sequence_1.fasta
ls
```

You should see your terminal change to a largely blank file box, with "example_sequence_1.fasta" [New] at the bottom. 

:rocket:**Output:**
```bash 
~
~
~
~
~
"example_sequence_1.fasta" [New] 
```
We need to use '**i**' to switch to **Insert mode**, which will allow us to write in this new file. Press the "**i**" on your keyboard, [you do not need to press Enter afterwards]

:pencil2: **Input:**
```bash 
i
```
At the bottom of your terminal, you should now see it is in Insert mode "-- INSERT -- ".
:rocket:**Output:**
```bash 
~
~
~
~
~
--INSERT-- 
```
Type the following into your file (i.e. two sequence headers followed by short sequences, seperated by lines):

:pencil2: **Input:**
```bash 
> Seq_1
AAGTCAACCT
> Seq_2
ATCGGGGTA
```
We now want to switch to **command mode**, to save and quit our new file. To do this, press the **Esc key**. You will see "**--INSERT--**" has disappeared from the bottom of your terminal. Now type **:wq**, which means save and quit, and then press the **Enter key**:

:pencil2: **Input:**
```bash 
:wq
```
#
You will now see you are out of the file, and back into your previous directory in the terminal. You can use **ls** again to check your new file is there.
To check the contents of your new file have been saved properly and are correct, you can use the cat (concatenate) command, which will print the specified file. Try:

:pencil2: **Input:**
```bash 
cat example_sequence_1.fasta
```
You should see the two fasta sequences you wrote printed out:

:rocket:**Output:**
```bash 
> Seq_1
AAGTCAACCT
> Seq_2
ATCGGGGTA 
```

We can also explore files using the '**head**' command, which will return the first lines of a file, depending on the options we specify. The default is the first 10 lines, but we can use **-n** (num) to specify the first '**num**' line instead of this default.

:pencil2: **Input:**
```bash 
head -1 example_sequence_1.fasta
```

You should now only see the first line printed out:


:rocket:**Output:**
```bash 
> Seq_1 
```

The **cat** (concatenate) command is more than just a file viewer - the name comes from concatenate, meaning to link together. 
#
**Let's try copying this file** to create a second fasta file, and using cat to merge the two together.
To copy something we can use the **cp** (copy) command, where we specify what we want to copy and where we want to copy it to. 

:pencil2: **Input:**
```bash 
cp example_sequence_1.fasta example_sequence_2.fasta
ls
```

The above command copies 'example_sequence_1.fasta' to a new file, named example_sequence_2.fasta, and using '**ls**' you should now see it exists within your directory.

:pencil2: **Input:**
```bash 
ls
```

:rocket:**Output:**
```bash 
example_sequence_1.fasta
example_sequence_2.fasta 
```

Check the contents of the new file using cat:

:pencil2: **Input:**
```bash 
cat example_sequence_2.fasta
```

You should see the two fasta sequences you wrote printed out.

:rocket:**Output:**
```bash 
>Seq_1
AAGTCAACCT
>Seq_2
ATCGGGGTA 
```
#

**cat** can also be used to print the contents of multiple files at once, so we can now try both:

:pencil2: **Input:**
```bash 
cat example_sequence_1.fasta example_sequence_2.fasta
```

:rocket:**Output:**
```bash 
>Seq_1
AAGTCAACCT
>Seq_2
ATCGGGGTA

>Seq_1
AAGTCAACCT
>Seq_2
ATCGGGGTA
```
#
If you want to pass multiple file names to a single command, there are some useful shortcuts that can save a lot of typing if the files have similar names. For example - a question mark ('**?**') can be used to indicate 'any single character' within the file name. An asterisk ('*****') can be used to indicate 'zero or more characters'. These are sometimes referred to as 'wildcard' characters. The following commands all do the same thing but using wildcards, try them out:

:pencil2: **Input:**
```bash 
cat example_sequence_1.fasta example_sequence_2.fasta
```
:pencil2: **Input:**
```bash 
cat example_sequence_?.fasta
```
:pencil2: **Input:**
```bash 
cat *.fasta
```
*what are the outputs**
#
So now let's use the **cat** to **merge** our new files together into a single new file. The command below will concatenate the two files into a new file named "**combined.fasta**". Type the following and press Enter:

:pencil2: **Input:**
```bash 
cat example_sequence_1.fasta example_sequence_2.fasta > combined.fasta
```

The output is redirected into combined.fasta by using "**>**" 
View the contents of combined.fasta using **cat** again:

:pencil2: **Input:**
```bash 
cat combined.fasta
```

You should see the one file (**combined.fasta**) has two copies of Seq_1 and Seq_2.

:rocket:**Output:**
```bash 
>Seq_1
AAGTCAACCT
>Seq_2
ATCGGGGTA
>Seq_1
AAGTCAACCT
>Seq_2
ATCGGGGTA
```
#
**EXERCISE**
*Create your own fasta file using the **vi** editor called '**test_sequence.fasta**' that contains 3 short sequences of your choosing. Use '**head**' and '**cat**' to explore this file.
#


