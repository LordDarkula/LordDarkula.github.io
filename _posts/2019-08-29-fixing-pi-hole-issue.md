---
layout: post
title:  "Fixing Pi Hole Dashboard Issue"
date:   2019-08-29
categories: tech
---

## The Problem

I was setting up a network adblocker on my Raspberry Pi using 
[Pi-hole](https://pi-hole.net) when I ran into a strange issue while attampting to load queries on the web dashboard.

![Image unavailable](/img/blog/json-php-error-msg.png)
> An unkown error occured while loading the data. 
> Fatal error
> Uncaught error: Call to unidentified function json_encode() in ``/var/www/admin/api.php:139``

While trying to access the ``Networks`` tab on Pi-hole web dashboard, I got a similar issue, but this time the culprit was sqlite3. PHP is unable to access ``json`` or ``sqlite3``. Here is how I managed to fix the issue.

## Installing the missing extensions

First, install both `php-sqlite3` and `php-json`.
```bash
sudo apt-get upgrade
sudo apt-get install php-sqlite3
sudo apt-get install php-json
```

Restart lighttpd service to activate the changes.
```bash
sudo systemctl restart lighttpd
```

## Adding extensions to PHP configuration

That might fix the issue. If it does not, we will have to add the dependencies to `PHP` configuration files. These files will end in `.ini` and will be located wherever your php installation is. Mine were located in `/etc/php/7.3/mods-available`. Open `sqlite3.ini` and add the following line.
```
extension=sqlite3.so
```

Open `json.ini` and make a similar edit.
```
extension=sqlite3.so
```

Restart lighttpd and the dashboard should start working again.