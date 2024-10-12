From : https://medium.com/@pratik.941/building-rest-api-using-spring-boot-a-comprehensive-guide-3e9b6d7a8951


curl -X GET http://localhost:8080/api/books -H "Accept: application/json"

curl -X POST http://localhost:8080/api/books  -H 'Content-Type: application/json' -d '{"title": "Spring Boot in Action","author": "Craig Walls","isbn": "9781617292545"}'