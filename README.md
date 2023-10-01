**Eureka Server: Working as a Discovery Client**

![eureka.png](asset%2Feureka.png)

**Hystrix: Fault Tolerance and Resilience** 

> Handling the Fault such as Instance Down, In this case we return data through fallback either it will come from Cache or Hard-Coded

All Instances are UP. So, Services are providing response.↴

![allup.png](asset%2Fallup.png)

_Movie-Info-Service_ is down, but we are getting response from rating service. So It only impacts on Movie Info Service else other Services are working.↴

![moviedown.png](asset%2Fmoviedown.png)

_Rating-Data-Service_ is down, but we are getting response from Movie Info Service. So now It only impacted the Rating Data Service else other Services are working.↴

![ratingdown.png](asset%2Fratingdown.png)

**Hystrix Dashboard**

Showcasing what did happen when services go down and after recovery in UI.↴

![dashboard.png](asset%2Fdashboard.png)
![abbr.png](asset%2Fabbr.png)

**Microservice Cloud Config Server**

> External Config file will override the configuration which is available in internal properties file. You can see that application name is overridden in below picture.

Why do we need that?
1. Externalised Properties So we can change the data according to environment and profile
2. For Consistency across the multiple instances of single microservice.
3. Version Control over these config properties
4. Realtime updates in value with redeploying and restarting the server

How Does it work ?
1. Properties file exits on remote git 
2. Properties file should have same name as microservice name with ext that will work as private entity accessed by particular instance else it will be treated as public.
3. Cloud Config Server always look for git changes
4. Bean should be annotated with RefreshScope annotation 
5. Note: Actuator provides manny types of hook with endpoint, in which we need to include that endpoint in application properties of that microservice project
6. After the git changes, we need to call a post method api call to the instance of that particular microservice such as : http://localhost:8081/actuator/refresh
7. Vallah Done, Properties updated with restart and redeployment

![config-server.png](asset%2Fconfig-server.png)

**Microservice Security: Encryption and Decryption for properties data**
To encrypt and decrypt properties data we can use Spring Cloud Config Server's encryption feature. Here are the steps:

There are two-way to implement Encryption and Decryption 
1. Symmetric Encryption/Decryption [Secret Key defines in bootstrap.properties]
2. Asymmetric Encryption/Decryption [Keystore generated through keytool and define in bootstrap.properties]

You need to add `{cipher}+encrypted key` like `{cipher}hg3472gsyf7t8f374tgwbddyi` in properties file.
When config server reads this value, it will decrypt it using the secret key/keystore defined in bootstrap.properties and return plain text value.
Similarly, you can encrypt values in code and store encrypted string in properties file. Config server will decrypt it automatically.

To test, you can use POST API by sending encrypted value and decrypted value.
http://127.0.0.1:8888/encrypt
![encrypt.png](asset%2Fencrypt.png)
http://127.0.0.1:8888/decrypt
![decrypt.png](asset%2Fdecrypt.png)

_**Implementation in code**_
![implementation.png](asset%2Fimplementation.png)
![user.png](asset%2Fuser.png)

    