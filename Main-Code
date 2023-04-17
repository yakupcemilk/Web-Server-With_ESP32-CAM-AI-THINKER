#include <WiFi.h>
#include <AsyncTCP.h>
#include <ESPAsyncWebServer.h>

const char* ssid = "your_SSID";
const char* password = "your_PASSWORD";

AsyncWebServer server(80);

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  Serial.println("Connected to WiFi");

  server.on("/capture", HTTP_GET, [](AsyncWebServerRequest *request){
    String html = "<html><body><img src=\"/photo.jpg\"></body></html>";
    request->send(200, "text/html", html);
  });

  server.on("/photo.jpg", HTTP_GET, [](AsyncWebServerRequest *request){
    String response = "HTTP/1.1 200 OK\r\n";
    response += "Content-Type: image/jpeg\r\n";
    response += "Content-Disposition: inline; filename=photo.jpg\r\n";
    response += "Connection: close\r\n\r\n";
    request->send(response.c_str(), response.length());
  });

  server.begin();
  Serial.println("Web server started");
}

void loop() {
}
