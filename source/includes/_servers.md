# Servers

## Servers list

```ruby
id = '5999b763474b0eafa5fafb64bff0ba80'
response = token.get("#{api_url}/stacks/#{id}/servers.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{id}/servers HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response": [
    {
      "uid": "f8468fc145ea49bac474b30a8fea888d",
      "vendor_uid": "2492780",
      "name": "Caribou",
      "address": "146.185.133.183",
      "distro": "ubuntu",
      "distro_version": "14.04",
      "dns_record": "caribou.sb-elastic-1.dev.c66.me",
      "user_name": "root",
      "server_type": "Cloud (DigitalOcean) ",
      "server_roles": [
        "rails",
        "postgresql",
        "elasticsearch",
        "web",
        "app",
        "db"
      ],
      "server_group_id": 128,
      "stack_uid": "5acd43412ea412e32897c40d46f91183",
      "has_agent": true,
      "params":
        {
          "availability_zone": "2",
          "size": "63",
          "region": "2",
          "ips":["146.185.133.183"],
          "was_baselined": true,
          "cached_cores":1,
          "cached_memory": 1042336972,
          "passenger_version": "4.0.48",
          "passenger_enterprise": false,
          "supports_nginx_realip": true,
          "passenger_pool_max": 4
        },
      "created_at": "2014-08-29T17:21:47Z",
      "updated_at": "2014-08-29T17:54:41Z",
      "region":"2",
      "availability_zone": "2",
      "ext_ipv4": "146.185.133.183",
      "health_state": 3,
      "int_ipv4": "146.185.133.183",
      "int_ipv6": null,
      "ext_ipv6": null
    }
  ],
  "count":1,
  "pagination":
    {
      "previous": null,
      "next": null,
      "current": 1,
      "per_page": 30,
      "count": 1,
      "pages": 1
    }
}
```

Get list of all servers of stack

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{id}/servers`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`

## Servers

```ruby
stack_id = 'a6b583684833a2cf4845079c9d9350a8'
id = 'f8468fc145ea49bac474b30a8fea888d'
response = token.get("#{api_url}/stacks/#{stack_id}/servers/#{id}.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{stack_id}/servers/{id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":
    {
      "uid": "f8468fc145ea49bac474b30a8fea888d",
      "vendor_uid": "2492780",
      "name": "Caribou",
      "address": "146.185.133.183",
      "distro": "ubuntu",
      "distro_version": "14.04",
      "dns_record": "caribou.sb-elastic-1.dev.c66.me",
      "user_name": "root",
      "server_type": "Cloud (DigitalOcean) ",
      "server_roles":[
        "rails",
        "postgresql",
        "elasticsearch",
        "web",
        "app",
        "db"
      ],
      "server_group_id": 128,
      "stack_uid": "5acd43412ea412e32897c40d46f91183",
      "has_agent": true,
      "params":
        {
          "availability_zone": "2",
          "size": "63",
          "region": "2",
          "ips":["146.185.133.183"],
          "was_baselined": true,
          "cached_cores": 1,
          "cached_memory": 1042336972,
          "passenger_version": "4.0.48",
          "passenger_enterprise": false,
          "supports_nginx_realip": true,
          "passenger_pool_max":4
        },
       "created_at": "2014-08-29T17:21:47Z",
       "updated_at": "2014-08-29T17:54:41Z",
       "region": "2",
       "availability_zone": "2",
       "ext_ipv4": "146.185.133.183",
       "health_state":3,
       "int_ipv4": "146.185.133.183",
       "int_ipv6": null,
       "ext_ipv6": null
    }
}
```

Get information of a single server

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{stack_id}/servers/{id}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
id | **required** | string | The server ID | `f8468fc145ea49bac474b30a8fea888d`
include_private_key | optional | integer | if set to `1` then private_key will included in response | `1`

## Reboot server

```ruby
stack_id = 'a6b583684833a2cf4845079c9d9350a8'
response = token.post("#{api_url}/stacks/#{stack_id}/servers/#{server_id}/reboot_server"

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/servers/#{server_id}/reboot_server HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":
    {
      "id":10,
      "user":"test@cloud66.com",
      "resource_type":"stack",
      "action":"server_reboot",
      "resource_id":"283",
      "started_via":"api",
      "started_at":"2016-01-01T19:08:05Z",
      "finished_at":null,
      "finished_success":null,
      "finished_message":null
    }
}
```

You can use this method to reboot a speific server of a stack.

<aside class="notice">
<b>Scope:</b> <i>reboot</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/servers/#{server_id}/reboot_server`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`
server_id | **required** | string | Unique identifier of the server | `f8468fc145ea49bac474b30a8fea888d`

