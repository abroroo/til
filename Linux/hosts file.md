# What is `hosts` file?

Before creation of DNS(Domain Name System) ,when internet had around 5000-10000 users, computers used `hosts` file to store names for different ip addresses. 

Now since there are billions users on internet, it became obsolete. But computers still keep `hosts` file. For Mac/Linux systems it is in `/etc/hosts` directory.           

However, it is very convenient when it comes to __use it as a list of shortcuts for your favorite websites__.

For example, you can just add `ip addresses` of your favorite websites with a shortcut text to your computer's `hosts` file

> A Linux/Mac computer keeps `hosts` file in `/etc/hosts` directory.

```
123.4545.656.7  g # for www.google.com
123.4.66.234.56 re # www.reddit.com 
```
and now you can just enter `g` or `re` to your browser it will redirect to websites your have configured in the hosts file. 

# Alternative use as an adblocker: 

You can also use `hosts` file as adblocker or to avoid pirate sites, there is a regularly updated `hosts` file online, which you can use for free [someonewhocares.org](https://someonewhocares.org/hosts/)

__How it works:__ when router recognizes the domain name that is on the list of hosts file, it will redirect it to origin. 

If you want to use the hosts file from that website, it’s super simple:
```bash
$ wget someonewhocares.org/hosts/hosts
$ sudo cat hosts >> /etc/hosts
$ rm hosts
```
