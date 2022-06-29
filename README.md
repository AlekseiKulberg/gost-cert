# gost-cert
Creation GOST certificate on Astra Linux
установка: apt install libgost-astra

Создание ключа: 
```
openssl genpkey -algorithm gost2012_256 -pkeyopt paramset:A -out <имя ключа>
```
Создание CA-сертификата:
```
openssl req -new -x509 -days 365 -key <ключ на gost> -out <имя серта>
```
Создание запроса на серт:
```
openssl req -config <имя конфига> -new -key <имя ключа> -out <имя файла с запросом>
```

Подпись сетификата:
```
openssl -req -in <имя запроса на сертификат> -CA <корневой серт> -CAkey <ключ корневого серта> -CAcreateserial -out <имя серта сервера> -days <срок действия в днях>
```
конфиг ssl для генерации запроса (остальные конфиги по дефолту):
```
[ req ]

default_bits = 4096

distinguished_name = req_distinguished_name

req_extensions = req_ext

[ req_distinguished_name ]

countryName = Country Name (2 letter code)

countryName_default = RU

stateOrProvinceName = State or Province Name (full name)

stateOrProvinceName_default = Moscow

localityName = Locality Name (eg, city)

localityName_default = Moscow

organizationName = Organization Name (eg, company)

organizationName_default = DemoLab

commonName = Common Name (e.g. server FQDN or YOUR name)

commonName_max = 64

[ req_ext ]

subjectAltName = @alt_names

#изменить альтернативные имена!!!!!!

[alt_names]

DNS.1 = <your.server.fqdn>
#DNS.2 = <your.server.fqdn>
```
