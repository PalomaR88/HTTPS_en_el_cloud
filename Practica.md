# HTTPS
El siguiente paso de nuestro proyecto es configurar de forma adecuada el protocolo HTTPS en nuestro servidor nginx para nuestras dos aplicaciones web. Para ello vamos a emitir un certificado wildcard en la AC Gonzalo Nazareno utilizando para la petición la utilidad "gestiona".

- Debes hacer una redirección para forzar el protocolo https.

Se instala openssl:
~~~
[centos@salmorejo ~]$ sudo dnf install mod_ssl
~~~

Se crea la clave:
~~~
[centos@salmorejo ~]$ sudo openssl genrsa -out paloma.gonzalonazareno.org.key 4096
Generating RSA private key, 4096 bit long modulus (2 primes)
...............................................................................................................................................................................................................................................................................................++++
......................................................................................................................................................................................................++++
e is 65537 (0x010001)
~~~

Y se crea un fichero llamado paloma.gonzalonazareno.org.conf para la configuración del certificado:
~~~
[ req ]
default_bits       = 4096
default_keyfile    = paloma.gonzalonazareno.org.key
distinguished_name = req_distinguished_name

[ req_distinguished_name ]
countryName                 = Country Name (2 letter code)
countryName_default         = sp
stateOrProvinceName         = State or Province Name (full name)
stateOrProvinceName_default = Seville
localityName                = Locality Name (eg, city)
localityName_default        = Dos Hermanas
organizationName            = Organization Name (eg, company)
organizationName_default    = paloma 
commonName                  = Common Name (e.g. server FQDN or YOUR name)
commonName_max              = 64
commonName_default          = *.paloma.gonzalonazareno.org
~~~

Y se crea el fichero .csr:
~~~
[centos@salmorejo ~]$ sudo openssl req -new -nodes -sha256 -config paloma.gonzalonazareno.org.conf -out paloma.gonzalonazareno.org.csr
~~~

