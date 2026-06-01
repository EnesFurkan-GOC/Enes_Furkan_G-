# 📊 GM Parfümleri: Yapay Zeka Tabanlı Koku Kategorisi Sınıflandırma ve Nota Arama Motoru

**Ders:** Yapay Zeka Temelleri Dönem Sonu Proje Sunumu
**Öğrenci:** Enes Furkan Göç
**Tarih:** 01/06/2026

---

## 🎯 BÖLÜM 1: PROBLEM TANIMI & AMAÇ

### Neden Bu Problem?
- Parfüm endüstrisindeki koku kombinasyonları ve notalar (vanilya, nane, odunsu vb.) tüketiciler için oldukça karmaşık ve kafa karıştırıcıdır.
- Kullanıcılar e-ticaret sitelerinde arama yaparken sıklıkla harf hataları yapmakta (Örn: "vanilyalı" yerine "vanılyalı" veya "tatli") ve geleneksel veri tabanı sorgularında doğru sonuçlara ulaşamayıp boş sayfalarla karşılaşmaktadır.

### Projenin Amacı
- Parfümlerin marka, isim ve hedef kitle verilerinden koku kategorisini %90+ doğrulukla tahmin edebilen bir yapay zeka sınıflandırma modeli geliştirmek.
- Kullanıcı hatalarını tolere eden Levenshtein tabanlı akıllı bir Türkçe Nota Arama Motoru entegre ederek kullanıcı deneyimini maksimuma çıkarmak.

---

## 💾 BÖLÜM 2: VERİ SETİ & ÖN İŞLEME (DATA PREPROCESSING)

### Veri Kaynağı
- Kaggle üzerinde açık kaynak olarak paylaşılan **Perfume Dataset (Ayush Ghawana)** veri seti projenin temel kaynağıdır.

### Veri Ön İşleme Adımları
1. **Türkçeleştirme:** Orijinal veri setindeki İngilizce koku terimleri (`woody`, `citrus`, `floral`, `sweet` vb.) kodun ilk adımında otomatik olarak Türkçeye çevrilmiştir.
2. **Veri Genişletme (Data Augmentation):** Projenin ticari vizyonunu desteklemek amacıyla popüler lüks parfüm markaları (Chanel, Dior, Creed, Versace vb.) ve niş kokular el ile geniş bir havuz olarak veri setine entegre edilmiştir.
3. **Kararlılık Filtrelemesi:** Modelin ezberlemeden, kararlı bir şekilde öğrenebilmesi adına veri setinde 3'ten az tekrar eden nadir koku kombinasyonları elenerek veri dengesizliği (data imbalance) giderilmiştir.

---

## ⚙️ BÖLÜM 3: YÖNTEM & MODEL MİMARİSİ

### 1. Doğal Dil İşleme (NLP) - Öznitelik Çıkarımı
- Modele parfümlerin marka, hedef kitle ve isim bilgileri tek bir metin bloğu olarak birleştirilerek verilmiştir.
- `TfidfVectorizer` kullanılarak `ngram_range=(1, 3)` ve `sublinear_tf=True` parametreleriyle metinler sayısal öznitelik matrisine dönüştürülmüştür. Kelime üçlemeleri (Örn: "chanel men odunsu") modelin hafızasında ayırt edici birer öznitelik haline getirilmiştir.

### 2. Sınıflandırma Modeli: Random Forest (Rastgele Orman)
- Gelişmiş doğrusal olmayan ilişkileri çözebilmek adına `RandomForestClassifier` algoritması seçilmiştir.
- **Hiperparametre Optimizasyonu:** 500 karar ağacı (`n_estimators=500`) ve dengeli sınıf ağırlıkları (`class_weight='balanced'`) kullanılarak ezberleme (overfitting) engellenmiş, modelin genelleme yeteneği artırılmıştır.

### 3. Esnek Arama Motoru: Levenshtein Algoritması
- Kullanıcıların yazım ve harf hatalarını yakalamak için iki metin arasındaki düzenleme mesafesini (edit distance) ölçen **Levenshtein Mesafe Algoritması** harici bir kütüphane kullanılmadan sıfırdan implement edilmiştir.

---

## 📈 BÖLÜM 4: PERFORMANCE METRİKLERİ VE SONUÇLAR

### Model Performansı
- Yapay zeka modelimiz test verileri üzerinde test edilmiş ve yüksek başarı oranları yakalamıştır:
  - **Doğruluk (Accuracy) Skoru:** 0.90+
  - **F1 Skoru (Ağırlıklı):** 0.90+

### Hata Matrisi (Confusion Matrix) Görselleştirmesi
- İlk denemelerde veri setindeki tüm kategoriler eksenlere sığmadığı için grafik okunmaz bir hal almıştı.
- Yapılan veri filtrelemesi sayesinde `Seaborn` ve `Matplotlib` kütüphaneleriyle **sınıfların dağılımını, modelin doğru tahminlerini ve bocaladığı noktaları net bir şekilde gösteren** şık bir Hata Matrisi grafiği elde edilmiştir.

---

## 💡 BÖLÜM 5: ÇIKARIMLAR & GELECEK ÇALIŞMALAR

### Projeden Elde Edilen Çıkarımlar
- `TfidfVectorizer` girdisine sadece marka değil parfüm isimlerini de eklemek modelin öğrenme kapasitesini ve doğruluğunu doğrudan zirveye taşımıştır.
- Sektörel yapay zeka projelerinde veri setindeki gürültülü (az tekrarlayan) verileri temizlemenin, modelin genel performansını korumak için ne kadar kritik olduğu deneyimlenmiştir.
- Klasik veri tabanı aramaları yerine Levenshtein tabanlı bir yapay zeka algoritması kullanmanın kullanıcı deneyimini ciddi oranda artırdığı görülmüştür.

### Gelecek Geliştirme Önerileri
- Veri seti ilerleyen süreçte daha fazla niş parfüm girdisiyle genişletilebilir.
- Sınıflandırma performansını daha da ileriye taşımak adına Derin Öğrenme (MLP veya LSTM) mimarileri projeye dahil edilebilir.