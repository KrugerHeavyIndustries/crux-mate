# Ports collection for MATE Desktop Environment on CRUX Linux #

## Current release is CRUX 3.1 with MATE 1.8 (as of 3 Sept 2014) ##

An introduction to the world of [CRUX Linux](http://crux.nu/)

## Credits ##

[Kruger Heavy Industries](http://www.krugerheavyindustries.com) initiated and maintains the port of the MATE desktop environment for CRUX Linux with the help of [Matt Housh aka Jaeger](http://jaeger.morpheus.net).

## Quickstart ##

The CRUX MATE svn repository is also a ports collection. You can enable it like so:

On your CRUX Linux target installation create the file /etc/ports/mate.httpup

Quickly like this

```
curl http://crux-mate.googlecode.com/svn/trunk/mate.httpup -o /etc/ports/mate.httpup
```

Enable the contrib ports collection sync in /etc/ports

```
mv contrib.rsync.inactive contrib.rsync
```

Edit the file /etc/prt-get.conf and enable the contrib collection (it is needed for some dependencies). Then in /etc/prt-get.conf put

```
prtdir /usr/ports/mate 
```

**before** any of the other prtdir configurations. This makes sure packages from the MATE collection are preferenced correctly over packages with the same name from other collections.

Then issue

```
ports -u
```

at the command line to get the ports collection (and any updates to other port collections)

It is a good idea to update the system before you install MATE.

```
prt-get sysup 
```

This will find out of date packages, preferencing versions in the MATE collection, installing new dependencies, then updating the packages themselves.

Then you can install mate by issuing the following command. This will preference packages in the MATE port collection over packages in other collections. This will ensure they all work nicely together.

```
prt-get depinst mate --install-scripts
```

When this completes (it will take some time - assuming there are no problems or conflicts)

Enable dbus daemon at startup in your /etc/rc.conf file (example below)

```
SERVICES=(dbus net crond) 
```

If using startx configure your .xinitrc with

```
xscreensaver -nosplash &
exec /usr/bin/start-mate
```

Then issue '**startx**' at the command line. Assuming kernel compile options are correct you should find yourself with a working MATE desktop (basic).

If it doesn't work like this. Please [report your issues](https://code.google.com/p/crux-mate/issues/list). We'd love it to be this simple.