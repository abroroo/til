# What is `hosts` file?

Before creation of DNS(Domain Name System) ,when internet had around 500-5000 users, computers used `hosts` file to store names for different ip addresses. 

Now since there are billions users on internet, it became obsolete.    

However, it is very convenient when it comes to use it as shortcuts for your favorite websites.

For example, you can just add `ip addresses` of your favorite websites with a shortcut text to your computer's `hosts` file

> A Linux/Mac computer keeps `hosts` file in `/etc/hosts` directory.

```
123.4545.656.7  g # for www.google.com
123.4.66.234.56 re # www.reddit.com 
```
and now you can just enter `g` or `re` to your browser it will redirect to websites your have configured in the hosts file. 

# Alternative use as an adblocker: 

You can also use `hosts` file as adblocker or to avoid pirate sites, there is a regularly updated `hosts` file online, which you can use for free [someonewhocares.org](https://someonewhocares.org/hosts/)

How it works: when router recognizes the domain name that is on the list of hosts file, it will redirect it to origin. 

If you want to use the hosts file too from that website, it’s super simple:
```bash
$ wget someonewhocares.org/hosts/hosts
$ sudo cat hosts >> /etc/hosts
$ rm hosts
```
