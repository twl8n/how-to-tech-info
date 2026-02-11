date: Apr 13  2007

title:Apache logging and  favicon.ico

keywords:favicon,error,404,missing,logs,logging

description:Workarounds and suggestions for not logging requests for favicon.ico.

The simplest way to deal with favicon.ico is probably to put a zero
length copy of this file in your document root (or the document root
for each vitually hosted site).

`cat /dev/null > favicon.ico`

This prevents the file from showing up in the error log (since the
file does exist). Now the file might show up in the access log (it
shows up on one of my servers, not not on another; I haven't tracked
down the difference). Perhaps the way to keep it from showing up in
the access log (www.log) is the following CustomLog directive (I'm not
sure what this does, and I don't currently have one of these on my
servers):

```
# Don't bother looking for favicon.ico
#Redirect 404 /favicon.ico

# If you are using CustomLogs, setting an env variable
# allows selective logging. This does not work with TransferLog
SetEnvIf Request_URI "^/favicon\.ico$" dontlog

# Don't bother sending the custom error page for favicon.ico
<Location /favicon.ico>
#    Order Deny,Allow
#    Deny from all
    ErrorDocument 404 "No favicon
</Location>

<VirtualHost example.com >
  CustomLog             /home/mst3k/logs/www.log common env=!dontlog
  # TransferLog           /home/mst3k/logs/www.log
</VirtualHost>
```
