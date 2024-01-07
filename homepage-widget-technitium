---
layout: default
title: Homepage Plugin for Technitium DNS Server 
description: How to use their API and configure the custom API plugin in Technitium
---

Ever since I was forced to work with DNS at my first IT job, I found it deeply interesting. I hated it at first, then I became better at it, then I became good at it, and now I like DNS. DNS is friend.

I started using [Homepage](https://gethomepage.dev) to have a convenient launchpad for my home server stuff and recently found out about their [Widgets](https://gethomepage.dev/latest/widgets/) which are essentially plugins to work with tons of services and display convenient information. There is a Plugin for [AdGuardHome](https://github.com/AdguardTeam/AdGuardHome) which is a great home DNS application with tons of features and easy configuration.

However, I've since switched to using a relatively new product, [Technitium DNS Server](https://technitium.com). It's fast. It's easy. It's super configurable. It supports direct DNS recursion without relying on external applications like Unbound. I love it. Unfortunately, there is no widget for Homepage. *Fortunately, Homepage supports a widget called "custom API" which is exactly what we need.* And thankfully, the folks at Technitium have a truly great [API documentation](https://github.com/TechnitiumSoftware/DnsServer/blob/master/APIDOCS.md) which helped me get the basics down in no less than 2 minutes.

It sounds a little complicated, but do not worry, it's actually really easy and took me, a guy who wouldn't touch programming with a 10-foot pole, around 10 minutes to figure out (while my fiancé was trying to explain a psychological concept to me). So you can do it aswell.

Here's how.

### Creating the API token and querying the Technitium DNS API

#### Prerequisites

First, you need an active Technitium DNS server running in your home network that has the management interface exposed to the server running Homepage. If they're on the same machine, that shouldn't be a problem, but if you have a management VLAN, make sure to take note of this.

You will also need access to a browser that can parse JSON or know your way around curl, I used Firefox but it shouldn't really matter.

My Technitium server runs on the IP address 172.16.10.3 - please replace this with the IP address *your* server is running on.

#### Creating the API token

To create an API token, we need to access a special URL containing

* The username for the user the token should be created for
* The password for the user the token should be created for
* The name the token should have

So far I don't know of a GUI way to do this. In this example, we'll use the user **admin** with the password **password** and the API token will be called **Token1** - replace these with the credentials of your user account. I simply entered this into the URL bar of Firefox:

```
http://172.16.10.3:5380/api/user/createToken?user=admin&pass=password&tokenName=Token1
```

You will get a reply back from the server, and it will be formatted in JSON. The reply should look like this:

```json
{
	"username": "admin",
	"tokenName": "Token1",
	"token": "lYNEVlz0YZBzEVtyurTQSuFsNgfIul7J63zyGzx8FASIzEc6xlbHekCGsrbGwezW",
	"status": "ok"
}
```

Make sure to copy the Token - which is a 64 character string as seen above.

#### Plugging it into Homepage

How you just need to edit your Homepage's services.yaml file and specify the API endpoints for whatever you want. The Dashboard statistics will probably be the most useful thing to be displayed, and to change what you want displayed on your widget, you just need to change the field name - the [API documentation](https://github.com/TechnitiumSoftware/DnsServer/blob/master/APIDOCS.md) has all the info you need.

I have the total amount of queries, the amount of blocked queries, and the amount of clients on display.

This is what I specified in my services.yaml:

```yaml
    - Technitium DNS Server:
        href: http://172.16.10.3:5380/
        description: Cutting Edge IPv4 and IPv6 DNS Server
        icon: technitium
        widget:
          type: customapi
          url: http://172.16.10.3:5380/api/dashboard/stats/get?token=lYNEVlz0YZBzEVtyurTQSuFsNgfIul7J63zyGzx8FASIzEc6xlbHekCGsrbGwezW&type=lastHour
          refreshInterval: 10000 
          method: GET 
          mappings:
            - field:
                response:
                  stats: totalQueries
              label: Queries
              format: text
            - field:
                response:
                  stats: totalBlocked
              label: Blocked
              format: text
            - field:
                response:
                  stats: totalClients
              label: Clients
              format: text
```

And that's it! It really was that easy:

![Widget](https://raw.githubusercontent.com/stepsysadmin/stepsysadmin.github.io/c1256f46f4d9737517d0677816ca0e40554b3c46/images/technitium_widget.png)
