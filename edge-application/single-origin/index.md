# Single **Origin**

[Edit on GitHub <svg width="14" height="14" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke="#F3652B"><path d="M4.81.71H.672v11.43H12.1V8.001" stroke-width=".8"/><path d="M6.87.786h5.155V5.94M6.31 6.5L12.026.786"/></g></svg>](https://github.com/aziontech/docs_en/edit/master/edge-application/single-origin/index.md)

Through Single Origin you may set up the address of your origin and adjust parameters.

> 1. [Single Origin Features](#single-origin-features)
> 2. [How to set up a Single Origin](#how-to-set-up-a-single-origin)

---

## 1. Single Origin Features {#single-origin-features}

With Single Origin you add an origin for your content and customize Host Header, connection method and authentication credentials.

### Host Header {#host-header}

The Host header is used by your origin to identify the *virtualhost* and locate your content or application. When setting up an origin in Real-Time Manager, you can customize the value that must be sent by Azion in the Host header.

If this field is left blank, Azion will use, by default, the same address defined in the Address field. Leave the Host Header field blank if your origin is configured to respond to *virtualhost* by the same address that is configured in DNS.

You can fill in a custom value for Host Header to be sent to your origin. For example, *www.azion.com*. You must customize the Host Header if your origin is configured to respond to a *virtualhost* at an address other than the one configured in DNS.

Or, you can use the variable *$host* in the Host Header field, to instruct the edge nodes to pass on to the origin the same Host header received from your visitors. Use this set up if you multiple *virtualhosts* being replied by the same origin.

### Origin Path  {#origin-path}

If you need that the Edge Nodes of Azion request the content of your origin in a different URL path, you may define an Origin Path. Azion will concatenate the Origin Path with the URI requested by the user.

The definition of the Origin Path is optional. If it is not defined, it will only consider the URI.

For example, if in your origin the whole content is under the path */secure*, though this path is not shown in the URL for your users, you may define the */secure* as the Origin Path in your origin settings. The rest of the path will be preserved, in accordance with the user’s request.

### Origin Protocol Policy {#origin-protocol-policy}

Azion’s delivery architecture allows you to customize the desired type of connection of the Edge Nodes to your origin:

* Preserve HTTP/HTTPS protocol: will keep the same connection protocol (HTTP or HTTPS) and ports used by your user when accessing your content on Azion to connect to your origin.

* Enforce HTTP: the connection between Azion’s Edge Nodes and your origin will be through HTTP, regardless of the connection protocol (HTTP or HTTPS) and ports used by your user to access Azion’s content. With this new option, you may customize a port to your origin in the Address field different from the default port (80 for HTTP) if you wish.

* Enforce HTTPS: the connection between Azion’s Edge Nodes and your origin will be through HTTPS, regardless of the connection protocol (HTTP or HTTPS) and ports used by your user to access Azion’s content. With this new option, you may customize a port to your origin in the Address field different from the default port (443 for HTTPS) if you wish.

  

### Address {#address}

After the definition of the fields above, add an origin informing the IP address or hostname (FQDN – Full Qualified Domain Name) of your origin.

You may also customize the origin port, if you defined the *Origin Protocol Policy* in the *Enforce HTTP* or *Enforce HTTPS*, using the notation *host:port.*

### HMAC Authentication {#hmac-authentication}

You may include a Single Origin where the origin is found in an Object Storage with private access, with authentication through HMAC.

<p style="background-color:#ddeef8; color:#1574ba"> When enabling HMAC Authentication, your private content will begin to be delivered to your users through Edge Application.</p>

You should include in the access credentials HMAC, Region, Access Key and Secret Key provided by your Object Storage provider. 

Google Cloud Storage™ supports buckets with local type single region (us-east1 for example) and multiregional and if this is your case, you can set the value "auto" to Region. 

Secret Key is protected by being displayed only to its users with write permission and maintaining their access security.


> :warning: **_Query Strings_ are not supported with HMAC enabled at this moment**
>
> If you still need to use query strings, please, contact us.


_©2020 Google LLC All rights reserved. Google Cloud Storage is a trademark of Google LLC._



### Timeouts {#timeouts}

Displays timeout setting in seconds pre-defined by Azion. Timeout values cannot be customized.

---

## 2. How to set up a Single Origin {#how-to-set-up-a-single-origin}

To set up a Single Origin:

1.  **Access** [**Real-Time Manager**](https://manager.azion.com/) and click the menu **“Edge Services”** and select the option **“Edge Application”**.
2.  Add or edit the desired **“Edge Application”** settings.
3.  At the tab **“Origins”**, add or edit an origin to your content.
4.  Select **“Single Origin”** as **“Origin Type"** and fill the requested fields.
5.  After saving, access the tab “**Rules Engine”** to edit or add rules for one of more **“paths”** through the **“Behavior: Set Origin”**.

---

Didn't find what you were looking for? [Open a support ticket.](https://tickets.azion.com/)

