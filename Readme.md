# DTC-Bioinformatic-Course

## **TABLE OF CONTENTS**
- [1. Introduction to command line](#1-Introduction-to-command-line)
   - [1.1 Open the Ubuntu terminal](#11-Open-the-Ubuntu-terminal)
   - [1.2 Creating directories](#12-Creating-directories)
   - [1.3 Creating files](#13-Creating-files)
   - [1.4 Searching within files](#14-Searching-within-files)
   - [1.5 Deleting files and folders](#15-Deleting-files-and-folders)
   - [1.6 Writing a bash script](#16-Writing-a-bash-script)
   - [1.7 Manuals](#17-Manuals)
- [2.1 Install Miniconda](#21-Install-miniconda)
   - [2.1.1 Update Ubuntu](#211-Update-Ubuntu)
   - [2.1.2. Download and Install Miniconda](#212-Download-and-Install-Miniconda)
- [2.2 Create a conda environment](#22-Create-a-conda-environment)
   - [2.2.1 Configure Conda](#221-Configure-Conda)
   - [2.2.2 Create the dtc-bio conda environment](#222-Create-the-dtc-bio-conda-environment)
   - [2.2.3 Activate dtc-bio environment](#223-Activate-dtc-bio-environment)
   - [2.2.4 Check the tools are available](#224-Check-the-tools-are-available)
- [3. Bacterial genome assembly](#3-Bacterial-genome-assembly)
   - [3.1 Manage data](#31-Manage-data)
   - [3.2 Running fastQC](#32-Running-fastQC)
   - [3.3 Genome assembly](#33-Genome-assembly)
   - [3.4 Quality assesment of your assembly](#34-Quality-assesment-of-your-assembly)
- [4. Species identity check](#4-Species-identity-check)
   - [4.1 Download *Pseudomonas* type genomes](#41-Download-Pseudomonas-type-genomes)
      - [4.1.1 Create the PATHS](#411-Create-the-PATHS)
      - [4.1.2 Create the corresponding folders](#412-Create-the-corresponding-folders)
      - [4.1.3 Download the *Pseudomonas* genomes from NCBI](#413-Download-the-Pseudomonas-genomes-from-NCBI)
      - [4.1.4 Check you have the files](#414-Check-you-have-the-files)
      - [4.1.5 Decompress the fastas](#415-Decompress-the-fastas)
   - [4.2 Build a Kraken2 database](#42-Build-a-Kraken2-database)
   - [4.3 Classify your assembly](#43-Classify-your-assembly)
      - [4.3.1 Maximise hits](#431-Maximise-hits)
      - [4.3.2 Stricter classification](#432-Stricter-classification)
   - [4.5 Optional: Evidence of AMR genes in your genome](#45-Optional:Evidence-of-AMR-genes-in-your-genome) 

---

## 1 Introduction to command line
Just like Windows and macOS, Linux is an operating system (OS). It is hugely popular in bioinformatics because most tools are built for Unix-like systems. Linux comes in many versions called distributions (“distros”). In this course we will use Ubuntu—a widely used distro—running inside Windows Subsystem for Linux (WSL). WSL gives you a real Ubuntu environment on your Windows machine without a virtual machine.
You will interact with Ubuntu using the command line (also called the terminal or shell): instead of pointing and clicking, you type commands. This is powerful because bioinformatics programs share similar Unix conventions, so you can chain them together and make reproducible workflows. You will also write a bash script—a text file containing a series of commands that bash executes line by line—so you do not have to retype long command sequences.
>From now on, run commands in the Ubuntu (WSL) terminal, not in PowerShell or CMD, unless the instructions say otherwise.

---

### 1.1 Open the Ubuntu terminal
Pick any one of these:
- Start menu: Press Win → type Ubuntu → open Ubuntu.
- Start menu: Press Win → type WSL → open WSL.

:desktop_computer:
```r
you@PC:~$
```

>[!TIP]
>- Your Linux home is **/home/you**. Keep course files under your Linux home for speed and fewer permission issues..
>- Paste in Windows Terminal with **Ctrl+V** (some Linux terminals use Ctrl+Shift+V).
>- The prompt shows your active folder; ~ means your home directory.

> [!Note]
> If something like this appears:
> ```r
> you@PC:/mnt/c/Windows/system32$
> ```
> type:
> ```bash
> cd
> ```

---

### 1.2 Creating directories

First, let's work out where we are. As said above, the terminal is just another way of interacting with your computer. So like how you can use your mouse and clicking to navigate through your folders, you can use your terminal to do the same thing.

:keyboard:Click the mouse into the window and type the following command (all in lowercase) then press the **Enter** key to run it:
```bash
pwd
```
**pwd** is an abbreviation of 'print working directory'. All it does is print out the shell's current working directory. You should see a directory path printed out, something like '**/home/YOUR_USERNAME**'.

:desktop_computer:
```r
/home/$USER
```
#
**Now let's create a new directory** (i.e. folder) to work in. 

:keyboard:Type the following command then press the **Enter** key to run it:
```bash
mkdir intro
```
This should create a new directory (mkdir - '**mk** (make) **dir** (directory)') within the directory you are currently in called '**intro**'. 
#
**Now let's check it is there**.

:keyboard:We can list everything contained within our current directory using the **ls** (list).
```bash
ls
```

:desktop_computer:You should see your terminal return the name of the directory you just made (**intro**).
```ruby
intro
```
#

:keyboard: You can **change directories** using the **cd** (change directory) command.
```bash
cd intro
```

:keyboard: We can check we have successfully changed directory by using **pwd** again:
```bash
pwd
```

:desktop_computer: You should see a directory path printed out, which now ends in intro, something like '**/home/$USER/intro**'.
```r
/home/$USER/intro
```
#

:keyboard: If we try using the **ls** (list):
```bash
ls
```

:desktop_computer: You should see your terminal return an empty directory, because you have not added anything to your intro directory.
```r

```
#

:keyboard: To move back up one directory (i.e. back to '/home/$USER'), we can use '**cd**':
```bash
cd ..
```
Using '**cd ..**' makes you move back up one directory. You can use **ls** or **pwd** to check that you are now back in the directory that contains your intro folder, e.g.:

:keyboard:
```bash
pwd
```

:desktop_computer:
```r
/home/$USER
```

The two full stops after '**cd ..**' are important, and say to only go back one. If you leave out the two full stops and just use '**cd**', it goes to your 'upper most' directory (i.e. /home/$USER). 

You can also use **cd** to specify a directory to move to using the path description as is given by **pwd** (e.g. cd /home/$USER/intro). Play with 'cd', 'cd ..' and 'cd /home/$USER/intro'

#

:keyboard: Move back into your intro folder:
```bash
cd intro
```

:keyboard: Check you are there:
```bash
pwd
```

:desktop_computer: You should see a directory path printed out, which now ends in intro, something like '/home/$USER/intro'.
```r
/home/bea/intro
```
#
**What about creating multiple directories?**

You can also use **mkdir** to make multiple directories and name them all in one command. Let's try that. 

:keyboard:Create multiple directories named *dir1* *dir2* and *dir3*:
```bash
mkdir dir1 dir2 dir3
```

:keyboard:Confirm they have been created:
```bash
ls
```

:desktop_computer: You should see your terminal return the names of the three new directories you made just now (*dir1*, *dir2*, *dir3*).
```r
dir1 dir2 dir3
```

:keyboard: You can get more information if:
```bash
ls -l
```
ls -l shows a **long** listing: one file per line with the file type and permissions, link count, owner, group, size (bytes), last-modified time, and then the filename.

:desktop_computer:
```r
total 0
drwxr-xr-x 2 bea staff 64 28 Nov 15:25 dir1
drwxr-xr-x 2 bea staff 64 28 Nov 15:25 dir2
drwxr-xr-x 2 bea staff 64 28 Nov 15:25 dir3
```

Notice that mkdir created all the folders in one directory. It did not create *dir3* inside *dir2* inside *dir1*, or any other nested structure. But sometimes it is handy to be able to do exactly that, and **mkdir** does have a way
#
**Create nested directories**

:keyboard:
```bash
mkdir -p dir4/dir5/dir6
ls
```

:desktop_computer:
```r
dir1 dir2 dir3 dir4
```

This time you will see that only *dir4* has been added to the list, because *dir5* is inside it, and *dir6* is inside *dir5*.
>The '**-p**' that we used is called an option or a switch (in this case it means 'create the parent directories too, and do not give an error if the directories already exist'). Options are used to modify the way in which a command operates, allowing a single command to behave in a variety of different ways. Options can take different forms in different commands. You will often see them as single characters preceded by a hyphen (as in this case), or as longer words preceded by two hyphens.
#
>[!Note]
>**Navigate in your terminal** [e.g. using 'cd' 'pwd' and 'cd ..'] to enter *dir4* and *dir5* and check the appropriate folders are there.
>
>:keyboard: Make sure you return back to within your intro folder before proceeding, e.g.:
>```bash
>cd /home/$USER/intro
>```
>
>:desktop_computer:
>```r
>/home/$USER/intro
>```

#
**What happens if you want to create a directory with a space in its name?** Let's try it:

:keyboard:
```bash
mkdir folder two
ls
```
:desktop_computer:
```r
folder
two 
```
You should see your terminal has actually returned two new directories, one named 'folder' and one named 'two'. 
If you want to work with spaces in directory or file names, you need to 'escape' them. Escaping is a computing term that refers to using special codes to tell the computer to treat particular characters differently to normal. Try the following:

:keyboard:
```bash
mkdir 'folder two'
ls 
```
:desktop_computer:
```r
'folder two' 
```
Although the command line can be used to work with files and folders with spaces in their names, the need to escape them with quote marks or backslashes makes things more difficult. You can often tell a person who uses the command line a lot just from their file names: they will tend to stick to letters and numbers, and use underscores ('**_**') or hyphens ('**-**') instead of spaces. Try the following:

:keyboard:
```bash
mkdir "folder_two" 
ls
```
:desktop_computer:
```r
folder_two 
```

---

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

:keyboard:
```bash
vi example_sequence_1.fasta
```

:desktop_computer: You should see your terminal change to a largely blank file box, with "example_sequence_1.fasta" [New] at the bottom. 
```r
~
~
~
~
~
"example_sequence_1.fasta" [New] 
```

:keyboard: We need to use '**i**' to switch to **Insert mode**, which will allow us to write in this new file. Press the'**i**' on your keyboard, [you do not need to press Enter afterwards]
```bash
i
```

:desktop_computer:At the bottom of your terminal, you should now see it is in Insert mode "-- INSERT -- ".
```r
~
~
~
~
~
--INSERT-- 
```

:keyboard: Type the following into your file (i.e. two sequence headers followed by short sequences, seperated by lines):
```bash
> Seq_1
AAGTCAACCT
> Seq_2
ATCGGGGTA
```
We now want to switch to **command mode**, to save and quit our new file. To do this, press the **Esc key**. You will see "**--INSERT--**" has disappeared from the bottom of your terminal. 

:keyboard: Now type **:wq**, which means save and quit, and then press the **Enter key**:
```bash
:wq
```
#
You will now see you are out of the file, and back into your previous directory in the terminal. You can use **ls** again to check your new file is there.

:keyboard: To check the contents of your new file have been saved properly and are correct, you can use the **cat** (concatenate) command, which will print the specified file. Try:
```bash
cat example_sequence_1.fasta
```

:desktop_computer:You should see the two fasta sequences you wrote printed out:
```r
> Seq_1
AAGTCAACCT
> Seq_2
ATCGGGGTA 
```

We can also explore files using the '**head**' command, which will return the first lines of a file, depending on the options we specify. The default is the first 10 lines, but we can use **-n** (num) to specify the first '**num**' line instead of this default.

:keyboard:
```bash
head -1 example_sequence_1.fasta
```

:desktop_computer:You should now only see the first line printed out:
```r
> Seq_1 
```

The **cat** (concatenate) command is more than just a file viewer - the name comes from concatenate, meaning to link together. 

#

**Let's try copying this file** to create a second fasta file, and using cat to merge the two together.

:keyboard: To copy something we can use the **cp** (copy) command, where we specify what we want to copy and where we want to copy it to. 
```bash
cp example_sequence_1.fasta example_sequence_2.fasta
```

The above command copies 'example_sequence_1.fasta' to a new file, named example_sequence_2.fasta, and using '**ls**' you should now see it exists within your directory.

:desktop_computer:
```r
example_sequence_1.fasta
example_sequence_2.fasta 
```

:keyboard:Check the contents of the new file using cat:
```bash
cat example_sequence_2.fasta
```

:desktop_computer:You should see the two fasta sequences you wrote printed out.
```r
>Seq_1
AAGTCAACCT
>Seq_2
ATCGGGGTA 
```
#
**cat** can also be used to print the contents of multiple files at once, so we can now try both:

:keyboard:
```bash
cat example_sequence_1.fasta example_sequence_2.fasta
```

:desktop_computer:
```r
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
If you want to pass multiple file names to a single command, there are some useful shortcuts that can save a lot of typing if the files have similar names. For example - a question mark ('**?**') can be used to indicate 'any single character' within the file name. An asterisk (**'*'**) can be used to indicate 'zero or more characters'. These are sometimes referred to as 'wildcard' characters. The following commands all do the same thing but using wildcards, try them out:

:keyboard:
```bash
cat example_sequence_1.fasta example_sequence_2.fasta
```
:keyboard:
```bash
cat example_sequence_?.fasta
```
:keyboard:
```bash
cat *.fasta
```
>what are the outputs?
#
So now let's use the **cat** to **merge** our new files together into a single new file. The command below will concatenate the two files into a new file named "**combined.fasta**". Type the following and press Enter:

:keyboard:
```bash
cat example_sequence_1.fasta example_sequence_2.fasta > combined.fasta
```

The output is redirected into combined.fasta by using "**>**" 

:keyboard:View the contents of combined.fasta using **cat** again:
```bash
cat combined.fasta
```

:desktop_computer: You should see the one file (**combined.fasta**) has two copies of Seq_1 and Seq_2.
```r
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
>[!NOTE]
>**EXERCISE**
>Create your own fasta file using the **vi** editor called '**test_sequence.fasta**' that contains 3 short sequences of your choosing. Use '**head**' and '**cat**' to >explore this file.

---

### 1.4 Searching within files
Occasionally, you might want to search for particular words, expressions or even an isolate or gene name in a document. Using Microsoft word or excel, you would use 'find' to search for this. An alternative to this in Linux is the **grep** command (Global Regular Expression Print). **grep** is a Linux / Unix command-line tool used to search for a string of characters in a specified file. The text search pattern is called regular expression. When it finds a match, it prints the line with the result. The **grep** command is a very handy when searching through large files.
#

:keyboard: Let's try searching for a particular (nucleotide) string in our fasta file:
```bash 
grep 'GTC' example_sequence_1.fasta
```

:desktop_computer: This will return the line that contains the search string 'GTC', i.e. so you should see "AAGTCAACCT"
``` 
AAGTCAACCT
```
#

:keyboard: What happens if we change the case used? Is this important?
```bash 
grep 'gtc' example_sequence_1.fasta
```

:desktop_computer:
```bash

```

Unix systems are case-sensitive, that is, they consider "GTC" and "gtc" to be different. This applies to file and folder names too.
This leads to an important point however, in that you should avoid creating files and folders whose name only varies by case. Not only will it avoid confusion, but it will also prevent problems when working with different operating systems. Windows, for example, is case-insensitive, so it would treat file names that differ by case as a single file, potentially causing data loss or other problems. You might be tempted to just hit the Caps Lock key and use upper case for all your file names. But the **vast majority of shell commands are lower case**, so you would end up frequently having to turn it on and off as you type. Most seasoned command line users tend to stick primarily to lower case names for their files and directories so that they rarely have to worry about file name clashes, or which case to use for each letter in the name.
#
Now, let's try searching for sequence headers in our fasta file. Remember, sequence headers always begin with a '**>**' in fasta file format, which gives us an easy search term. 

:keyboard:
```bash 
grep '>' example_sequence_1.fasta
```

This will return only the lines that contain the search string ">", i.e. so you should see > Seq_1 and > Seq_2 printed on your terminal screen.

:desktop_computer:
```bash 
>Seq_1
>Seq_2
```

**grep** can also be used to count the number of line occurrences of a string within a file. The option **-c** (count) is used for this. Count the number of lines that contain "**>**" within the fasta file. For this, you simply specify "**-c**" before the search terms:

:keyboard:
```bash 
grep -c '>' example_sequence_1.fasta
```

:desktop_computer:This should return the number 2. 
```bash 
2
```
#

:keyboard:Now try in your combined fasta file:
```bash 
grep -c '>' combined.fasta
```

:desktop_computer:This should return the number 4. 
```bash 
4
```

By FASTA format definition, we know that number of sequences in a file should be equal to the number of description lines. So by counting *>* in file, you can count the number of sequences in a fasta file.
#
What if you had lots of files and you wanted to perform the same count in all of your files and save the output of this to a new text file?
You can use grep and the **'*'** wildcard to do this!

Let's try counting the number of lines that contain ">" in all our files with the.fasta extension, and write/save this output to a new text file:

:keyboard:
```bash 
grep -c '>' *.fasta > output.txt
ls
```

You are directing the output of this search to a new file (output.txt), the output is no longer returned to us on the terminal screen. Then using ls we see that this new file (output.txt) is now present in our directory.

:desktop_computer:
```bash 
combined.fasta
example_sequence_1.fasta
example_sequence_2.fasta
output.txt
```

Use the **vi editor** or **cat** to see the contents of this file. 
:keyboard:
```bash 
vi output.txt
ls
```
You should see it lists all the files ending with the fasta extension and gives the count score for ">" line occurances.

:desktop_computer:
```bash 
combined.fasta: 4
example_sequence_1.fasta: 2
example_sequence_2.fasta: 2
```
#
> [!NOTE]
> **EXERCISE**
>Use grep to explore the fasta file (test_sequence.fasta) you made previously. How do you search for the lines that contain "AA"? How many sequences does it contain?

---

### 1.5 Deleting files and folders
In this next section we are going to start deleting files and folders. To make absolutely certain that you do not accidentally delete anything in your home folder, use the **pwd** command to double-check that you are still in the **/intro** directory before proceeding.
#
To delete things, we can use the **rm** (remove) command.

>[!WARNING]
>Unlike in windows/mac where you might get a prompt asking if you are sure you want to delete something... this will not happen in command line. When you use **rm** and **press Enter**
>***- whatever you're trying to delete is deleted!***

>[!TIP]
>Similarly, unlike in windows/mac where the things you delete are moved to a folder called "trash" or similar, **rm** will delete them totally, utterly, and irrevocably. You need to be careful with the parameters you use with **rm** to make sure you are only deleting the file(s) you intend to. You should take particular care when using wildcards (e.g. **'*'**), as it is easy to accidentally delete more files than you intended. If you are at all uncertain use the **-i** (interactive) option to **rm**, which will prompt you to confirm the deletion of each file; enter **Y** to delete it, **N** to keep it, and press **Ctrl-C** to stop the operation entirely.
#
Let's try deleting one of the extra files we created earlier (example_sequence_2.fasta). 

:keyboard: First, double-check it is there in your current folder space using '**ls**'
```bash 
rm example_sequence_2.fasta
```

Using '**ls**' you should now be able to see that the *example_sequence_2.fasta* file has been deleted.
#
**What about folders?** 

:keyboard:Let's try deleting a folder we created earlier but didn't use (folder_two).
```bash 
rm folder_two
```

:desktop_computer: When you press Enter, you should see your terminal return:
```bash 
rm folder_two: is a directory
```

What happened there? Well, it turns out that **rm** does have one little safety net to make sure you do not accidentally delete a directory and all of the files inside it with one single command. Luckily there's a **rmdir** (remove directory) command that will do the job for us instead:

:keyboard:
```bash 
rmdir folder_two
```

>[!NOTE]
>**rmdir** will only delete empty folders. Another small safety net to prevent you from accidentally deleting a folder full of files when you did not mean to. The addition of options to our **rm** or **rmdir** commands will let us perform more dangerous actions without the aid of a safety net. In the case of **rmdir** we can add a **-p** switch to tell it to also remove the parent directories. Think of it as the counterpoint to **mkdir -p**. 

---

### 1.6 Writing a bash script
A **bash script** is a series of commands written in a file. These are read and executed by the bash program. The program executes line by line.

For example, you can navigate to a certain path, create a folder and spawn a process inside it using the command line. You can do the same sequence of steps by saving the commands in a bash script and running it. You can **run the script** any number of times, and only need to **'press Enter' once**.

**Bash scripts** effectively allow you to automate a series of commands so you do not have to type them all individually.

By naming conventions, bash scipts end with a **.sh** file extension. Scripts are also identified by containing the path to the bash interpretor at the start (i.e. #!
/bin/bash). This is known as a shebang statement, and will be the first line of the script.
We are going to create a very simple **bash script** to give you a taste of how they work. We are going to create a script that when executed **echos Hello World** to the terminal console.
#

:keyboard: To create our bash script, we can again use the **vi editor**:
```bash 
vi hellow_world.sh
```

As seen previously, this will open up a new file, and you will need to press '**i**' to enter insert mode. 

:keyboard: Once in insert mode, write the following into your new file:
```bash 
#!bin/bash
echo 'Hello World'
```

Use **Esc** and **:wq** to save and quit your new file. Test it has been written and saved correctly by using **vi hello_world.sh** to reopen and check.

:keyboard: In order to execute the script the file needs to be made **executable** by the use of **chmod u+x** filename:
```bash 
chmod u+x hellow_world.sh
```

**chmod** modifies the existing rights of a file for a particular user. We are adding **+x** (make executable) to user **u**.

:keyboard: You can now run the script in the following ways:
```bash 
./hellow_world.sh 
```

or

:keyboard:
```bash 
bash hellow_world.sh 
```
Try them both, and you should see **Hello World** returned to you on the terminal console.

:desktop_computer:
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

---

### 1.7 Manuals
Most Linux command line tools include a man page. Try taking a brief look at the pages for some of the commands you've already encountered: **man ls**, **man grep**, **man cp**, **man rmdir** and so on. There's even a man page for the man program itself, which is accessed using **man man**. e.g.:

:keyboard:
```bash 
man grep 
```

:keyboard:
```bash 
man ls 
```

:keyboard:
```bash 
man cp 
```

Exit the manual pages by pressing '**q**' for quit!

---


# 2. Miniconda 

Miniconda is a lightweight installer for conda, an open-source package and environment manager used to install software and their dependencies across Linux, macOS, and Windows (including WSL) without needing admin rights. With conda you create isolated environments—self-contained sandboxes—so different projects can use different versions of Python/R and bioinformatics tools without conflicts. It solves dependency hell, makes setups reproducible (via environment.yml), and lets you swap or pin versions easily. Miniconda gives you just conda and Python (no extra bundles), so installs are faster and smaller, and you can pull exactly what you need from channels like conda-forge and bioconda.

---

### **TABLE OF CONTENTS**
- [2.1 Install Miniconda](#21-Install-miniconda)
   - [2.1.1 Update Ubuntu](#211-Update-Ubuntu)
   - [2.1.2 Download and Install Miniconda](#212-Download-and-Install-Miniconda)
- [2.2 Create a conda environment](#22-Create-a-conda-environment)
   - [2.2.1 Configure Conda](#221-Configure-Conda)
   - [2.2.2 Create the dtc-bio conda environment](#222-Create-the-dtc-bio-conda-environment)
   - [2.2.3 Activate dtc-bio environment](#223-Activate-dtc-bio-environment)
   - [2.2.4 Check the tools are available](#224-Check-the-tools-are-available)

---

## 2.1 Install Miniconda

### 2.1.1 Update Ubuntu

:keyboard: Refreshes package lists and upgrades core tools so the installer works smoothly.
```bash 
sudo apt update && sudo apt -y upgrade 
sudo apt -y install wget git 
```
>It will ask for your password
>You will see lot of lines starting with Get: and Hit: during apt update.
>A summary such as X upgraded, Y newly installed... for apt -y upgrade.
>wget and git will show as setting up ... if they were not already installed.
#
### 2.1.2 Download and Install Miniconda

:keyboard: We download the Linux installer and start the text-based setup.
```bash 
cd ~
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```
\
:desktop_computer: You will see a prompt like:
```bash 
In order to continue the installation process, please review the license agreement. Please, press ENTER to continue
```

\
Press **ENTER** to show the license text (pages will scroll).

\
:desktop_computer: After the license text:
```bash 
Do you accept the license terms? [yes|no]
```

\
Type **yes** and press **ENTER**.

\
:desktop_computer: Install location prompt (default is your home, e.g. /home/<you>/miniconda3):
```bash 
Press **ENTER** to confirm the location, CTRL-C to abort, or specify a different location
```

\
Press **ENTER** to accept the default.

\
:desktop_computer: Initialization prompt:
```bash 
Do you wish the installer to initialize Miniconda3 by running conda init? [yes|no]
```

\
Type **yes** and press **ENTER**.

\
:desktop_computer: When it finishes you’ll see something like:
```bash 
Thank you for installing Miniconda3!
```

\
:keyboard: Reload your shell so conda is on PATH
```bash 
exec bash
```

\
:desktop_computer:
```r 
(base)you@PC:~$
```

>If exec bash isn’t available or you still get “conda: command not found”, run source ~/.bashrc or simply close and reopen the terminal.

\
:keyboard: Verify the installation
```bash 
conda --version
```
:desktop_computer:
```bash 
conda 25.9.0
```

\
Accept terms of Service (toS)

:keyboard: Some installs pull packages from Anaconda’s default channels, which now require ToS acceptance. Safe to do now.
```bash 
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r
```
---

## 2.2 Create a conda environment

### 2.2.1 Configure Conda

Conda needs two things to behave well in bioinformatic course:
1. Where to look for packages (the *channels*)
2. How to decide versions quickly and reliably (the *solver*)
- **Channels**:
   - **conda-forge** community-maintained, modern compilers; the base for most current builds
   - **bioconda** bioinformatics packages compiled to work with conda-forge
   - **defaults** Anaconda’s repository; keep as a fallback
> The order is important: it controls which repository conda prefers when the same package exists in multiple places.
-**Strict channel priority** tells conda: “If a package exists in a higher-priority channel, don’t mix in lower-priority builds.” This reduces version conflicts and makes environments more reproducible.
-The **solver** decides a set of package versions that satisfy all dependencies. libmamba is a drop-in replacement for the classic solver that is much faster and tends to backtrack less, so students spend time learning, not waiting.
Install the faster solver and set channels with strict priority

\
:keyboard: Install and enable the faster solver
```bash
conda install -n base -y conda-libmamba-solver
conda config --set solver libmamba
```

\
:keyboard:Tell conda where to get the packages (in priority)
```bash 
conda config --add channels conda-forge
conda config --add channels bioconda
conda config --add channels defaults
```

\
:keyboard:Avoid mixing packages across channels
```bash 
conda config --set channel_priority strict
```
**What this does?**
- **libmamba solver**: a much faster dependency solver than the classic one.
- **Channels**: define the sources; we put conda-forge first (it’s the base for most modern builds), bioconda second (depends on conda-forge), and defaults last as a fallback.
- **Strict priority**: prevents mixing packages from lower-priority channels when a higher-priority one provides them—this improves reproducibility.

#
### 2.2.2 Create the dtc-bio conda environment

A conda environment is a clean sandbox with its own packages and versions. For a practical, this means:
- **Reproducibility**: everyone has the same toolchain.
- **Isolation**: no conflicts with other projects or the base env.
- **Portability**: easy to recreate on another machine.

This environment bundles the exact tools you’ll use today:
- **fastqc** (quality checks), **spades** (assembly), **kraken2** (taxonomic classification), **bwa** (read mapping), **samtools** (BAM/CRAM utilities), **quast** (assembly QC),
- **NCBI helpers**: ncbi-datasets-cli (the datasets command) and ncbi-genome-download,
- **Utilities**: pigz (faster gzip), unzip,
- **python 3.10**: so scripts/examples work consistently.

:keyboard:
```bash 
conda create -n test -y -c conda-forge -c bioconda --strict-channel-priority python=3.10 fastqc spades kraken2 bwa samtools quast=5.2.* ncbi-datasets-cli ncbi-genome-download pigz unzip
```

:desktop_computer:
```bash 
Collecting package metadata: done
Solving environment: done
## Package Plan ##
  environment location: /home/<you>/miniconda3/envs/dtc-bio
Proceed ([y]/n)?  --> auto-yes because -y
Downloading and Extracting Packages ...
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
```
#
### 2.2.3 Activate dtc-bio environment

Conda environments isolate tools and libraries so this practical doesn’t clash with other projects. When an env is active, any python or tool you run comes from that env—not your system install.

:keyboard:
```bash 
conda activate dtc-bio
```

:desktop_computer: your shell prompt gains an (dtc-bio) prefix—this is your visual cue that the env is active.
```bash 
(dtc-bio) you@PC:~$
```
#
### 2.2.4 Check the tools are available

:keyboard: Confirm each command is on your PATH inside the environment
```bash 
ncbi-genome-download --version
python --version
fastqc --version
spades.py --version
kraken2 --version
bwa 2>&1 | head -n3 # first line from bwa help
samtools --version | head -n1 # first line from samtools help
quast.py --version
```
> **--version** or help text proves the executable is installed and visible in **current**
> **bwa** prints help to stderr, so we capture the first lines to show it’s working.
> **samtools** prints multiple lines; **head -n1** shows the top line only.

:desktop_computer:
```bash 
0.3.3 #this corresponds to ncbi-genome-download 
Python 3.10.14
FastQC v0.12.1
SPAdes genome assembler v4.0.0
Kraken version 2.1.3

Program: bwa (alignment via Burrows-Wheeler transformation)
Version: 0.7.18-r1243-dirty 
Copyright 2013-2023, Derrick Wood (dqood@cs.jhu.edu)
samtools 1.21 
QUAST v5.2.0
```
#

**Deactivate (leave) the environment**

When you finish, deactivate the environment so your shell goes back to its previous PATH.

:keyboard:
```bash 
conda deactivate
```

\
**What happens**

- Your prompt loses the (*dtc-bio*) prefix (it may show (*base*) or no prefix, depending on your settings).
- Tools like *python*, *fastqc*, etc., will now be the versions from your base setup (or won’t be found if only installed in *dtc-bio*).
  
:desktop_computer:
```bash
(dtc-bio) you@host:~$ conda deactivate
you@host:~$            # prompt no longer shows (dtc-bio); often switches to (base) or no prefix
```

---

# 3. Bacterial genome assembly
The goal of the second part of this practical is to assemble a bacterial genome using sequencing reads. The genome will be assembled using short-read sequencing data to produce '**contigs**'. **Contigs** is a term that means contiguous DNA and refers to the consensus sequence that is formed when sequencing reads (usually from fastq files) are ‘stitched together’ to form regions of the genome. With short reads, repetitive sequences usually prevent complete closed genomes from being produced and instead the end result is usually smaller pieces of contiguous DNA that make up most of the genome. Hybrid assembly approaches (i.e. using long and short read sequencing data together) can be used to try and 'close the genome', to give you a complete genome where you know how everything fits together. For this practical we will be working with short reads only, obtained from illumina sequencing of a *Pseudomonas aeruginosa* genome.

---

### **TABLE OF CONTENTS**
- [3.1 Manage data](#31-Manage-data)
- [3.2 Running fastQC](#32-Running-fastQC)
- [3.3 Genome assembly](#33-Genome-assembly)
- [3.4 Quality assesment of your assembly](#34-Quality-assesment-of-your-assembly)

*Pseudomonas aeruginosa* is a Gram-negative bacterium and opportunistic pathogen. It is a major problem in clinical settings and is as a major caustive pathogen of ventilator-associated pneumonia. *P. aeruginosa* is becoming increasingly resistant to the antibiotics we use to treat it. Genome sequencing data is useful for understanding what the population of *P. aeruginosa* looks like, how many acquired antibiotic resistance genes this pathogen carries, and understanding how *P. aeruginosa* is evolving in clinically relevant environments (such as within ICU patients with pneumonia infections).

---

## 3.1 Manage data

:keyboard: Let's first create a new directory (within our intro folder) to work in:
```bash
mkdir assembly
cd assembly
```

Check you are now in your new folder.

For the purposes of this practical, we will be using a pair of forward and reverse fastq.gz (comparessed gzipped fastq) files from *P. aeruginosa* available from the European Nucleotide Archive. 

:keyboard: You can download this data using the command wget followed by the address to that file(s)
```bash
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_1.fastq.gz
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_2.fastq.gz
```

To check that the files have downloaded we can use the **ls -lh** command (**-l** long; **-h** human-readable), which also allows us to check the size of the files:

:keyboard:
```bash
ls -lh
```

The files that we've downloaded are gzipped **FASTQ** files. Take a look at one of them:

```bash
PSA-2017-01_1.fastq.gz
PSA-2017-01_2.fastq.gz
```

:keyboard: We can use a combination of commands to view the first few lines of a compressed files. 
```bash
zcat PSA-2017-01_1.fastq.gz | head -n 20
```
**zcat** decompress the file and shows it in the terminal. However, **fastq** files contained millions of reads, and we want to avoid “seing” the whole file in the terminal. In order to avoid this, we add another command, in this case head, after the symbol | which pipes the output zcat as an input of the next command head -n 20. In the end, you’ll see only the first 20 lines of the fastq.gz file. 

**How does it look like commpare to a fasta file?**

---

## 3.2 Running fastQC
The tool **fastqc** assesses the quality scores across all of the reads in your data. You can read more about it here: https://dnacore.missouri.edu/PDF/FastQC_Manual.pdf

:keyboard: First, create a folder to save fastqc results
```bash
mkdir fq-results
```

:keyboard: Let’s run fastqc on our 2 samples:
```bash
fastqc PSA-2017-01_1.fastq.gz -o fq-results
fastqc PSA-2017-01_2.fastq.gz -o fq-results
```

**-o**: output directory. Location where the files will save.

:keyboard: View the files that have been generated:
```bash
cd fq-results
ls *fastqc*
```

:desktop_computer:
```bash
PSA-2017-01_1_fastqc.html
PSA-2017-01_1_fastqc.zip
PSA-2017-01_2_fastq.html
PSA-2017-01_2_fastq.zip
```

For each file, **fastQC** has produced both a .zip archive containing all the plots, and a html report. 

:keyboard: We can open the html files using a web browser: e.g.:
```bash
explorer.exe PSA-2017-01_1_fastqc.html
```

For each position, a boxplot is drawn with:

• the median value, represented by the central red line

• the inter-quartile range (25-75%), represented by the yellow box

• the 10% and 90% values in the upper and lower whiskers

• the mean quality, represented by the blue line

The y-axis shows the quality scores. The higher the score, the better the base call. The background of the graph divides the y-axis into very good quality scores (green), scores of reasonable quality (orange), and reads of poor quality (red). It is normal with all Illumina sequencers for the median quality score to start lower over the first 5-7 bases and to then rise. The quality of reads on most platforms will drop at the end of the read. This is often due to signal decay or phasing during the sequencing run. We can see that our sequence length is 35-250bp. This makes sense, because this was sequenced with a 250 bp paired-end sequencing run on an Illumina MiSeq sequencer. The sequencing reads have a %GC of 65, this is within the expected
%GC range for Pseudomonas aeruginosa (which has a highly GC biased genome). Anything above a score of 25 is usually considered good quality, so we can see these are reasonable quality reads.

\
**Check the fastqc reports for both files, which file is of better quality?**

#
**Optional step: trimming & filtering data**

Low quality sequences and adapters can be removed used programs such as trimmomatic (read more here: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4103590/ , https://www.melbournebioinformatics.org.au/tutorials/tutorials/assembly/assembly- protocol/).
Whether you should do this can depend on the objective of your sequencing experiments (e.g. read more here: https://dnatech.genomecenter.ucdavis.edu/faqs/when-should-i- trim-my-illumina-reads-and-how-should-i-do-it/).
We will not do this today, but you should be aware of it for genome assemblies in the future.

---

## 3.3 Genome assembly
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

:keyboard: To run **SPAdes** to assemble our paired fastq reads PSA-2017-01_1.fastq.gz and PSA-2017-01_2.fastq.gz in assembly mode only:
```bash
spades.py -1 [location-to-read-1] -2 [location-to-read-2] –-only-assembler -o spades_assembly
```

Replace the information in **[ ]** to the path of each fastq file. Wait for the command to run. **SPAdes** should give some output about what it is doing. At the end, you might see an assembly warning about erroneous kmer, that is OK for the sake of this exercise (re. run in assembly mode only).

>this will take 5-10min

:keyboard: Navigate into your spades_assembly output folder and check whats there:
```bash
cd spades_assembly
```

The file *contigs.fasta* is the contig file produced from the reads, and what we will be working with. You can read more about what the other files are on the GitHub page: https://github.com/ablab/spades

#
**Exercice**

How many contigs (sequences) have the result of the assembly (*contigs.fasta*)? 
#
## 3.4 Quality assesment of your assembly 

We can run **QUAST** (QUality ASsessment Tool) for an overview of our assembly metrics. You can read more about QUAST here: https://quast.sourceforge.net/docs/manual.html:

:keyboard:
```bash
quast.py contigs.fasta
```

After it has finished running, you should see a new folder with the results in has been created - '**quast_results**'.

Navigate into this folder, and then into the new results (**results_[data]_[hour]**) sub-folder. In this folder use '**ls**' to check what is there. We are interested in the '**report.html**' file, which is a summary report file.

:keyboard:
```bash
explorer.exe report.html
```
Quck readings order:
- Total length & GC% – sanity check they match the organism (ballpark genome size and GC).
   - *P. aeruginosa strans have genomes between 5.5-7 Mb, with GC ~66-67%*
- Continuity – how fragmented is the assembly? Look at # contigs, N50/L50, largest contig.
- Accuracy (needs a reference) – genome fraction, misassemblies, mismatches/indels per 100 bp, duplication ratio.
- Gaps/ambiguity – # N’s per 100 kbp (lower is better).

Key Metrics:
- **contigs (≥ X bp**): how many pieces your genome is split into. Fewer is better.
- **Total length (≥ X bp)**: sum of contig lengths. Should be close to the expected genome size (too big → potential contamination/duplication; too small → missing sequence).
- **Largest contig**: size of the biggest piece. Bigger is better.
- **N50**: the contig length at which **half** of the assembly is in contigs **at least** that long. Higher = more contiguous.
- **L50**: the **number** of contigs needed to reach 50% of the assembly when sorted by size. Lower = more contiguous.
- **NG50 / LG50**: same as N50/L50 but uses an expected **genome size** (from the reference) instead of your assembly size. Useful when assemblies differ in total length.
- **Genome fraction** (%) (with reference): fraction of the reference covered by your assembly. Higher is better.
- **Misassemblies** (with reference): structural errors (joins, inversions, relocations) relative to the reference. 0 is ideal; a few may be acceptable.
- **Mismatches / indels per 100 kbp** (with reference): base-level accuracy. Lower is better.
- **Duplication ratio** (with reference): aligned bases in the assembly divided by bases covered on the reference; ~**1.0** is ideal. >1 hints at duplicated content.
- **#N’s per 100 kbp**: number of unknown bases (gaps). Lower is better.
- **GC** (%): should match the organism’s typical GC content.

---

# 4. Species identity check
A final step in our genome quality check is to confirm that the genome and the DNA it is composed of belongs to our species of interest and that it is not contaminated with DNA from another bacterium. There are a number of tools that can do this and this depends on whether you want to check your data before it has been assembled using software such as **KRAKEN** 
#
>[!NOTE]
>Before runing the following commands go back to your directory by typing **cd**
#
### **TABLE OF CONTENTS**
- [4.1 Download *Pseudomonas* type genomes](#41Download-Pseudomonas-type-genomes)
   - [4.1.1 Create the PATHS](#411-Create-the-PATHS)
   - [4.1.2 Create the corresponding folders](#412-Create-the-corresponding-folders)
   - [4.1.3 Download the *Pseudomonas* genomes from NCBI](#413-Download-the-Pseudomonas-genomes-from-NCBI)
   - [4.1.4 Check you have the files](#414-Check-you-have-the-files)
   - [4.1.5 Decompress the fastas](#415-Decompress-the-fastas)
- [4.2 Build a Kraken2 database](#42-Build-a-Kraken2-database)
- [4.3 Classify your assembly](#43-Classify-your-assembly)
   - [4.3.1 Maximise hits](#431-Maximise-hits)
   - [4.3.2 Stricter classification](#432-Stricter-classification)
- [4.5 Optional: Evidence of AMR genes in your genome](#45-Optional:Evidence-of-AMR-genes-in-your-genome)
   - [4.5.1 Find cadidate AR genes](#451-Find-cadidate-AR-genes)
   - [4.5.2 Make your genome searchable](#452-Make-your-genome-searchable)
   - [4.5.3 Search your AR genes against your genome](#453-Search-your-AR-genes-against-your-genome)
#

## 4.1 Download *Pseudomonas* type genomes

Kraken needs a reference database; we’ll build one by downloading the type-strain genomes for each *Pseudomonas* species from NCBI. The type strain is the official reference that defines a species.

#

### 4.1.1 Create the PATHS

We’ll keep downloads, intermediate FASTA files, and the Kraken2 database in predictable folders under your home directory. Using variables makes later commands shorter and less error-prone.

Define the folders and the number of threads to use.

:keyboard:
```bash
# paths
SRC=~/genomes/pseudomonas_type                 # where raw genomes will be saved 
STAGE=~/genomes/pseudomonas_type_fna           # where we'll stage/extract FASTA files
DB=~/dbs/k2_pseudomonas_type                   # where the Kraken2 database will be built
ASMB=~/assembly/spades_assembly/contigs.fasta  # where contigs.fasta file is
THREADS=8                                      # how many CPU threads to use
```

**What is this important?**
- These are **shell variables**, not the global **PATH** environment variable
- **~** expands to your **home directory** (eg /home/you)
- **THREADS** is just a number we pass to tools that support parallelism (tune it to your machine; on shared machines, keep it modest).

>[!TIP]
>Always **quote** variables in commands (**"$SRC"**), especially if paths might contain spaces

>[!NOTE]
>These variables last only for the **current shell** (ie, until you close this terminal window). To keep them for future terminals, add the four lines to your ~/.bashrc (Linux).

#
### 4.1.2 Create the corresponding folders

We’ll create the directories pointed to by your variables and a library/ subfolder for Kraken2’s DB.

:keyboard:
```bash
mkdir -p "$SRC" "$STAGE" "$DB"/library
```
**What this does**
- **-p** creates parent directories as needed (no error if they already exist).
- **"$SRC"** and "$STAGE" become your download and staging folders.
- **"$DB"/library** creates the standard subfolder where Kraken2 stores library files.

>[!WARNING]
>**Mind the variable names and $**:
> - If you misspell a variable (e.g., **SCR** instead of **SRC**) and run mkdir -p "$SCR", the variable is empty and you’ll get an error like *mkdir: missing operand*—nothing useful is created. Use the exact names you defined.
> - If you forget the **$** and write **mkdir -p "SRC"**, you’ll create a folder literally named SRC in the current directory (wrong place).
> - Keep the quotes: **"$SRC"** prevents paths with spaces from splitting into multiple directories.

>[!NOTE]
>Prefer **~** (your home) over absolute paths like **/genomes/...** unless you know you have permissions; otherwise you may hit *Permission denied*. On a new terminal, re-run the variable definitions (they don’t persist unless added to your shell startup file).

#
### 4.1.3 Download the *Pseudomonas* genomes from NCBI

We’ll fetch **type-strain genomes** for *Pseudomonas* to use later (e.g., for Kraken2). Downloads go into "$SRC".

:keyboard: Run the downloader (use your THREADS if you set it earlier).
```bash
ncbi-genome-download bacteria --section genbank --genera "Pseudomonas" --assembly-levels chromosome,complete,scaffold --type-materials type,neotype,proxytype,synonym --formats fasta --parallel "${THREADS:-4}" --no-cache --output-folder "$SRC"
```
What the options means:
- **bacteria** → limit to bacterial genomes.
- **--section genbank** → pull from GenBank (not RefSeq).
- **--genera "Pseudomonas"** → only this genus.
- **--assembly-levels chromosome,complete,scaffold** → choose assembly completeness tiers to include.
- **--type-materials ...** → only **type/neo/proxy/synonym** type-material strains (good species references).
- **--formats fasta** → download FASTA sequence files (*.fna.gz).
- **--parallel N** → use N workers in parallel (speeds downloads).
- **--no-cache** → don’t reuse stale metadata.
- **--output-folder "$SRC"** → where files will be saved (ie ~/genomes/pseudomonas_type)

>[!NOTE]
>“It looks like nothing is happening” — that’s normal
>The tool may be quiet while it’s communicating with NCBI and downloading. If you want more messages, add -v (verbose) to the command.
>You can check in your Linux, open home → genomes/pseudomonas_type/
> You should see compressed FASTA files like *.fna.gz and a checksums file (often MD5SUMS or md5checksums.txt).

#
### 4.1.4 Check you have the files

This command counts how many FASTA files were downloaded under **"SCR"**

:keyboard:
```bash
find "$SRC" -type f \( -name "*_genomic.fna.gz" -o -name "*.fna.gz" \) | wc -l
```
**What it does**
- **find "$SRC"**: search recursively inside your download folder.
- **-type f**: only real files (skip directories).
- **\( ... -o ... \)**: group an OR match:
- **-name "*_genomic.fna.gz"** → typical NCBI genomic FASTA names
- **-name "*.fna.gz"** → catch any other FASTA files
- **| wc -l**: count the matching files (one line per file ⇒ number of files).

**What to expect**

For this practical, you should see: 226

(Counts can change over time if NCBI updates type strains; for class reproducibility we expect 226.)

#
### 4.1.5 Decompress the fastas

**Why this step?** 

Kraken2’s “add to library” step works best with plain FASTA files (.fna), not compressed *.fna.gz. We’ll unpack the downloads into your staging folder ($STAGE).

:keyboard: decompress every *.fna.gz under "$SRC" into "$STAGE".
```bash
while IFS= read -r -d '' f; do
  out="$STAGE/$(basename "$f" .gz)"
  gzip -dc -- "$f" > "$out"
done < <(find "$SRC" -type f \( -name "*_genomic.fna.gz" -o -name "*.fna.gz" \) -print0)
```
**What that script is doing** (step-by-step)
- **find "$SRC" ... -print0**. Searches recursively for *.fna.gz files and prints each match NUL-terminated (safe for spaces/newlines in filenames). 
- **while IFS= read -r -d '' f; do ... done < <( ... )**. Reads those NUL-separated paths one by one into variable f.
   - -d '' → read until NUL
   - -r → don’t treat backslashes specially
   - IFS= → don’t trim leading/trailing spaces
- **out="$STAGE/$(basename "$f" .gz)"**. Builds the output path by stripping the trailing .gz and placing the file in "$STAGE", e.g. .../X_genomic.fna.gz → .../pseudomonas_type_fna/X_genomic.fna
- **gzip -dc -- "$f" > "$out"**. Decompress d (-d) to cstdout (-c) and redirect to the output file. -- ends option parsing (safety).

>[!NOTE]
>Make sure "$STAGE" exists first: mkdir -p "$STAGE".

**Sanity check** do the FASTAs look valid? 

:keyboard: count the number of FASTA records (headers) per file; the numbers should be > 0.
```bash
grep -c '^>' "$STAGE"/*.fna | head
```

What this does
- **'^>'** matches FASTA headers (each sequence starts with >).
- **-c** prints a count per file.
- **head** shows the first few lines to avoid dumping hundreds of entries.

#

## 4.2 Build a Kraken2 database

**Kraken2** needs two things: (1) your reference sequences (the staged FASTA files) and (2) the NCBI taxonomy. This step indexes the staged genomes into a searchable database keyed by k-mers/minimizers and links them to taxonomy IDs.

:keyboard: Start clean and make the standard folders
```bash
rm -rf "$DB"; mkdir -p "$DB/library"
```

**What this does**
- **rm -rf "$DB"** removes any old database so you don’t accidentally mix versions. *Be careful: this permanently deletes that folder*.
- **mkdir -p "$DB/library"** recreates the database directory with the library/ subfolder where Kraken2 stores input sequences before building.

:keyboard: Add the staged FASTAs, download taxonomy, and build.
```bash
# Add every staged FASTA to the Kraken2 library
find "$STAGE" -type f -name "*.fna" -print0 \
  | xargs -0 -I{} kraken2-build --add-to-library "{}" --db "$DB"

# Get the current NCBI taxonomy for the DB
kraken2-build --download-taxonomy --db "$DB"

# Build the DB index (uses $THREADS if you set it earlier)
kraken2-build --build --threads "$THREADS" --db "$DB"

# Optional: remove temporary files to save space
kraken2-build --clean --db "$DB"
```

**What each command does**
- **--add-to-library copies** (or links) each **.fna** into **"$DB"/library/** so they’re included in the build.
- **--download-taxonomy** fetches NCBI taxonomy files (**names.dmp**, **nodes.dmp**, etc.).
- **--build** creates the search index from your sequences + taxonomy (this step is CPU/disk heavy and can take a while, depending on your machine and the number of genomes).
-** --clean** deletes intermediate files after a successful build (saves disk space).

:keyboard: Quick verify
```bash
du -sh "$DB"
kraken2-inspect --db "$DB" | head
```
:desktop_computer:
```bash
1.5G    /home/teaching/dbs/k2_pseudomonas_type
# Database options: nucleotide db, k = 35, l = 31
# Spaced mask = 11111111111111111111111111111111110011001100110011001100110011
# Toggle mask = 1110001101111110001010001100010000100111000110110101101000101101
# Total taxonomy nodes: 213
# Table size: 239895392
# Table capacity: 381643337
# Min clear hash value = 0
100.00  239895392       0       R       1       root
100.00  239895392       0       R1      131567    cellular organisms
100.00  239895392       0       R2      2           Bacteria
```

**How to read this output**
- **du -sh "$DB"** shows the total size of the database directory (a rough sanity check that something substantial was created).
- ** kraken2-inspect --db "$DB" | head** prints the database summary followed by the first taxonomy lines with counts (number of minimizers/k-mers assigned per taxon).
   - You should see top-level taxa (e.g., “root”, “Bacteria”) and then entries for **Pseudomonas** with non-zero counts.
   - If you see an empty or tiny report, the library may be empty or the build failed—recheck the steps above.

#
## 4.3 Classify your assembly

Kraken2 assigns each contig to a taxon by matching its k-mers to your database. We’ll first classify with no confidence filter (maximise hits), then show how to add one.

### 4.3.1 Maximise hits

:keyboard:
```bash
# Replace this with your assembler’s output path, e.g. SPAdes:
# ASMB="spades_output/contigs.fasta"
ASMB="[path to contigs.fasta]"

kraken2 --db "$DB" --threads "$THREADS" --use-names --report k2_pseudo.report --output k2_pseudo.out "$ASMB"
```
**What the options mean**
- **--db "$DB"**: the Kraken2 DB you built (taxonomy + your staged genomes).
- **--threads "$THREADS"**: parallelism.
- **--use-names**: show scientific names (not just NCBI taxids).
- **--report k2_pseudo.report**: machine-readable summary table by taxon.
- **--output k2_pseudo.out**: per-contig classifications (each line = one contig).
- Final arg = your **contigs FASTA** (e.g., spades_output/contigs.fasta).

:desktop_computer:
```bash
Loading database information... done.
2464 sequences (6.93 Mbp) processed in 0.331s (446.5 Kseq/m, 1256.68 Mbp/m).
  2385 sequences classified (96.79%)
  79 sequences unclassified (3.21%)
```
- **classified**: contigs asigned to some taxon
- **unclassified**: contigs with no match
#
**Read the species level summary**

:keyboard:Show the top species (S) lines sorted by % of contigs)
```bash
grep $'\tS\t' k2_pseudo.report | sort -nr -k1,1 | head
```

:desktop_computer:
```bash
92.29  2274    2176    S       287                         Pseudomonas aeruginosa
  1.38  34      34      S       2994495                     Pseudomonas paraeruginosa
  0.45  11      11      S       78327                       Pseudomonas mosselii
  0.32  8       8       S       2961893                   Pseudomonas triclosanedens
  0.16  4       4       S       46680                         Pseudomonas nitroreducens
  0.12  3       3       S       2906062                   Pseudomonas wenzhouensis
  0.08  2       2       S       706570                    Pseudomonas flexibilis
  0.08  2       2       S       53408                       Pseudomonas citronellolis
  0.08  2       2       S       2320867                   Pseudomonas cavernae
  0.08  2       0       S       76759                       Pseudomonas monteilii
```
**How to read the report (columns)**
1. % of sequences (contigs) in this clade.
2. Number of fragments covered by the clade rooted at this taxon
3. Number of fragments covered by the clade rooted at this taxon
4. Rank ((U)nclassified, (R)oot, (D)omain, (K)ingdom, (P)hylum, (C)lass, (O)rder, (F)amily, (G)enus, or (S)pecies).
5. NCBI taxonomic ID number.
6. Scientific name (indented in the full report to show hierarchy).

So “92.29” means 92.29% of contigs fall within the P. aeruginosa clade.
#
### 4.3.2 Stricter classification

We’ll re-run Kraken2 with options that reduce weak/ambiguous assignments. You should see slightly fewer classified contigs but a cleaner top species.

:keyboard: Run with a confidence cutoff, require multiple hit groups, and use quick mode.
```bash
# Set your contigs path if you haven't already
ASMB="[path to contigs.fasta]"   # e.g. spades_output/contigs.fasta
kraken2 --db "$DB" --threads "$THREADS" --use-names –quick --confidence 0.1 --minimum-hit-groups 3 -report k2_pseudo_fast.report --output k2_pseudo_fast.out "$ASMB"
```
Copy/paste gotchas: make sure --quick uses two ASCII hyphens, and --report has two hyphens (not -report).

**What these options do**
- **--confidence 0.1** → require at least 10% of a read/contig’s k-mer evidence to support the assigned taxon. Filters out very weak matches.
- **--minimum-hit-groups 3** → need support from ≥3 distinct hit groups (independent k-mer/minimizer groups) before assigning; reduces one-off spurious hits.
- **--quick** → faster pass that stops searching once sufficient evidence is found; tends to lower sensitivity a bit but speeds up classification.
- Reports/outputs are written to new files (**k2_pseudo_fast.***) so you can compare with Step 1.

:desktop_computer:
```bash
89.61  2208    2207    S       287                         Pseudomonas aeruginosa
  0.85  21      21      S       2994495                     Pseudomonas paraeruginosa
  0.28  7       7       S       78327                       Pseudomonas mosselii
  0.08  2       2       S       2961893                   Pseudomonas triclosanedens
  0.04  1       1       S       53408                       Pseudomonas citronellolis
```

**How to interpret**
- The top line means ~89.6% of contigs fall in the P. aeruginosa clade after filtering.
- Compared to Step 1 (no filter), you should expect slightly lower % classified (some marginal contigs drop to “unclassified”) but a similar top species if your assembly is truly *P. aeruginosa*.

>Does the filtered result still point to *Pseudomonas aeruginosa* as the dominant species? If not, which parameters changed the outcome?

---

## 4.5 Optional: Evidence of AMR genes in your genome
Here is an optional data analysis exercise you can try to explore your assembled genome:

**Learning goals**:
1. Find curated antibiotic-resistance (AR) genes to test.
2. Build a local BLAST database from your assembly.
3. Use blastn with sensible thresholds; read and summarise the results.

#
### 4.5.1 Find cadidate AR genes

Pick 3–5 acquired genes relevant to *Pseudomonas* (e.g., β-lactamases, aminoglycoside mods, sulfonamide/tetracycline genes). Get nucleotide FASTA for each gene from a curated source:
- CARD (Comprehensive Antibiotic Resistance Database) — browse and download gene FASTA.
- ResFinder (DTU) — web and downloadable database for acquired genes.
- (Optional) NCBI AMRFinderPlus — curated AMR gene set and tool; good for reference and cross-checking. 

>[!TIP]
>Prefer acquired genes (e.g., *blaVIM*, *blaNDM*, *aadA*, *sul1*, *tetA*), not broad intrinsic systems (big efflux pumps), to keep interpretation simple.

Collect your chosen sequences into one file, e.g. **arg_candidates.fna** (multiple FASTA entries).

#

### 4.5.2 Make your genome searchable

Create a nucleotide BLAST database from your assembled contigs (this is faster and more flexible than using -subject for many queries). Use **makeblastdb** with your **contigs.fasta**; the BLAST+ manual/help page covers this.

:keyboard: 
```bash
makeblastdb -in <path/to/contigs.fasta> -dbtype nucl -parse_seqids -out <genome_db_prefix>
```
- **-dbtype nucl** → nucleotide DB
- **-parse_seqids** keeps your contig IDs intact (handy for locating hits).

>**Sanity Check**
>after running, you should see several index files sharing the <genome_db_prefix>.* names.

#

### 4.5.3 Search your AR genes against your genome

Run **blastn** with thresholds that balance sensitivity and specificity for acquired genes.

:keyboard: **Template** (fill in; not a turnkey command):
```bash
blastn -query <arg_candidates.fna> -db <genome_db_prefix> -out <results.tsv> -outfmt '6 qseqid sseqid pident length qcovs evalue bitscore sstart send' -perc_identity <e.g.,95> -qcov_hsp_perc <e.g.,90> -max_target_seqs 1 -num_threads <N>
```

- **-perc_identity** sets the % identity cutoff.
- **-qcov_hsp_perc** sets query coverage per HSP (how much of the gene aligns). (This maps to BLAST’s qcov_hsp_perc parameter in docs.)

**Interpreting hits** (suggested rules of thumb)

- **Likely present**: identity ≥ **95–98%** and coverage ≥ **90–100%** (single, clean HSP).
- **Maybe**: identity **90–95%** or coverage **70–90%** → check gene family, partial hits, or frameshifts.
- **No**: below thresholds or only very short fragments.

Open the TSV in a spreadsheet. Sort by **pident** and **qcovs**; note the top hit per gene and the **contig ID**/coordinates.

>**Copy/paste warning**:
>options start with ASCII hyphens **-** (not long dashes), and options like **-subject** have no space after the dash.

#

**Stretch ideas (pick one)**

- If a hit is partial, inspect the contig in a genome viewer (**Quast output: ICARUS**) and check for truncations or assembly gaps nearby.
- Try a stricter search (**-perc_identity 98 -qcov_hsp_perc 95**) and see what drops out.
- Compare two databases (e.g., **CARD** vs **ResFinder**) and reconcile differences.

#

**Questions** 

1. Which AR genes you queried (source + accession).
2. Top hit(s) per gene with % identity, % coverage, contig, coordinates.
3. Your call: present/absent/ambiguous, and why (justify with thresholds).
4. One caveat you considered (e.g., gene families, partial matches, plasmid vs chromosome).

---
