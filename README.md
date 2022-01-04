# Mule to Splunk Demo 
    > (Splunk installation is docker based)

Files:Usage
1. Docker Compose file: to install splunk. 
2. Splunk/Dockerfile : To build splunk image. 
3. Volumes: "/opt/splunk/var" contains all the index's

############################################################################################################
## Splunk
1. Adding the HTTP Event Collector (HEC) in splunk settings.
 ![Splunk-settings](Images/Add_HEC.png)
2. Create or Assign appropriate settings and token for HEC.
 ![HEC-settings](Images/Add_HEC_DETAILS.png)
3. Check the HEC Port and disble the SSL [for Demo purpose]
 ![Global-settings](Images/Add_GLOBAL_SETTINGS.png)

############################################################################################################
## Mule Configuration
Log4j2.xml configuration in Mule

    <http name="splunk" url="http://host:port/services/collector/raw">
        <property name="Authorization" value="Splunk abcd1234"></property>
        <PatternLayout pattern="%m%n"/>
    </http>
    > Note: http://localhost:8088/services/collector/raw or http://localhost:8088/services/collector/event URLs could be used depending on what kind of messages are pushed.

############################################################################################################
## Postman -> Splunk
To Call Splunk HTTP Event Collector (HEC) from Postman or curl.

    http://localhost:8088/services/collector/raw or http://localhost:8088/services/collector/event both are fine

    curl --location --request POST 'http://localhost:8088/services/collector/raw' \
    --header 'Authorization: Basic U3BsdW5rOmFiY2QxMjM0' \
    --header 'Content-Type: application/json' \
    --data-raw '{"event": "hello Anup"}'
    
############################################################################################################
## Verification:

    1. Run the application
    2. Check logs in Splunk
