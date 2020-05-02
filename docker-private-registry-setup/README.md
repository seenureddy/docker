# Private Docker registry Certificate/key pair 

Info: https://docs.docker.com/registry/configuration/

`mdkdir certs`

* Copy below content to `openssl.conf` and update the docker Ip address

`[ req ]
distinguished_name = req_distinguished_name
x509_extensions     = req_ext
default_md         = sha256
prompt             = no
encrypt_key        = no

[ req_distinguished_name ]
countryName            = ""
localityName           = ""
organizationName       = ""
organizationalUnitName = ""
commonName             = "<Docker Server IP>"
emailAddress           = "test@example.com"

[ req_ext ]
subjectAltName = @alt_names

[alt_names]
DNS = "<Docker Server IP>"
`

# Generating the certificate and private key

`openssl req -x509 -newkey rsa:4096 -days 365 -config openssl.conf -keyout certs/domain.key -out certs/domain.crt`

# To verify your certificate 

`openssl x509 -text -noout -in certs/domain.crt`

# Insecure registries

* Connect to private docker registry without configuring the `https`.

add these configuration to `/etc/docker/daemon.json`

`
{
	  "insecure-registries": ["<ip>:<port>"]
}
`
* Restart the docker service

`sudo systemctl restart docker`


# Docker registry UI

https://github.com/Joxit/docker-registry-ui

https://github.com/Quiq/docker-registry-ui

# Docker-registry-info

https://github.com/Evedel/bow
https://www.macadamian.com/learn/creating-a-private-docker-registry/



