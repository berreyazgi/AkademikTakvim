# TEDÜ 2026 Güz — Akademik Takvim & Çalışma Takip Sistemi (Academic Tracker SPA)

Modern, son derece duyarlı (responsive), tamamen sunucusuz (zero-backend, zero-database) ve ücretsiz olarak Vercel'e tek komutla dağıtılabilen akademik dönem ve çalışma verimliliği takip platformu.

---

## 🌟 Temel Mimari ve Özellikler

### 1. Sıfır Veritabanı & Sunucusuz Kalıcılık (Zero Database Persistence)
- **Runtime Veri Depolama**: Tarayıcının `localStorage` mekanizması birincil depolama alanı olarak kullanılır. Sayfa yenilendiğinde veya tarayıcı kapatılıp açıldığında kullanıcı verileri asla kaybolmaz.
- **IndexedDB Yedek Katmanı**: Veri boyutu arttığında veya kotalara karşı dayanıklılık için arka planda asenkron IndexedDB desteği sağlanır.
- **JSON Import / Export Motoru**:
  - **Export Data (JSON)**: `academic_tracker_backup_YYYY-MM-DD_HHmm.json` şeklinde zaman damgalı tam veri yedeği üretir ve indirir.
  - **Import Data (JSON)**: Kullanıcının yüklediği JSON yedeğinin şemasını doğrular (validation), verileri mevcut durumla birleştirme (**Merge**) veya üzerine yazma (**Replace**) seçenekleri sunar ve anlık bildirim (toast) verir.
  - **Varsayılan Verilere Sıfırla (Reset)**: İstendiğinde tek tıkla TED Üniversitesi 2026 Güz seed verilerine dönülmesini sağlar.
- **Bulut Senkronizasyonu (İsteğe Bağlı - Gist API)**: Veritabanı kurmadan cihazlar arası JSON senkronizasyonu için GitHub Personal Access Token + Gist ID entegrasyonu sunar (Push / Pull).

---

## 📚 Modüller ve Yetenekler

### 1. Görsel Haftalık Ders Programı (Visual Timetable)
- **7 Gün & Saat Çizelgesi**: Pazartesi'den Pazar'a, **08:00 - 22:00** arası tam haftalık üniversite programı.
- **Ön Yüklü TEDÜ 2026 Güz Dersleri**:
  - `MATH 240`: Salı 11:00–12:50 (G103), Çarşamba 13:00–13:50 (G103)
  - `CMPE 472`: Pazartesi 09:00–10:50 (G108), Çarşamba 09:00–10:50 (GB13-PC-L)
  - `CMPE 421`: Pazartesi 13:00–15:30 (D026)
  - `CMPE 414`: Pazartesi 18:00–20:30 (D028)
  - `CMPE 325`: Salı 15:00–17:30 (G103)
  - `PHYS 120`: Cuma 16:00–17:50 (D032)
  - `SENG 491`: Cuma 18:00–19:00 (Online)
  - `SENG 499`: Cuma 20:00–21:00 (Online)
  - `HIST 102`: Pazar Quiz ve hazırlık blokları
- **Tam CRUD Desteği**: Arayüz üzerinden yeni ders bloğu ekleme, derslik/saat/renk düzenleme ve silme.
- **Mobil Görünüm Uyumluluğu**: Mobilde gün seçici sekmeler (Pzt-Paz) ve yatay kaydırma desteği.

### 2. Haftalık Çalışma Planı & Odak Görevleri (Study Planner)
- **3 Aşamalı Görev Durumu**: `Planlandı` (Bekliyor), `Devam Ediyor` (In Progress), `Tamamlandı` (Done).
- **Gerçek Zamanlı İlerleme Çubuğu**: Haftalık görev tamamlama yüzdesi ve oranı (`X / Y tamamlandı`).
- **Dinamik CRUD**: İstenen gün ve saate yeni çalışma bloğu ekleme, düzenleme ve silme.
- **Hızlı Sayaç Entegrasyonu**: Görev kartından tek tıkla hedef ders ve konuyu Pomodoro sayacına aktarma.

### 3. Odak Sayacı & Çalışma Günlüğü (Pomodoro / Stopwatch & Logger)
- **Zamanlayıcı Ön Ayarları**: 25 dk Pomodoro, 5 dk Kısa Mola, 15 dk Uzun Mola ve Serbest Kronometre.
- **Web Audio API Ses Bildirimi**: Harici ses dosyası bağlantısına ihtiyaç duymadan tarayıcı içi sentezlenen zarif zil/çan uyarısı (çevrimdışı ve sessiz mod desteği).
- **Global Sayaç Rozeti**: Farklı sekmelerde gezinirken üst çubukta sayacın canlı akışı izlenebilir.
- **Çalışma Günlüğü (Excel Şablonu Formatı)**:
  - Planlanan dakika vs. Gerçekleşen dakika karşılaştırması
  - Odak puanı (1 - 5 yıldız)
  - Retrospektif ve zorluk günlüğü ("Ne öğrendim / nerede takıldım?")
- **Analitik Grafikler**: Chart.js ile ders bazlı odaklanma süresi dağılımı (koyu/açık tema uyumlu).

### 4. Sınavlar, Quizler & Teslimler (Deadlines & Milestones)
- **Akademik Teslimler**: MATH 240 sınavları, CMPE 325 vize ve quizleri, SENG 491 proje proposal/spec/analysis raporları, HIST 102 sınav ve quizleri, CMPE 421 ödevleri.
- **Gerçek Zamanlı Geri Sayım**: "Bugün!", "X gün kaldı" veya "Sona erdi" rozetleri ile aciliyet renklendirmesi.
- **Filtreleme**: Derse ve öncelik derecesine (`Kritik`, `Yüksek`, `Orta`, `Düşük`) göre süzme.
- **CRUD**: Yeni sınav veya proje teslimi ekleme, düzenleme, silme.

### 5. Not ve GPA Simülatörü (Grade & Weight Simulator)
- **Syllabus Ağırlıkları**: Vize (%35), Quiz/Ödev (%25), Final (%40) bileşenleri.
- **Harf Notu & Katsayı Hesaplama**: AA (4.0) - FF (0.0) aralığı.
- **Dönem GPA Tahmini**: Derslerin AKTS (ECTS) kredilerine göre ağırlıklı genel not ortalaması simülasyonu.
- **Ders Ekleme & Düzenleme**: Yeni ders ekleyebilme, not hedeflerini dinamik değiştirme.

---

## 🚀 Kurulum ve Vercel Üzerinde Yayınlama

Proje tamamen statik ve bağımsızdır (`index.html` ve `vercel.json`).

### 1. Yerel Olarak Çalıştırma
Herhangi bir terminalden projeyi açabilir veya doğrudan `index.html` dosyasına çift tıklayabilirsiniz:
```bash
# Seçenek A: Python basit sunucu
python3 -m http.server 8080

# Seçenek B: npx serve
npx serve .
```
Tarayıcınızda `http://localhost:8080` adresine gidin.

### 2. Vercel'e Ücretsiz Dağıtım (Deploy to Vercel)

#### Yöntem A: Vercel CLI ile (En Hızlı)
```bash
npm install -g vercel
vercel --prod
```
Tüm soruları varsayılan ayarlarla onaylayın. Statik siteniz saniyeler içinde canlıya alınacaktır.

#### Yöntem B: GitHub Entegrasyonu ile
1. Bu dizini bir GitHub reposuna gönderin:
   ```bash
   git init
   git add .
   git commit -m "feat: TEDÜ Akademik Takvim & Çalışma Sistemi"
   git remote add origin https://github.com/<KULLANICI_ADINIZ>/<REPO_ADI>.git
   git push -u origin main
   ```
2. [Vercel Dashboard](https://vercel.com/dashboard) sayfasına gidin.
3. **"Add New Project"** butonuna tıklayıp GitHub reponuzu seçin.
4. Framework Preset olarak **"Other"** (veya varsayılan) seçin, Build Command gerekmez.
5. **"Deploy"** butonuna basın.

---

## 🔒 Gizlilik ve Güvenlik
- Hiçbir veri üçüncü taraf veritabanlarına gönderilmez.
- Tüm takvim kayıtları, çalışma notları ve kişisel hedefler yalnızca kullanıcının yerel tarayıcısında saklanır.
- JSON yedek dosyası oluşturularak istenen bilgisayara veya cihaza taşınabilir.
