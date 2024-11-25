# DTC-Bioinformatic-Course
# Part 1: Introduction to command line
Just like Windows, iOS, and Mac OS, Linux is an operating system (OS). It is in fact, one of the most popular platforms used, particularly in bioinformatics. Linux has a number of different versions to suit any type of user. These versions are called distributions (or, ?distros?) and nearly every distribution of Linux can be downloaded for free, burned onto disk (or USB thumb drive), and installed (on as many machines as you like). We are using UBUNTU, which is a popular Linux distribution. Most bioinformatics tools run on Linux operating systems and/or on Mac OS since this is also a Unix-like operating system. Interacting with and running programs on Unix-like operating systems usually means using the Unix ?command line? user interface, or ?terminal?.
Using the terminal means interacting with the computer by typing commands, rather than pointing and clicking. A familiarity with the use of the command line can be very helpful. Most bioinformatics programs run on the Unix command line and follow similar logic and rules, so they can easily be combined together. In this first practical you will learn some of the most commonly used commands, and how to produce a bash script. A bash script is a series of commands written in a file. These are read and executed by the bash program. The program executes line by line. This saves you time because you do not have to write certain commands again and again (so is a very handy bioinformatics tool to know!).
## 1.1 Find and launch your terminal
The terminal can be accessed in different ways on different versions of Linux, but there should be either a menu entry or icon for ?console? or ?terminal?. We will be using Ubuntu and a terminal can be opened by clicking on activities at the top left of the screen, then typing the first few letters of either ?terminal?, ?command?, ?prompt?, or ?shell? in the ?Type to search? box. If you want a faster way of bringing up a terminal, you can use the shortcut keys: Ctrl+Alt+T.
Open the terminal and you should see a large mostly empty box area, with a space to type at the top.
## 1.2 Creating directories (i.e. folders)
First, let's work out where we are. As said above, the terminal is just another way of interacting with your computer (so like how you can use your mouse and clicking to navigate through your folders.... you can use your terminal to do the same thing).
Click the mouse into the window and type the following command (all in lowercase) then press the Enter key to run it:
```bash
pwd
```
***Explanation:*** pwd is an abbreviation of 'print working directory'. All it does is print out the shell?s current working directory. You should see a directory path printed out, something like '/home/YOUR_USERNAME'.

Now let's create a new directory (i.e. folder) to work in. Type the following command then press the Enter key to run it: 
```bash
/home/bea
```
Now let's create a new directory (i.e. folder) to work in. Type the following command then press the Enter key to run it: 
```bash
mkdir intro
```
This should create a new directory (mkdir - '**mk** (make) **dir** (directory)') within the directory you are currently in called 'intro'. Now let?s check it is there. We can list everything contained within our current directory using the ls (list).
```bash
ls
```
You should see your terminal return the name of the directory you just made (intro).
```bash
intro
```
