date: Apr 14  2009

title:Bash info, scripting examples, regex parameter substitution, interactive shell, and more

keywords:bash,shell,commmand,parameter,file,name,path,regular,expression,glob,login,mingetty,tty,console,terminal,screen,prompt,sudo,stdout,permission,permissions

description:Shell trivia and scripting examples including file name and path substitutions, as well as how to detect a live human logging in, and how to fix the session title and titlebar.


Table of contents
-----------------
- Introduction
- Link to list of hints
- Disabling xon xoff and detecting interactive login
- Regular expressions and globbing
- Checking return status (return value) of programs
- Can't write a file
- Fixing the session title
- Using dd and gmime-uuencode to create passwords
- A little rant about examples



Introduction
------------

Shell programming and expecially shell variables are weird things. The
rules are bizarre to those of use schooled in normal programming
languages such as C, Perl, or Java. I'm not a shell programmer, but
after much painful, irritating, frustrating trial and error, (and
hours of Google searches) I've managed to glean a few really useful
facts. This document assumes that you are facile with the Linux shell
bash, and that you are comfortable with shell commands and with
viewing files, and comfortable viewing (and searching) man pages.

By the way, it appears that the man page for bash is missing most of
the available content. Heaven only knows why. For instance the man
page says "Expressions are composed of the primaries described above
under CONDITIONAL EXPRESSIONS." There is no heading "CONDITIONAL
EXPRESSIONS" in the man page.

I couldn't find the list of CONDITIONAL EXPRESSIONS via the "info
bash" command either. However, hope is not lost. Fedora (and probably
most distros of Linux) have full docs on the hard drive. Mine are at:

`file:///usr/share/doc/bash-3.1/bash.html`

Simply use your web browser to read the docs off your hard drive. For
Fedora these docs are mostly in HTML format. They also appear to be
complete.

You can always search Google, and many web sites will have the full
docs.

If you are frustrated with the shell, I feel your pain. Except for the
most trivial operations, I use Perl for all sysadmin scripting
tasks. (I don't want to start a religious war here: if you like shell
programming I'm happy for you. However, most of us will be more
productive in Perl.) Perl makes sense and has many examples and
encyclopedic documentation. For those times where Perl does't make
sense (which I will readily admit occur on a regular basis), check
Google or "man perltoc" for the Perl docs table of contents.

For examples of shell scripts, check out the scripts in /etc/init.d. 




Link to list of hints
---------------------

This information is implied by the bash man page (which is lacking
examples). There are also home nice hints at:

http://linuxgazette.net/issue18/bash.html




Disabling xon xoff and detecting interactive login
--------------------------------------------------

As of KDE4 (2008 and 2009) the terminal application konsole is
broken. It no longer accepts -ls. See my work around below.

Reading between the lines, the -ls may have been added by one of the
konsole developers, and then removed by another developer (who I
presume did not understand the implications).

http://www.linuxquestions.org/questions/slackware-14/kde-konsole-gone-after-installing-kde4-608652/

The work around is simple enough, and I hope you haven't wasted an
hour looking for the solution.

1) Run konsole

2) Settings menu -> Edit Current Profile... -> General tab -> Command:

3) Change to /bin/bash --login

This changes a KDE config file Shell (probably some where such as
/home/mst3k/.kde/share/apps/konsole/Shell.profile) that konsole uses
at startup. By invoking bash as --login, shopt login_shell will be
"on".

Now your .bashrc or whatever will be able to distinguish when a human
is logged in, and when a script is running. The reason for this would
be to disable xon/xoff flow control for the human.

From the bash prompt, "konsole -e /bin/bash --login" seems to work,
but gives an interesting KDE error:

[zeus ~]$ konsole -e /bin/bash --login
konsole(659): Attempt to use QAction "change-profile" with KXMLGUIFactory!
[zeus ~]$ Undecodable sequence: \001b(hex)[?1034h

Also "/bin/bash -i" does *not* create an interactive session. I'm
guessing this is due to shopt login_shell being somehow inherited by
child processes.

Note: This information has subtle inaccuracies in the distinction
between "interactive shells" and "login shells". I hope to clarify
this soon. The Bash documentation says there is a difference, but does
not get around to giving the reason(s) for the distinction.


This example shows the solution two problems: how to disable the very
irritating software flow control xon and xoff mapped to keys control-x
(C-x) and control-s (C-s). I'm an emacs user, and in emacs I use those
keys constantly. Bash is set up for emacs command line editing, so all
my emacs reactions get used on the command line too, but co-mingling
emacs with the semi-emacs keystroke support in bash can lead to
issues. The big one was accidentally stopping i/o by hitting the xoff
key. This key hasn't been needed since they days of dedicated CRT
terminals (without scroll back buffers). Heaven only knows why it is
still the bash default. I don't even use flow control on a runlevel 3
non-graphical console session.

Using shopt -q login_shell seems to be the modern and reliable way to
detect interactive shell sessions. When the session is interactive,
disable start and stop which are xon and xoff. 

******
Note: -ls only applies to older versions of konsole. See above.
******

There is a potential problem with this. The default state of terminal
(console) applications such as KDE's konsole is *not* as a login
shell. This seems like a bug. To cure this obscure issue launch
Konsole as:

konsole -ls

Change how Konsole is run in you start menu. Right click your start
button (Fedora button, KDE button, whatever you call it). Select "Menu
Editor". Click on one or more of the Terminal (konsole) entries, and
add " -ls" at the end of the "Command".


******
Note: -ls only applies to older versions of konsole. See above.
******

You can see the output of shopt in human readable form by leaving off
the -q option (-q for quiet):

shopt login_shell

or 

shopt

# The newer (?) method of detecting an interactive shell.
# This works with Fedora Core 6, and probably most modern versions of
# Linux. Disable xon xoff, and alias rm to rm -i
if shopt -q login_shell ; then
      stty stop undef
      stty start undef
     alias rm='rm -i'
fi


Below is another technique for testing to see if a login is an
interactive session. For reasons not quite clear, Apple's OSX has a 
problem setting and resetting the session name. It works under Linux,
but not with OSX, and I can't figure out why Linux works
seamlessly. In any case, I created a weak workaround for OSX.

The character strings being echoed are "escape sequences" for the
terminal program. This seems to be more or less the same between
xterm, "linux" (a terrible name for a tty since this is also the true
and real name of the operating system/kernel(?)), vt100, and mabe even
"ansi" (another terrible name for a tty).

# This works for OSX and should be fine for Linux too.
# if [ ! -z "$(echo $- | grep i)" ]

# Similar to the line above, but tests for 1 match instead of a
# non-zero length return string. The shell variable $- contains the
# values of the "set" command (which is different in Bash than in
# csh(?) or some other shells). Do this:

echo $-

The result in my shell is "himBH". The "i" undocumented, but means
that the shell is "interactive". The bash man page describes the other
options under the "set" section (try searching the man page for set
with multiple spaces in front "    set " or better yet forget man and
use browse the docs with Firefox from /usr/share/doc/ )

Bash's "if" command with [ ] checks the boolean result. The shopt
method is checking the command return value. Therefore using "echo"
piped to "grep" you must check against equivalence to 1.

I don't know why the command has to be surrounded by double quotes,
parentheses, and preceded by $. 

if [ "$(echo $- | grep -c i)" == 1 ]
then
    stty stop undef
    stty start undef
    alias rm='rm -i'

    # Don't echo except for a tty. Non-ttys (like scp) will break if
    # you echo text to them.
    # hostname -s
    # id -nu
    # echo -e -n  is bash specific (as opposed to a feature of /bin/echo)
    # http://www.mit.edu/afs/sipb/project/outland/doc/rxvt/html/refer.html#XTerm
    # 0 window title and icon name(?)
    # 1 icon name
    # 2 window title
    # 30 type-of(?), usually Shell
    #echo -ne "\033]1;one\007"
    #echo -ne "\033]2;two\007"
    echo -ne "\033]0;`id -nu`@`hostname -s`\007"
fi


# The following older code worked for a while, or at least in some cases.
# This checks to see if the session has a prompt string of non-zero
# length.
# http://www.faqs.org/docs/bashman/bashref_68.html
# Perhaps it stopped working when I made a small modification to my prompt.
# In any case, it is less robust than the method above.
# For interactive shells disable xon and xoff, and alias rm to rm -i
# Use the a modern test.

if [ ! -z "$PS1" ]
then
    stty stop undef
    stty start undef
    alias rm='rm -i'
fi

This older method didn't work when scp'ing into the machine.
I got the following result when using scp into the machine:

[mst3k@zeus ~]$ scp tmp.txt hera.example.com:
stty: standard input: Invalid argument
stty: standard input: Invalid argument
tmp.txt                                                       100% 1919     1.9KB/s   00:00
[mst3k@zeus ~]$ scp x_next.txt hera.example.com:







Regular expressions and globbing
--------------------------------

Globbing is use of * as a wildcard to glob file name list
together. Use of wildcards is not a regular expression.

These following examples should also work inside bash scripts. These may or may
not be compatible with sh. These are "interesting" regex or globbing
examples. I say "interesting" because they don't seem to follow the
path of "true" regular expressions used by Perl.

[mst3k@zeus ~]$ echo ${HOME/\/home\//}
mst3k
[mst3k@zeus ~]$ echo ${HOME##home}
/home/mst3k
[mst3k@zeus ~]$ echo ${HOME##/home}
/mst3k
[mst3k@zeus ~]$ echo ${HOME##/home/}
mst3k
[mst3k@zeus ~]$ echo ${HOME##*}

[mst3k@zeus ~]$ echo ${HOME##*/}
mst3k
[mst3k@zeus ~]$




Checking return status (return value) of programs
-------------------------------------------------

Linux and unix-like systems are not inclined to tell you the return
status of commands you run at the shell prompt. Use this little one
line shell if statement to check true/false return values.

[zeus ~]$ if  shopt -q login_shell; then echo "yes"; fi;
yes
[zeus ~]$ if !  shopt -q login_shell; then echo "yes"; fi;
[zeus ~]$   


Here is a better example, and includes a Perl script with different
exit values.

Create a Perl script try.pl just like my try.pl that I've cat'ed
below. Here is a session transcript that should be clear. Yes, the
Perl script is 6 lines. Yes, I strongly prefer my curly braces on
separate lines.

[zeus ~]$ cat try.pl
#!/usr/bin/perl
if ($ARGV[0])
{
    exit(0);
}
exit(1);
[zeus ~]$ if ./try.pl stuff ; then echo "yes"; else echo "no"; fi;
yes
[zeus ~]$ if ./try.pl ; then echo "yes"; else echo "no"; fi;
no
[zeus ~]$



Can't write a file
------------------

There are cases (especially with Apache and CGI scripts) where you (at
the shell command line) or one or your scripts is unable to write to a
file due to permissions. This will be true even when you sudo the
writing command. The short answer is: the shell permissions control
file writing, not the permissions of the command. We will use an
example of a user www (think: apache) trying to write to a file owned
by mst3k. In reality mst3k wrote the script but due to various
configuration issues, the CGI scripts are running as www.

Here is the solution (more explanation below). Add a tee command to
your sudoers file:

www  ALL=(ALL) NOPASSWD:  /usr/bin/tee

Or perhaps the more secure version:

www  ALL=(ALL) NOPASSWD:  /usr/bin/tee -a /var/log/text.txt

Use this command in your script:

/bin/echo "i like pie" | sudo /usr/bin/tee -a /var/log/test.txt >/dev/null


For instance you have a CGI script written in Perl, and www is in
sudoers for /bin/echo and the following does *not* work. I'll use a
Perl script, but it is probably true even at the bash prompt. Note:
adding /bin/echo to your sudoers doesn't solve the problem. You might
solve the problem by using another shell and su'ing or sudo'ing the
new shell.


#!/usr/bin/perl
`/bin/echo "i like pie" | sudo /usr/bin/tee -a /var/log/test.txt > /dev/null`;
my $id = `/usr/bin/id`;
print "Content-type: text/html\n\n<html><body>Script runs as:<br>$id</body></html>\n";
exit(0);



Keep in mind when trying to diagnose this problem that your script has
to run. The debugging processs has steps such as:

1) Does the command work at the bash command line for the owner of the
   directory/file?

2) Does the command work at the bash command line for non-owners in sudoers?

3) Did the CGI script run? CGI scripts can silently fail. There won't
   be any http output, but you'll get no errors in your web browser
   (unless you've got CGI::Carp enabled). There will be messages in
   the Apache logs. Apache won't run scripts with group-write or
   other-write privs, directories with group-write or other-write
   privs, or that aren't owned by the directory owner
   (/home/mst3k/public_html has to be owned by mst3k) and won't run
   scripts that have no AddHandler or if ExecCGI is not enabled. There
   are details about this elsewhere in these readme and mini howto
   documents, but your .htaccess should include:

Options +ExecCGI
AddHandler cgi-script .pl


Fixing the session title
------------------------

Most xterm software will put a session title in the window
titlebar. The bash shell has an environment variable PROMPT_COMMAND
that is run every time the prompt is printed. This env var is missing
on Apple Mac OSX, but you can easily add it to your .bashrc on any
system.

Briefly, the format is:

export PROMPT_COMMAND='echo -ne "\033]0;title; echo -ne "\007"'

Usually, we want this to be the userid, hostname, and current directory (pwd
is "print working directory").

export PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME%%.*}:${PWD/#$HOME/~}"; echo -ne "\007"'

Put the line above into your .bashrc file. You can test this two ways:

1) "source" .bashrc by typing ". .bashrc"
2) enter the export command at the bash prompt

This is how the prompt changes correctly when you log off a host. This
might also be called fixing the prompt, fixing the titlebar, title
bar, session name, xterm session name, konsole session name, change
session name, change title bar, change session when logging off,
logoff session change, terminal session name change, titlebar tweaks,
escape sequence to change titlebar, vt100 sequence, vt102 sequences. 

Related information is:shell variables, environment variables, env,
set, bash, .bashrc, bashrc, .bash_profile.

Not related to this (at least not directly related) is
.bash_logout. There is no magic at logout that "resets" the prompt or
title bar. Each shell knows what its prompt and title bar should be,
and the prompt and titlebar commands are run every time bash prints
the prompt. However you *must* have the shell variable PROMPT_COMMAND
set and this is one of many fundamental features that OSX fails to set.

Note that the env command doesn't show PROMPT_COMMAND. This is because
PROMPT_COMMAND is a variable. You can only see PROMPT_COMMAND's value
with the "set" command or with "echo $PROMPT_COMMAND". 

In fact, if you really want to know all about your environment (in the
general sense of the word) you need two commands, and I like to have
the env vars sorted (set automatically sorts):

env | sort
set

When I export PROMPT_COMMAND is it both an env var and a set var. I'm
missing the distinction between the two kinds of variables. 



Using dd and gmime-uuencode to create passwords
-----------------------------------------------

Use /dev/urandom instead of /dev/random. Urandom gives better data and
works better with dd.

if=file  is read from file instead of rading from stdin

ibs=n  is read n bytes at a time

count=n   is copy n input blocks

Getting the random input is easy, however, it is binary. We need to
convert to normal printing characters to produce a random string
useful as a password. Encoding as uuencode or base64 handles this
problem. 

dd if=/dev/urandom ibs=6 count=1 | base64

dd if=/dev/urandom ibs=6 count=1 | gmime-uuencode -m -




A little rant about examples
----------------------------

Authors of documentation, need to include a large number of examples.
If you love your operating system then please include examples. The
operating system with the most documentation examples will win the
war.




