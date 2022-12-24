# UJIAN AKHIR SEMESTER
## ANGGOTA KELOMPOK
<div align='center'>
 
![Teams](https://img.shields.io/badge/Anggota%20Kelompok-Kelompok%207-purple)
 
<br>
 
![1197050051](https://img.shields.io/badge/103-Muhammad%20Syamil-blue)
![1197050049](https://img.shields.io/badge/107-Nada%20Fadhillah-blue)
![1197050085](https://img.shields.io/badge/113-Nur%20Halizah-blue)
![1197050119](https://img.shields.io/badge/121-Ridwan%20Ahmad%20Fauzan-blue)
![1197050079](https://img.shields.io/badge/136-Sopian%20Abdul%20Malik-blue)
![1197050079](https://img.shields.io/badge/142-Wildan%20Sophal%20Jamil-blue)
 
<br> 
 
[Teknik Informatika](http://if.uinsgd.ac.id/) [UIN Sunan Gunung Djati Bandung](https://uinsgd.ac.id/) 

</div>

## Deskripsi Umum
Sensor api (Flame sensor) adalah perangkat yang dapat digunakan untuk mendeteksi keberadaan sumber api atau sumber cahaya terang lainnya. Ada beberapa cara untuk mengimplementasikan Sensor Api tetapi modul yang digunakan dalam proyek ini adalah Sensor Peka Radiasi Inframerah. Dengan menghubungkan Flame Sensor dengan Arduino, Anda dapat mendeteksi api dan mengaktifkan Buzzer (implementasi sederhana dan mudah) atau pengukuran keselamatan darurat lainnya.

Flame Sensor bisa memiliki tiga pin atau empat pin, diantaranya yaitu VCC, GND dan DO. Hubungkan VCC dan GND ke +5V dan GND catu daya (dapat dihubungkan ke +5V Arduino). DO (kependekan dari Digital Output) terhubung ke Digital I/O Pin 11 Arduino. Untuk menunjukkan deteksi api, Buzzer digunakan. Rangkaian Buzzer terdiri dari Resistor 1KΩ, Transistor NPN (seperti 2N2222 atau BC548), Buzzer 5V dan Dioda Persimpangan PN. Lalu untuk buzzer digerakkan melalui Digital I/O 12 pin Arduino UNO.

### Alat dan Bahan
- Arduino Uno SMD, <p align="justify">sebagai komponen utama dari rangkaian ini, berfungsi mengontrol alur rangkaian. Terdapat berbagai port, yaitu POWER untuk kelistrikannya, ANALOG IN untuk input sensor yang mengeluarkan data analog, dan DIGITAL untuk input dan output data digital.</p>
- Flame Sensor IR (Infrared), <p align="justify">sensor utama yang mendeteksi api, dengan menggunakan inframerah. Terdapat 3 pin yaitu, VCC untuk input listriknya, GND untuk jalur minusnya, DO untuk mengeluarkan data digital ke Arduino.</p>
- Active Buzzer 5v, <p align="justify">berfungsi mengeluarkan suara. Dalam rangkaian ini, buzzer akan menyala ketika sensor mendeteksi api. Terdapat dua pin yaitu VCC dan GND.</p>
- LCD I2C 16x2, <p align="justify">mengeluarkan keterangan berbentuk text, dapat mengeluarkan text 2 baris dengan panjang 16 karakter. Terdapat 4 pin yaitu SDA dan SDL untuk data input dan outputnya lalu ada VCC dan GND.</p>
- Breadboard, <p align="justify">project board untuk menghubungkan berbagai komponen.</p>
- Kabel Jumper, <p align="justify">untuk menghubungkan pin komponen.</p>

### Cara Perangkaian
Pasang flame sensor dan buzzer pada breadboard.
Hubungkan pin ground (GND) flame sensor dan buzzer ke jalur negatif pada breadboard.
Hubungkan pin VCC dari flame sensor ke jalur positif pada breadboard.
Hubungkan pin VCC dari buzzer ke pin 9 pada arduino.
Hubungkan pin digital output (DO) dari flame sensor ke pin 8 pada arduino.
Hubungkan power out 5v dari arduino ke jalur positif pada breadboard.
Hubungkan GND dari arduino ke jalur negatif pada breadboard.
Hubungkan pin VCC dari LCD I2C ke jalur positif pada breadboard.
Hubungkan pin GND dari LCD I2C ke jalur negatif pada breadboard.
Hubungkan pin SDA dan SCL ke port SDA dan SCL pada arduino.
Colokkan usb dari arduino ke komputer atau laptop untuk proses coding.

## Coding
Install terlebih dahulu Arduino IDE-nya, lalu buka aplikasinya, untuk codingan dari rangkaian ini adalah sebagai berikut.

```C++
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,16,2);
const int buzzer = 9;
const int sensor = 8;
int readSensor = 0;

void setup()
{
  lcd.init();                      
  lcd.backlight();
  pinMode(buzzer, OUTPUT);
}

void loop()
{
  readSensor = digitalRead(sensor);
  lcd.setCursor(0, 0);
  lcd.print("  FLAME SENSOR");
  lcd.setCursor(0, 1);
  lcd.print("Fire Undetected!");
  if (readSensor == LOW) {
    lcd.setCursor(0, 1);
    lcd.print(" Fire Detected! ");
    digitalWrite(firstBuzzer, HIGH);
    delay(500);
    digitalWrite(firstBuzzer, LOW);
  }
}
```

## Output

<p align="justify">
 Output dari rangkaian di atas adalah ketika ada api dalam jarak dibawah 1 meter, sensor akan mendeteksinya dan buzzer akan menyala serta pada lcd akan muncul tulisan “Fire Detected”, ketika tidak ada api buzzer akan mati dan tulisan di lcd akan berganti menjadi “Fire Undetected”.
</p>

<div align='center'>
 
![Ketika Mendeteksi Api](https://miro.medium.com/max/640/1*iuMl6kcJYKmbi9v7xNY7Ag.webp)
 
 *Ketika Mendeteksi Api*
 </div>

Laporan lengkapnya bisa dilihat pada link berikut:

## Referensi
- Arkan, F. (2014). Sistem Detektor Kebakaran untuk Rumah Susun dengan Sistem Wireless Sensor Network. Jurnal Ecotipe (Electronic, Control, Telecommunication, Information, and Power Engineering), 1(1), 5–13.
- Kali, M. M., Tarigan, J., & Louk, A. C. (2016). Sistem Alarm Kebakaran menggunakan sensor infra red dan sensor suhu berbasis Arduino uno. Jurnal Fisika: Fisika Sains dan Aplikasinya, 1(1), 25–31.
- Yulianto, B. A. (2021). Simulasi Sistem Proteksi Untuk Kebakaran Pada Ruangan Bersekat Menggunakan Gas Sensor MQ2 Berbasis Internet of Things. (Doctoral dissertation, Universitas 17 Agustus 1945 Surabaya).
