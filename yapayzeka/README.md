# GM Parfümleri - Yapay Zeka Tabanlı Koku Kategorisi Sınıflandırma ve Nota Arama Motoru

Bu proje, parfümlerin marka ve hedef kitle verilerinden yola çıkarak koku kategorilerini tahmin eden bir makine öğrenmesi modeli ile kullanıcıların harf hatası yapsalar dahi aradıkları koku notalarına ulaşmasını sağlayan akıllı bir arama motoru içermektedir.

## 📌 Problem Tanımı
Parfüm endüstrisinde binlerce farklı koku bileşeni (nota) ve karmaşık koku kategorileri bulunmaktadır. Tüketiciler kendilerine uygun doğru kokuyu seçerken veya belirli notaları (vanilya, nane vb.) ararken hem veri karmaşası yaşamakta hem de arama motorlarında harf hataları yaptıklarında doğru sonuçlara ulaşamamaktadır. 

Bu projede;
1. Parfümlerin marka, hedef kitle ve isim algoritmalarından koku kategorisini yüksek doğrulukla tahmin edebilen bir yapay zeka modeli geliştirilmiştir.
2. Kullanıcıların "vanilyalı", "tatli" gibi ekli veya harf hatalı aramalarında dahi doğru parfümleri eşleştirebilen Levenshtein tabanlı bir Türkçe Nota Arama Motoru entegre edilmiştir.

## 📊 Kullanılan Veri Seti ve Kaynağı
Projede Kaggle üzerinde açık kaynak olarak paylaşılan [Perfume Dataset (Ayush Ghawana)](https://www.kaggle.com/datasets/ayushghawana/perfume-dataset) veri seti kaynak olarak kullanılmıştır. 

- **Veri Seti İçeriği:** Orijinal veri setindeki İngilizce koku terimleri (woody, citrus, floral vb.) kodun ilk adımında otomatik olarak Türkçeleştirilmiştir.
- **Veri Genişletme (Data Augmentation):** Yapay zeka modeline zenginlik katması ve projenin ticari vizyonunu desteklemesi amacıyla popüler lüks parfüm markaları ile niş kokular (Bleu De Chanel, Creed Aventus, Sauvage vb.) geniş bir ek havuz olarak Python üzerinde bu veri setine entegre edilmiştir.

## 🛠 Kullanılan Model ve Yöntemler
- **Doğal Dil İşleme (NLP):** `TfidfVectorizer` kütüphanesi kullanılarak `ngram_range=(1, 3)` ve `sublinear_tf=True` parametreleriyle metinsel veriler sayısal öznitelik matrisine dönüştürülmüştür.
- **Sınıflandırma Modeli:** `RandomForestClassifier` (Rastgele Orman) algoritması tercih edilmiştir. Model hiperparametreleri 500 karar ağacı (`n_estimators=500`) ve dengeli sınıf ağırlıkları (`class_weight='balanced'`) ile optimize edilerek ezberleme (overfitting) engellenmiştir.
- **Harf Hatası Yakalama:** İki metin arasındaki düzenleme mesafesini ölçen **Levenshtein Mesafe Algoritması** sıfırdan implement edilerek Türkçe arama motoruna entegre edilmiştir.

## 🚀 Nasıl Çalıştırılır (Kurulum Adımları)
1. Proje reposunu bilgisayarınıza indirin veya klonlayın.
2. Gerekli kütüphaneleri yüklemek için terminale şu komutu yazın:
   ```bash
   pip install -r requirements.txt