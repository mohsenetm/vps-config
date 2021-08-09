

ابتدا تنظیمات دی ان اس انجام می شود در گام اول نرم افزار bind9 که برای دی ان اس است نصب می شود.

```
apt update
```

```
apt install bind9
```

تنظیمات زیر را در فایل domainName.db ذخیری می کنیم

```nginx
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     ns1.learnvps.ir.  root.ns1.learnvps.ir. (
                        6
                        604800
                        86400
                        2419200
                        604800 )
;
;
;@      IN      NS      localhost.
;@      IN      A       127.0.0.1
;@      IN      AAAA    ::1

;Name Server Information

@        IN      NS      ns1.learnvps.ir.

;IP address of Name Server

ns1     IN      A       138.201.101.50

;Mail Exchanger

learnvps.ir.   IN     MX   10   mail.learnvps.ir.

;A – Record HostName To Ip Address

www     IN       A      138.201.101.50
mail    IN       A      138.201.101.50

;CNAME record

ftp     IN      CNAME   www.learnvps.ir.
```

سپس این فایل را در named.conf به صورت زیر فراخوانی می کنیم

```
// This is the primary configuration file for the BIND DNS server named.
//
// Please read /usr/share/doc/bind9/README.Debian.gz for information on the 
// structure of BIND configuration files in Debian, *BEFORE* you customize 
// this configuration file.
//
// If you are just adding zones, please do that in /etc/bind/named.conf.local

include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
zone "learnvps.ir" { type master; file "/etc/bind/learnvps.ir.db"; };
```

