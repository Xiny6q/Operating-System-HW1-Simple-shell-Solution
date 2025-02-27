Download link :https://programming.engineering/product/operating-system-hw1-simple-shell-solution/

# Operating-System-HW1-Simple-shell-Solution
Operating System HW1 Simple-shell Solution
Outline:

1 Requirement (作業要求)

1.1 run built-in command

1.2 run single process command

1.3 run two-process pipelines

1.4 handle input and output redirection

1.5 execute commands in the background

1.6 run multi-pipelines

Built-in command requirement (1.1 的要求細節) 2.1 help/cd/echo/exit

2.2 record/replay

2.3 mypid

Input format (TA 會怎麼輸入測資)

Grading (評分規則)



5 Precautions/Reference (注意事項/參考連結)

2

1 Requirement

1.0 hello-message and prompt symbol (e.g., >>> $ )

You can customize your hello-message when your shell starts running.

The messages will not affect your score.

You must print prompt symbol.


3

1 Requirement

1.2 run single process command

If user input a line with only “space“ or “\t” characters, you should do nothing, and print another prompt symbol.


5

1 Requirement

1.3 run two-process pipelines


6

1 Requirement

1.4 handle input and output redirection


7

1 Requirement

1.5 execute commands in the background

The parent-process (which runs the shell) should print the pid of the child-process (that runs the command in the background).


8

1 Requirement

1.6 run multi-pipelines

With all the functionalities mentioned before (1.1~1.5), your shell should run the command smoothly.

When run multi-pipelines in the background, the original shell process

should print the process’ pid of the right most command.

(For example, in the screenshot below, you will print the pid of the process that runs “grep” command.)

Alternative: 如果同學的 ‘&’ 是用類似「先 fork 一個 child，再由這個 child 來處理這個 multi-pipe 」的方法，那助教可以接受你原本的 shell process 印出的 pid 是這個 child 的 pid，而不是印出「執行最右邊指令的 process」 的 pid。

原本的規定是目前 bash 的做法，這和 bash 如何處理 multi-pipe 的方法有關，同學也可以嘗試看看要如何做到。


9

2 Built-in command requirement

2.1 help/cd/echo/exit


NAME help – print information to stdout SYNOPSIS help

DESCRIPTION You should at least print how to use the built-in functions.

EXAMPLE

10

2 Built-in command requirement

2.1 help/cd/echo/exit


NAME cd – change the working directory

SYNOPSIS cd [directory]

EXAMPLE

11

2 Built-in command requirement

2.1 help/cd/echo/exit


NAME echo – print a line of text to stdout SYNOPSIS echo [-n] [strings]

DESCRIPTION If “-n” flag is set, “echo” will not output the trailing newline.

EXAMPLE

12

2 Built-in command requirement

2.1 help/cd/echo/exit


NAME exit – terminate your shell

SYNOPSIS exit

DESCRIPTION This command will not run in the backgound.

You may print some goodbye-message before terminate.

EXAMPLE

13

2 Built-in command requirement

2.2 record/replay


NAME record – show the last-16 commands SYNOPSIS record

DESCRIPTION Your shell will always record the last-16 commands that user used in the shell. When user type the “record” command, the shell will print the last-16 commands to stdout, including “record” itself. The biggest number indicate the latest command being used (i.e., “record” itself).

If the command is not a legal command (e.g., “recorf” in p.17), that command will still be recorded. The only exception is the “replay” command, which itself will not be recorded.

See next page for example.

14

2 Built-in command requirement

2.2 record/replay


NAME record – show the last-16 commands EXAMPLE

15

according to the number listed in the “record” command.

If “replay” is used with wrong argument (not a legal number), your shell will output an error message: “replay: wrong args”.

No other command will be executed, and “record” will not update.

IMPORTANT: The “replay” command itself will not be recorded in the shell. Instead, the command which is actually “replayed” is recorded.

If “replay” is used with pipeline, the command being “replayed” will be recorded along with other commands in the pipeline.

For example, if “replay 3” will run “echo 300”, “replay 3 | grep 3” will run “echo 300 | grep 3”, and “echo 300 | grep 3” will be recorded.

See next page for some examples.

User should use the “replay” command with a number.

If the number is in legal range, the shell should re-execute the command

(1 <= number <= 16)

NAME replay – re-execute the command that is listed in record SYNOPSIS replay [number]

DESCRIPTION

2 Built-in command requirement

2.2 record/replay

16

2 Built-in command requirement

2.2 record/replay


NAME replay – re-execute the command listed in record EXAMPLE

17

2 Built-in command requirement

2.3 mypid


NAME mypid – show the related pids about the process

SYNOPSIS mypid [-i|-p|-c] [number] (number indicate a process’ pid) DESCRIPTION Depend on the flag used with the command,

mypid will list the related process’ pid(s).

-i: print process’ pid, which execute “mypid”. (ignore [number])

-p: print process’ parent’s pid (i.e., who has child [number])

-c: print process’ child’s pid (i.e., whose parent is [number])

You must implement this command through parsing information in the /proc directory. (except for implementing the “-i” option).

See next two pages for examples and hints.

18

2 Built-in command requirement

2.3 mypid


NAME mypid – show the related pids about the process EXAMPLE

19

2 Built-in command requirement

3 Input format

Only 4 special operators: |, >, < and & .

No quotation marks( ” or ‘ ), e.g., “string”, ‘string’

All the cmds, args, operators will be separated by space char.

指令(cmd), 引數(arg) , 特殊符號(operators) 都會用 空白符號 隔開

Input/ redirection (<) only show up after first command.

Input redirection 的檔名一定會接在 < 後面，且如果有，一定會緊接在第一個指令後面

Output redirection (>) only show up after last command.

Output redirection 的檔名一定會接在 > 後面，且如果有，一定會緊接在最後一個指令後面

Background-execution operator (&) will only show up at last.

& 如果有，一定會出現在最後面

格式

$

cmd args < infile | cmd args

| cmd args > outfile &

範例1

$

cat < t1.txt > t2.txt

&

範例2

$

record | head –c 32 >

t2.txt

&

範例3

$

cat < t1.txt | head -5 | tail -3 | grep pid > t2.txt &

21


Grading

For each part in the requirement, TA will do some testing in your shell and ask you questions.

助教會針對每一個要求 (1.1~2.3) 做測試，並詢問你問題。

You need to explain to TA how you implement your shell with those requirements.

你必須要能流暢的解釋 你如何實做你的 shell 與如何完成這些功能要求。

If you cannot explain smoothly, you will not get scored.

如果你無法解釋你是怎麼寫出這些功能的，你就不會拿到分數


22

5 Precautions/Reference

Github classroom:

Click here to start your assignment.

Due Date:

2022/11/04 (Fri.) 23:59:59 (以 github 上傳的時間為準)


23

Precautions/Reference

You should implement HW1 with C language.

You will get two files: makefile, my_shell.c from the hw1 github classroom.

Make sure your main() function is written in the file my_shell.c.

You can modify makefile as you want.

E.g., add other files and compile them with your my_shell.c using your modified makefile.

Make sure your makefile can compile your codes and create the executable smoothly .

The executable name should be: my_shell.

Make sure your codes can be compiled and run in the DEMO environment introduced in the hw0 slide.


24

5 Precautions/Reference

System-calls/library-calls that might help:

getline / strtok_r / strsep / strtol

fork / execvp / waitpid / exit

pipe / dup2

open / close / read / write

opendir / readdir / closedir

chdir/ getcwd

Other reference link:

Tutorial – Write a Shell in C

GNU Libc Manual Page – Implementing a Shell

/proc filesystem

GNU Makefile Documentation
