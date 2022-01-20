# How to generate certificates

To create certificate files use `openssql`
```
openssl genrsa -out privatekey.pem 1024 --SHA-1
openssl genrsa -out privatekey.pem 2048   --SHA-256
openssl req -new -x509 -key privatekey.pem -out publickey.cer -days 10000
openssl pkcs12 -export -out public_privatekey.pfx -inkey privatekey.pem -in publickey.cer
```