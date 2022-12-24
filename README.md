# UJIAN AKHIR SEMESTER
## ANGGOTA KELOMPOK
<div align='center'>
 
![Teams](https://img.shields.io/badge/Anggota%20Kelompok-Kelompok%207-purple)
 
<br>
 
![1197050051](https://img.shields.io/badge/103-Muhammad%20Syamil%20Hamami-blue)
![1197050049](https://img.shields.io/badge/107-Nada%20Fadhillah%20Balqis-blue)
![1197050085](https://img.shields.io/badge/113-Nur%20Halizah-blue)
![1197050119](https://img.shields.io/badge/121-Ridwan%20Ahmad%20Fauzan-blue)
![1197050079](https://img.shields.io/badge/136-Sopian%20Abdul%20Malik-blue)
![1197050079](https://img.shields.io/badge/142-Wildan%20Sophal%20Jamil-blue)
 
<br> 
 
[Teknik Informatika](http://if.uinsgd.ac.id/) [UIN Sunan Gunung Djati Bandung](https://uinsgd.ac.id/) 

</div>

## Deskripsi Umum
<p align="justify">
Sensor api (Flame sensor) adalah perangkat yang dapat digunakan untuk mendeteksi keberadaan sumber api atau sumber cahaya terang lainnya. Ada beberapa cara untuk mengimplementasikan Sensor Api tetapi modul yang digunakan dalam proyek ini adalah Sensor Peka Radiasi Inframerah. Dengan menghubungkan Flame Sensor dengan Arduino, Anda dapat mendeteksi api dan mengaktifkan Buzzer (implementasi sederhana dan mudah) atau pengukuran keselamatan darurat lainnya.
</p>
<p align="justify">
Flame Sensor bisa memiliki tiga pin atau empat pin, diantaranya yaitu VCC, GND dan DO. Hubungkan VCC dan GND ke +5V dan GND catu daya (dapat dihubungkan ke +5V Arduino). DO (kependekan dari Digital Output) terhubung ke Digital I/O Pin 11 Arduino. Untuk menunjukkan deteksi api, Buzzer digunakan. Rangkaian Buzzer terdiri dari Resistor 1KΩ, Transistor NPN (seperti 2N2222 atau BC548), Buzzer 5V dan Dioda Persimpangan PN. Lalu untuk buzzer digerakkan melalui Digital I/O 12 pin Arduino UNO.
</p>

### Alat dan Bahan
- <p align="justify">Arduino Uno SMD, sebagai komponen utama dari rangkaian ini, berfungsi mengontrol alur rangkaian. Terdapat berbagai port, yaitu POWER untuk kelistrikannya, ANALOG IN untuk input sensor yang mengeluarkan data analog, dan DIGITAL untuk input dan output data digital.</p>
<div align='center'>
 
![Arduino Uno SMD](https://miro.medium.com/max/640/1*U9NqSqX69NY-0Se2EZYc5g.webp)
 
 *Arduino Uno SMD*
 </div>
- <p align="justify">Flame Sensor IR (Infrared), sensor utama yang mendeteksi api, dengan menggunakan inframerah. Terdapat 3 pin yaitu, VCC untuk input listriknya, GND untuk jalur minusnya, DO untuk mengeluarkan data digital ke Arduino.</p>
<div align='center'>
 
![Flame Sensor IR](https://miro.medium.com/max/578/1*yUEXt9Fwl1pGXH-rx7oGEQ.webp)
 
 *Flame Sensor IR (Infrared)*
 </div>
- <p align="justify">Active Buzzer 5v, berfungsi mengeluarkan suara. Dalam rangkaian ini, buzzer akan menyala ketika sensor mendeteksi api. Terdapat dua pin yaitu VCC dan GND.</p>
<div align='center'>
 
![Active Buzzer](https://miro.medium.com/max/486/1*AV5i2FhI_0BmEpu4T4UuCw.webp)
 
 *Active Buzzer 5v*
 </div>
- <p align="justify">LCD I2C 16x2, mengeluarkan keterangan berbentuk text, dapat mengeluarkan text 2 baris dengan panjang 16 karakter. Terdapat 4 pin yaitu SDA dan SDL untuk data input dan outputnya lalu ada VCC dan GND.</p>
<div align='center'>
 
![LCD I2C 16x2](https://miro.medium.com/max/502/1*qsuxi7TNTjikzq4SfziTFg.webp)
 
 *LCD I2C 16x2*
 </div>
- <p align="justify">Breadboard, project board untuk menghubungkan berbagai komponen.</p>
<div align='center'>
 
![Breadboard](https://miro.medium.com/max/552/1*2Gd1RQjMCtg2e3OzrigkIg.webp)
 
 *Breadboard*
 </div>
- <p align="justify">Kabel Jumper, untuk menghubungkan pin komponen.</p>
<div align='center'>
 
![Kabel Jumper](https://miro.medium.com/max/486/1*c5dL2Onv3bd7V3gFPs-mOw.webp)
 
 *Kabel Jumper*
 </div>

### Cara Perangkaian
- <p align="justify">Pasang flame sensor dan buzzer pada breadboard</p>
- <p align="justify">Hubungkan pin ground (GND) flame sensor dan buzzer ke jalur negatif pada breadboard.</p>
- <p align="justify">Hubungkan pin VCC dari flame sensor ke jalur positif pada breadboard.</p>
- <p align="justify">Hubungkan pin VCC dari buzzer ke pin 9 pada arduino.</p>
- <p align="justify">Hubungkan pin digital output (DO) dari flame sensor ke pin 8 pada arduino.</p>
- <p align="justify">Hubungkan power out 5v dari arduino ke jalur positif pada breadboard.</p>
- <p align="justify">Hubungkan GND dari arduino ke jalur negatif pada breadboard.</p>
- <p align="justify">Hubungkan pin VCC dari LCD I2C ke jalur positif pada breadboard.</p>
- <p align="justify">Hubungkan pin GND dari LCD I2C ke jalur negatif pada breadboard.</p>
- <p align="justify">Hubungkan pin SDA dan SCL ke port SDA dan SCL pada arduino.</p>
- <p align="justify">Colokkan usb dari arduino ke komputer atau laptop untuk proses coding.</p>

## Coding

<p align="justify">Install terlebih dahulu Arduino IDE-nya, lalu buka aplikasinya, untuk codingan dari rangkaian ini adalah sebagai berikut.</p>

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
