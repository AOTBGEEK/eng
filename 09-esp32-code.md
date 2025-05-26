# 09 - كود ESP32 الكامل | Complete ESP32 Code

## الكود الشامل للمشروع 💻

### مكتبات النظام المطلوبة 📚

```cpp
// مكتبات الحساسات والمكونات
#include "DHT.h"              // حساس الحرارة والرطوبة
#include <ESP32Servo.h>       // محركات Servo
#include <LiquidCrystal_I2C.h> // شاشة LCD
#include <WiFi.h>             // الواي فاي
#include <ArduinoJson.h>      // معالجة البيانات

// إعدادات الشبكة
const char* ssid = "اسم_الشبكة";
const char* password = "كلمة_المرور";

// تعريف المنافذ
#define DHT_PIN 4
#define PIR_PIN_1 5
#define PIR_PIN_2 12
#define LDR_PIN_1 13
#define LDR_PIN_2 14
#define GAS_PIN 15
#define ULTRASONIC_TRIG 17
#define ULTRASONIC_ECHO 16
#define LED_PIN_1 18
#define LED_PIN_2 19
#define LCD_SDA 21
#define LCD_SCL 22
#define SERVO_PIN_1 23
#define SERVO_PIN_2 25
#define BUZZER_PIN 26
#define FAN_PIN 27

// إعداد الحساسات
DHT dht(DHT_PIN, DHT22);
Servo windowServo;
Servo doorServo;
LiquidCrystal_I2C lcd(0x27, 16, 2);

// العتبات والحدود
const float TEMP_HIGH = 28.0;
const float TEMP_LOW = 18.0;
const int LIGHT_THRESHOLD = 30;
const int GAS_DANGER = 70;
const int GAS_WARNING = 40;

// بنية بيانات النظام
struct SmartHome {
  float temperature;
  float humidity;
  int lightLevel1;
  int lightLevel2;
  int gasLevel;
  bool motion1;
  bool motion2;
  bool light1;
  bool light2;
  bool cooling;
  bool gasAlert;
  unsigned long uptime;
} homeStatus;

void setup() {
  Serial.begin(115200);
  Serial.println("🏠 مرحباً بكم في البيت الذكي البيئي!");
  
  // تهيئة المنافذ
  setupPins();
  
  // تهيئة المكونات
  setupComponents();
  
  // الاتصال بالواي فاي
  connectWiFi();
  
  // اختبار النظام
  systemTest();
  
  Serial.println("✅ النظام جاهز للعمل!");
}

void loop() {
  // قراءة الحساسات
  readSensors();
  
  // معالجة الأنظمة
  processTemperature();
  processLighting();
  processSecurity();
  processGasDetection();
  
  // تحديث العرض
  updateDisplay();
  
  // إرسال البيانات
  sendData();
  
  delay(1000);
}

void setupPins() {
  // منافذ الإدخال
  pinMode(PIR_PIN_1, INPUT);
  pinMode(PIR_PIN_2, INPUT);
  pinMode(GAS_PIN, INPUT);
  pinMode(ULTRASONIC_ECHO, INPUT);
  
  // منافذ الإخراج
  pinMode(LED_PIN_1, OUTPUT);
  pinMode(LED_PIN_2, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(FAN_PIN, OUTPUT);
  pinMode(ULTRASONIC_TRIG, OUTPUT);
}

void setupComponents() {
  dht.begin();
  lcd.init();
  lcd.backlight();
  windowServo.attach(SERVO_PIN_1);
  doorServo.attach(SERVO_PIN_2);
  
  lcd.setCursor(0, 0);
  lcd.print("البيت الذكي");
  lcd.setCursor(0, 1);
  lcd.print("جاري التشغيل...");
}

void readSensors() {
  homeStatus.temperature = dht.readTemperature();
  homeStatus.humidity = dht.readHumidity();
  homeStatus.lightLevel1 = map(analogRead(LDR_PIN_1), 0, 4095, 0, 100);
  homeStatus.lightLevel2 = map(analogRead(LDR_PIN_2), 0, 4095, 0, 100);
  homeStatus.gasLevel = map(analogRead(GAS_PIN), 0, 4095, 0, 100);
  homeStatus.motion1 = digitalRead(PIR_PIN_1);
  homeStatus.motion2 = digitalRead(PIR_PIN_2);
  homeStatus.uptime = millis() / 1000;
}

void processTemperature() {
  if (!isnan(homeStatus.temperature)) {
    if (homeStatus.temperature > TEMP_HIGH) {
      digitalWrite(FAN_PIN, HIGH);
      homeStatus.cooling = true;
      Serial.println("❄️ تشغيل التبريد");
    } else if (homeStatus.temperature < TEMP_LOW) {
      digitalWrite(FAN_PIN, LOW);
      homeStatus.cooling = false;
      Serial.println("🔥 الحاجة للتدفئة");
    } else {
      digitalWrite(FAN_PIN, LOW);
      homeStatus.cooling = false;
    }
  }
}

void processLighting() {
  // إضاءة غرفة المعيشة
  if (homeStatus.lightLevel1 < LIGHT_THRESHOLD && homeStatus.motion1) {
    digitalWrite(LED_PIN_1, HIGH);
    homeStatus.light1 = true;
  } else {
    digitalWrite(LED_PIN_1, LOW);
    homeStatus.light1 = false;
  }
  
  // إضاءة المطبخ
  if (homeStatus.lightLevel2 < LIGHT_THRESHOLD && homeStatus.motion2) {
    digitalWrite(LED_PIN_2, HIGH);
    homeStatus.light2 = true;
  } else {
    digitalWrite(LED_PIN_2, LOW);
    homeStatus.light2 = false;
  }
}

void processSecurity() {
  static unsigned long lastAlert = 0;
  
  if ((homeStatus.motion1 || homeStatus.motion2) && 
      (millis() - lastAlert > 30000)) {
    lastAlert = millis();
    activateAlarm();
    Serial.println("🚨 حركة مكتشفة!");
  }
}

void processGasDetection() {
  if (homeStatus.gasLevel > GAS_DANGER) {
    homeStatus.gasAlert = true;
    emergencyProtocol();
  } else if (homeStatus.gasLevel > GAS_WARNING) {
    warningBeep();
  } else {
    homeStatus.gasAlert = false;
  }
}

void activateAlarm() {
  for (int i = 0; i < 3; i++) {
    digitalWrite(BUZZER_PIN, HIGH);
    delay(500);
    digitalWrite(BUZZER_PIN, LOW);
    delay(500);
  }
}

void emergencyProtocol() {
  digitalWrite(FAN_PIN, HIGH);
  windowServo.write(90);
  
  for (int i = 0; i < 10; i++) {
    digitalWrite(BUZZER_PIN, HIGH);
    digitalWrite(LED_PIN_1, HIGH);
    digitalWrite(LED_PIN_2, HIGH);
    delay(200);
    digitalWrite(BUZZER_PIN, LOW);
    digitalWrite(LED_PIN_1, LOW);
    digitalWrite(LED_PIN_2, LOW);
    delay(200);
  }
}

void updateDisplay() {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("T:");
  lcd.print(homeStatus.temperature, 1);
  lcd.print("C H:");
  lcd.print(homeStatus.humidity, 0);
  lcd.print("%");
  
  lcd.setCursor(0, 1);
  if (homeStatus.gasAlert) {
    lcd.print("خطر! غاز مكتشف");
  } else if (homeStatus.motion1 || homeStatus.motion2) {
    lcd.print("حركة مكتشفة");
  } else {
    lcd.print("النظام آمن");
  }
}

void connectWiFi() {
  WiFi.begin(ssid, password);
  Serial.print("الاتصال بالواي فاي");
  
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  
  Serial.println();
  Serial.println("✅ متصل بالواي فاي!");
  Serial.print("العنوان: ");
  Serial.println(WiFi.localIP());
}

void sendData() {
  // إنشاء JSON للبيانات
  StaticJsonDocument<300> doc;
  doc["temperature"] = homeStatus.temperature;
  doc["humidity"] = homeStatus.humidity;
  doc["light1"] = homeStatus.lightLevel1;
  doc["light2"] = homeStatus.lightLevel2;
  doc["gas"] = homeStatus.gasLevel;
  doc["motion1"] = homeStatus.motion1;
  doc["motion2"] = homeStatus.motion2;
  doc["uptime"] = homeStatus.uptime;
  
  String jsonString;
  serializeJson(doc, jsonString);
  Serial.println("📊 البيانات: " + jsonString);
}

void systemTest() {
  Serial.println("🧪 اختبار النظام...");
  
  // اختبار الأضواء
  digitalWrite(LED_PIN_1, HIGH);
  digitalWrite(LED_PIN_2, HIGH);
  delay(1000);
  digitalWrite(LED_PIN_1, LOW);
  digitalWrite(LED_PIN_2, LOW);
  
  // اختبار الجرس
  digitalWrite(BUZZER_PIN, HIGH);
  delay(500);
  digitalWrite(BUZZER_PIN, LOW);
  
  // اختبار المحركات
  windowServo.write(45);
  delay(1000);
  windowServo.write(0);
  
  Serial.println("✅ اكتمل الاختبار!");
}

void warningBeep() {
  digitalWrite(BUZZER_PIN, HIGH);
  delay(100);
  digitalWrite(BUZZER_PIN, LOW);
}
```

## وظائف إضافية للتطوير 🚀

### 1. نظام التحكم عن بُعد
```cpp
#include <WebServer.h>
WebServer server(80);

void setupWebServer() {
  server.on("/", handleRoot);
  server.on("/status", handleStatus);
  server.on("/control", handleControl);
  server.begin();
}

void handleRoot() {
  String html = "<!DOCTYPE html>";
  html += "<html><head><title>البيت الذكي</title></head>";
  html += "<body><h1>لوحة التحكم</h1>";
  html += "<p>درجة الحرارة: " + String(homeStatus.temperature) + "°C</p>";
  html += "<p>الرطوبة: " + String(homeStatus.humidity) + "%</p>";
  html += "<button onclick='toggleLight(1)'>إضاءة 1</button>";
  html += "<button onclick='toggleLight(2)'>إضاءة 2</button>";
  html += "</body></html>";
  server.send(200, "text/html", html);
}
```

### 2. نظام حفظ البيانات
```cpp
#include <SPIFFS.h>

void saveData() {
  File file = SPIFFS.open("/data.txt", "w");
  if (file) {
    file.println(homeStatus.temperature);
    file.println(homeStatus.humidity);
    file.println(homeStatus.gasLevel);
    file.close();
  }
}

void loadData() {
  File file = SPIFFS.open("/data.txt", "r");
  if (file) {
    float lastTemp = file.readStringUntil('\n').toFloat();
    Serial.println("آخر درجة حرارة محفوظة: " + String(lastTemp));
    file.close();
  }
}
```

### 3. نظام التنبيهات الذكية
```cpp
void smartNotifications() {
  static unsigned long lastCheck = 0;
  
  if (millis() - lastCheck > 60000) { // كل دقيقة
    lastCheck = millis();
    
    // تحليل الأنماط
    if (homeStatus.temperature > TEMP_HIGH + 2) {
      sendAlert("🌡️ تحذير: درجة حرارة عالية جداً!");
    }
    
    if (homeStatus.gasLevel > 0 && homeStatus.gasLevel < GAS_WARNING) {
      sendAlert("⚠️ ملاحظة: مستوى غاز منخفض مكتشف");
    }
    
    // توفير الطاقة
    if (!homeStatus.motion1 && !homeStatus.motion2) {
      energySaveMode();
    }
  }
}

void energySaveMode() {
  static bool energyMode = false;
  
  if (!energyMode) {
    energyMode = true;
    digitalWrite(LED_PIN_1, LOW);
    digitalWrite(LED_PIN_2, LOW);
    Serial.println("💡 تفعيل وضع توفير الطاقة");
  }
}
```

## نصائح التطوير والتحسين 💡

### 1. تحسين استهلاك الطاقة:
- استخدم Deep Sleep عند عدم النشاط
- قلل تكرار قراءة الحساسات
- أطفئ WiFi عند عدم الحاجة

### 2. معالجة الأخطاء:
- تحقق من صحة قراءات الحساسات
- أعد تشغيل النظام عند الأخطاء الخطيرة
- احفظ السجلات للتشخيص

### 3. الأمان:
- شفّر البيانات المرسلة
- استخدم كلمات مرور قوية
- فعّل جدار الحماية

هذا الكود يوفر أساساً قوياً لبيتكم الذكي! 🏠✨ 