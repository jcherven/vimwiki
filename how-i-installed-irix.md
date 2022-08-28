# irix 6.5.30 installation over network on an IP30 Octane(2)

- Top
	- [temporary instructions](#temporary instructions)
	- [post installation tasks](#post installation tasks)
		- [configure networking](#configure networking)
		- [configure screen resolution](#configure screen resolution)

## temporary instructions

until i get a moment to type up a good docpage, follow the instructions at [this up to date techpub](http://techpubs.spinlocksolutions.com/irix/remote-irix-6.5-installation-from-linux.html)

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
