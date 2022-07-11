# shell-lab
The shell is a implementation of lab assignments from [Computer Systems: A Programmer's Perspective](http://csapp.cs.cmu.edu/3e/labs.html). In this lab you would be required to implement an the shell program. By this lab, you would gain much more experiences on process controlling and signaling. The shell program is an terminal based user interface program which allows users to perform their task on the computer.

The command line is a sequence of ASCII text words delimited by whitespace. The first word in the
command line is either the name of a built-in command or the pathname of an executable file. The remaining
words are command-line arguments. If the first word is a built-in command, the shell immediately executes
the command in the current process. Otherwise, the word is assumed to be the pathname of an executable
program. In this case, the shell forks a child process, then loads and runs the program in the context of the
child. The child processes created as a result of interpreting a single command line are known collectively
as a job. In general, a job can consist of multiple child processes connected by Unix pipes.

If the command line ends with an ampersand ”&”, then the job runs in the background, which means that
the shell does not wait for the job to terminate before printing the prompt and awaiting the next command
line. Otherwise, the job runs in the foreground, which means that the shell waits for the job to terminate
before awaiting the next command line. Thus, at any point in time, at most one job can be running in the
foreground. However, an arbitrary number of jobs can run in the background.
For example, typing the command line

```

```

# Usage

We have provided some tools to help you check your work.
Reference solution. The Linux executable tshref is the reference solution for the shell. Run this program
to resolve any questions you have about how your shell should behave. Your shell should emit output that is
identical to the reference solution (except for PIDs, of course, which change from run to run).
Shell driver. The sdriver.pl program executes a shell as a child process, sends it commands and signals
as directed by a trace file, and captures and displays the output from the shell.
Use the -h argument to find out the usage of sdriver.pl:
