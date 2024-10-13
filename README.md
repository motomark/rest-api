## Enable REST:
https://medium.com/@pratik.941/building-rest-api-using-spring-boot-a-comprehensive-guide-3e9b6d7a8951

## Use HTTPS:
https://medium.com/@ankita.ashreet/securing-your-spring-boot-app-a-guide-employing-https-with-self-signed-certificates-b16f16ca25d6

and

https://www.geeksforgeeks.org/how-to-enable-https-in-spring-boot-application/

## To extract the certificate from the keystore:
https://docs.redhat.com/en/documentation/red_hat_jboss_data_virtualization/6.2/html/security_guide/extract_a_self-signed_certificate_from_the_keystore#Extract_a_Self-signed_Certificate_from_the_Keystore


## Basic Curl requests.
```
curl -X GET http://localhost:8080/api/books -H "Accept: application/json"
```

```
curl -X POST http://localhost:8080/api/books  -H 'Content-Type: application/json' -d '{"title": "Spring Boot in Action","author": "Craig Walls","isbn": "9781617292545"}'
```

## Curl requests using the extracted self-signed certificate.

POST request over https:
```
curl --cacert public.cert -X POST https://localhost/api/books  -H  'Content-Type: application/json' -d '{"title": "Spring Boot in Action","author": "Craig Walls","isbn": "9781617292545"}'
```
Using a GET request over https:
```
curl --cacert public.cert -X GET https://localhost/api/books -H "Accept: application/json"
```