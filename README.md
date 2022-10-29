
mariatorres-medidorCO/mariatorres-medidorCO is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
//codigo solo del arduino sensor y los leds 
 
int sensorlimite = 30;

void setup() {
  Serial.begin(9600);

   pinMode(4, OUTPUT); // LED
   pinMode(9, INPUT); // Valor digital sensor
   pinMode(2, OUTPUT);//LED
   pinMode(5, OUTPUT);
}
void loop() {
  int MQ7 = analogRead(A0); //Lemos la salida analógica  del MQ
  float voltaje = MQ7 * (5.0 / 1023.0); //Convertimos la lectura en un valor de voltaje
  float Rs= 1000*((5-voltaje)/voltaje);  //Calculamos Rs con un RL de 1k
  double PPM = 100*pow(Rs/2116.4, -1.513); // calculamos la concentración  de CO
  //-------Enviamos los valores por el puerto serial------------
  Serial.print("Valor PPM: ");
  Serial.println(PPM);
  delay(1000);

   if (PPM > sensorlimite){ // Capturo analogRead (0) que es el valor analogico del sensor
      digitalWrite(4, HIGH); // Enciendo LED ROJO
      digitalWrite(2,LOW);}
      
   else {
        digitalWrite(4, LOW);
        digitalWrite(2, HIGH);}
}
