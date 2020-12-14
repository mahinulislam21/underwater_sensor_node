dynamic sleep awake protocol code:




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
digitalWrite(2, LOW); // if delay(200) 
digitalWrite(2, HIGH); // if delay(200);                         
 if (led=="ON" )
{ 
digitalWrite(D7, 1);  
Serial.print("ON");       
 }
 else 
digitalWrite(D7, 0); 
 Serial.print("OFF");
 }     
 } 
code output:
 we have established a deep sleep/awake dynamic power management scheme for the sensor node. The sensor node is connected to the cloud server with IoT platform ESP-8266. We have seen when ESP-8266 goes to deep sleep, the node goes automatically off from recording data and it starts taking reading again when ESP-8266 wakes up from sleep. This full procedure can also be controlled by the designated website control panel section which is discussed at chapter 3-section 3.4. next chapter discusses on the future possibilities on our designed wireless underwater sensor node (UWSN) 