# shadowsocks

[![PyPI version](https://camo.githubusercontent.com/456057b5417e5091770cf070cf8297a5d21c2dde872c64fa7a98745eb8e949f8/68747470733a2f2f696d672e736869656c64732e696f2f707970692f762f736861646f77736f636b732e7376673f7374796c653d666c6174)](https://pypi.python.org/pypi/shadowsocks) [![Build Status](https://camo.githubusercontent.com/f7c07e0f90043d2603bad5dc9f7393b274f188e22ed5368db9fdc5154aad530c/68747470733a2f2f696d672e736869656c64732e696f2f7472617669732f736861646f77736f636b732f736861646f77736f636b732f6d61737465722e7376673f7374796c653d666c6174)](https://travis-ci.org/shadowsocks/shadowsocks) 

A fast tunnel proxy that helps you bypass firewalls.

## Server

### Install

Debian / Ubuntu:

```
apt-get install python-pip
pip install shadowsocks
```

CentOS:

```
yum install python-setuptools && easy_install pip
pip install shadowsocks
```

Windows:

See [Install Server on Windows](https://github.com/shadowsocks/shadowsocks/wiki/Install-Shadowsocks-Server-on-Windows)

### Usage

```
ssserver -p 443 -k password -m aes-256-cfb
```

To run in the background:

```
sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start
```

To stop:

```
sudo ssserver -d stop
```

To check the log:

```
sudo less /var/log/shadowsocks.log
```

Check all the options via `-h`. You can also use a [Configuration](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File) file instead.

## Client

- [Windows](https://github.com/shadowsocks/shadowsocks-csharp) / [OS X](https://github.com/shadowsocks/shadowsocks-iOS/wiki/Shadowsocks-for-OSX-Help)
- [Android](https://github.com/shadowsocks/shadowsocks-android) / [iOS](https://github.com/shadowsocks/shadowsocks-iOS/wiki/Help)
- [OpenWRT](https://github.com/shadowsocks/openwrt-shadowsocks)

Use GUI clients on your local PC/phones. Check the README of your client for more information.

## Documentation

You can find all the documentation in the [Wiki](https://github.com/shadowsocks/shadowsocks/wiki).

## License

Copyright 2015 clowwindy

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

## Bugs and Issues

- [Troubleshooting](https://github.com/shadowsocks/shadowsocks/wiki/Troubleshooting)
- [Issue Tracker](https://github.com/shadowsocks/shadowsocks/issues?state=open)
- [Mailing list](https://groups.google.com/group/shadowsocks)