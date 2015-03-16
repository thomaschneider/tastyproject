

# Installation #

## Dependencies ##
  * >=python-2.6.6 or >=python-2.7.1
  * gnuplot-4.4.x with python bindings : 0 <= x <= 2
  * gmpy-1.x : 11 <= x http://code.google.com/p/gmpy/
  * distribute : http://pypi.python.org/pypi/distribute#downloads

## Linux ##
Unpack TASTY tarball:

```
tar xvjf Tasty-Binary-VERSION-py2.X.tar.bz2
```

Change current directory to your copy of TASTY:

```
cd Tasty-Binary-VERSION-py2.X.egg
```

Install into system path:

```
sudo python install.py
```

Uninstallation:

```
cd Tasty-VERSION-py2.X.egg
sudo python install.py -u
```

## MacOSX ##
Unpack TASTY tarball:
```
tar xvjf Tasty-Binary-VERSION-py2.X.tar.bz2
sudo easy_install -Z Tasty-Binary-VERSION-py2.X.egg
```

# Using TASTY #

## Quickstart ##

create default protocol:
```
tasty_init tasty_test
```

start server process:
```
tasty -sv tasty_test
```

start client process:

```
tasty -cv tasty_test
```

## Options ##

TASTY provides the following options which we explain by different use cases.

### Deploy changed protocol from party A to party B ###

The TASTY tool checks if both parties are using the same protocol by comparing hash values and exits with error when both hash values differ. To be able to deploy an updated protocol to party B, we are introducing 2 flags.
Party A (the sender) uses the flag **-f** to force usage of given protocol and send it to party B. Party B uses the flag **-A** to accept the incoming protocol version and overwrites his old protocol version. Only activate this flag, if you are controlling both
parties and keeping in mind that this is a potential security thread.

### Making TASTY more verbose ###

Use the flag **-v**, which can be repeated to increase verbosity.

### Creating a cost analyzation report ###

Use the flag **-a**, and the report will be shown on exit, and writting to a file in the protocol environments' results directory.

### Daemon mode ###

To run a protocol forever use the flag **-F** in conjuntion with client or server mode.

### Network options ###

The flags **-p PORT** and **-H HOST** are controlling to which host and port the party will bind/connect.
Party A (the sender) and Party B (the receiver ) use e.g in an IPv4 network the flag **-H localhost** and **-p 9999** to bind to localhost on port 9999.
Alternatively TASTY supports setting its host and port via the protocol.ini file. You can use common ip address notations like "127.0.0.1", "localhost" or the equivalent IPv6 forms.
Tasty prefers IPv6 addresses and sockets, but also supports IPv4 networks. Command line flags overwrite config.ini values.

### Keeping multiple protocols and drivers in a protocol environment ###

The default method name for protocols is 'protocol'. When providing multiple protocols in one protocol file, the intended one can be chosen with the flag **-P METHOD\_NAME**.

It is also possible to write multiple drivers into one protocol file. The intended driver can be chosen with the flag **-D DRIVER\_NAME**.

To interactively run a protocol without using a driver, the compile-time parameters provided in the 3<sup>rd</sup> formal parameter of the protocol ("params") need to be assigned by setting the special variable params as in the following example::

```python


__params__ = {'foo' : 23, 'bar' : 42}

def protocol(client, server, params):
pass
```

Alternatively, a driver can be set explicitly and the parameters are given as an argument::

```py


driver = YourIODriverClass({'foo' : 23, 'bar' : 42})

def protocol(client, server, params):
pass

```

## Generating nice graphs with TASTY ##

You will need a protocol with a corresponding protocol driver. Start 'tasty' with the **-d** flag, create an analyzation script, and run this script via the tool 'tasty\_post' on the collected costs data in the environments' results directory.
A step by step guide is given in Appendix C of our paper mentioned below.

## Protocol examples and TASTY grammar ##

A step-by-step example is given in Appendix C of [TASTY: Tool for Automating Secure Two-partY computations](http://eprint.iacr.org/2010/365.pdf).

To learn more about using primitives of TASTY, have a look at the protocols provided in the tests subdirectory.

Have fun with TASTY...