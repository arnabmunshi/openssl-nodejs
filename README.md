### Set OpenSSL globally

```bash
# If you have git installed then copy the following path and set as environment path variable
C:\Program Files\Git\usr\bin
```

### Check OpenSSL

```bash
$ openssl
OpenSSL> exit
```

### Generate a Private Key

```bash
$ openssl genrsa -out key.pem
```

### Create a CSR using private key

```bash
$ openssl req -new -key key.pem -out csr.pem
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) []:
Organization Name (eg, company) [Internet Widgits Pty Ltd]:INT
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:
Email Address []:arnab.munshi@indusnet.co.in

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

### Generate SSL certification from CSR

```bash
$ openssl x509 -req -days 365 -in csr.pem -signkey key.pem -out cert.pem
```

### Include the Node default packages

```js
var https = require("https");
const path = require("path");
const fs = require("fs");
```

### Modifiy the create server method

```js
var server = https.createServer(
  {
    key: fs.readFileSync(path.join(__dirname, "../cert/key.pem")),
    cert: fs.readFileSync(path.join(__dirname, "../cert/cert.pem")),
  },
  app
);
```

### Run it on browser

```
https://localhost:3000
```
