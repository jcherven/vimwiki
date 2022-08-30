# irix 6.5.30 installation over network on an IP30 Octane(2)

- Top
	- [temporary instructions](#temporary instructions)
	- [post installation tasks](#post installation tasks)
		- [configure networking](#configure networking)
		- [configure screen resolution](#configure screen resolution)

## temporary instructions

until i get a moment to type up a good docpage, follow the instructions at [this up to date techpub](http://techpubs.spinlocksolutions.com/irix/remote-irix-6.5-installation-from-linux.html). Stop after adding all installation sources to proceed after the section below.
## ensure zero conflicts

after adding installation sources, send `q` to stop adding installation sources and return to the inst prompt.

```
Inst> keep *

Inst> install standard

Inst> keep java2_plugin.sw32.mozilla_freeware

Inst> keep inventor_dev.sw.base

Inst> keep inventor_dev.sw.lib

Inst> install eoe.sw.fonttools

Inst> install eoe.sw.uucp

Inst> install eoe.sw.xlv

Inst> install eoe.sw.spell

Inst> install ftn_eoe

Inst> install inventor_eoe.sw64

Inst> install ifl_eoe.sw64

Inst> install dmedia_eoe.sw64

Inst> prereqs
No matches for "prereqs" were found # <-this is okay

Inst> keep incompleteoverlays

Inst> rem java_dev*

Inst> conflicts
No conflicts

Inst> go
```

after installtion has completed, finish the rest of the above section.

## post installation tasks

### configure networking

best way to get started is to run the guided setup from the login screen. after completing this, login as root to manually configure `/etc/hosts`, `/etc/resolvd.conf`, and setting up the gateway static route.

```
/etc/hosts
...
...
<this host's ip>	<hostname>.<domain>
```

```
/etc/resolv.conf
domain whatever.home.arpa
nameserver <ip address of local dns resolver>
```

i think it's a good idea to also link the resolv.conf file to /usr/etc/resolv.conf.

```
> rm /usr/etc/resolv.conf
> ln -s /etc/resolv.conf /usr/etc/resolv.conf
```

in irix 6.5 setting the static route is simple:

```
/etc/config/static-route.options
...
...
$ROUTE $QUIET add -net default <gateway ip address>
```

finally, disable the routing daemon:

```
> chkconfig routed off
```
### configure screen resolution

as root:

```
> /usr/gfx/setmon -x 1280x1024_60
> (/usr/gfx/stopgfx;/usr/gfx/startgfx)&
```
