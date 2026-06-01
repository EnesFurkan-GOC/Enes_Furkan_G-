
# Yapay Zeka Temelleri - Proje Günlüğü

### 20.05.2026
* **Ne yaptım?:** Proje konusuna karar verdim. Kullanıcı tercihlerine göre parfüm önerisi yapacak bir sistem geliştirmeyi seçtim. Kaggle üzerinden "Perfumes Dataset" isimli veriyi bulup bilgisayarıma indirdim.
* **Hangi AI Aracını/Kaynağını Kullandım?:** Kaggle arama motoru ve Gemini (veri seti fikirleri için).
* **Karşılaştığım Sorun ve Nasıl Çözdüm?:** Parfüm verilerinin neredeyse tamamı kategorik (metin) verilerden oluşuyordu. Sayısal veri olmadığı için klasik regresyon modelleri yerine metin benzerliği ve içerik tabanlı filtreleme (Content-Based Filtering) kullanmam gerektiğine karar verdim.
* **Bir Sonraki Adım:** Veriyi yüklemek ve ilk keşifsel analizleri (EDA) yapmak.

### 23.05.2026
* **Ne yaptım?:** Python ortamında Pandas kütüphanesini kullanarak veri setini projeye dahil ettim. Verinin satır/sütun sayılarına, eksik veri olup olmadığına (isnull) ve tekrarlanan verilere (duplicated) baktım.
* **Hangi AI Aracını/Kaynağını Kullandım?:** Google Gemini (Pandas fonksiyonlarını doğru parametrelerle kullanmak için yardım aldım).
* **Karşılaştığım Sorun ve Nasıl Çözdüm?:** `target_audience` ve `type` sütunlarında küçük-büyük harf uyumsuzlukları olduğunu fark ettim (Örn: "edp" ve "EDP", "Male" ve "Men"). Modelin hata yapmaması için bu verileri standart hale getirmem gerekecek.
* **Bir Sonraki Adım:** Veriyi temizlemek ve yapay zeka modelinin anlayacağı sayısal formata dönüştürmek.

### 26.05.2026
* **Ne yaptım?:** Metin tabanlı verileri (kategori, marka, hedef kitle, kalıcılık) birleştirerek her parfüm için tek bir "özellik metni" oluşturdum. Bu metinleri TF-IDF vektörleştiricisi kullanarak yapay zekanın işleyebileceği sayısal matislere dönüştürdüm.
* **Hangi AI Aracını/Kaynağını Kullandım?:** Scikit-learn dökümantasyonu ve ChatGPT.
* **Karşılaştığım Sorun ve Nasıl Çözdüm?:** TF-IDF uygularken bazı stop-words (etkisiz kelimeler) sütun kalitesini bozuyordu. `ngram_range` parametresiyle oynayarak ikili kelime gruplarını da dahil ettim ve daha anlamlı bir matris elde ettim.
* **Bir Sonraki Adım:** Kosinüs Benzerliği (Cosine Similarity) matrisini hesaplamak ve öneri fonksiyonunu yazmak.

### 28.05.2026
* **Ne yaptım?:** Hesaplanan TF-IDF matrisi üzerinden parfümlerin birbirine olan benzerlik oranlarını bulan Kosinüs Benzerliği algoritmasını entegre ettim. Bir parfüm adı girildiğinde ona en benzer 5 parfümü getiren fonksiyonu yazdım.
* **Hangi AI Aracını/Kaynağını Kullandım?:** Stack Overflow ve Gemini.
* **Karşılaştığım Sorun ve Nasıl Çözdüm?:** Kullanıcı var olmayan veya küçük-büyük harfi farklı bir parfüm girdiğinde sistem hata veriyordu. Girdileri `.lower().strip()` fonksiyonlarıyla temizleyerek ve hata yakalama (try-except) blokları ekleyerek bu sorunu çözdüm.
* **Bir Sonraki Adım:** Modeli test etmek, metrikleri değerlendirmek ve dokümantasyonu tamamlamak.

### 30.05.2026
* **Ne yaptım?:** Geliştirdiğim öneri sistemini test ettim. Örneğin "nitro red" girildiğinde sistemin getirdiği diğer parfümlerin gerçekten de benzer kategoride (Fresh Scent) ve hedef kitlede (Male) olduğunu doğrulayarak kullanıcı testini başarıyla tamamladım. GitHub reposunu hazırladım, README ve gereksinimler dosyasını oluşturdum.
* **Hangi AI Aracını/Kaynağını Kullandım?:** Gemini (README şablonu ve sunum hatları için).
* **Karşılaştığım Sorun ve Nasıl Çözdüm?:** Doğruluk ölçümü için elimizde etiketli bir test verisi yoktu (Öneri sistemlerinin genel sınırlılığı). Bu yüzden değerlendirme metriği olarak "Kullanıcı Testi ve Manuel Alaka Düzeyi Oranı" (Relevance Rate) yöntemini seçtim ve sonuçları yorumladım.
* **Bir Sonraki Adım:** 1 Haziran'daki sözlü savunma ve sunuma hazırlanmak.