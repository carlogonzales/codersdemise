# Use Raspberry PI 4 model B as Local Network Private DNS server on Ubuntu

Tested on the following Ubuntu Version
- Ubuntu 19.10 (eoan)

There's not much configuration change when configuring Bind 9 on an ARM architecture over an x86 or x64 this steps can be interchangeable except for different Linux distro which places default configuration files on a different folder (e.g CentOS uses `/etc/named` while Ubuntu uses `/etc/bind`) or some preset configurations has already been set and default config locations.

## Step 1
Install Bind 9 DNS Server, Bind 9 Utilities and Bind 9 Docs

    sudo apt install bind9 bind9utils dnsutils bind9-doc

## Step 2
Make sure Bind 9 uses only IPv4, add `named` arguments for IPv4:

    sudo vi /etc/default/bind9

Then add `-4` on `OPTIONS`

    # run resolvconf?
    RESOLVCONF=no
    
    # startup options for the server
    OPTIONS="-4 -u bind"


## Step 3
After installation we're gonna remove some preset. First, open `/etc/bind/named.conf.options`

    sudo vi /etc/bind/named.conf.options
    
Then remove the following line:

    listen-on-v6 { any; };

Then add the following inside `options { ... };`

    // Allow dns query on localhost and all host within the subnet
    allow-query     { localhost;192.168.1.0/24; };
    // Listen on port 53 with any IP or host (This is the default). 
    // In case you're using DHCP for your IP 
    // or there are not any statically assigned IP for you NS. 
    // You can also use your subnet's CIDR.
    listen-on port 53 {any;}

## Step 4
Now, we're gonna add Zone configuration and configure each zone files.

    sudo vi /etc/bind/named.conf.default-zones

For CentOS/Fedora, the default file can be at `/etc/named.conf.local` 
Then add the following line:

    zone "1.168.192.in-addr.arpa" {
        type master;
        file "/etc/bind/db.1.168.192";
        allow-update { none; };
    };
    
    zone "sample.net" {
        type master;
        file "/etc/bind/db.sample.net";
        allow-update { none; };
    };

## Step 5
After setting up the zone info, we'll now proceed at configuring each zone. First create `/etc/bind/db.sample.net` and add the following:

    TTL    604800
    @    IN    SOA   ns1.sample.net.    admin.sample.net. (
         6        ; Serial
         604800   ; Refresh
         86400    ; Retry
         2419200  ; Expire
         604800 ) ; Negative Cache TTL
    ; name servers - NS records
        IN    NS    ns1.sample.net.
    ; name servers - A records
    ns1      IN    A    192.168.1.10
    desktop  IN    A    192.168.1.20

Next, create the reverse lookup record, `/etc/bind/db.1.168.192`

    $TTL 604800
    @ IN SOA ns1.cerberos.net. root.cerberos.net. (
              5     ; Serial
        6048000     ; Refresh
          86400     ; Retry
        2419200     ; Expire
         604800 )   ; Negative Cache TTL
    ;
    @  IN NS ns1.cerberos.net.
    ; PTR Records
    101    IN    PTR    ns1.sample.net.     ; 192.168.1.10
    200    IN    PTR    desktop.sample.net. ; 192.168.1.20

## Step 6
After creating DNS record, we'll have to test the configuration. To check the configuration files for error run `named-checkconfig`

    sudo named-checkconfig

This will output the error and on which specific line the error occurred on your config file. It won't output any if there are no error on your configurations. 
For your zone file, we'll use `named-checkzone`. This requires you to input the zone name and zone file. In our case, we'll do the following:

    sudo named-checkzone sample.net db.sample.net
    sudo named-checkzone 1.192.168.in-addr.arpa db.1.168.192

It will output `OK` if no issues are found in your zone file/s.

## Step 7
When all configurations are set we'll have to start/restart the `bind9` service. 

    sudo server bind9 start

## Step 8
**Make sure you have set your new server as the default or primary DNS on you client/s.**
To check if your client can now query from your DNS, do the following:
 
    # use `@` to query on the specific DNS
    # We're using `localhost` since we're inside the DNS
    #   if you're on your client, you have to provide the DNS IP
    dig ns1.sample.net @localhost
    # For reverse lookup
    dig -x 192.168.1.200 @localhost
    
    # Don't point to the DNS if you already have configured your
    #   client's network interface's DNS, 
    #   pointing at your new server
    dig ns1.sample.net
    dig desktop.sample.net
    # For reverse lookup
    dig -x 192.168.1.200

### References

1. [MIT Bind Config](http://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-rg-en-4/s1-bind-namedconf.html)
2. [ISC: Bind 9 Documentation](https://kb.isc.org/docs/aa-01031)
3. [ISC: Bind 9.14 named.conf Docs](https://downloads.isc.org/isc/bind9/9.14.6/doc/arm/man.named.conf.html)

> Written with [StackEdit](https://stackedit.io/).

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMDI3MjAzNjNdfQ==
-->