# Cisco DNA Spaces Firehose API Sample Application - Detect And Locate

To realise the use case "Detect and Locate", this sample application consumes "Device Location Update" Event of the Cisco DNA Spaces Firehose API. This can be used as a starting point and reference for consuming the Cisco DNA Spaces Firehose API events.

Sample Application consists of 3 components namely
1) API Server
2) Proxy Server
3) Client

## 1) API Server
The API Server consumes "Device Location Update" event and keeps updating Redis cache for each Device MAC address. Server also exposes an HTTP GET API which can be invoked with a MAC address param(mac), to get recent location update for the given mac


### Steps to run the API Server application
1) Clone the Repository server folder
2) Update app.properties file (/server/src/main/resources/app.properties) with appropriate values. All the below mentioned properties are mandatory.
```properties

api.key={{Firehose API Key}}
api.url={{Firehose API URL}}

http.port={{http server port}}

```
3) Build the project by using ```mvn install```.
4) Set the classes folder path in the classspath and execute com.cisco.dnaspaces.APIConsumer class to run the application.


## 2) Proxy Server
Proxy Server is used to avoid CORS restriction while using the partners api for retrieving map information and image from client application. This takes the request and communicates with API and serves response to client application without any CORS Restriction

### Steps to run the Proxy Server application
1) Clone the Repository client folder
2) Rename or copy /proxy-server/proxy-server.template.properties file to /proxy-server/proxy-server.properties and update below mentioned properties with appropriate Partners API details
```properties

apiserver.host={{Partners API Host}}
apiserver.apikey={{Partners API Key}}

```
3) In console move to /client directory of project
4) Start the node server using command ```node server```

## 3) Client

The client application provides an UI to enter MAC address of client and when user clicks on "start polling", Ajax polling starts with a certain time interval to server. On each location update, co-ordinates are stacked to the screen.

### Steps to run the Client application
1) Clone the Repository client folder
2) Rename or copy /client/src/environments/environment.template.ts file to /client/src/environments/environment.ts and update below mentioned properties with appropriate Partners API details
```json
  {
  "apiUrl":"{{API Server url}}",
  "serverUrl":"{{Proxy Server url}}"
  }

```
3) In console move to /client directory of project
4) Start the Angular application by using command ```ng serve```

### DEMO
Once all the applications are started,
1) Client UI can be accessed by opening http://localhost:4200 in the browser.
3) By providing the Device MAC Address, Device can be detected and located.
4) Given user current location is plotted in the map using small red dot icon.
5) Given user locatoin updates starting from the time of request are listed below the map
