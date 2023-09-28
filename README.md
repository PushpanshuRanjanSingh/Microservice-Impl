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
