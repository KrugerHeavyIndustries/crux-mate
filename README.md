# Ports collection for [MATE Desktop Environment](http://www.mate-desktop.org/) on [CRUX](https://crux.nu/) Linux #

## The current release is MATE 1.8 for CRUX 3.1 (as of 3 Sept 2014) ##

## Credits ##

[Kruger Heavy Industries](http://www.krugerheavyindustries.com) initiated and maintains the port of the MATE desktop environment for CRUX Linux with the help of Matt Housh.

## Quickstart ##

The CRUX MATE git repository is also a ports collection. You can enable it like so:

On your CRUX Linux target installation download the file /etc/ports/mate.httpup:


```
curl https://raw.githubusercontent.com/KrugerHeavyIndustries/crux-mate/master/mate.httpup -o /etc/ports/mate.httpup
```

Enable the contrib ports collection sync in /etc/ports if it's not already enabled:

```
mv contrib.rsync.inactive contrib.rsync
```

Edit the file /etc/prt-get.conf and enable the contrib collection (it is needed for some dependencies). Then in /etc/prt-get.conf put

```
prtdir /usr/ports/mate 
```

**before** any of the other prtdir configurations. This makes sure packages from the MATE collection are preferred correctly over packages with the same name from other collections.

Then issue

```
ports -u
```

at the command line to get the ports collection (and any updates to other port collections)

It is a good idea to update the system before you install MATE.

```
prt-get sysup 
```

This will find out of date packages, preferring versions in the MATE collection, installing new dependencies, then updating the packages themselves.

Then you can install mate by issuing the following command. This will prefer packages in the MATE port collection over packages in other collections. This will ensure they all work nicely together.

```
prt-get depinst mate --install-scripts
```

When this completes (it will take some time - assuming there are no problems or conflicts), enable the dbus daemon at startup in your /etc/rc.conf file (example below)

```
SERVICES=(dbus net crond) 
```

If using startx configure your .xinitrc with

```
exec /usr/bin/start-mate
```

Then issue '**startx**' at the command line. Assuming kernel compile options are correct you should find yourself with a working MATE desktop (basic).

If it doesn't work like this. Please [report your issues](https://code.google.com/p/crux-mate/issues/list). We'd love it to be this simple.
