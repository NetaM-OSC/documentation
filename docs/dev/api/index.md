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
