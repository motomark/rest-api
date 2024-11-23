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

## Testing

Read this:
https://www.baeldung.com/spring-boot-testing


https://medium.com/simform-engineering/testing-spring-boot-applications-best-practices-and-frameworks-6294e1068516


## Building Docker image

https://spring.io/guides/gs/spring-boot-docker

## Telepresence

https://www.getambassador.io/docs/telepresence/latest/quick-start

1. The command I used:

```
telepresence connect
```

```
telepresence intercept book-deployment --port 443:443 --env-file ~/example-service-intercept.env
```

2. Need the following configuration in VSCode point the envFile to the ~/example-service-intercept.env file with environment variables.
```
"configurations": [
        {
            "type": "java",
            "name": "Spring Boot-RestApiApplication<rest-api>",
            "request": "launch",
            "cwd": "${workspaceFolder}",
            "mainClass": "com.example.restapi.RestApiApplication",
            "projectName": "rest-api",
            "args": "",
            "envFile": "/Users/markhawkins/example-service-intercept.env"
        }
    ]
```

3. Then browse to any one of the nodes to pick up the NodePort service. This will route back to vscode n the laptop e.g. where we ran telepresence from (127.0.0.1)

https://192.168.64.4:30001/api/books
(see deploy.yaml)

With telepresence status we get: 

```
Using Deployment book-deployment
   Intercept name         : book-deployment
   State                  : ACTIVE
   Workload kind          : Deployment
   Destination            : 127.0.0.1:443
   Service Port Identifier: 443/TCP
   Volume Mount Error     : sshfs is not installed on your local machine
   Intercepting           : all TCP connections
markhawkins@Marks-MacBook-Pro ~ % telepresence status                                                                                 
OSS User Daemon: Running
  Version           : 2.20.0
  Executable        : /usr/local/bin/telepresence
  Install ID        : fbd4c5e0-d44c-4eee-a94b-3205812e1f9e
  Status            : Connected
  Kubernetes server : https://192.168.64.3:6443
  Kubernetes context: default
  Namespace         : default
  Manager namespace : ambassador
  Intercepts        : 1 total
    book-deployment: markhawkins@Marks-MacBook-Pro.local
OSS Root Daemon: Running
  Version    : v2.20.0
  DNS        : 
    Remote IP       : 127.0.0.1
    Exclude suffixes: [.com .io .net .org .ru]
    Include suffixes: []
    Timeout         : 8s
  Subnets    : (4 subnets)
    - 10.43.0.0/16
    - 10.42.0.0/24
    - 10.42.1.0/24
    - 10.42.2.0/24
  Never Proxy: (1 subnets)
    - 192.168.64.3/32
OSS Traffic Manager: Connected
  Version      : v2.20.0
  Traffic Agent: ghcr.io/telepresenceio/tel2:2.20.0
```






