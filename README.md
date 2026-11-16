# Zelfrijdende-auto
Dit project beschrijft het ontwerpen, bouwen en programmeren van een zelfrijdende auto die zelfstandig een stuk tape volgt met behulp van een Arduino Uno.

// Linker motor (Motor A)
const int enA = 9;
const int in1 = 8;
const int in2 = 7;

// Rechter motor (Motor B)
const int enB = 3;
const int in3 = 5;
const int in4 = 4;

int snelheid = 220; // Net onder maximum (255) om stroompieken en resets te voorkomen

void setup() {
  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(enB, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);

  stopMotoren();
  delay(2000); // 2 seconden wachten voor de start

  // 1. 2 seconden vooruit
  vooruit();
  delay(2000);
  stopMotoren();
  delay(1000); // 1 seconde rust tegen stroompieken

  // 2. 2 seconden naar links
  links();
  delay(2000);
  stopMotoren();
  delay(1000);

  // 3. 2 seconden naar rechts
  rechts();
  delay(2000);
  stopMotoren();
  delay(1000);

  // 4. 2 seconden naar achter
  achteruit();
  delay(2000);
  stopMotoren();
}

void loop() {
  // Blijft leeg: na setup() is de auto helemaal klaar
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
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
}

void rechts() {
  analogWrite(enA, snelheid);
  analogWrite(enB, snelheid);
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
