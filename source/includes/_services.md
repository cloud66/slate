# Services

## Services list

```ruby
id = 'a6b583684833a2cf4845079c9d9350a8'
response = token.get("#{api_url}/stacks/#{id}/services.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{id}/services HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response": [
    {
      "name": "web",
      "containers": [
        {
          "uid": "1339d2dfa5a86dfce497f8f2e1bb29492f246288c722d11c8e6fc9348bfeece6",
          "server_uid": "edfbd7a9b97e999ebf17984282d4b457",
          "server_name": "Cormorant",
          "service_name": "web",
          "image": "quay.io/cloud66/sample-rails",
          "port_list": "[\"5128:3000\"]",
          "command": "rackup -p 3000",
          "started_at": "2014-09-30T09:59:45Z",
          "web_ports": "80:443",
          "created_at": "2014-09-30T09:59:45Z",
          "updated_at": "2014-09-30T09:59:48Z"
        }
      ]
    }
  ],
  "count": 1,
  "pagination": {
    "previous": null,
    "next": null,
    "current": 1,
    "per_page": 30,
    "count": 1,
    "pages": 1
  }
}
```

Get a list of all services of the stack

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{id}/services`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
server_uid | optional | string | Server UID | `1239b763474b0eafa5fafb64bff0ba80`

## Service show

```ruby
stack_id = 'ec28beaa0e324c21ab2f9c5a153189a2'
id = 'web'
response = token.get("#{api_url}/stacks/#{stack_id}/services/#{id}.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{stack_id}/services/{id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response": {
    "name": "web",
    "containers": [
      {
        "uid": "1339d233a5a86dfce497f8f2e1bb29492f246288c722d11c8e6fc9348bfeece6",
        "server_uid": "1239b763474b0eafa5fafb64bff0ba80",
        "server_name": "Cormorant",
        "service_name": "web",
        "image": "quay.io/cloud66/sample-rails",
        "port_list": "[\"5128:3000\"]",
        "command": "rackup -p 3000",
        "started_at": "2014-09-30T09:59:45Z",
        "web_ports": "80:443",
        "created_at": "2014-09-30T09:59:45Z",
        "updated_at": "2014-09-30T09:59:48Z"
      }
    ]
  }
}
```

Get information of a service of the stack

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{stack_id}/services/{id}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
id | **required** | string | The service name | `web`
server_uid | optional | string | Server UID | `1239b763474b0eafa5fafb64bff0ba80`

## Service scale

```ruby
stack_id = 'ec28beaa0e324c21ab2f9c5a153189a2'
id = 'web'
response = token.post("#{api_url}/stacks/#{stack_id}/services.json", {body: {:service_name => id}})

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/services HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response": {
    "id": 1234,
    "user": "theuser@yourdomain.com",
    "resource_type": "stack",
    "action": "service_scale",
    "resource_id": "15633",
    "started_via": "api",
    "started_at": "2014-09-30T11:36:58Z",
    "finished_at": null,
    "finished_success": null,
    "finished_message": null
  }
}
```

Scale the given service over the stack

<aside class="notice">
<b>Scope:</b> <i>admin</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/services`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
service_name | **required** | string | The service name | `web`
server_count | optional | string | A hash of server uid to count of containers desired on that server | `{"123123cfcb7d3d2b54614b19e2a6c673":2}`
server_group_count | optional | string | A hash of server_group to count of containers across the servers of that group | `{"web":4}`

## Service stop

```ruby
stack_id = 'ec28beaa0e324c21ab2f9c5a153189a2'
id = 'web'
response = token.delete("#{api_url}/stacks/#{stack_id}/services/#{id}.json")

puts JSON.parse(response.body)['response']
```

```http
DELETE /stacks/{stack_id}/services/{id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response": {
    "id": 1234,
    "user": "theuser@yourdomain.com",
    "resource_type": "stack",
    "action": "service_stop",
    "resource_id": "15633",
    "started_via": "api",
    "started_at": "2014-09-30T11:36:58Z",
    "finished_at": null,
    "finished_success": null,
    "finished_message": null
  }
}
```

Stop all of the given service on the stack (across all servers, unless `server_uid` is supplied)

<aside class="notice">
<b>Scope:</b> <i>admin</i>
</aside>

### HTTP Request

`DELETE /stacks/{stack_id}/services/{id}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
id | **required** | string | The service name | `web`
server_uid | optional | string | Server UID | `1239b763474b0eafa5fafb64bff0ba80`
