Nodemcu code for underwater sensor node



#include <SoftwareSerial.h>
#include <ArduinoJson.h>

#ifdef ESP32
  #include <WiFi.h>
  #include <HTTPClient.h>
#else
  #include <ESP8266WiFi.h>
  #include <ESP8266HTTPClient.h>
  #include <WiFiClient.h>
#endif

SoftwareSerial wifi_end(D5,D6);//rx tx

this is for my wifi collaboration
// Replace with your network credentials
const char* ssid     = "nahin";
const char* password = "nahin12345";

// REPLACE with your Domain name and URL path or IP address with path
const char* serverName = "http://hexagonal-millimete.000webhostapp.com/uncoll.php";


// Keep this API Key value to be compatible with the PHP code provided in the project page. 
// If you change the apiKeyValue value, the PHP file /post-esp-data.php also needs to have the same key 
String apiKeyValue = "1234";

String sensorName = "pH_Temp_PIR";
String sensorLocation = "Padma";
float time_lap=0;
String sen1;
String sen2;
String sen3;


void setup() 
{
  wifi_end.begin(9600);
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  Serial.println("Connecting");
  
  while(WiFi.status() != WL_CONNECTED) 
  { 
    delay(500);
    Serial.print(".");
  }
  
  Serial.println("");
  Serial.print("Connected to WiFi network with IP Address: ");
  Serial.println(WiFi.localIP());
  pinMode(D7, OUTPUT);
  pinMode(2, OUTPUT);
  digitalWrite(D7, 0);
}

void loop() 
{
    //receiving data from Arduino_end
    wifi_end.write("s");
    if (wifi_end.available()>0)
    {
      sen1=wifi_end.readStringUntil('\n');
      Serial.println(sen1);
    }
    
    wifi_end.write("k");
    if (wifi_end.available()>0)
    {
      sen2=wifi_end.readStringUntil('\n');
      Serial.println(sen2);
    }

    wifi_end.write("l");
    if (wifi_end.available()>0)
    {
      sen3=wifi_end.readStringUntil('\n');
      Serial.println(sen3);
    }
        
    //Post Request:
 
    //Check WiFi connection status
     if(WiFi.status()== WL_CONNECTED){
     HTTPClient http;
    
    // Your Domain name with URL path or IP address with path
     http.begin(serverName);
    
    // Specify content-type header
     http.addHeader("Content-Type", "application/x-www-form-urlencoded");
    
    // Prepare your HTTP POST request data
    String httpRequestData = "api_key=" + apiKeyValue + "&sensor=" + sensorName
                          + "&location=" + sensorLocation + "&value1=" + String(sen1)
                          + "&value2=" + String(sen2) + "&value3=" + String(sen3) + "";
    Serial.print("httpRequestData: ");
    Serial.println(httpRequestData);
    
    //Send HTTP POST request
    int httpResponseCode = http.POST(httpRequestData);
  
    if (httpResponseCode>0) 
    {
      Serial.print("HTTP Response code: ");
      Serial.println(httpResponseCode);
    }
    else 
    {
      Serial.print("Error code: ");
      Serial.println(httpResponseCode);
    }
    // Free resources
    http.end();
  }
  else 
  {
    Serial.println("WiFi Disconnected");
  }

  //GET Request:

    if (WiFi.status() == WL_CONNECTED) 
    {
     HTTPClient http;
     http.begin("http://hexagonal-millimete.000webhostapp.com/status.php?id=1");
     int httpCode = http.GET();
     //Check the returning code                                                                  
     if (httpCode > 0) 
    {
     // Parsing
       const size_t bufferSize = JSON_OBJECT_SIZE(2) + JSON_OBJECT_SIZE(3) + JSON_OBJECT_SIZE(5) + JSON_OBJECT_SIZE(8) + 370;
       DynamicJsonBuffer jsonBuffer(bufferSize);
       JsonObject& root = jsonBuffer.parseObject(http.getString());
       int id = root["id"]; // 1
       const char* state = root["status"]; 
       Serial.print("ID:");
       Serial.println(id);
       Serial.print("Status:");
       Serial.println(state);
       String led = root["status"];
       digitalWrite(2, LOW); 
       //delay(200);   
       digitalWrite(2, HIGH);  
       //delay(200);                         
       if (led=="ON" )
       { 
        digitalWrite(D7, 1);  
        Serial.print("ON");       
       }
       else 
       {
        digitalWrite(D7, 0); 
        Serial.print("OFF");
       }     
    }
    http.end(); 
  }
  delay(1000);
}




code description:
The nodeMCU ESP-8266 collects all the real time data from the sensor part and sent them to cloud storage via an asynchronous reception and transmission communication system. All the data is stored in online database. The cloud database along with an apache http server can store around 1GB of files. Here point should be noted that, sensor reading data is only of 1.5-2Kb. All the fetched data are showed in the table of developed website. By login into it with proper password one user can see all the data and can control the module from any place of the world. 





code output:


code output is showoed in picture 2