# *Medical Cost Analysis*

The main goal of this project is to estimate the potential cost of health insurance for individuals using various factors.

▶Exploratory Data Analysis

In this section of the code, the data was analyzed and meaningful conclusions were drawn from the data. Data visualization techniques were used whenever possible during the analysis.

⊿Dataset Import and First Look:
</br>
Health insurance data was read from a CSV file and assigned to a variable named data.
To preserve the data, the data was copied into a copy called df.
The first few lines of data were displayed with df.head().
Basic statistical information was examined with df.describe() to obtain a general idea about the data.

⊿Veri Görselleştirmesi:
</br>
Histogram çizerek Vücut Kitle İndeksi (BMI) dağılımını görüntülendi.
Nokta grafiği ile "Sigara içenlerin" sağlık masraflarını inceleyerek ilişki anlaşılmaya çalışıldı.
Gruplanmış çubuk grafiği ile "Bölge" ve "Sigara içenlerin" sayısını karşılaştırarak ilişkiyi görüntülendi.
Kutu grafiği ile "Cinsiyet" ve "BMI" arasındaki ilişkiyi değerlendirildi.
Diğer grafiklerle "Yaş-BMI", "Çocuk-BMI", "BMI-Maliyet" gibi ilişkiler görselleştirilerek incelemeye alındı.

⊿Aykırı Değer İncelemesi:
</br>
Kutu grafiği ile "BMI" verisinin aykırı değerlerini görüntülendi.
Aykırı değerleri tespit etmek için IQR yöntemini kullanarak hesaplamalar yapıldı.

▶Data Preprocessing

Kodun bu kısmında ise veri setini düzenlemek ve model eğitimi için uygun hale getirmek için çeşitli ön işleme adımları gerçekleştirilmiştir.
Bu bölümdeki işlemler, verileri sayısal formata dönüştürmek, kategorik değişkenleri kodlamak ve veriyi eğitim-test kümelerine bölmek gibi veri hazırlığı adımlarını içermektedir.

⊿Label Encoding (Etiket Kodlama):
</br>
"sex" ve "smoker" sütunlarını kategorik verileri sayısal değerlere dönüştürmek için etiket kodlama yöntemi kullanıldı.
"sex" sütunu: Kadın (0) ve Erkek (1) olarak kodlandı.
"smoker" sütunu: Sigara İçmeyen (0) ve Sigara İçen (1) olarak kodlandı.

⊿One-Hot Encoding:
</br>
"region" sütunu kategorik olduğu için her bir bölgeyi ayrı bir sütun olarak kodlamak için one-hot kodlama kullanıldı.
"drop='first'" parametresi ile bir bölge sütunu düşürülür çünkü diğer sütunlar zaten o bilgiyi taşıyor.
Yeni kodlanmış "region" sütunları: "region_1", "region_2", "region_3".

⊿Veri Bölme ve Ölçeklendirme:
</br>
Veriler, bağımlı değişken ("charges") ve bağımsız değişkenler ("sex", "smoker", "age", "bmi", "children", "region_1", "region_2", "region_3") olarak ayırıldı.
Veriler eğitim ve test kümelerine ayırıldı (80% eğitim, 20% test).
Veriler standartlaştırarak ölçeklendirildi. Bu, her özelliği aynı ölçüde etkili hale getirdi.

⊿Veri Dağılımını Görselleştirme:
</br>
İki ayrı histogram ile ölçeklendirilmiş eğitim ve test verilerinin dağılımını karşılaştırıldı.
Birinci grafikte, ölçeklendirilmiş eğitim verisinin dağılımı görselleştirildi.
İkinci grafikte, ölçeklendirilmiş test verisinin dağılımını görselleştirildi.

▶Model Selection

Bu kod parçası, farklı regresyon modellerini oluşturup değerlendirmek amacıyla kullanılmıştır.

⊿Modellerin Oluşturulması:
</br>
Bir liste olan models içerisine farklı modelleri ve bu modellere isimlerini ekliyoruz. Modeller: Doğrusal Regresyon, Ridge Regresyon, Lasso Regresyon, Karar Ağacı ve Rastgele Orman Regresyonu.

⊿Çapraz Doğrulama ile Modellerin Değerlendirilmesi:
</br>
Bir döngü yardımıyla her bir model için çapraz doğrulama sonuçlarını değerlendiriyoruz.
cross_val_predict fonksiyonuyla model, ölçeklenmiş eğitim verileri üzerinde çapraz doğrulama yaparak tahminler üretir.
Üretilen tahminlerle gerçek değerler arasındaki ortalama karesel hatayı (RMSE) hesaplayarak modellerin performansını değerlendiriyoruz.
Bu sonuçları cv_rmse_scores adlı bir sözlüğe kaydediyoruz.

⊿Performansın Görselleştirilmesi:
</br>
Oluşturulan modellerin çapraz doğrulama sonuçlarını karşılaştırmak için çubuk grafik çizdiriyoruz.
Grafikte modellerin isimleri x ekseni üzerinde, RMSE değerleri y ekseni üzerinde gösteriliyor.

⊿Model Performans Sonuçlarının Yazdırılması:
</br>
Tüm modellerin çapraz doğrulama sonuçlarını yazdırarak karşılaştırıyoruz.

⊿En İyi Modelin Seçilmesi:
</br>
min fonksiyonu ile en düşük RMSE değerine sahip modeli seçiyoruz.
En iyi modelin adını ve bu modelin en düşük RMSE değerini yazdırıyoruz.

▶Hyperparameter Optimization

Bu kod parçası, Random Forest Regressor modeli için en iyi hiperparametreleri belirlemek ve bu parametrelerle daha iyi bir performans elde etmek amacıyla hiperparametre optimizasyonu yapmaktadır.

⊿Model ve Parametrelerin Belirlenmesi:
</br>
"Random Forest Regressor" modeli oluşturulur.
param_grid adlı bir sözlük oluşturulur, bu sözlük içinde modelin hiperparametrelerinin olası değerleri belirtilir. Bu değerler üzerinde deneme yapılacaktır.

⊿Izgara Arama (Grid Search):
</br>
GridSearchCV kullanılarak parametrelerin farklı kombinasyonları üzerinde deneme yapılır.
cv=5 ile 5 katlı çapraz doğrulama yapılır.
scoring='neg_mean_squared_error' ile hata karesinin negatifini en aza indirgeyerek skorlama yapılır.
En iyi parametreleri ve bu parametrelerle elde edilen en iyi RMSE skorunu yazdırır.

⊿Parametre Kombinasyonlarının Görselleştirilmesi:
</br>
İlk olarak, "n_estimators" ve "max_depth" parametrelerinin RMSE skorlarını bir ısı haritasıyla görselleştirir.
İkinci olarak, "max_depth" ve "n_estimators" parametrelerinin RMSE skorlarını başka bir ısı haritasıyla görselleştirir.

⊿"max_features" Parametresinin Görselleştirilmesi:
</br>
"max_features" parametresinin farklı değerlerine göre elde edilen RMSE skorlarını çubuk grafiği ile görselleştirir.
Her çubuğun üstüne ilgili RMSE değeri yazdırır.

▶Model Evaluation

Bu kod parçası, eğitilmiş Random Forest Regressor modelinin performansını değerlendirmek için MSE, MAE ve R-kare gibi metrikleri hesaplar ve sonuçları yazdırır. 
Bu metrikler, modelin ne kadar iyi çalıştığını anlamak için kullanılır.

⊿Modelin Tahminleri:
</br>
grid_search.best_estimator_ ile hiperparametre optimizasyonu sonucunda bulunan en iyi modeli kullanarak test verileri üzerinde tahminler yapılır.
Bu tahminler y_pred_rf değişkeninde saklanır.

⊿MSE (Mean Square Error) Hesaplama:
</br>
Gerçek değerlerle tahmin edilen değerler arasındaki karesel farkların ortalama değeri olan MSE hesaplanır.
Daha düşük MSE değeri, tahminlerin gerçek değerlere ne kadar yakın olduğunu gösterir.

⊿MAE (Mean Absolute Error) Hesaplama:
</br>
Gerçek değerlerle tahmin edilen değerler arasındaki mutlak farkların ortalama değeri olan MAE hesaplanır.
Daha düşük MAE değeri, tahminlerin gerçek değerlere ne kadar yakın olduğunu gösterir.

⊿R-kare (Coefficient of Determination) Hesaplama:
</br>
Gerçek değerlerle tahmin edilen değerler arasındaki varyans oranını hesaplayan R-kare hesaplanır.
1'e yaklaşan R-kare değeri, tahmin modelinin gerçek verileri ne kadar iyi açıkladığını gösterir.
