# Zelfrijdende-auto
Dit project beschrijft het ontwerpen, bouwen en programmeren van een zelfrijdende auto die zelfstandig een stuk tape volgt met behulp van een Arduino Uno.
// L298N Robotauto - Volgorde: 2s vooruit -> 2s links -> 2s rechts -> 2s achteruit

// Pin-definities voor de motordriver
const int enA = 9;  // PWM snelheid linkermotor
const int in1 = 8;  // Richting linkermotor
const int in2 = 7;  // Richting linkermotor

const int enB = 3;  // PWM snelheid rechtermotor
const int in3 = 5;  // Richting rechtermotor
const int in4 = 4;  // Richting rechtermotor

// Snelheid op maximum (255) gezet om te zorgen dat de motoren niet gaan brommen maar direct starten
int snelheid = 255; 

void setup() {
  // Stel alle motordriver-pinnen in als uitgang
  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(enB, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);

  // Start in stilstand
  stopMotoren();
  delay(2000); // 2 seconden wachten na het opstarten voordat de auto begint
}

void loop() {
  // 1. 2 seconden vooruit
  vooruit();
  delay(2000);
  stopMotoren();
  delay(300); // Korte pauze voor stabiliteit

  // 2. 2 seconden naar links (draait om zijn as)
  links();
  delay(2000);
  stopMotoren();
  delay(300);

  // 3. 2 seconden naar rechts (draait om zijn as)
  rechts();
  delay(2000);
  stopMotoren();
  delay(300);

  // 4. 2 seconden naar achter
  achteruit();
  delay(2000);
  stopMotoren();

  // Stopt de reeks permanent nadat hij één keer is uitgevoerd
  while (true); 
}

// --- Bewegingsfuncties ---

void vooruit() {
  analogWrite(enA, snelheid);
  analogWrite(enB, snelheid);
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
}

void achteruit() {
  analogWrite(enA, snelheid);
  analogWrite(enB, snelheid);
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  digitalWrite(in3, LOW);
  digitalWrite(in4, HIGH);
}

void links() {
  analogWrite(enA, snelheid);
  analogWrite(enB, snelheid);
  // Linkerwiel achteruit, rechterwiel vooruit (draait naar links)
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
}

void rechts() {
  analogWrite(enA, snelheid);
  analogWrite(enB, snelheid);
  // Linkerwiel vooruit, rechterwiel achteruit (draait naar rechts)
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
  digitalWrite(in3, LOW);
  digitalWrite(in4, HIGH);
}

void stopMotoren() {
  analogWrite(enA, 0);
  analogWrite(enB, 0);
  digitalWrite(in1, LOW);
  digitalWrite(in2, LOW);
  digitalWrite(in3, LOW);
  digitalWrite(in4, LOW);
}
