# NTPClient 

Connect to a NTP server, here is how:

```cpp
#include <NTPClient.h>
// change next line to use with another board/shield
#include <ESP8266WiFi.h>
//#include <WiFi.h> // for WiFi shield
//#include <WiFi101.h> // for WiFi 101 shield or MKR1000
#include <WiFiUdp.h>

const char *ssid     = "<SSID>";
const char *password = "<PASSWORD>";

WiFiUDP ntpUDP;

// By default 'time.nist.gov' is used.
NTPClient timeClient(ntpUDP);

// You can specify the time server pool and the offset, (in seconds)
// additionaly you can specify the update interval (in milliseconds).
// NTPClient timeClient("europe.pool.ntp.org", 3600, 60000);

void setup(){
  Serial.begin(11520);
  WiFi.begin(ssid, password);

  while ( WiFi.status() != WL_CONNECTED ) {
    delay ( 500 );
    Serial.print ( "." );
  }

}

void loop() {
  timeClient.update();
  
  Serial.println(timeClient.getFormattedTime());
  
  delay(1000);
}
```
