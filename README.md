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

8. Lakukan signup/login ke akun ThingSpeak dan buat Channel baru untuk menampilkan data yang dikirim dari perangkat-perangkat sensor yang terhubung ke internet

(image)

## Penjelasan Code
1.
```
#define TRIG_PIN 5
#define ECHO_PIN 13
#define LED_PIN  2
``` 
- #define digunakan untuk mendefinisikan konstanta (nilai tetap).
- TRIG_PIN adalah pin trigger sensor ultrasonik (HC-SR04), diset di pin GPIO 5.
- ECHO_PIN adalah pin echo '
- sensor ultrasonik, diset di pin GPIO 13.
- LED_PIN adalah pin untuk LED indikator, diset di pin GPIO 2.
Fungsinya: supaya kalau kita mau ganti pin, cukup ubah angka di atas tanpa harus ubah di seluruh kode.

2.
```
long duration;
int distance;
```
duration: variabel bertipe long untuk menyimpan lama waktu pantulan ultrasonik diterima (dalam microsecond).
distance: variabel bertipe int untuk menyimpan hasil perhitungan jarak (dalam cm).

3.
```
  void setup() {
  Serial.begin(115200);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);
}
```
- Serial.begin(115200); → mengaktifkan komunikasi serial dengan baud rate 115200 bps. Berguna untuk menampilkan data jarak di Serial Monitor.
- pinMode(TRIG_PIN, OUTPUT); → menentukan bahwa pin trigger berfungsi sebagai output (mengirim sinyal).
- pinMode(ECHO_PIN, INPUT); → menentukan bahwa pin echo berfungsi sebagai input (menerima pantulan sinyal).
 -pinMode(LED_PIN, OUTPUT); → menentukan pin LED sebagai output.

4.
```
digitalWrite(TRIG_PIN, LOW);
delayMicroseconds(2);
digitalWrite(TRIG_PIN, HIGH);
delayMicroseconds(10);
digitalWrite(TRIG_PIN, LOW);
```
- Bagian ini mengirimkan pulsa trigger ke sensor ultrasonik:
- Pertama pin trigger di-reset ke LOW selama 2 µs.
- Lalu dikasih sinyal HIGH selama 10 µs (pulsa trigger).
- Setelah itu dikembalikan lagi ke LOW. 
- Pulsa 10 µs ini memberi instruksi sensor ultrasonik untuk mengeluarkan gelombang suara ultrasonik.

5.
```
duration = pulseIn(ECHO_PIN, HIGH);
```
- Fungsi pulseIn(pin, HIGH) menghitung berapa lama pin echo bernilai HIGH.
- Nilai yang dikembalikan berupa waktu (dalam mikrodetik) yaitu lamanya gelombang ultrasonik pergi dan kembali setelah memantul dari objek.

6.
```
distance = duration * 0.034 / 2;
```
- Rumus: jarak = (waktu × kecepatan suara) / 2
- Kecepatan suara di udara = 0.034 cm/µs.
- Dibagi 2 karena suara menempuh pergi dan pulang. Jadi hasilnya adalah jarak dari sensor ke objek dalam satuan cm.

7.
```
Serial.print("Jarak: ");
Serial.print(distance);
Serial.println(" cm");
```
- Serial.print("Jarak: "); → menampilkan teks.
- Serial.print(distance); → menampilkan angka jarak yang dihitung.
- Serial.println(" cm"); → menampilkan " cm" dan pindah baris.

8.
```
  if (distance < 10) {
  digitalWrite(LED_PIN, HIGH);
  delay(200);
  digitalWrite(LED_PIN, LOW);
  delay(200);
} else {
  digitalWrite(LED_PIN, LOW); 
  delay(200);
}
```
- if (distance < 10) → jika jarak objek kurang dari 10 cm, LED akan berkedip:
- Nyalakan LED (HIGH) selama 200 ms.
- Matikan LED (LOW) selama 200 ms.
- else → jika jarak objek ≥ 10 cm, LED mati terus.
