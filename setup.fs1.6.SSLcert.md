# Setup Self-signed rootCA and WebServer SSL Cert  

ref:

```
http://datacenteroverlords.com/2012/03/01/creating-your-own-ssl-certificate-authority/
http://serverfault.com/questions/476576/how-to-combine-various-certificates-into-single-pem
https://www.digicert.com/ssl-support/pem-ssl-creation.htm
```

```
ssl-cert CN: fs.192.168.42.246.xip.io
```

## Create the Root Certificate (Done Once)
### Create the Root Key

`
openssl genrsa -out rootCA.key 2048
`

### Self-sign RootCA certificate
`
openssl req -x509 -new -nodes -key rootCA.key -days 1024 -out rootCA.pem
`

**before you can start your own certificate authority, remember the trick is getting those certs in  every browser in the entire world.**


## Create A Certificate (Done Once Per Device, everytime u need on a new server)
Every device that you wish to install a trusted certificate will need to go through this process.

### create a private key (different from the root CA)
`
openssl genrsa -out server01.key 2048
`

### generate the certificate signing request
`
openssl req -new -key server01.key -out server01.csr
`

### Sign the CSR with rootCA key
`
openssl x509 -req -in server01.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server01.crt -days 3650
`

### Import rootCA into debian
ref: http://wiki.cacert.org/FAQ/ImportRootCert#Debian

### add/import rootCA into Mac OSX 10.10
http://djmadeira.com/2015/02/adding-an-ssl-certificate-to-mac-os-x-server-10-10/