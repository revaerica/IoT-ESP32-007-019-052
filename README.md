# IoT-ESP32-007-019-052

### Anggota
1. Revalina Erica Permatasari (5027241007)
2. Syifa Nurul Alfiah (5027241019)
3. Salsa Bil Ulla (5027241052)

## Langkah-Langkah Pengerjaan Project ESP32 
1. Pada Arduine IDE kita buka File > Preferences dan kita input https://dl.espressif.com/dl/package_esp32_index.json di additional boards manager URLs

<img width="959" height="603" alt="image" src="https://github.com/user-attachments/assets/be94547c-8495-47fe-8edf-e33a382e5388" />

2. Lalu buka menu Tools > Board > Boards Manager

<img width="1919" height="1201" alt="image" src="https://github.com/user-attachments/assets/8d02cbdd-2b44-4803-8771-938b2fb6e18a" />

3. Cari ESP32 dan install

<img width="1919" height="1191" alt="image" src="https://github.com/user-attachments/assets/0605f07f-528f-477c-86f9-3fa33e48b067" />

4. Tancapkan kabel USB dari ESP32 ke laptop

![photo_6266859186612275982_y](https://github.com/user-attachments/assets/335a8c74-fcb5-415f-b9f0-ae696da01709)

5. Pilih port yang sesuai dengan port pada device manager dan sesuaikan pada arduino IDE

<img width="1919" height="1210" alt="image" src="https://github.com/user-attachments/assets/d4c0373e-16df-4713-8b0e-04111540d2f2" />

6. Input kode berikut

```
#define TRIG_PIN 5   
#define ECHO_PIN 13  
#define LED_PIN  2  

long duration;
int distance;

void setup() {
  Serial.begin(115200);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  
  duration = pulseIn(ECHO_PIN, HIGH);
  distance = duration * 0.034 / 2; 

  Serial.print("Jarak: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance < 10) {
    digitalWrite(LED_PIN, HIGH);
    delay(200);
    digitalWrite(LED_PIN, LOW);
    delay(200);
  } else {
    digitalWrite(LED_PIN, LOW); 
    delay(200);
  }
}
```

7. Maka LED dapat berkedip/blink saat jarak kurang dari 10cm 

![photo_6266859186612275983_y](https://github.com/user-attachments/assets/741f7ef8-811c-476f-adb5-2610bcbfa4db)

8. Lakukan signup/login ke akun ThingSpeak dan buat Channel baru untuj menampilkan data yang dikirim dari perangkat-perangkat sensor yang  terhubung ke internet

(image)

## Penjelasan Code
1. 
