# WAF

[Edit on GitHub <svg width="14" height="14" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke="#F3652B"><path d="M4.81.71H.672v11.43H12.1V8.001" stroke-width=".8"/><path d="M6.87.786h5.155V5.94M6.31 6.5L12.026.786"/></g></svg>](https://github.com/aziontech/docs_en/edit/master/api/v2/cloud-security/web-app-firewall/index.md)

> 1. [Look up a list of the rule sets in WAF](#consulta-lista-de-rule-sets-do-waf)
> 2. [Look up details of a rule set in WAF](#consulta-dados-de-uma-rule-set-do-waf)

---

## 1. Look up a list of the rule sets in WAF {#consulta-lista-de-rule-sets-do-waf}

Returns a list of the rule sets in WAF.

#### **GET** */waf/rulesets*

Permission necessary: **View Security Settings**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-------------|-------------------|--------------|
| Authorization *(mandatory)*| Authentication through the Token, previously created through the endpoint of [Token Creation](% tl api_v2_authentication %}#criacao-de-token).<br><br>e.g.:<br><br>Authorization: Token<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |

**Example Request**

~~~
GET /waf/rulesets
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
      "id": 3,
      "name": "WAF for myApp",
      "mode": "blocking",
      "active": true,
      "sql_injection": true,
      "sql_injection_sensitivity": "medium",
      "remote_file_inclusion": true,
      "remote_file_inclusion_sensitivity": "medium",
      "directory_traversal": true,
      "directory_traversal_sensitivity": "medium",
      "cross_site_scripting": true,
      "cross_site_scripting_sensitivity": "medium",
      "evading_tricks": true,
      "evading_tricks_sensitivity": "medium",
      "file_upload": true,
      "file_upload_sensitivity": "medium",
      "unwanted_access": true,
      "unwanted_access_sensitivity": "medium",
      "identified_attack": true,
      "identified_attack_sensitivity": "medium",
      "whitelist": "BasicRule wl:1 \"mz:$ARGS_VAR:foo|$URL:/x\";"
   },
   {
      "id": 4,
      "name": "WAF for Stage",
      "mode": "counting",
      "active": true,
      "sql_injection": true,
      "sql_injection_sensitivity": "medium",
      "remote_file_inclusion": true,
      "remote_file_inclusion_sensitivity": "medium",
      "directory_traversal": true,
      "directory_traversal_sensitivity": "medium",
      "cross_site_scripting": true,
      "cross_site_scripting_sensitivity": "medium",
      "evading_tricks": true,
      "evading_tricks_sensitivity": "medium",
      "file_upload": true,
      "file_upload_sensitivity": "medium",
      "unwanted_access": true,
      "unwanted_access_sensitivity": "medium",
      "identified_attack": true,
      "identified_attack_sensitivity": "medium"
   }
]
~~~

---

## 2. Look up details of a rule set in WAF {#consulta-dados-de-uma-rule-set-do-waf}

Returns details of a rule set in WAF.

#### **GET** */waf/rulesets/:ruleset_id*

Permission necessary: **View Security Settings**

| Parameter | Description | Type of Parameter | Type of Data |
|-----------|-------------|-------------------|--------------|
| Authorization *(mandatory)*| Authentication through the Token, previously created through the endpoint of [Token Creation](% tl api_v2_authentication %}#criacao-de-token).<br><br>e.g.:<br><br>Authorization: Token<br>583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf | header | string |
| :ruleset_id *(mandatory)* | Id of the WAF rule set to be queried. To get the ID of a rule set, look up the [Rule Sets List](#consulta-lista-de-rule-sets-do-waf). | path | number |

**Example Request**

~~~
GET /waf/rulesets/3
Accept: application/json; version=2
Authorization: Token 583f8a9ca8d6d5ff2cb50f1d3c4d35cb8939f1bf
~~~

**Example Response**

~~~
HTTP/2 200
~~~

~~~
{
    "id": 3,
    "name": "WAF for myApp",
    "mode": "blocking",
    "active": true,
    "sql_injection": true,
    "sql_injection_sensitivity": "medium",
    "remote_file_inclusion": true,
    "remote_file_inclusion_sensitivity": "medium",
    "directory_traversal": true,
    "directory_traversal_sensitivity": "medium",
    "cross_site_scripting": true,
    "cross_site_scripting_sensitivity": "medium",
    "evading_tricks": true,
    "evading_tricks_sensitivity": "medium",
    "file_upload": true,
    "file_upload_sensitivity": "medium",
    "unwanted_access": true,
    "unwanted_access_sensitivity": "medium",
    "identified_attack": true,
    "identified_attack_sensitivity": "medium",
    "whitelist": "BasicRule wl:1 \"mz:$ARGS_VAR:foo|$URL:/x\";"
}
~~~

---

Didn't find what you were looking for? [Open a ticket.](https://tickets.azion.com/)

