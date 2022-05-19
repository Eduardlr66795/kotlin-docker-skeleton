# KOTLIN SPRINGBOOT SKELETON
The following code example serves as a skeleton structure to building a service using Maven, Kotlin, Springboot and a MySQL database. 

## RUNNING THE APPLICATION
The application can be run in one of two ways:     

    1. Manually - This would require you to setup the database and run the migrations via liquibase  
    2. Docker - As with all things docker, things will happen automagically

### <u> RUNNING THE APPLICATION: MANUALLY </u>
STEP 01: DATABASE SETUP

Before we can run the application locally we need to ensure that the database has been created and 
the configuration in the application has been updated accordingly. 

        Command 01 : $mysql -h localhost -P 3306 -u {USERNAME} -p {PASSWORD}
    
        Command 02: $CREATE DATABASE skeleton;
    
        Command 03: $SHOW DATABASE;

        Command 04: EXIT;

        Command 05: mvn liquibase:update


STEP 02: RUNNING THE APPLICATION

Once the database has been setup, you can now run the application using the folowing command
        
        mvn spring-boot:run

STEP 03: TESTING THE APPLICATION
        
The application can be tested with the following two endpoints that we created.

    Endpoint 01: POST (create-user-entry) this endpoint can be used to create and persist a new user entry into the databse. 

    NOTE: The email & phone values have to be unique otherwise the application will raise an exception

        curl -X "POST" "http://localhost:8080/api/v1/create-user-entry?first_name=Eddie&last_name=Le%20Roux&email=eduardlero2ux1%40gmail.com&phone=07272964992" \
            -H 'Content-Type: application/json; charset=utf-8' \
            -H 'Cookie: JSESSIONID=3E9A419E8768C41E82FF9B5A6B17B2BE' \
            -d $'{}'
        
    ------------------
    
    Endpoint 02: GET (find-user-entry) - This endpoint is used to find a user-entry using the ID of the entry.

        curl "http://localhost:8080/api/v1/find-user-entry?user_id=3" \
            -H 'Content-Type: application/json; charset=utf-8' \
            -H 'Cookie: JSESSIONID=3E9A419E8768C41E82FF9B5A6B17B2BE' \
            -d $'{}'

### <u> RUNNING THE APPLICATION: DOCKER </u>
STEP 01: RUNNING THE APPLICATION
    
Running the application via Docker, the database setup & migrations will be run as part of the
build phase. You won't have to do any of the setup yourself. Simply run the following command
it will ensure that the database is setup and the migrations are completed before the service 
starts. 

     bash buildFile.sh

STEP 02: TESTING THE APPLICATION

Testing the application can be done by opening a new terminal window and running the following 
curl commands. 

    Endpoint 01: POST (create-user-entry) this endpoint can be used to create and persist a new user entry into the databse. 

    NOTE: The email & phone values have to be unique otherwise the application will raise an exception

        curl -X "POST" "http://localhost:8080/api/v1/create-user-entry?first_name=Eddie&last_name=Le%20Roux&email=eduardlero2ux1%40gmail.com&phone=07272964992" \
            -H 'Content-Type: application/json; charset=utf-8' \
            -H 'Cookie: JSESSIONID=3E9A419E8768C41E82FF9B5A6B17B2BE' \
            -d $'{}'
        
    ------------------
    
    Endpoint 02: GET (find-user-entry) - This endpoint is used to find a user-entry using the ID of the entry.

        curl "http://localhost:8080/api/v1/find-user-entry?user_id=3" \
            -H 'Content-Type: application/json; charset=utf-8' \
            -H 'Cookie: JSESSIONID=3E9A419E8768C41E82FF9B5A6B17B2BE' \
            -d $'{}'
