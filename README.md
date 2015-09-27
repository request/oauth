
# request-oauth


## Options

###### Required

- **oauth** `{}` see below
- **uri** `url.parse()`'d object
- **method** `GET` | `POST` ..

###### Optional

- **query** `a=1&b=2`
- **form** `a=1&b=2`
- **body** `{a:1,b:2}`


## OAuth Options

###### Required

- **consumer_key** OAuth application key
- **consumer_secret** OAuth application secret
- **private_key** in [PEM format][pem-format], set this key instead of `consumer_secret` when using `RSA-SHA1` signing
- **token** user's access token
- **token_secret** user's token secret

###### Defaults

- **version** **`1.0`**
- **signature_method** **`HMAC-SHA1`** | `RSA-SHA1` | `PLAINTEXT`
- **transport_method** [type][transport-method] **`header`** | `query` | `form`

###### Generated

- **timestamp**
- **nonce**
- **signature**

###### Optional

- **realm** 
- **body_hash** pass you own [Body Hash][body-hash] as string or pass `true` to get one generated for you


## Result

###### Error

```js
var result = oauth(options)
if (result instanceof Error) {
  // handle error
}
```

###### Success

```js
var result = oauth(options)

var transport = options.oauth.transport_method || 'header'
if (transport === 'header') {
  req.headers['authorization'] = result
}
else if (transport === 'query') {
  // append result to your querystring
}
else if (transport === 'body') {
  // append result to your form body
}
```


  [pem-format]: http://how2ssl.com/articles/working_with_pem_files/
  [body-hash]: https://oauth.googlecode.com/svn/spec/ext/body_hash/1.0/oauth-bodyhash.html
  [transport-method]: http://oauth.net/core/1.0/#consumer_req_param
