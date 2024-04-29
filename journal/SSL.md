# adding an SSL certificate

## the command

I used the following command to create the SSL certificate

```bash
openssl req -new -newkey rsa:2048 -nodes -keyout kuaminikakonbit.key -out kuaminikakonbit.csr
```


## Sources

I followed instructions [Here](https://www.ssldragon.com/how-to/install-ssl-certificate/ubuntu/)