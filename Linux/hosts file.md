Before creation of DNS(Domain Name System) ,when internet had around 100 users, computers used `hosts` file to store names for different ip addresses. 

Now since there are billions users on internet, it became obsolete. 

However, it is very convenient when it comes to use it as website shortcuts.

For example , you can just add `ip addresses` of your favorite websites with a shortcut name 

> A Linux computer keeps a similar short-list of addresses it’s expected to need in a file called /etc/hosts.

```

123.4545.656.7  g # for www.google.com
123.4.66.234.56 re # www.reddit.com 

```
and now you can just enter `g` or `re` to your browser it will redirect to websites your have configured in the hosts file. 


There is also []()

If you want to use the hosts file too, it’s super simple:
```bash
$ wget someonewhocares.org/hosts/hosts
$ sudo cat hosts >> /etc/hosts
$ rm hosts
```
