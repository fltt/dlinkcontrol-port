FreeBSD port of D-Link Control
==============================
This is a *FreeBSD* port of the [dlinkcontrol][] utility.

Build and install
-----------------
To build and install the package:

```
cd path/to/dlinkcontrol-port/dlinkcontrol
make install
```

You will be asked to enter `root`'s password to gain write access to the
`DISTDIR` and `PORT_DBDIR` directories and to install the built package.

If you want to build the package as a regular user, just redefine the
`DISTDIR` and `PORT_DBDIR` variables, e.g.:

```
cd path/to/dlinkcontrol-port/dlinkcontrol
export DISTDIR="$HOME/ports/distfiles"
export PORT_DBDIR="$HOME/ports/db"
make package
```

> **NOTE:** To install the package you still need `root` privileges.

For more information about the available `make` targets and the *FreeBSD
Port Collection*, see `ports(7)`.


[dlinkcontrol]: https://github.com/fltt/dlinkcontrol
