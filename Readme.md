# DTC-Bioinformatic-Course

## **TABLE OF CONTENTS**
- [1. Introduction to command line](#1-Introduction-to-command-line)
   - [1.1 Find and launch your terminal](#11-Find-and-launch-your-terminal)
   - [1.2 Creating directories (i.e. folders)](#12-Creating-directories-(i.e.-folders))
   - [1.3 Creating files](#13-Creating-files)
   - [1.4 Searching within files](#14-Searching-within-files)
   - [1.5 Deleting files and folders](#15-Deleting-files-and-folders)
   - [1.6 Writing a bash script](#16-Writing-a-bash-script)
   - [1.7 Manuals](#17-Manuals)
- [2. Bacterial genome assembly](#2-Bacterial-genome-assembly)
   - [2.1 Manage data](#21-Manage-data)
   - [2.2 Running fastQC](#22-Running-fastQC)
   - [2.3 Genome assembly](#23-Genome-assembly)
   - [2.4 Species identity check](#24-Species-identity-check)
   - [2.5 Extra - further data analysis](#25-Extra---further-data-analysis)

## 1. Introduction to command line
Just like Windows, iOS, and Mac OS, Linux is an operating system (OS). It is in fact, one of the most popular platforms used, particularly in bioinformatics. **Linux** has a number of different versions to suit any type of user. These versions are called distributions (or, 'distros') and nearly every distribution of Linux can be downloaded for free, burned onto disk (or USB thumb drive), and installed (on as many machines as you like). We are using **UBUNTU**, which is a popular Linux distribution. Most bioinformatics tools run on Linux operating systems and/or on Mac OS since this is also a Unix-like operating system. Interacting with and running programs on Unix-like operating systems usually means using the Unix '**command line**' user interface, or '**terminal**'.
Using the **terminal** means interacting with the computer by typing commands, rather than pointing and clicking. A familiarity with the use of the **command line** can be very helpful. Most bioinformatics programs run on the **Unix command line** and follow similar logic and rules, so they can easily be combined together. In this first practical you will learn some of the most commonly used commands, and how to produce a **bash script**. A **bash script** is a series of commands written in a file. These are read and executed by the bash program. The program executes line by line. This saves you time because you do not have to write certain commands again and again (so is a very handy bioinformatics tool to know!).

### 1.1 Find and launch your terminal
The **terminal** can be accessed in different ways on different versions of Linux, but there should be either a menu entry or icon for '**console**' or '**terminal**'. We will be using Ubuntu and a **terminal** can be opened by clicking on activities at the top left of the screen, then typing the first few letters of either '**terminal**', '**command**', '**prompt**', or '**shell**' in the 'Type to search' box. If you want a faster way of bringing up a terminal, you can use the shortcut keys: **Ctrl+Alt+T**.

Open the terminal and you should see a large mostly empty box area, with a space to type at the top.
### 1.2 Creating directories (i.e. folders)
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
cd ..
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
/home/bea/intro
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

### 1.3 Creating files
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

### 1.4 Searching within files
Occasionally, you might want to search for particular words, expressions or even an isolate or gene name in a document. Using Microsoft word or excel, you would use 'find' to search for this. An alternative to this in Linux is the **grep** command (Global Regular Expression Print). **grep** is a Linux / Unix command-line tool used to search for a string of characters in a specified file. The text search pattern is called regular expression. When it finds a match, it prints the line with the result. The **grep** command is a very handy when searching through large files.
#
Let's try searching for a particular (nucleotide) string in our fasta file:

:pencil2: **Input:**
```bash 
grep "GTC" example_sequence_1.fasta
```

This will return the line that contains the search string "GTC", i.e. so you should see "AAGTCAACCT"

:rocket:**Output:**
```bash 
AAGTCAACCT
```

What happens if we change the case used? Is this important?

:pencil2: **Input:**
```bash 
grep "gtc" example_sequence_1.fasta
```

:rocket:**Output:**
```bash 

```

Unix systems are case-sensitive, that is, they consider "GTC" and "gtc" to be different. This applies to file and folder names too.
This leads to an important point however, in that you should avoid creating files and folders whose name only varies by case. Not only will it avoid confusion, but it will also prevent problems when working with different operating systems. Windows, for example, is case-insensitive, so it would treat file names that differ by case as a single file, potentially causing data loss or other problems. You might be tempted to just hit the Caps Lock key and use upper case for all your file names. But the **vast majority of shell commands are lower case**, so you would end up frequently having to turn it on and off as you type. Most seasoned command line users tend to stick primarily to lower case names for their files and directories so that they rarely have to worry about file name clashes, or which case to use for each letter in the name.
#
Now, let's try searching for sequence headers in our fasta file. Remember, sequence headers always begin with a '**>**' in fasta file format, which gives us an easy search term. Type the following and press Enter:

:pencil2: **Input:**
```bash 
grep ">" example_sequence_1.fasta
```

This will return only the lines that contain the search string ">", i.e. so you should see > Seq_1 and > Seq_2 printed on your terminal screen.

:rocket:**Output:**
```bash 
>Seq_1
>Seq_2
```

**grep** can also be used to count the number of line occurrences of a string within a file. The option **-c** (count) is used for this. Count the number of lines that contain "**>**" within the fasta file. For this, you simply specify "**-c**" before the search terms:

:pencil2: **Input:**
```bash 
grep -c ">" example_sequence_1.fasta
```

This should return the number 2. 

:rocket:**Output:**
```bash 
2
```
#
Now try in your combined fasta file:

:pencil2: **Input:**
```bash 
grep -c ">" combined.fasta
```

This should return the number 4. 

:rocket:**Output:**
```bash 
4
```

By FASTA format definition, we know that number of sequences in a file should be equal to the number of description lines. So by counting *>* in file, you can count the number of sequences in a fasta file.
#
What if you had lots of files and you wanted to perform the same count in all of your files and save the output of this to a new text file?
You can use grep and the * wildcard to do this!

Let's try counting the number of lines that contain ">" in all our files with the.fasta extension, and write/save this output to a new text file:

:pencil2: **Input:**
```bash 
grep -c ">" *.fasta > output.txt
ls
```

You are directing the output of this search to a new file (output.txt), the output is no longer returned to us on the terminal screen. Then using ls we see that this new file (output.txt) is now present in our directory.

:rocket:**Output:**
```bash 
combined.fasta
example_sequence_1.fasta
example_sequence_2.fasta
output.txt
```

Use the **vi editor** or **cat** to see the contents of this file. 

You should see it lists all the files ending with the fasta extension and gives the count score for ">" line occurances.

:rocket:**Output:**
```bash 
combined.fasta: 4
example_sequence_1.fasta: 2
example_sequence_2.fasta: 2
```
#
**EXERCISE**
Use grep to explore the fasta file (test_sequence.fasta) you made previously. How do you search for the lines that contain "AA"? How many sequences does it contain?
#

### 1.5 Deleting files and folders
In this next section we are going to start deleting files and folders. To make absolutely certain that you do not accidentally delete anything in your home folder, use the **pwd** command to double-check that you are still in the **/intro** directory before proceeding.
#
To delete things, we can use the **rm** (remove) command.

***Important warning:***
Unlike in windows/mac where you might get a prompt asking if you are sure you want to delete something... this will not happen in command line. When you use **rm** and **press Enter**
***- whatever you're trying to delete is deleted!***

Similarly, unlike in windows/mac where the things you delete are moved to a folder called "trash" or similar.... **rm** will delete them totally, utterly, and irrevocably. You need to be careful with the parameters you use with **rm** to make sure you are only deleting the file(s) you intend to. You should take particular care when using wildcards (e.g. *****), as it is easy to accidentally delete more files than you intended. If you are at all uncertain use the **-i** (interactive) option to **rm**, which will prompt you to confirm the deletion of each file; enter **Y** to delete it, **N** to keep it, and press **Ctrl-C** to stop the operation entirely.
#
Let's try deleting one of the extra files we created earlier (example_sequence_2.fasta). First, double-check it is there in your current folder space using '**ls**', then type the following command and press Enter:

:pencil2: **Input:**
```bash 
rm example_sequence_2.fasta
```

Using '**ls**' you should now be able to see that the *example_sequence_2.fasta* file has been deleted.
#
**What about folders?** Let's try deleting a folder we created earlier but didn't use (folder_two).

:pencil2: **Input:**
```bash 
rm folder_twoa
```

When you press Enter, you should see your terminal return:

:rocket:**Output:**
```bash 
rm folder_two: is a directory
```

What happened there? Well, it turns out that **rm** does have one little safety net to make sure you do not accidentally delete a directory and all of the files inside it with one single command. Luckily there's a **rmdir** (remove directory) command that will do the job for us instead:

:pencil2: **Input:**
```bash 
rmdir folder_two
```

*Note*: **rmdir** will only delete empty folders. Another small safety net to prevent you from accidentally deleting a folder full of files when you did not mean to. The addition of options to our **rm** or **rmdir** commands will let us perform more dangerous actions without the aid of a safety net. In the case of **rmdir** we can add a **-p** switch to tell it to also remove the parent directories. Think of it as the counterpoint to **mkdir -p**. 

### 1.6 Writing a bash script
A **bash script** is a series of commands written in a file. These are read and executed by the bash program. The program executes line by line.
For example, you can navigate to a certain path, create a folder and spawn a process inside it using the command line. You can do the same sequence of steps by saving the commands in a bash script and running it. You can **run the script** any number of times, and only need to **'press Enter' once**.
**Bash scripts** effectively allow you to automate a series of commands so you do not have to type them all individually.
By naming conventions, bash scipts end with a **.sh** file extension. Scripts are also identified by containing the path to the bash interpretor at the start (i.e. #!
/bin/bash). This is known as a shebang statement, and will be the first line of the script.
We are going to create a very simple **bash script** to give you a taste of how they work. We are going to create a script that when executed **echos Hello World** to the terminal console.
#
To create our bash script, we can again use the **vi editor**:

:pencil2: **Input:**
```bash 
vi hellow_word.sh
```

As seen previously, this will open up a new file, and you will need to press '**i**' to enter insert mode. Once in insert mode, write the following into your new file:

:pencil2: **Input:**
```bash 
#!bin/bash
echo "Hello World"
```

Use **Esc** and **:wq** to save and quit your new file. Test it has been written and saved correctly by using **vi hello_world.sh** to reopen and check.

In order to execute the script the file needs to be made **executable** by the use of **chmod u+x** filename:

:pencil2: **Input:**
```bash 
chmod u+x hellow_word.sh
```

**chmod** modifies the existing rights of a file for a particular user. We are adding **+x** (make executable) to user **u**.
You can now run the script in the following ways:

:pencil2: **Input:**
```bash 
./hellow_word.sh 
```

or

:pencil2: **Input:**
```bash 
bash hellow_word.sh 
```
Try them both, and you should see **Hello World** returned to you on the terminal console.

:rocket:**Output:**
```bash 
Hello World
```
#
**EXERCISE**
1. Create and execute a bash script that when executed creates a new folder called "bash"
2. Create and execute a bash script that when executed does the following series of commands (these will need to be seperated by lines in the bash script):
   1. Copy one of your previous fasta files into the new bash folder you created.
   2. Changes directory into the new folder with the fasta file now in,
   3. then searches the fasta file for line occurances of ">" and prints this output to a new text file.

Check the script has completed properly by checking the new output text file within your 'bash' folder.
#

### 1.7 Manuals
Most Linux command line tools include a man page. Try taking a brief look at the pages for some of the commands you've already encountered: **man ls**, **man grep**, **man cp**, **man rmdir** and so on. There's even a man page for the man program itself, which is accessed using **man man**. e.g.:

:pencil2: **Input:**
```bash 
man grep 
```

:pencil2: **Input:**
```bash 
man ls 
```

:pencil2: **Input:**
```bash 
man cp 
```

Exit the manual pages by pressing '**q**' for quit!

---
END OF PRACTICAL PART 1
--- 


# 2. Bacterial genome assembly
The goal of the second part of this practical is to assemble a bacterial genome using sequencing reads. The genome will be assembled using short-read sequencing data to produce '**contigs**'. **Contigs** is a term that means contiguous DNA and refers to the consensus sequence that is formed when sequencing reads (usually from fastq files) are ‘stitched together’ to form regions of the genome. With short reads, repetitive sequences usually prevent complete closed genomes from being produced and instead the end result is usually smaller pieces of contiguous DNA that make up most of the genome. Hybrid assembly approaches (i.e. using long and short read sequencing data together) can be used to try and 'close the genome', to give you a complete genome where you know how everything fits together. For this practical we will be working with short reads only, obtained from illumina sequencing of a *Pseudomonas aeruginosa* genome.

## **TABLE OF CONTENTS**
- [2.1 Manage data](#21-Manage-data)
- [2.2 Running fastQC](#22-Running-fastQC)
- [2.3 Genome assembly](#23-Genome-assembly)
- [2.4 Species identity check](#24-Species-identity-check)
- [2.5 Extra - further data analysis](#25-Extra---further-data-analysis)

*Pseudomonas aeruginosa* is a Gram-negative bacterium and opportunistic pathogen. It is a major problem in clinical settings and is as a major caustive pathogen of ventilator-associated pneumonia. *P. aeruginosa* is becoming increasingly resistant to the antibiotics we use to treat it. Genome sequencing data is useful for understanding what the population of *P. aeruginosa* looks like, how many acquired antibiotic resistance genes this pathogen carries, and understanding how *P. aeruginosa* is evolving in clinically relevant environments (such as within ICU patients with pneumonia infections).

## 2.1 Manage data

Let's first create a new directory (within our intro folder) to work in:

:pencil2:**code:**
```bash
mkdir assembly
cd assembly
```

Check you are now in your new folder.

For the purposes of this practical, we will be using a pair of forward and reverse fastq.gz (comparessed gzipped fastq) files from *P. aeruginosa* available from the European Nucleotide Archive. 
You can download this data using the command wget followed by the address to that file(s)

:pencil2:**code:**
```bash
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_1.fastq.gz
```

However, all the data needed for the first week of this course is already available in DTC computer in the followed location

```bash
/usr/local/bioinformatics
```
If you navigate to this location you will see four folders, one for each practical. 

If you are working in your own computer / VM follow the next steps to get the pair of reads:


:pencil2:**code:**
```bash
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_1.fastq.gz
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_2.fastq.gz
```

To check that the files have downloaded we can use the **ls -lh** command (**-l** long; **-h** human-readable), which also allows us to check the size of the files:

:pencil2:**code:**
```bash
ls -lh
```

The files that we've downloaded are gzipped **FASTQ** files. Take a look at one of them:

```bash
PSA-2017-01_1.fastq.gz
PSA-2017-01_2.fastq.gz
```

We can use a combination of commands to view the first few lines of a compressed files. 

```bash
zcat /usr/local/bioinformatics/1-intro/PSA-2017-01_1.fastq.gz | head -n 20
```
**zcat** decompress the file and shows it in the terminal. However, **fastq** files contained millions of reads, and we want to avoid “seing” the whole file in the terminal. In order to avoid this, we add another command, in this case head, after the symbol | which pipes the output zcat as an input of the next command head -n 20. In the end, you’ll see only the first 20 lines of the fastq.gz file. 

How does it look like commpare to a fasta file?

## 2.2 Running fastQC
The tool **fastqc** assesses the quality scores across all of the reads in your data. You can read more about it here: https://dnacore.missouri.edu/PDF/FastQC_Manual.pdf
First, create a folder to save fastqc results

:pencil2:**code:**
```bash
mkdir fq-results
```

Let’s run fastqc on our 2 samples:

:pencil2:**code:**
```bash
fastqc /usr/local/bioinformatics/1-intro/PSA-2017-01_1.fastq.gz -o fq-results
fastqc /usr/local/bioinformatics/1-intro/PSA-2017-01_2.fastq.gz -o fq-results
```

**-o**: output directory. Location where the files will save.

View the files that have been generated:

:pencil2:**code:**
```bash
cd fq-results
ls *fastqc*
```

:rocket:**Output:**
```bash
PSA-2017-01_1_fastqc.html
PSA-2017-01_1_fastqc.zip
PSA-2017-01_2_fastq.html
PSA-2017-01_2_fastq.zip
```

For each file, **fastQC** has produced both a .zip archive containing all the plots, and a html report. We can open the html files using a web browser: e.g.:

:pencil2:**code:**
```bash
google-chrome PSA-2017-01_1_fastqc.html&
```

For each position, a boxplot is drawn with:

• the median value, represented by the central red line

• the inter-quartile range (25-75%), represented by the yellow box

• the 10% and 90% values in the upper and lower whiskers

• the mean quality, represented by the blue line

The y-axis shows the quality scores. The higher the score, the better the base call. The background of the graph divides the y-axis into very good quality scores (green), scores of reasonable quality (orange), and reads of poor quality (red). It is normal with all Illumina sequencers for the median quality score to start lower over the first 5-7 bases and to then rise. The quality of reads on most platforms will drop at the end of the read. This is often due to signal decay or phasing during the sequencing run. We can see that our sequence length is 35-250bp. This makes sense, because this was sequenced with a 250 bp paired-end sequencing run on an Illumina MiSeq sequencer. The sequencing reads have a %GC of 65, this is within the expected
%GC range for Pseudomonas aeruginosa (which has a highly GC biased genome). Anything above a score of 25 is usually considered good quality, so we can see these are reasonable quality reads.
Check the fastqc reports for both files, which file is of better quality?


**Optional step: trimming & filtering data**
Low quality sequences and adapters can be removed used programs such as trimmomatic (read more here: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4103590/ , https://www.melbournebioinformatics.org.au/tutorials/tutorials/assembly/assembly- protocol/).
Whether you should do this can depend on the objective of your sequencing experiments (e.g. read more here: https://dnatech.genomecenter.ucdavis.edu/faqs/when-should-i- trim-my-illumina-reads-and-how-should-i-do-it/).
We will not do this today, but you should be aware of it for genome assemblies in the future.

## 2.3 Genome assembly
**SPAdes** is one of a number of de novo assemblers that uses short read sets as input (e.g. Illumina Reads). When a genome is sequenced, it is fragmented into lots of short sequencing fragments called ‘**reads**’. Assembling the genome means putting the pieces back together. The assembly method **SPAdes** uses is based on de Bruijn graphs, which you can read about on wikipedia: they use overlaps between reads to build up the genome.
So in simple words, assembling a genome means putting together the sequenced random fragments (known as **reads**) into longer sequences (called **contigs**).
The **SPAdes** program has several options (read more here: https://github.com/ablab/spades), which can be listed if you test **spades.py** and press **Enter**. The most basic options to specify are:

- **-1** is input file of forward reads
- **-2** is input file of reverse reads
- **-o** is the output directory

As a pipeline, SPAdes will perform both a read error corection step and then an assembler step. Automatically, it will perform both. But you can also get it to run just one by using:

- **--only-error-correction** [Performs read error correction only]
- **--only-assembler** [Runs assembly module only]

For the sake of time, we are going to run **SPAdes** in assembler mode only (running both would take >1 hour). This will likely effect the downstream quality of our genome (e.g. a higher number of contigs!), so is not something you would generally want to do, but will allow us to produce assembled genomes which we can continue the practical with.

To run **SPAdes** to assemble our paired fastq reads PSA-2017-01_1.fastq.gz and PSA-2017-01_2.fastq.gz in assembly mode only:

:pencil2:**code:**
```bash
spades.py -1 [location-to-read-1] -2 [location-to-read-2] –-only-assembler -o spades_assembly
```

replace the information in [ ] to the path of each fastq file. Wait for the command to run. **SPAdes** should give some output about what it is doing. At the end, you might see an assembly warning about erroneous kmer, that is OK for the sake of this exercise (re. run in assembly mode only).

Navigate into your spades_assembly output folder and check whats there:

:pencil2:**code:**
```bash
cd spades_assembly
```

The file '*contigs.fasta*' is the contig file produced from the reads, and what we will be working with. You can read more about what the other files are on the GitHub page: https://github.com/ablab/spades

#
Exercice
How many contigs (sequences) have the result of the assembly (*contigs.fasta*)  
#

We can run *QUAST* (QUality ASsessment Tool) for an overview of our assembly metrics. You can read more about QUAST here: https://quast.sourceforge.net/docs/manual.html:

:pencil2:**code:**
```bash
quast.py contigs.fasta
```

After it has finished running, you should see a new folder with the results in has been created - '**quast_results**'.

Navigate into this folder, and then into the new results (**results_data_hour**) sub-folder. In this folder use '**ls**' to check what is there. We are interested in the '**report.txt**' file, which is a summary report file.

To see the contents, we can use the **vi editor** or **cat**:

:pencil2:**code:**
```bash
cat report.txt
```

Looking at this report we can see there are a total of 864 contigs with a size of >= 1000bp. The total length is ~6.56Mb, which is within the size range we expect for a *P. aeruginosa* genome (5.5Mb - 7Mb). The GC is ~66%, which again is within the GC range we expect for a *P. aeruginosa genome*. The largest contig is ~47,000bp.

## 2.4 Species identity check
A final step in our genome quality check is to confirm that the genome and the DNA it is composed of belongs to our species of interest and that it isn’t contaminated with DNA from another bacterium. There are a number of tools that can do this and this depends on whether you want to check your data before it has been assembled using software such as **KRAKEN** or after it has been assembled using tools such as **MASH**. We will query our assembled genome against a reference database called **rMLST** available on the online, publicly available website https://pubmlst.org/species-id.

Species identification in **rMLST** uses genes involved in the ribosome machinery which are core to all bacteria and for which sequence variations are associated with specific bacterial species. You can query your data by directly uploading your **contigs.fasta** file to the database via the webserver.

Search '**identify species pubmlst**' using google or (https://pubmlst.org/bigsdb? db=pubmlst_rmlst_seqdef_kiosk)
Once you have navigated to this page, click in the '**select FASTA file**' box, navigate to where the **SPAdes** assembled 'contigs.fasta' file is and select this file, then click
**Submit**.

Your sequence data will be compared against all of the >400,000 genomes present in the **rMLST** database to see how closely it matches in its ribosome sequences to ones defined in the database.
Does the output match your expectations? (*Pseudomonas aeruginosa*)

## 2.5 Extra - further data analysis
Here is an (optional) data analysis exercise you can try to explore your assembled genome:

1. Does your assembled genome contain any acquired antibiotic resistance genes? (hint: try finding some antibiotic resistance gene databases and blasting these gene fasta sequences against your genome using blastn in command line)
**Blast** (command line version) has been installed on the computers + virtual machines (read more here: https://www.ncbi.nlm.nih.gov/books/NBK279690/)
As with the webserver, you can run **blastn** queries against a database (quick start here: https://www.ncbi.nlm.nih.gov/books/NBK569856/) or against another file.
To list these options available:

:pencil2:**code:**
```bash
blastn -help
```

A basic quickstart on how to query one file (e.g. an antibiotic resistance gene) against another (e.g. a genome):

:pencil2:**code:**
```bash
blastn -query queryfilename.fasta – subject subjectfilename.fasta -out outputfilename.txt
```

You can specify search options, e.g. "-perc_identity 95 -qcov_hsp_perc 95 - num_alignments 1".
