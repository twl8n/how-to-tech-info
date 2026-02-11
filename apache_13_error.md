date: Apr  9  2005

title:Apache Explanation of (13)Permission denied: cannot read directory for multi:

keywords:apache,httpd,permissions,multiview,multi,view,error,apache 2,apache2

description:When permissions are NOT the problem, a common cause of the 13 error explained.

The error:

`(13)Permission denied: cannot read directory for multi: /home/mst3k/public_html/`

is caused my having the MultiViews enabled when public_html
permissions are 711.

Normally for security reasons your home directory and web accessible
directories will be permissions 711 (rwx--x--x). Execute on a directory
means that if you know a filename in that directory, you can read
it. However, you cannot get a listing of the directory. The x
(execute) permissions for directories have this special meaning. This
meaning is different from the meaning of x for files (where it means
the file is executable).

In order to get a listing of a directory, the permissions must be set
to r (read). For security reasons you *do not* want web accessible
directories to have read permissions. In other words, if someone
doesn't know the file they want, then they can't have a
listing. Listings of web accessible directories are a (minor) security
hazard. As a webmaster you *only* want people getting to web pages
that you have explicitly linked to.

However, the Apache MultiViews option makes a listing, and therefore
it needs r (read) permissions. MultiViews is only useful if you are
lazy and have web content but you do not want to create a home page.

I run scripts out of my public_html, and I've got some other stuff
going on. This is my Options line from my .htaccess file (the same
line works just as well in a <Directory> directive in your httpd.conf
file). 

`Options +ExecCGI +FollowSymLinks -Indexes -MultiViews`

Given the example case where you serve web pages from a public_html
directory in the user's home directory, here are the following
ownership and permissions for a mythical user "mst3k" on a machine
named "example".

```
[mst3k@example mst3k]$ ls -ld /home /home/mst3k
/home/mst3k/public_html
drwx--x--x  111 root     root           4096 Mar 11 18:56 /home
drwx--x--x   24 mst3k    mst3k          4096 Apr  9 10:19 /home/mst3k
drwx--x--x   32 mst3k    mst3k          8192 Apr  9 11:05 /home/mst3k/public_html
[mst3k@example mst3k]$
```

1) root owns /home and users are not allowed to get a listing of
   /home. This prevents users from listing all the home directories.
   This is a security feature. (see footnote A)

2) User home directory contentes cannot be listed. Known files and/or
   directories in the home directory can be read. This is required to
   allow access to public_html.  However, other users can guess file
   names in your home directory, which is a small security flaw. Any
   critical information should be in a subdirectory in your home
   directory, and that subdirectory should have permissions 700
   (rwx------).

3) The public_html also cannot be listed. However, like the home
   directory, known files in public_html are readable. Web pages have
   known file names (that's what is in a URL). 



Footnote A. On all the unix systems I know, anyone can read
/etc/passwd and see all the user ids. However, not all user ids have
home directories. Any time you hide information, you raise the level
of security.

