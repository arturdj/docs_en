# Network **Lists**

Network Lists is the Azion platform feature that allows you to create and manage whitelists *, *blacklists* or even *greylists* based on the user's network or location. With it, it is possible to prevent different types of attacks to your network, as well as to prevent users with malicious behavior from having access to your applications.

Through restrictions rules by IPs, ASN or *geolocation*. Network Lists are used in the business rules of the Edge Firewall Rules Engine, mitigating security risks and optimizing the performance of your resources.

~~~
Attention: To use the Network Lists feature, it is necessary to enable the Network Layer Protection module.
~~~

> 1. [How does it work?](#how-does-it-work)
> 2. [Hands-On](#hands-on)
> 3. [Support Documents](#support-documents)

---

## 1. How does it work? {#how-does-it-work}

With Azion Network Lists, you can create and manage lists that are loaded on all Azion Edge Nodes. Whenever a Network List is associated with a rule, it is compared with the IP address of the client performing the HTTP request, taking into account the comparison operators configured in the Rules Engine Rule.

A Network List can be these types:

* IP/CIDR: It corresponds to a list of IP addresses or CIDR, one address per line must be filled in. If you prefer, also enter the subnet mask of the IP addresses.
* ASN: AS Number refers to Autonomous System Number Allocation which corresponds to a group of IP address networks managed by one or more network operators that have a clear and unique routing policy. Consulting the ASN Whois service for [LACNIC](http://lacnic.net/cgi-bin/lacnic/whois?lg=EN), Azion's ASN, for example, is AS52580. Choose the ASN type to represent a list of AS groups, filling in one address per line, with only the number without the prefix.
* Countries: Corresponds to a list of Countries. To include Countries in the list, select the items in the Available Countries tab and move to the Chosen Countries tab.

After creating a Network List, associate it with one or more Rules or Rule Sets that have the Network Layer Protection module activated.

> Attention: A Network Lists will have effective use when it is associated with one or more Rules on the Edge Firewall Rules Engine through the conditional (Criteria) Network, for this, the Network Layer Protection module must be enabled.

To provide even more agility to your processes, Azion provides and maintains some Network Lists that are updated automatically and ready to use. One of them is the *Azion IP Tor Exit Nodes* *Network List*, which contains the IP addresses of the *Tor* network exits and can be used in one or more Rules, through the condition (Criteria) Network, according to your business needs.

> The content of the Network Lists provided by Azion cannot be modified.

## 2. Hands-on. Step by Step to create a Network List {#hand-on}

1. From Real-Time Manager, access the menu Libraries> Network Lists.
2. To add a new list, click the Add button.
3. Fill in the field which will appear, as shown below:

  - Add Network List (Name of your list): Give your *Network List* a descriptive name. This name will appear in the list of options in the *Criteria* section, within the *Rules Engine* configuration.
  - Type: Type of *Network List*. They can be the following types:
      - ASN (*Autonomous System Number*)
      - *Countries
      - **IP/CIDR* (IP addresses or classes of addresses)
  - List: Add the items that will make up your list here. For *ASN* and *IP/CIDR* types, a typing field will be displayed. Include one address per line. Duplicated items will be deleted automatically. For the Countries type, a selection list will be presented. Select the items in the Available Countries tab and move to the Chosen Countries tab to include them in the list.

4. Click on *Save* to finalize the configuration.

## 3. Support Documents {#support-documents}

* [Network Lists API]({% tl api_v3_network_lists %})
* [Edge Firewall]({% tl documentation_products_edge_firewall %})

---

Didn't find what you were looking for? [Open a ticket.](https://tickets.azion.com/)

[Edit this page](https://github.com/aziontech/docs_en/blob/master/edge-firewall/network-lists/index.md) on GitHub.