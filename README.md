# ⚔️ İnsan İmparatorluğu vs Ork Lejyonu - Savaş Simülasyonu

Bu proje, C programlama dili kullanılarak geliştirilmiş, **İnsan İmparatorluğu** ve **Ork Lejyonu** arasındaki savaşları simüle eden izometrik bir strateji oyunudur. Proje, senaryo verilerini internetten çeker, birliklerin özelliklerini işler ve savaş sonucunu hem görsel bir arayüzde (SDL2) sunar hem de detaylı bir metin günlüğü (log) oluşturur.


## 🚀 Proje Hakkında

Bu simülasyon, iki farklı ırkın askeri birliklerini, kahramanlarını, canavarlarını ve araştırma geliştirmelerini karşılaştırarak tur tabanlı bir savaş algoritması çalıştırır.

### Temel Özellikler
* **🌐 Dinamik Senaryo Yükleme:** `libcurl` kütüphanesi kullanılarak `yapbenzet.org.tr` üzerinden JSON formatındaki savaş senaryoları dinamik olarak indirilir.
* **🎨 İzometrik Grafik Motoru:** `SDL2` kullanılarak geliştirilen özel bir görüntüleme motoru ile savaş alanı ve birlikler izometrik perspektifte çizilir.
* **📊 Detaylı Veri Analizi:** Birliklerin saldırı, savunma, sağlık ve kritik vuruş şansları JSON dosyalarından (parser) okunur.
* **🧠 Stratejik Hesaplamalar:** Araştırma seviyeleri (Savunma Ustalığı, Elit Eğitim vb.) ve Kahraman bonusları (Fatih Sultan Mehmet, Goruk Vahsi vb.) savaşın gidişatını doğrudan etkiler.
* **📝 Savaş Günlüğü:** Savaşın her turu, alınan hasarlar ve sonuçlar `Savas_sim.txt` dosyasına detaylıca kaydedilir.

---

## 🛠️ Kullanılan Teknolojiler ve Kütüphaneler

Proje **C** dili ile geliştirilmiştir ve aşağıdaki kütüphanelere ihtiyaç duyar:

* **SDL2 (Simple DirectMedia Layer):** Grafik çizimi, pencere yönetimi ve olay döngüsü için.
    * `SDL2_image`: PNG formatındaki görselleri yüklemek için.
    * `SDL2_ttf`: Yazı tiplerini render etmek için.
* **libcurl:** HTTP üzerinden veri (JSON senaryoları) indirmek için.
* **Standard C Libraries:** `stdio`, `stdlib`, `string`, `math`, `locale`.

---

## 📂 Dosya Yapısı ve Varlıklar

Projenin çalışması için aşağıdaki klasör yapısının ve dosyaların mevcut olması gerekmektedir:

```text
Proje_Klasoru/
├── main.c              # Ana oyun döngüsü ve mantığı
├── renderer.c / .h     # SDL render işlemleri
├── texture.c / .h      # Doku yükleme işlemleri
├── isoEngine.c / .h    # İzometrik harita motoru
├── initclose.c / .h    # SDL başlatma ve kapatma fonksiyonları
├── LemonMilkbolditalic.otf  # Kullanılan yazı tipi
├── isotiles.png        # Zemin kaplamaları
├── Savas_sim.txt       # (Program çalışınca oluşur) Savaş çıktıları
│
├── Files/              # Veri dosyaları klasörü
│   ├── unit_types.json # Birim özellikleri
│   ├── creatures.json  # Canavar özellikleri
│   ├── heroes.json     # Kahraman özellikleri
│   └── research.json   # Araştırma verileri
│
└── (Resim Dosyaları)   # piyade.png, okcu.png, ejder.png vb.
```

⚙️ Derleme ve Kurulum
Projeyi derlemek için GCC derleyicisi ve gerekli kütüphanelerin (SDL2, cURL) bilgisayarınızda kurulu olması gerekir.

Örnek Derleme Komutu (Windows - MinGW):

```bash

gcc main.c renderer.c texture.c initclose.c isoEngine.c -o SavasSim -lmingw32 -lSDL2main -lSDL2 -lSDL2_image -lSDL2_ttf -lcurl
```

Örnek Derleme Komutu (Linux):

```bash
gcc main.c renderer.c texture.c initclose.c isoEngine.c -o SavasSim -lSDL2 -lSDL2_image -lSDL2_ttf -lcurl -lm
```

### 🎮 Nasıl Kullanılır?
1. Uygulamayı çalıştırın (SavasSim.exe veya ./SavasSim).

2. Konsol ekranında karşınıza çıkan menüden oynamak istediğiniz Senaryo Numarasını (1-10) seçin.

3. Program, seçilen senaryoyu sunucudan indirecek (senerio.json olarak kaydeder) ve savaşı başlatacaktır.

4. Grafik Ekranı: Savaş alanını ve birliklerin durumunu görsel olarak takip edebilirsiniz.

* Yeşil/Sarı/Kırmızı barlar birliklerin sağlık durumunu gösterir.

* Birimlerin üzerindeki sayılar kalan asker miktarını belirtir.

5. Sonuç: Simülasyon bittiğinde detaylı rapor Savas_sim.txt dosyasında bulunabilir.

### ⚔️ Oyun Mekanikleri
 # Irklar ve Birimler
* İnsan İmparatorluğu: Piyadeler, Okçular, Süvariler, Kuşatma Makineleri.

* Ork Lejyonu: Ork Dövüşçüleri, Mızrakçılar, Varg Binicileri, Troller.

# Kritik Faktörler
# 1. Araştırmalar:

* Savunma Ustalığı: Birimlerin savunma gücünü artırır.

* Saldırı Geliştirmesi: Hasar kapasitesini artırır.

* Elit Eğitim: Kritik vuruş şansını artırır.

# 2. Kahramanlar & Canavarlar:

* Her kahraman ve canavar, belirli birlik türlerine (örn: Piyadelere) ekstra bonuslar (Saldırı, Savunma vb.) sağlar.

# 3. Yorgunluk:

Her 5 turda bir, savaşan tüm birimler yorulur ve güçleri %10 azalır.

### 📷 Ekran Görüntüleri
<img width="1917" height="1022" alt="Image" src="https://github.com/user-attachments/assets/d712665c-ea3c-4ea4-ac1a-b99e9577a706" />
