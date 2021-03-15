# Edge **Application - Edge Functions Instances**

[Edit on GitHub <svg width="14" height="14" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke="#F3652B"><path d="M4.81.71H.672v11.43H12.1V8.001" stroke-width=".8"/><path d="M6.87.786h5.155V5.94M6.31 6.5L12.026.786"/></g></svg>](https://github.com/aziontech/docs_en/edit/master/edge-application/edge-functions-instances/index.md)

By activating the Edge Functions module, you can instantiate serverless functions in your Edge Application at Azion, as well as set up the conditions for its execution. Available for Edge Application and Edge Firewall products, its use allows you to run serveless functions in our robust distributed network of Edge Nodes, responding to events closer to the end user, ensuring greater scalability and availability

> 1. [How does it work?](#how-does-it-work)
> 2. [How to set up?](#how-to-set-up)
> 3. [Support Documents](#support-documents)

---
#  **Edge Functions Instances**

[Edite no GitHub <svg width="14" height="14" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke="#F3652B"><path d="M4.81.71H.672v11.43H12.1V8.001" stroke-width=".8"/><path d="M6.87.786h5.155V5.94M6.31 6.5L12.026.786"/></g></svg>](https://github.com/aziontech/docs_en/edit/master/api/v3/edge-applications/edge_functions_instances/index.md)

With the API of Edge Functions Instances, you can check, remove or update existing settings, besides creating new ones.

> 1. [Looking up a list of Edge Functions Instances](#looking-up-a-list-of-functions-instances)
> 2. [Looking up details of Edge Functions Instances](#looking-up-details-of-functions-instances)
> 3. [Deleting Edge Functions Instances](#deleting-functions-instances)
> 4. [Creating new Edge Functions Instances](#creating-new-functions-instances)
> 5. [Overwriting Edge Functions Instances](#overwriting-functions-instances)
> 6. [Updating the fields of Edge Functions Instances](#updating-fields-of-functions-instances)

---

## 1. Looking up a list of Edge Functions Instances {#consultar-lista-de-functions-instances}

This return results in a list of Edge Functions Instances.

#### **GET** */edge_applications/:edge_application_id:/functions_instances*

Necessary permission: **View Edge Application**

**Mandatory parameters**

| Parameter                               | Description                                                  | Type   | Type of Data                            |
| --------------------------------------- | ------------------------------------------------------------ | ------ | --------------------------------------- |
| Authorization *(mandatory)*             | Authentication through the Token, previously created through the endpoint of [Token Creation]({% tl api_v3_authentication %}#criacao-de-token) | header | string                                  |
| Accept *(mandatory)*                    | Details about the type of return and version                 | header | string;<br>*application/json;version=3* |
| :edge_application_id<br />*(mandatory)* | The id of the edge application you plan to query             | path   | number                                  |



**Request Example**

~~~
GET /edge_applications/1570451232/functions_instances 
Accept: application/json; version=3
Authorization: token cf2078926f91a6e638af3f4a6977b505edfe5941
~~~

**Response Example**

~~~
{
    "count": 3,
    "total_pages": 1,
    "schema_version": 3,
    "links": {
        "previous": null,
        "next": null
    },
    "results": [
        {
            "id": 522,
            "edge_function_id": 13,
            "name": "Hello World",
            "args": {
                "param": {
                    "body": "Azion - Move to the Edge",
                    "http_status": 200
                }
            }
        },
        {
            "id": 565,
            "edge_function_id": 312,
            "name": "My Hello World",
            "args": {
                "param": {
                    "body": "It works!",
                    "http_status": 200
                }
            }
        },
        {
            "id": 2360,
            "edge_function_id": 13,
            "name": "Edge Function",
            "args": {}
        }
    ]
}
~~~

---

## 2. Looking up details of Edge Functions Instances{#looking-up-details-of-functions-instances}

Results in details of Edge Functions Instances. The information originated by this return refers to the edge function instance of an Edge Application.

#### **GET** */edge_applications/:edge_application_id:/functions_instances/:functions_instances_id:*

Necessary permission: **View Edge Application**

**Mandatory parameters**

| Parameters                            | Description                                                  | Type   | Type of Data                            |
| ------------------------------------- | ------------------------------------------------------------ | ------ | --------------------------------------- |
| Authorization *(mandatory)*           | Authentication through the Token, previously created through the endpoint of [Token Creation]({% tl api_v3_authentication %}#criacao-de-token) | header | string                                  |
| Accept *(mandatory)*                  | Details about the type of return and version                 | header | string;<br>*application/json;version=3* |
| :edge_application_id *(mandatory)*    | The id of the edge application you plan to query           | path   | number                                  |
| :functions_instances_id *(mandatory)* | The id of the edge function instance you plan to query     | path   | number                                  |



**Request Example**

~~~
GET /edge_applications/161231227352/functions_instances/1031231
Accept: application/json; version=3
Authorization: token cf2078926f91a6e638af3f4a6977b505edfe5941
~~~

**Response Example**

~~~
{
    "results": {
        "id": 565,
        "edge_function_id": 312,
        "name": "My Hello World",
        "args": {
            "param": {
                "body": "It works!",
                "http_status": 200
            }
        }
    },
    "schema_version": 3
}
~~~

---

## 3. Deleting Edge Functions Instances {#deleting-functions-instances}

This return removes Edge Functions Instances. This operation is final: there is no way to roll back the information after it has been confirmed by the user.

All information associated with this Edge Functions Instance will also be removed.

If an Edge Function Instance is in use by any rule on Rules Engine, you will not be able to delete the edge function instance unless the rule is deleted or disabled.

The API does not require confirmation in order to run this instruction.

#### **DELETE** */edge_applications/:edge_application_id:/functions_instances/:functions_instance_id:*

Necessary permission: **Edit Edge Application**

**Mandatory parameters**

| Parameter                             | Description                                                  | Type   | Type of Data                            |
| ------------------------------------- | ------------------------------------------------------------ | ------ | --------------------------------------- |
| Authorization *(mandatory)*           | Authentication through the Token, previously created through the endpoint of [Token Creation]({% tl api_v3_authentication %}#criacao-de-token) | header | string                                  |
| Accept *(mandatory)*                  | Details about the type of return and version                 | header | string;<br>*application/json;version=3* |
| :edge_application_id *(mandatory)*    | The id of the edge application you plan to delete            | path   | number                                  |
| :functions_instances_id *(mandatory)* | The id of the edge function instance you plan to delete      | path   | number                                  |



**Request Example**

~~~
DELETE /edge_applications/16076123352/functions_instances/10764
Accept: application/json; version=3
Authorization: token 2909f3932069047f4736dc87e72baaddd19c9f75
~~~

**Response Example**

~~~
HTTP/2 204
~~~

---

## 4. Creating new Edge Functions Instances {#creating-new-functions-instances}

This return enables the creation of new Edge Functions Instances.

#### **POST** */edge_application/:edge_application_id:/functions_instances*

Necessary permission: **Edit Edge Application**

**Mandatory parameters**

| Parameter                          | Description                                                  | Type   | Type of data                            |
| ---------------------------------- | ------------------------------------------------------------ | ------ | --------------------------------------- |
| Authorization *(mandatory)*        | Authentication through the Token, previously created through the endpoint of [Token Creation]({% tl api_v3_authentication %}#criacao-de-token) | header | string                                  |
| Accept *(mandatory)*               | Details about the type of return and version                 | header | string;<br>*application/json;version=3* |
| Content-Type *(mandatory)*         | The type of coding used in the Body (application/json).<br><br>example:<br><br>Content-Type: application/json | header | string                                  |
| :edge_application_id *(mandatory)* | The id of the edge application you plan to create            | path   | number                                  |



**Request Example**

~~~
POST /edge_applications/:edge_application_id:/functions_instances
Accept: application/json; version=3
Authorization: token cf2078926f91a6e638af3f4a6977b505edfe5941
Content-Type: application/json
~~~

~~~
{
		"name": "Criar Edge Functions Instance",
  		"edge_function_id": 13,
  		"args": {
            "param": {
                "body": "It works!",
                "http_status": 200
		}
	}
}
~~~

**Response Example**

~~~
{
    "results": {
        "edge_function_id": 13,
        "name": "Criar Edge Functions Instance",
        "args": {
        	"param": {
                "body": "It works!",
                "http_status": 200
        },
        "id": 2361
    },
    "schema_version": 3
}
~~~

---

## 5. Overwriting Edge Functions Instances {#overwriting-functions-instances}

This return overwrites all the fields of  Edge Functions Instances, retaining the id.

If you only want to update some fields without changing the values of the rest, consider using the PATCH method, instead of PUT.

#### **PUT** */edge_applications/:edge_application_id:/functions_instances/:functions_instances_id:*

Necessary permission: **Edit Edge Applications**

**Mandatory parameters**

| Parameter                             | Description                                                  | Tipe   | Type of Data                            |
| ------------------------------------- | ------------------------------------------------------------ | ------ | --------------------------------------- |
| Authorization *(mandatory)*           | Authentication through the Token, previously created through the endpoint of [Token Creation]({% tl api_v3_authentication %}#criacao-de-token) | header | string                                  |
| Accept *(mandatory)*                  | Details about the type of return and version                 | header | string;<br>*application/json;version=3* |
| Content-Type *(mandatory)*            | The type of coding used in the Body (application/json).<br/><br/>example:<br/><br/>Content-Type: application/json | header | string                                  |
| :edge_application_id *(mandatory)*    | The id of the edge application you plan to overwrite         | path   | number                                  |
| :functions_instances_id *(mandatory)* | The id of the edge function instance you plan to overwrite   | path   | number                                  |



**Request Example**

~~~
PUT /edge_applications/16076123352/functions_instances/10764
Accept: application/json; version=3
Authorization: token ec6aabdc0b6bbeed826a36d8731630e36b6e3f24
Content-Type: application/json
~~~

~~~
{
		"name": "Sobrescrever Edge Functions Instance",
  		"edge_function_id": 13,
  		"args": {
            "param": {
                "body": "It works!",
                "http_status": 200
		}
	}
}
~~~

**Response Example**

~~~
{
    "results": {
        "edge_function_id": 13,
        "name": "Sobrescrever Edge Functions Instance",
        "args": {
        	"param": {
                "body": "It works!",
                "http_status": 200
        },
        "id": 2361
    },
    "schema_version": 3
}
~~~

---

## 6. Updating the fields of Edge Functions Instances {#updating-fields-of-functions-instances}

This return updates one or more fields of Edge Functions Instances, retaining the value of those fields not included.

#### **PATCH** /edge_applications/:edge_application_id:/functions_instances/:functions_instances_id:

Necessary permission: **Edit Edge Application**

**Mandatory parameters**

| Parameters                            | Description                                                  | Type   | Type of Data                            |
| ------------------------------------- | ------------------------------------------------------------ | ------ | --------------------------------------- |
| Authorization *(mandatory)*           | Authentication through the Token, previously created through the endpoint of [Token Creation]({% tl api_v3_authentication %}#criacao-de-token) | header | string                                  |
| Accept *(mandatory)*                  | Details about the type of return and version                 | header | string;<br>*application/json;version=3* |
| Content-Type *(mandatory)*            | The type of coding used in the Body (application/json).<br/><br/>example:<br/><br/>Content-Type: application/json | header | string                                  |
| :edge_application_id *(mandatory)*    | The id of the edge application you plan to update            | path   | number                                  |
| :functions_instances_id *(mandatory)* | The id of the edge function instance you plan to update      | path   | number                                  |



**Request Example**

~~~
PATCH /edge_applications/16076123352/functions_instances/10764
Accept: application/json; version=3
Authorization: token ec6aabdc0b6bbeed826a36d8731630e36b6e3f24
Content-Type: application/json
~~~

~~~
{
		"name": "Atualizar Edge Functions Instance",
  		"edge_function_id": 13,
  		"args": {
            "param": {
                "body": "It works!",
                "http_status": 200
		}
	}
}
~~~

**Response Example**

~~~
{
    "results": {
        "edge_function_id": 13,
        "name": "Atualizar Edge Functions Instance",
        "args": {
        	"param": {
                "body": "It works!",
                "http_status": 200
        },
        "id": 2361
    },
    "schema_version": 3
}
~~~

---

Didn't find what you were looking for? [Start a ticket with our support team.](https://tickets.azion.com/)