# Spring-Email-Verification
A Spring Boot project to send and verify email using tokens

# Prerequisite:
1. Node.js installed

# How to install:

There are two ways by which you can try this out:
Easy way is to use Docker:
```
docker pull ritish56/spring-email-verification
```
Then, to run the docker image:
```
docker run -p 8090:8090 ritish56/spring-email-verification
```
You also need to start Maildev. To do so, in separate terminal, give command:
```
docker pull maildev/maildev
```
Then, run the maildev with the required port:
```
docker run -p 1025:1025 -p 1080:1080 maildev/maildev
```

And the second way is to clone the repo if you don't have docker. In terminal:

````
git clone https://github.com/ritish78/Spring-Email-Verification.git
````

Then, after this repository is installed. Open the project in IDE using Maven. Then in terminal of IDE,

````
mvn clean install
````

Before starting the Spring Boot application, you need to install [Maildev](https://github.com/maildev/maildev). 
To install Maildev, you can follow their Readme for latest updates or you can follow:

First verify if Node is installed or not. In terminal run:
````
Node -v
````
If it shows any version like: 
````
v15.14.1
````
then, Node is installed properly. If not install [Node](https://nodejs.org/en/).
If Node is installed then in terminal:
````
npm install -g maildev
````
Then, after the installation of maildev, type in terminal:
````
maildev
````
Maildev should start on Port 1080. [Link](http://localhost:1080/#/)

Then, run the Spring Boot application by:
````
mvn spring-boot:run
````

Tomcat should start on port 8090.

# Usage:

* Creating a user using Postman. Send a POST request to: http://localhost:8090/api/v1/registration with JSON body of User.
````
{
    "firstName": "Ritish",
    "lastName": "Testing",
    "email": "ritish78@email.com",
    "password": "password"
}
````

![In Postman creating a user](https://user-images.githubusercontent.com/36816476/105572756-40a1c100-5dad-11eb-9d81-fb7e8c0217ac.PNG)

* Checking the user in database. Here, we are using H2 database.
![User in database before accepting the token](https://user-images.githubusercontent.com/36816476/105572898-ff5de100-5dad-11eb-96c9-506539ae71c9.PNG)
We can see that the user is not enabled by default, as the email verification is not done.

* Checking the created token in databse.
![Confirmation Token](https://user-images.githubusercontent.com/36816476/105572927-2e745280-5dae-11eb-9ae6-526bd4dfb765.PNG)

* In [Mail Service](http://localhost:1080/#/), we get an email for confirmation:
![Confirmation Email](https://user-images.githubusercontent.com/36816476/105572974-67142c00-5dae-11eb-8c7e-f7cbc9a9610e.PNG)

* Then after the user clicks the 'Activate Now' link:
![After clicking the Activate Now in mail](https://user-images.githubusercontent.com/36816476/105572986-83b06400-5dae-11eb-8ac3-34e3d57a7421.PNG)

* After the activation of the email is successful, we can see in AppUser table, 'Enabled' column is true for the verified user.
![After the user clicks Activate Now, the email is enabled](https://user-images.githubusercontent.com/36816476/105573018-b78b8980-5dae-11eb-9050-1e85d0c8c32b.PNG)
