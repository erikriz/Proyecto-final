# Proyecto-final Sistema de riego automatizado
int relePin = 4;      
int sensorPin = A0;   

int humedadBaja = 600;    
int humedadMedia = 400;   
int humedadAlta = 250;    

void setup() {
  pinMode(relePin, OUTPUT);     
  digitalWrite(relePin, LOW);   
  Serial.begin(9600);           
}

void loop() {
  int humedadValor = analogRead(sensorPin);  
  
  
  Serial.print("Valor de humedad: ");
  Serial.println(humedadValor);

 
  if (humedadValor > humedadBaja) {
    // Suelo muy seco: enciende la bomba por 6 segundos
    digitalWrite(relePin, HIGH);
    Serial.println("Bomba activada: Suelo muy seco");
    delay(6000);  // La bomba se queda encendida por 6 segundos
    digitalWrite(relePin, LOW);
  } 
  else if (humedadValor > humedadMedia && humedadValor <= humedadBaja) {
    // Suelo intermedio: enciende la bomba por 3 segundos
    digitalWrite(relePin, HIGH);
    Serial.println("Bomba activada: Suelo intermedio");
    delay(3000);  // La bomba se queda encendida por 3 segundos
    digitalWrite(relePin, LOW);
  }
  else if (humedadValor <= humedadMedia) {
    // Suelo húmedo: apaga la bomba
    digitalWrite(relePin, LOW);
    Serial.println("Bomba desactivada: Suelo húmedo");
  }

  delay(2000);  
}
