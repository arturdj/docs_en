# Real-Time **Purge**

[Edit on GitHub <svg width="14" height="14" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke="#F3652B"><path d="M4.81.71H.672v11.43H12.1V8.001" stroke-width=".8"/><path d="M6.87.786h5.155V5.94M6.31 6.5L12.026.786"/></g></svg>](https://github.com/aziontech/docs_en/edit/master/api/v2/real-time-purge/index.md)

If you need to delete an object from the Edge Caching or L2 Caching layers before it expires, you can use the Real-Time Purge API. If you like, you can integrate your Azion API with your CMS to automate your content update processes.

Have a look at how to do the following:

> 1. [Create a request for a URL Purge](#criar-uma-solicitacao-de-url-purge)
> 2. [Create a request for a Cache Key Purge](#criar-uma-solicitacao-de-cache-key-purge)
> 3. [Create a request for a Wildcard Purge](#criar-uma-solicitacao-de-wildcard-purge)

---

# 1. Create a request for a URL Purge {#criar-uma-solicitacao-de-url-purge}

To delete a list of objects from your Azion Edge Caching layer, using your URLs, you can use the endpoint:

Permission necessary: **Purge**

#### **POST** */purge/url*

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-------------|------------------|--------------|
| Authorization *(mandatory)*| Authentication through the Token, previously created through the endpoint of [Token Creation](% tl api_v2_authentication %}#criacao-de-token).<br><br>e.g.:<br><br>Authorization: Token<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |
| Content-Type *(mandatory)* | The type of coding used in the Body (application/json).<br><br>e.g.:<br><br>Content-Type: application/json | header | string |
| Body *(mandatory)* | List of URLs you want to remove from your Azion Edge Servers cache.<br><br>**urls** (array): a list of up to 50 URLs that will be removed from the cache, per request.<br><br>**method** (choice): purging method, use the value “delete” to remove. | body | json |


**Example Request**

~~~
POST /purge/url
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
Content-Type: application/json
~~~

~~~
{
    "urls": [
       "http://www.domain.com/", 
       "http://www.domain.com/test.js", 
       "http://static.mistaken-domain.com/image1.jpg"
    ],
    "method": "delete"
}
~~~

**Example Response**

~~~
HTTP/1.1 207 MULTI-STATUS
~~~

~~~
[
   {
      "status": "HTTP/1.1 201 CREATED",
      "urls": [
         "http://www.domain.com/", 
         "http://www.domain.com/test.js"
      ],
      "details": "Purge request successfully created"
   },
   {
      "status": "HTTP/1.1 403 FORBIDDEN",
      "urls": ["http://static.mistaken-domain.com/image1.jpg"],
      "details": "Unauthorized domain for your account"
   }
]
~~~

---

## 2. Create a request for a Cache Key Purge {#criar-uma-solicitacao-de-cache-key-purge}

To delete a list of objects from your Azion Edge Caching layer, using your Cache Keys, you can use the endpoint:

#### **POST** */purge/cachekey*

Permission necessary: **Purge**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-------------|------------------|--------------|
| Authorization *(mandatory)*| Authentication through the Token, previously created through the endpoint of [Token Creation](% tl api_v2_authentication %}#criacao-de-token).<br><br>e.g.:<br><br>Authorization: Token<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |
| Content-Type *(mandatory)* | The type of coding used in the Body (application/json).<br><br>e.g.:<br><br>Content-Type: application/json | header | string |
| Body *(mandatory)* | List of Cache Keys you want to remove from your Azion Edge Servers cache.<br><br>**urls** (array): a list of up to 50 Cache Keys that will be removed from the cache, per request.<br><br>**method** (choice): purging method, use the value “delete” to remove.<br><br>**Layer** (choice): the layer to be purged. Use the value "edge_caching" (the default value if left blank) to purge the Edge Caching layer and the value "l2_caching" to purge the L2 Caching layer. | body | json |


**Example Request**

~~~
POST /purge/cachekey
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
Content-Type: application/json
~~~

~~~
{
    "urls": [
       "http://www.domain.com/@@cookie_name=cookie_value", 
       "http://www.domain.com/test.js", 
       "http://static.domain.com/image1.jpg?ims=arguments@@variants"
    ],
    "method": "delete",
    "layer": "l2_caching"

}
~~~

**Example Response**

~~~
HTTP/1.1 201 CREATED
~~~

~~~
{
    "details": "Purge request successfully created"
}
~~~

---

## 3. Create a request for a Wildcard Purge {#criar-uma-solicitacao-de-wildcard-purge}

To delete a list of objects from your Azion Edge Caching layer, using a Wildcard URL or Wildcard Cache Key, you can use the endpoint:

#### **POST** */purge/wildcard*

Permission necessary: **Purge**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-------------|------------------|--------------|
| Authorization *(mandatory)*| Authentication through the Token, previously created through the endpoint of [Token Creation](% tl api_v2_authentication %}#criacao-de-token).<br><br>e.g.:<br><br>Authorization: Token<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |
| Content-Type *(mandatory)* | The type of coding used in the Body (application/json).<br><br>e.g.:<br><br>Content-Type: application/json | header | string |
| Body *(mandatory)* | The Wildcard expression that represents the list of objects you want to remove from your Azion Edge Servers cache.<br><br>**urls** (array): he Wildcard URL or Wildcard Cache Key that represents the list of objects that you want to remove. You can only use one Wildcard expression per request.<br><br>**method** (choice): purging method, use the value “delete” to remove. | body | json |


**Example Request**

~~~
POST /purge/wildcard
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
Content-Type: application/json
~~~

~~~
{
    "urls": ["http://www.domain.com/path/image.jpg*"],
    "method": "delete"
}
~~~

**Example Response**

~~~ 
HTTP/1.1 201 CREATED
~~~

~~~
{
    "detail": "Purge request successfully created"
}
~~~

---

Didn't find what you were looking for? [Open a ticket.](https://tickets.azion.com/)