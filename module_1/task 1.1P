// Define the pins for the ultrasonic sensor
const int TRIGGER_PIN = 12;
const int ECHO_PIN = 13;

// Define the pins for the LED and button
const int LED_PIN = 8;
const int BUTTON_PIN = 4;

// Define a variable to store the state of the LED
bool ledOn = false;

// Define a variable to store the last time the button was pressed
unsigned long lastButtonPress = 0;

// Define the minimum time between button presses in milliseconds
const unsigned long debounceDelay = 50;

// Define the maximum distance to detect
const int MAX_DISTANCE = 200;

// Define a function to toggle the LED state
void toggleLed() {
  if (ledOn) {
    digitalWrite(LED_PIN, LOW);
    ledOn = false;
  } else {
    digitalWrite(LED_PIN, HIGH);
    ledOn = true;
  }
}

// Define the interrupt service routine for the button
void buttonPressed() {
  // Check if enough time has passed since the last button press
  if (millis() - lastButtonPress > debounceDelay) {
    toggleLed();
    lastButtonPress = millis();
  }
}

void setup() {
  // Initialize the ultrasonic sensor pins
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);

  // Initialize the LED and button pins
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);

  // Attach the interrupt to the button pin
  attachInterrupt(digitalPinToInterrupt(BUTTON_PIN), buttonPressed, FALLING);
}

void loop() {
  // Generate a pulse on the ultrasonic sensor trigger pin
  digitalWrite(TRIGGER_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIGGER_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIGGER_PIN, LOW);

  // Measure the duration of the echo pulse
  int duration = pulseIn(ECHO_PIN, HIGH, MAX_DISTANCE * 58);

  // Calculate the distance in centimeters
  int distance = duration / 58;

  // Print the distance on the serial monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // Check if the distance is less than 10cm
  if (distance < 10) 
  {
    toggleLed();
    delay(1000); // Wait for 1 second before toggling the LED again
  }

  // Wait for 1 second before measuring again
  delay(1000);
}
