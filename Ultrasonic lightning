#define TRIG_PIN 23
#define ECHO_PIN 22

#define RED_PIN 18
#define GREEN_PIN 21
#define BLUE_PIN 15

bool rgbState = false; // Состояние RGB (вкл/выкл)
bool objectDetected = false; // Флаг для фиксации первого обнаружения

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);

  pinMode(RED_PIN, OUTPUT);
  pinMode(GREEN_PIN, OUTPUT);
  pinMode(BLUE_PIN, OUTPUT);

  digitalWrite(RED_PIN, LOW);
  digitalWrite(GREEN_PIN, LOW);
  digitalWrite(BLUE_PIN, LOW);

  Serial.begin(115200);
  Serial.println("Система запущена");
}

void loop() {
  long distance = getDistance();

  if (distance >= 3 && distance <= 50) { // Если объект находится в диапазоне 3-50 см
    if (!objectDetected) { // Первое обнаружение объекта
      objectDetected = true; // Устанавливаем флаг
      rgbState = !rgbState; // Переключаем состояние RGB

      if (rgbState) {
        turnOnRGB(); // Включаем RGB
      } else {
        turnOffRGB(); // Выключаем RGB
      }

      delay(500); // Небольшая задержка для устранения дребезга
    }
  } else { // Если объекта нет в зоне действия
    objectDetected = false; // Сбрасываем флаг, чтобы зафиксировать новое движение
  }
}

long getDistance() {
  // Отправляем ультразвуковой импульс
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // Считаем время отклика
  long duration = pulseIn(ECHO_PIN, HIGH);

  // Переводим длительность в расстояние (см)
  long distance = duration * 0.034 / 2;

  // Выводим результат в Serial Monitor
  Serial.print("Измеренное расстояние: ");
  Serial.print(distance);
  Serial.println(" см");

  return distance;
}

void turnOnRGB() {
  digitalWrite(RED_PIN, HIGH);
  digitalWrite(GREEN_PIN, HIGH);
  digitalWrite(BLUE_PIN, HIGH);
  Serial.println("RGB включен");
}

void turnOffRGB() {
  digitalWrite(RED_PIN, LOW);
  digitalWrite(GREEN_PIN, LOW);
  digitalWrite(BLUE_PIN, LOW);
  Serial.println("RGB выключен");
}
