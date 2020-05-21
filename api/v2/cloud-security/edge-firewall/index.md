# Edge **Firewall**

[Edit on GitHub <svg width="14" height="14" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke="#F3652B"><path d="M4.81.71H.672v11.43H12.1V8.001" stroke-width=".8"/><path d="M6.87.786h5.155V5.94M6.31 6.5L12.026.786"/></g></svg>](https://github.com/aziontech/docs_en/edit/master/api/v2/cloud-security/edge-firewall/index.md)

The API of Edge Firewall allows you to check, remove or update your existing rule sets, as well as creating new Edge Firewall rule sets.

> 1. [Look up a list of the rule sets in Edge Firewall](#consulta-lista-de-rule-sets-do-edge-firewall)
> 2. [Look up details of a rule set in Edge Firewall](#consulta-dados-de-uma-rule-set-do-edge-firewall)
> 3. [Delete a rule set in Edge Firewall](#deletar-uma-rule-set-do-edge-firewall)
> 4. [Look up a list of the rule sets in Edge Firewall](#sobrescrever-uma-rule-set-do-edge-firewall)
> 5. [Update the fields of a rule set in Edge Firewall](#atualizar-campos-de-uma-rule-set-do-edge-firewall)

---

## 1. Look up a list of the rule sets in Edge Firewall {#consulta-lista-de-rule-sets-do-edge-firewall}

Returns a list of the rule sets in Edge Firewall.

#### **GET** */edge_firewall/rulesets*

Permission necessary: **View Security Settings**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-------------|-------------------|--------------|
| Authorization *(mandatory)* | Authentication through the Token, previously created through the endpoint of [Criação de Token](% tl api_v2_authentication %}/#criacao-de-token).<br><br>e.g.:<br><br>Authorization:<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |

**Example Request**

~~~
GET /edge_firewall/rulesets
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf 
~~~

**Example Response**

~~~
HTTP/2 200
~~~

~~~
[
   {
      "id": 533,
      "name": "Bloqueio por HTTP Referrer",
      "block_access_by_referer": true,
      "allow_blank_referer": true,
      "geo_block": "disabled",
      "accepted_domains": [
         {"url": "*.azion.com"},
         {"url": "*.azion.com.br"}
      ],
      "geo_countries": [],
      "ip_blocking_rule": "allow_from_all",
      "ip_blocking_addresses": [],
      "require_secure_token": false,
      "secret": null,
      "is_active": true
   },
   {
      "id": 534,
      "name": "Bloqueio de Países",
      "block_access_by_referer": false,
      "allow_blank_referer": false,
      "geo_block": "blacklist",
      "accepted_domains": [],
      "geo_countries": ["CHN","PRK","RUS"],
      "ip_blocking_rule": "allow_from_all",
      "ip_blocking_addresses": [],
      "require_secure_token": false,
      "secret": null,
      "is_active": true
   },
   {
      "id": 535,
      "name": "Secure Token",
      "block_access_by_referer": false,
      "allow_blank_referer": false,
      "geo_block": "disabled",
      "accepted_domains": [],
      "geo_countries": [],
      "ip_blocking_rule": "allow_from_all",
      "ip_blocking_addresses": [],
      "require_secure_token": true,
      "secret": "mysecret",
      "is_active": true
   }
]
~~~

---

## 2. Look up details of a rule set in Edge Firewall {#consulta-dados-de-uma-rule-set-do-edge-firewall}

Returns details of a rule set in Edge Firewall.

#### **GET** */edge_firewall/rulesets/:ruleset_id*

Permission necessary: **View Security Settings**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-------------|-------------------|--------------|
| Authorization *(mandatory)* | Authentication through the Token, previously created through the endpoint of [Criação de Token](% tl api_v2_authentication %}/#criacao-de-token).<br><br>e.g.:<br><br>Authorization:<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |
| :ruleset_id *(mandatory)* | Id of the Edge Firewall rule set to be queried. To get the ID of a rule set, look up the [Rule Sets List](#consulta-lista-de-rule-sets-do-edge-firewall). | path | number |

**Example Request**

~~~
GET /edge_firewall/rulesets/534
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
~~~

**Example Response**

~~~
HTTP/2 200
~~~

~~~
{
    "id": 534,
    "name": "Bloqueio de Países",
    "block_access_by_referer": false,
    "allow_blank_referer": false,
    "geo_block": "blacklist",
    "accepted_domains": [],
    "geo_countries": ["CHN","PRK","RUS"],
    "ip_blocking_rule": "allow_from_all",
    "ip_blocking_addresses": [],
    "require_secure_token": false,
    "secret": null,
    "is_active": true
}
~~~

---

## 3. Delete a rule set in Edge Firewall {#deletar-uma-rule-set-do-edge-firewall}

Remove a rule set in Edge Firewall. You cannot remove a rule set that is currently in use.

#### **DELETE** */edge_firewall/rulesets/:ruleset_id*

Permission necessary: **Edit Security Settings**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-----------|-------------------|--------------|
| Authorization *(mandatory)* | Authentication through the Token, previously created through the endpoint of [Token Creation](% tl api_v2_authentication %}/#criacao-de-token).<br><br>e.g.:<br><br>Authorization:<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |
| :ruleset_id *(mandatory)* | Id of the Edge Firewall rule set to be queried. To get the ID of a rule set, look up the [Rule Sets List](#consulta-lista-de-rule-sets-do-edge-firewall). | path | number |

**Example Request**

~~~
DELETE /edge_firewall/rulesets/535
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
~~~

**Example Response**

~~~
HTTP/2 204
~~~

---

## 4. Look up a list of the rule sets in Edge Firewall {#sobrescrever-uma-rule-set-do-edge-firewall}

Overwrite all the fields of an Edge Firewall rule set, retaining the id. Any optional fields left blank will use the default values. If you only want to update some fields of a rule set, without changing the values of the rest, consider using the PATCH method, instead of PUT.

#### **PUT** */edge_firewall/rulesets/:ruleset_id*

Permission necessary: **Edit Security Settings**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-----------|-------------------|--------------|
| Authorization *(mandatory)* | Authentication through the Token, previously created through the endpoint of [Token Creation](% tl api_v2_authentication %}/#criacao-de-token).<br><br>e.g.:<br><br>Authorization:<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf| header | string |
| Content-Type *(mandatory)* | The type of coding used in the Body (application/json).<br><br>e.g.:<br><br>Content-Type: application/json | header | string |
| :ruleset_id *(mandatory)* | Id of the Edge Firewall rule set to be overwritten. To get the ID of an Edge Firewall rule set, look up the [Rule Sets List](#consulta-lista-de-rule-sets-do-edge-firewall). | path | number |
| Settings *(mandatory)* | The new values of each field of the rule set. Any fields left blank, will be filled with the default values, with the exception of mandatory fields, which must be filled in. If you only want to change one of the fields, use the PATCH method instead of PUT.<br><br>**name** (string): mandatory field that defines the name of the Edge Firewall rule set.<br><br>**block_access_by_referer** (boolean): use *true* to activate the blocking of any content delivered, based on the HTTP Referer; or *false* to deactivate blocking.<br><br>**allow_blank_referer** (boolean): defines the value of allow_blank_referer as *true* if you want to allow content delivered by requests without a Referrer; or *false* if you want to block it, if you have enabled blocking by HTTP referrer.<br><br>**accepted_domains** (array): If you have enabled blocking by HTTP referrer, list those domains to which requests are to be released.<br><br>**geo_block** (choice): use the value *“whitelist“*, to enable blocking for all countries, with the exception of those you list; *“blacklist”* to only list those countries that you want to block; or *“disabled”* to disable geo-location blocking.<br><br>**geo_countries** (array): if you have enabled geo_block by *whitelist* or *blacklist*, list the three-letter codes of those countries (ISO 3166-1 alpha-3) that you want to release or block, depending on your geo_block option.<br><br>**ip_blocking_rule** (choice): use the value *“allow_from_all“*, to configure Edge Firewall to allow access from all IPs, by default, and define a blacklist in the field ip_blocking_address; or use the value “deny_from_all”, to block access from all IPs, by default, with the exception of the whitelist configured in the field ip_blocking_address.<br><br>**ip_blocking_addresses** (array): am list of IP addresses, or CIDR masks, that you want to block or allow. If you have configured ip_blocking_rule as “allow_from_all”, this field contains a blacklist to block the listed IPs; leave the array blank, if you don’t wish to block any address. If you have configured ip_blocking_rule as “deny_from_all”, this field contains a whitelist to release the listed IPs.<br><br>**require_secure_token** (boolean): use *true* to enable secure token validation or *false*, to disable it.<br><br>**secret** (string): if you have enabled secure token validation, define the secret that will be used when generating the hash. If not, use null. *null*.<br><br>**is_active** (boolean): use *true* to enable a rule set, or *false*, to disable it. | body | json |

**Example Request**

~~~
PUT /edge_firewall/rulesets/536
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
Content-Type: application/json
~~~

~~~
{
    "name": "Secure Token",
    "block_access_by_referer": false,
    "accepted_domains": [],
    "geo_block": "disabled",
    "geo_countries": [],
    "ip_blocking_rule": "allow_from_all",
    "ip_blocking_addresses": [],
    "require_secure_token": true,
    "secret": "myscret"
 }
~~~

**Example Response**

~~~
HTTP/2 200
~~~

~~~
{
    "id": 536,
    "name": "Secure Token",
    "block_access_by_referer": false,
    "accepted_domains": [],
    "geo_block": "disabled",
    "geo_countries": [],
    "ip_blocking_rule": "allow_from_all",
    "ip_blocking_addresses": [],
    "require_secure_token": true,
    "secret": "myscret",
    "is_active": true
 }
~~~

---

## 5. Update the fields of a rule set in Edge Firewall {#atualizar-campos-de-uma-rule-set-do-edge-firewall}

Update one or more fields of an Edge Firewall rule set, retaining the value of those fields not included.

#### **PATCH** */edge_firewall/rulesets/:ruleset_id*

Permission necessary: **Edit Security Settings**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-----------|-------------------|--------------|
| Authorization *(mandatory)* | Authentication through the Token, previously created through the endpoint of [Token Creation.](% tl api_v2_authentication %}/#criacao-de-token).<br><br>e.g.:<br><br>Authorization:<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf| header | string |
| Content-Type *(mandatory)* | The type of coding used in the Body (application/json)..<br><br>e.g.:<br><br>Content-Type: application/json | header | string |
| :ruleset_id *(mandatory)* | Id of the Edge Firewall rule set to be updated. To get the ID of a rule set, look up the [Rule Sets List](#consulta-lista-de-rule-sets-do-edge-firewall). | path | number |
| Settings *(mandatory)* | You must include one of more fields to be updated. Those fields left blank will not have their values changed.<br><br>**name** (string): defines the name of the Edge Firewall rule set.<br><br>****block_access_by_referer** (boolean): use *true* to activate the blocking of any content delivered, based on the HTTP Referer; or *false* to deactivate blocking.<br><br>**allow_blank_referer** (boolean): defines the value of allow_blank_referer as *true* if you want to allow content delivered by requests without a Referrer; or *false* if you want to block it, if you have enabled blocking by HTTP referrer.<br><br>**accepted_domains** (array): If you have enabled blocking by HTTP referrer, list those domains to which requests are to be released.<br><br>**geo_block** (choice): use the value *“whitelist“*, to enable blocking for all countries, with the exception of those you list; *“blacklist”* to only list those countries that you want to block; or *“disabled”* to disable geo-location blocking.<br><br>**geo_countries** (array): if you have enabled geo_block by *whitelist* or *blacklist*, list the three-letter codes of those countries (ISO 3166-1 alpha-3) that you want to release or block, depending on your geo_block option.<br><br>**ip_blocking_rule** (choice): use the value *“allow_from_all“*, to configure Edge Firewall to allow access from all IPs, by default, and define a blacklist in the field ip_blocking_address; or use the value “deny_from_all”, to block access from all IPs, by default, with the exception of the whitelist configured in the field ip_blocking_address.<br><br>**ip_blocking_addresses** (array): am list of IP addresses, or CIDR masks, that you want to block or allow. If you have configured ip_blocking_rule as “allow_from_all”, this field contains a blacklist to block the listed IPs; leave the array blank, if you don’t wish to block any address. If you have configured ip_blocking_rule as “deny_from_all”, this field contains a whitelist to release the listed IPs.<br><br>**require_secure_token** (boolean): use *true* to enable secure token validation or *false*, to disable it.<br><br>**secret** (string): if you have enabled secure token validation, define the secret that will be used when generating the hash. If not, use null. *null*.<br><br>**is_active** (boolean): use *true* to enable a rule set, or *false*, to disable it. | body | json |

**Example Request**

~~~
PATCH /edge_firewall/rulesets/533
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
Content-Type: application/json
~~~

~~~
{
    "accepted_domains": [
       {"url": "*.azion.com"},
       {"url": "*.azion.com.br"},
       {"url":"anotherdomain.com"}
    ]
}
~~~

**Example Response**

~~~
HTTP/2 200
~~~

~~~
{
    "id": 533,
    "name": "Bloqueio por HTTP Referrer",
    "block_access_by_referer": true,
    "allow_blank_referer": true,
    "geo_block": "disabled",
    "accepted_domains": [
       {"url":"*.azion.com"},
       {"url":"*.azion.com.br"},
       {"url":"anotherdomain.com"}
    ],
    "geo_countries": [],
    "ip_blocking_rule": "allow_from_all",
    "ip_blocking_addresses": [],
    "require_secure_token": false,
    "secret": null,
    "is_active": true
}
~~~

---

Didn't find what you were looking for? [Open a ticket.](https://tickets.azion.com/)