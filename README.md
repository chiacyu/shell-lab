# shell-lab
The shell is a implementation of lab assignments from [Computer Systems: A Programmer's Perspective](http://csapp.cs.cmu.edu/3e/labs.html). In this lab you would be required to implement an the shell program. By this lab, you would gain much more experiences on process controlling and signaling. The shell program is an terminal based user interface program which allows users to perform their task on the computer.

The command line is a sequence of ASCII text words delimited by whitespace. The first word in the
command line is either the name of a built-in command or the pathname of an executable file. The remaining
words are command-line arguments. If the first word is a built-in command, the shell immediately executes
the command in the current process. Otherwise, the word is assumed to be the pathname of an executable
program. In this case, the shell forks a child process, then loads and runs the program in the context of the
child. The child processes created as a result of interpreting a single command line are known collectively
as a job. In general, a job can consist of multiple child processes connected by Unix pipes.

If the command line ends with an ampersand `”&”`, then the job runs in the background, which means that
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
Use the `-h` argument to find out the usage of `sdriver.pl`:

```
unix> ./sdriver.pl -h
Usage: sdriver.pl [-hv] -t <trace> -s <shellprog> -a <args>
Options:

  -h Print this message
  -v Be more verbose
  -t <trace> Trace file
  -s <shell> Shell program to test
  -a <args> Shell arguments
  -g Generate output for autograder
  
```
We have also provided 16 trace files `trace{01-16}.txt` that you will use in conjunction with the shell
driver to test the correctness of your shell. The lower-numbered trace files do very simple tests, and the
higher-numbered tests do more complicated tests.
You can run the shell driver on your shell using trace file `trace01.txt` (for instance) by typing:

```
unix> ./sdriver.pl -t trace01.txt -s ./tsh -a "-p"
```
(the -a "-p" argument tells your shell not to emit a prompt), or
```
unix> make test01
```
Similarly, to compare your result with the reference shell, you can run the trace driver on the reference shell
by typing:
```
unix> ./sdriver.pl -t trace01.txt -s ./tshref -a "-p"
```
or
```
unix> make rtest01
```

For your reference, `tshref.out` gives the output of the reference solution on all races. This might be
more convenient for you than manually running the shell driver on all trace files.
The neat thing about the trace files is that they generate the same output you would have gotten had you run
your shell interactively (except for an initial comment that identifies the trace). For example:

```
bass> make test15
./sdriver.pl -t trace15.txt -s ./tsh -a "-p"
#
# trace15.txt - Putting it all together
#
tsh> ./bogus
./bogus: Command not found.
tsh> ./myspin 10
Job (9721) terminated by signal 2
tsh> ./myspin 3 &
[1] (9723) ./myspin 3 &
tsh> ./myspin 4 &
[2] (9725) ./myspin 4 &
tsh> jobs
[1] (9723) Running ./myspin 3 &
[2] (9725) Running ./myspin 4 &
tsh> fg %1
Job [1] (9723) stopped by signal 20
tsh> jobs
[1] (9723) Stopped ./myspin 3 &
[2] (9725) Running ./myspin 4 &
tsh> bg %3
%3: No such job
tsh> bg %1
[1] (9723) ./myspin 3 &
tsh> jobs
[1] (9723) Running ./myspin 3 &
[2] (9725) Running ./myspin 4 &
tsh> fg %1
tsh> quit
bass>
```
