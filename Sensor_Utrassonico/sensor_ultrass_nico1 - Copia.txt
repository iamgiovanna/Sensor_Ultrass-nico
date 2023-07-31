int pinLedVermelho = 11;
int pinLedAmarelo = 10;
int pinLedVerde = 9;
int pinTrigger = 7;
int pinEecho = 6;
float pulse;
float dist_cm;

void setup()
{
	pinMode (pinLedVermelho, OUTPUT);
  	pinMode (pinLedAmarelo,OUTPUT );
  	pinMode (pinLedVerde, OUTPUT);
	pinMode (pinTrigger , OUTPUT);
  	pinMode (pinEecho, INPUT);
    digitalWrite(pinTrigger , LOW);
	Serial.begin(9600);
}

void loop()
{
	trigPulse();
  	pulse = pulseIn(pinEecho , HIGH);
  	dist_cm = pulse / 58.82;
  
  	if(dist_cm < 30.00)
    {
    	digitalWrite(pinLedVermelho , HIGH);
        digitalWrite(pinLedAmarelo, LOW);
        digitalWrite(pinLedVerde, LOW);
    }
  	
  if(dist_cm >= 30.00 && dist_cm < 50.00)
  {
    
    	digitalWrite(pinLedVermelho ,LOW );
        digitalWrite(pinLedAmarelo,HIGH );
        digitalWrite(pinLedVerde, LOW);
    
  }
	  if(dist_cm >= 50.00)
      {
        digitalWrite(pinLedVermelho ,LOW );
        digitalWrite(pinLedAmarelo, LOW);
        digitalWrite(pinLedVerde, HIGH);
      }
		Serial.print("Valor do sensor de distância: ");
		
  		Serial.println(dist_cm);
}

void trigPulse()
{
  	digitalWrite(pinTrigger, HIGH);
	
  	delayMicroseconds(10);
  
  	digitalWrite(pinTrigger , LOW);
}