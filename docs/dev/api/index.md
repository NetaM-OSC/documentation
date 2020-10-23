# API documentation

All API except token generation are automatically documented directly inside application throught swagger.  
Internal documentation is accessible throught the url `http://<netam_host>/docs` when you're logged in.

## Get token

NetAM use oauth mechanism to provide tokens.  
To request token, you must send POST request to endpoint `http://<netam_host>/oauth/token` and fill form datas :

- username : <mail_address>
- password : <associated_password>
- grant_type : password

Token validity are limited to one day next to generation.

**The token must be declared in each API request into headers with format `'Authorization: Bearer <getted_token>'`**

### Request answer

This request give you an answer like:

```json
{
    "access_token": "zmL0UxPjqJhfzSXDcbjJp7Hs6wr6JF6SnHp1ybxBH_o",
    "token_type": "Bearer",
    "expires_in": 430010,
    "created_at": 1597607513
}
```

### Example

```bash
curl --location \
     -XPOST 'http://localhost:3000/oauth/token' \
     --form 'username=toto@me.com' \
     --form 'password=azazazazazaz' \
     --form 'grant_type=password'
```

## Sections

### Get Sections list

You could retrieve a list of all sections you was granted in software.

| Type   | Value                                 |
| ------ | ------------------------------------- |
| Method | GET                                   |
| URL    | http://<netam_server>/api/v1/sections |

#### Request answer

```json
[
  {
    "id": 2,
    "name": "example_v6",
    "description": "This section is designed for example with IPv6",
    "network": "::/124",
    "schedule": ""
  },
  {
    "id": 1,
    "name": "example_v4",
    "description": "This section is designed for example with IPv4",
    "network": "127.0.0.0/24",
    "schedule": ""
  }
]
```

#### Example

```bash
curl --location \
     -XGET 'http://<netam_host>/api/v1/sections' \
     --header 'Authorization: Bearer zmL0UxPjqJhfzSXDcbjJp7Hs6wr6JF6SnHp1ybxBH_o'
```

### Create Sections

You could create sections throught API if account as required hability.

| Type   | Value                                 |
| ------ | ------------------------------------- |
| Method | POST                                  |
| URL    | http://<netam_server>/api/v1/sections |

#### Request answer

```json
{
    "id": 3,
    "name": "example_api",
    "description": null,
    "network": "127.0.0.0/25",
    "schedule": ""
}
```

#### Example

```bash
curl --location \
     -XGET 'http://<netam_host>/api/v1/sections' \
     --header 'Authorization: Bearer zmL0UxPjqJhfzSXDcbjJp7Hs6wr6JF6SnHp1ybxBH_o' \
     -d '{
"id": 3,
"name": "example_api",
"description": null,
"network": "127.0.0.0/25",
"schedule": ""
}'
```

### Get Section details

You could retrieve details of specific section.

| Type   | Value                                              |
| ------ | -------------------------------------------------- |
| Method | GET                                                |
| URL    | http://<netam_server>/api/v1/sections/<section_id> |

#### Request answer

```json
[
  {
    "id": 1,
    "name": "example_v4",
    "description": "This section is designed for example with IPv4",
    "network": "127.0.0.0/24",
    "schedule": ""
  }
]
```

#### Example

```bash
curl --location \
     -XGET 'http://<netam_host>/api/v1/sections/1' \
     --header 'Authorization: Bearer zmL0UxPjqJhfzSXDcbjJp7Hs6wr6JF6SnHp1ybxBH_o'
```

### Launch section scan

You could launch section scan.

| Type   | Value                                                   |
| ------ | ------------------------------------------------------- |
| Method | POST                                                    |
| URL    | http://<netam_server>/api/v1/sections/<section_id>/scan |

#### Request answer

```json
{
  "status": "ack"
}
```

#### Example

```bash
curl --location \
     -XPOST 'http://<netam_host>/api/v1/sections/1/scan' \
     --header 'Authorization: Bearer zmL0UxPjqJhfzSXDcbjJp7Hs6wr6JF6SnHp1ybxBH_o'
```