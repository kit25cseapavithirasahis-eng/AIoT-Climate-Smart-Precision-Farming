#include <DHT.h>

#define DHTPIN D4
#define DHTTYPE DHT11
#define SOIL_PIN A0

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();
  int soilMoisture = analogRead(SOIL_PIN);

  if (isnan(temperature) || isnan(humidity)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.print(" °C | Humidity: ");
  Serial.print(humidity);
  Serial.print(" % | Soil Moisture: ");
  Serial.println(soilMoisture);

  delay(2000);
}
