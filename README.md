# iOS and Android: Sample library and application

*Version 1.2*

Create an iOS or Android library, and a simple app that uses the
library.  The library should:

+ Provide an endpoint/function that collects as much device
  information as possible (device name, model, IP address etc),
  encrypts and hashes it with a pre-defined secret, and returns the
  encrypted blob.
  
+ Provide an endpoint/function that calls a REST API endpoint and
  delivers the encrypted blob with an application defined tag.

Remember:
    
+ Good coding practices for your language and platform
+ Tests, tests, tests.
+ Create a github, gitlab or bitbucket repository for your code and
  share with us when done.
+ Include a README as documentation of your notes, approach, results
  etc.
  
## Device information

Generate as much device information as you can, store it in a JSON
blob, and encrypt and hash it.

Use AES encryption with the key and (optionally) the iv below, and
then perform a SHA1 hash of the result.  If you have issues using the
key in the format below, generate an AES key, and send it to us via
email.

    key=8C182623CD047A0D6593691B2179B98440A91AF01E4BB2BD90D49CC9E9D171E7
    iv =8DB023E39C39B95EBC0155DA9F14C37D


## Rest API call

API endpoint: `https://api-staging.ravelin.com/v2/customer`
API key: `secret_key_live_1Od41KPkFXqn9gR4KB8s5l3hvOaGAYqs`

The `/v2/customer` API documentation [here](https://developer.ravelin.com/apis/v2/#postv2customer).
More info on the Ravelin API is available [here](https://developer.ravelin.com/apis/v2/#postv2customer)

Use your email address as customerId, and use the encrypted and hashed
blob as a custom parameter called `deviceInfo`.  Sample values for
other parameters can be taken from the example in the documentation.

```POST /v2/customer
Authorization: token $key
Content-Type: application/json

{
    "timestamp": now(),
    "customer": {
        "customerId": "$email",
        "email": "$email",
        "name": "$name"
    },
    "device": {
        ..., 
        "custom": {
            ...
        }
    }
}
```

## Test application

The test application can be as simple as needed, a single screen with
a button for each function call in the library will be enough.

