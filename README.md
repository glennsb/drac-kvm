Dell DRAC KVM Launcher
=========

Fed up of logging into the DRAC web interface just to launch a KVM session?
This simple Go program should help ease the pain.

```bash
$ drac-kvm --help
Usage of drac-kvm
  -d, --delay=10: Number of seconds to delay for javaws to start up & read jnlp before deleting it
  -h, --host="some.hostname.com": The DRAC host (or IP)
  -j, --javaws="/usr/bin/javaws": The path to javaws binary
  -p, --password=false: Prompt for password (optional, will use 'calvin' if not present)
  -u, --username="root": The DRAC username

# Example using default dell credentials (root/calvin)
$ drac-kvm -h 10.25.1.100
2014/06/26 16:01:11 Detecting iDRAC version...
2014/06/26 16:01:11 Found iDRAC version 7
2014/06/26 16:01:11 Launching DRAC KVM session to 10.25.1.100

# Example using custom credentials
$ drac-kvm -h 10.25.1.100 -u bob -p
Password: **********
2014/06/26 16:01:11 Detecting iRAC version...
2014/06/26 16:01:11 Found iDRAC version 7
2014/06/26 16:01:11 Launching DRAC KVM session to 10.25.1.100
```
This has been tested on the following Dell servers:

 * 11th Generation (eg: Dell R710 / iDRAC6)

 * 12th Generation (eg: Dell R720 / iDRAC7)

It requires that you have java installed on your machine (specifically the `javaws` binary).

Installing (via Go)
----

If you already have Go configured on your system then you can just run the following to quickly install it:
```bash
$ go install github.com/paulmaddox/drac-kvm
```

Installing (pre built binaries)
----

If you don't have Go installed already on your system, then included in this repository are some prebuilt binaries:

* [Linux 64bit](https://github.com/PaulMaddox/drac-kvm/blob/master/binaries/drac.linux_64bit?raw=true)

* [Mac OSX 64bit](https://github.com/PaulMaddox/drac-kvm/blob/master/binaries/drac.osx_64bit?raw=true)

Configuration file
----

You can create a configuration file
```bash
$ cat ~/.drackvmrc
[192.168.0.42]
username = foo
password = bar

[web-1]
host = 10.33.0.1
username = root
password = password4root

[web-2]
host = 10.33.0.2
username = root

# Use IP, username and password from drackvmrc for this ip
$ drac-kvm -h 192.168.0.42
2014/06/26 16:01:11 Detecting iRAC version...
2014/06/26 16:01:11 Found iDRAC version 7
2014/06/26 16:01:11 Launching DRAC KVM session to 192.168.0.42

# Same for host alias web-1
$ drac-kvm -h web-1
2014/06/26 16:01:11 Detecting iRAC version...
2014/06/26 16:01:11 Found iDRAC version 7
2014/06/26 16:01:11 Launching DRAC KVM session to 10.33.0.1

# Specify -p option in order to do not use defaut password
$ drac-kvm -h web-2 -p
Password: **********
2014/06/26 16:01:11 Detecting iRAC version...
2014/06/26 16:01:11 Found iDRAC version 7
2014/06/26 16:01:11 Launching DRAC KVM session to 10.33.0.2
```
Credits
----
@jamesdotcuff's helpful blog post:

http://blog.jcuff.net/2013/10/fun-with-idrac.html
