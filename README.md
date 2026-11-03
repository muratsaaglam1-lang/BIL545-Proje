# BIL545 – Veri Madenciliğinde İleri Konular

**Üsküdar Üniversitesi – Bilgisayar Mühendisliği Yüksek Lisans Programı**  
**2026–2027 Güz Dönemi**

Bu depo, BIL545 Veri Madenciliğinde İleri Konular dersi kapsamında gerçekleştirilen proje çalışmalarını içerir.

## 1. Grup Bilgileri

| Bilgi | Açıklama |
|---|---|
| Öğrenci 1 | Murat Sağlam |
| Öğrenci No 1| 264327008 |
| Öğrenci 2 | Yasin Göktepe |
| Öğrenci No 2| 264327007 |
| Grup | 2 kişilik grup |
| Ders | BIL545 – Veri Madenciliğinde İleri Konular |
| Üniversite | Üsküdar Üniversitesi |

## 2. Proje 1 – COMPAS Risk Skoru Analizi

### Proje konusu

ProPublica tarafından yayımlanan COMPAS (Correctional Offender Management Profiling for Alternative Sanctions) veri kümesi kullanılarak, iki yıl içinde yeniden tutuklanma durumunun sınıflandırılması ve model sonuçlarının değerlendirilmesi amaçlanmıştır.

Çalışmada veri keşfi, ön işleme, veri sızıntısı kontrolleri, sınıflandırma algoritmaları, model değerlendirme ve alt gruplar açısından adillik incelemeleri gerçekleştirilmiştir.

**Veri kaynağı:**  
[ProPublica – COMPAS Analysis GitHub Repository](https://github.com/propublica/compas-analysis)

**Veri kümesi:** `compas-scores-two-years.csv`

**Lisans ve kullanım koşulları:**  
Kaynak ProPublica deposunda veri kümesi için açıkça tanımlanmış ayrı bir lisans dosyası bulunmamaktadır. Bu nedenle veri kümesi için ayrıca bir açık kaynak lisansı iddia edilmemektedir. Veri kaynağına atıf yapılmış, veri dosyaları bu proje deposuna yeniden yüklenmemiştir.

## 3. Veri Kümesinin İndirilmesi

Veri kümesi ProPublica'nın resmî GitHub deposundan temin edilmektedir:

https://github.com/propublica/compas-analysis

Notebook içerisindeki veri yükleme adımları takip edilerek veri kümesi çalışma ortamına alınabilir.

**Not:** Veri dosyaları GitHub proje deposuna eklenmemiştir. Bu tercih ders yönergesindeki veri paylaşım kuralına uygundur.

## 4. Projenin Çalıştırılması

1. `proje1/` klasöründeki `BIL545_Proje1_COMPAS_Murat_Saglam.ipynb` dosyasını açın.
2. Notebook'u Google Colab ortamına aktarın.
3. Gerekli kütüphanelerin kurulum hücrelerini çalıştırın.
4. Veri yükleme adımını tamamlayın.
5. Notebook hücrelerini yukarıdan aşağıya sırasıyla çalıştırın.
6. Tüm hücrelerin hatasız tamamlandığını kontrol edin.

## 5. Sonuç Özeti

### Sınıflandırma modelleri

Modeller çapraz doğrulama sonuçlarına göre değerlendirilmiştir.

| Model | Balanced Accuracy | F1 Score | ROC AUC |
|---|---:|---:|---:|
| Gradient Boosting | 0.680 ± 0.016 | 0.638 ± 0.019 | 0.741 ± 0.016 |
| Random Forest | 0.672 ± 0.014 | 0.637 ± 0.017 | 0.731 ± 0.016 |
| k-NN | 0.656 ± 0.016 | 0.609 ± 0.016 | 0.702 ± 0.021 |
| Decision Tree | 0.654 ± 0.012 | 0.625 ± 0.016 | 0.702 ± 0.013 |
| Dummy Classifier | 0.500 ± 0.000 | 0.000 ± 0.000 | 0.500 ± 0.000 |

Bu değerlendirmede Gradient Boosting en iyi aday model olarak seçilmiştir.

### Weka ile bağımsız kontrol

Python sonuçları Weka ortamında ZeroR ve J48 algoritmaları kullanılarak ayrıca kontrol edilmiştir.

- ZeroR doğruluk oranı: %54.49
- J48 doğruluk oranı: %64.89
- J48 Kappa: 0.2805
- J48 ROC Area: 0.677
- J48 Weighted F-Measure: 0.643

Weka sonuç ekran görüntüleri `proje1/` klasöründe bulunmaktadır.

### Adillik değerlendirmesi

Model sonuçları ırk ve cinsiyet grupları açısından ayrıca incelenmiştir. Gruplar arasında yanlış pozitif ve yanlış negatif oranlarının farklılaşabildiği gözlemlenmiştir. Özellikle küçük örneklem büyüklüğüne sahip grupların sonuçları dikkatli yorumlanmalıdır.

Bu değerlendirmede kullanılan test bölmesi, ana model değerlendirmesindeki rastgelelik tohumundan farklıdır. Bu nedenle sonuçlar ana model tablosuyla doğrudan aynı deneyin çıktıları olarak değerlendirilmemelidir.

### McNemar testi

Notebook içerisindeki model karşılaştırma bölümünde McNemar testi uygulanmıştır. Ana notebook sonucunda p-değeri 0.1709 olarak elde edilmiştir. Sonuç, kullanılan karşılaştırma koşulları çerçevesinde yorumlanmalıdır.

## 6. Katkı Beyanı

Proje 2 kişilik grup çalışması olarak yürütülmüştür.

## Contribution Statement – Grup Katkıları

### Murat Sağlam
- COMPAS veri setinin araştırılması ve veri keşif çalışmalarının yürütülmesi.
- Veri ön işleme, temizleme ve modelleme süreçlerinin gerçekleştirilmesi.
- Makine öğrenmesi modellerinin geliştirilmesi ve performans değerlendirmelerinin yapılması.
- Python ortamında model sonuçlarının karşılaştırılması ve istatistiksel değerlendirmelerin gerçekleştirilmesi.
- Jupyter/Google Colab notebook yapısının hazırlanması ve proje dokümantasyonunun oluşturulması.

### Yasin Göktepe
- ProPublica COMPAS araştırmasının incelenmesi ve kullanılan kaynakların doğrulanması.
- Weka ortamında ZeroR ve J48 algoritmalarına ait sonuçların incelenmesi.
- Python ve Weka ortamlarında elde edilen model sonuçlarının karşılaştırılması.
- Irk ve cinsiyet gruplarına göre model performanslarının ve adalet değerlendirmelerinin incelenmesi.
- Elde edilen bulguların yorumlanması ve proje sunumuna yönelik hazırlıkların yapılması.

### Genel Açıklama
Proje çalışması, grup üyeleri arasında belirlenen görev dağılımı doğrultusunda yürütülmüştür. Veri hazırlama, model geliştirme ve notebook oluşturma çalışmaları Murat Sağlam tarafından; literatür ve kaynak incelemesi, Weka sonuçlarının değerlendirilmesi, model karşılaştırmaları ve bulguların yorumlanmasına yönelik çalışmalar ise Yasin Göktepe tarafından üstlenilmiştir.

Proje kapsamındaki çalışmaların ve sunumun sorumluluğu Murat Sağlam ve Yasin Göktepe'ye aittir.

## 7. Yapay Zekâ Kullanım Beyanı

Bu proje sürecinde ChatGPT, kod ve analiz adımlarının anlaşılması, hata ayıklama, sonuçların yorumlanması ve dokümantasyonun düzenlenmesi aşamalarında yardımcı araç olarak kullanılmıştır.

Kodların çalıştırılması, elde edilen çıktıların kontrolü ve proje sonuçlarının değerlendirilmesi proje çalışması kapsamında gerçekleştirilmiştir.

## 8. Kaynaklar

1. ProPublica, *Machine Bias: Risk Assessments in Criminal Sentencing*.  
   https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing/

2. Larson, J., Mattu, S., Kirchner, L. ve Angwin, J. (2016). *How We Analyzed the COMPAS Recidivism Algorithm*. ProPublica.  
   https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm/

3. ProPublica – COMPAS Analysis Repository.  
   https://github.com/propublica/compas-analysis

4. Kaufman, S., Rosset, S., Perlich, C. ve Stitelman, O. (2012). *Leakage in Data Mining: Formulation, Detection, and Avoidance*. ACM Transactions on Knowledge Discovery from Data, 6(4).
