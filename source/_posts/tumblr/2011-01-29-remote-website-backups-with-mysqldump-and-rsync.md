---
layout: post
title: Remote website Backups with mysqldump and rsync
categories:
- web development
- backup
- system administration
---
Today I went through the process of creating a very simple automated backup
solution for my linux web server using mysqldump and rysnc. I thought id share
as its rreeaallllyy eeaassyy to do and you should always be backing up your info.
The machine im backing up hosts my live websites, database server (mysql) and
git repositories. I also have a linux machine at home that can be accessed over
ssh which will be receiving the backups. The rsync setup process will differ if
youre using a local machine.
The first thing to do is to setup mysqldump to output the contents of the
database. This can be fairly system intensive for large databases, but mine is
quite small so its ok to run and finishes fairly quickly.
The mysqldump tool should be included in your mysql installation, there are
similar tools for other DBMSs too. By default mysqldump outputs to the STDOUT,
so we can redirect the output to a file of our choice, heres how:
mysqldump -AR -u [username] -p[password] > [location]
Just fill in your database username, password and the output location you want
and run it on the terminal, aanndd yyeess tthheerree sshhoouulldd nnoott bbee aa ssppaaccee bbeettwweeeenn --pp aanndd
yyoouurr ppaasssswwoorrdd. You should have a sql file with all of your database data.
The dump can be setup as a cron task, ive set mine up to run every day at
midnight. Simply run ccrroonnttaabb --ee to modify your cron configuration and put in
the following line.
0 0 * * * mysqldump --all-databases -u [username] -p[password] > [location]
We can now go ahead and setup rsync to backup our information. Rsync was
already installed on my system but if you dont have it already you can grab it
using apt or any other package manage, heres how in apt.
sudo apt-get install rsync
Once installed we need to setup our backups. Rsync can be setup using
configuration files that can be altered to suit your needs. Just for
convenience ive just run rsync directly rather than using configuration files.
Heres how.
rsync -e ssh -p 50001 -azvP /var/backups/mysql/ [username]@[hostname]:[path]
OK, so theres a bit much there, heres what each part does. Were calling the
rsync command, my machine that will be getting the backups is available through
ssh on port 50001, so the -e command sets up rsync to use ssh on port 50001.
The -a flag sets archive mode which will recursively look through directories
and preserve symlinks/times/groups and owners of files, -v gives us a verbose
output with more info and -P gives us a nice little progress bar.
You can just copy the example code and fill in the username, hostname and path
with your own receiving servers details and then run the command on the command
line.
Once its all working we can put it into cron and specify that it gets run once
daily. We can set it up to run at 10 minutes past midnight, this should give
our mysql dump a chance to finish before we back it up. For the cron task we
wont need a verbose output or a progress bar so were only using -az and not -
azvP. The P flag does allow for partial transfers which we still want, so ive
added partial to the cron.
10 0 * * * rsync -e ssh -p 50001 -az --partial /var/backups/mysql/ [username]@
[hostname]:[path]
Thats it. Were all done!
