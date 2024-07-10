# **Veri Analizi Projesi: Müşteri Profili Analizi**<br/>
## **GİRİŞ**<br/>
Bu projede, bir CSV dosyasındaki veriler Pandas, NumPy ve Seaborn gibi Python kütüphaneleri kullanılarak bir veri çerçevesine yüklenmiş ve çeşitli veri analizleri yapılmıştır.
Analiz süreci, veri setinin incelenmesi, temizlenmesi, keşifsel veri analizi (EDA) yapılması ve görselleştirmelerle desteklenmiştir.<br/>

## **Proje Amaçları**<br/>
- Veri setinin yüklenmesi ve ilk inceleme yapılması<br/>
- Eksik verilerin tespit edilmesi ve gerekirse işlenmesi<br/>
- Cinsiyet dağılımının incelenmesi ve grafikle gösterilmesi<br/>
- En çok tekrar eden yaş grubunun ve coğrafi bölgenin belirlenmesi<br/>
- İspanyol müşterilerin kredi skorlarının ortalamasının hesaplanması<br/>
- Kadın müşterilerin kredi skorlarının yaş ve skor arasındaki ilişkinin analiz edilmesi<br/>
- En az süre çalışan kadın müşterinin bilgilerinin belirlenmesi<br/>
- Veri setinde soyadı en az iki kez tekrar eden müşterilerin listelenmesi<br/>
- Kodu Çalıştırma Talimatları
## **İçindekiler**
1. Veri Yükleme ve İlk İnceleme<br/>
2. Eksik Verilerin Tespiti<br/>
3. Cinsiyet Dağılımı Analizi<br/>
4. En Çok Tekrar Eden Yaş ve Coğrafi Bölge Tespiti<br/>
5. İspanyol Müşterilerin Kredi Skor Ortalaması Analizi<br/>
6. Kadın Müşterilerin Kredi Skor Analizi<br/>
7. En Az Süre Çalışan Kadın Müşterinin Belirlenmesi<br/>
8. Soyadı En Az İki Kez Tekrar Eden Müşterilerin Tespiti<br/>
9. Cinsiyete Göre Müşteri Sayısı Grafiği<br/>
10. Yaş ve Kredi Skoru Dağılımı Grafiği<br/>
11. Kodu Çalıştırma Talimatları
        
## **Projenin Adım Adım Özeti:**<br/>
1. **Veri Yükleme ve Görüntüleme:**
   - CSV dosyasındaki veriler `pandas` kütüphanesi kullanılarak okunmuş ve `data_set` adlı bir veri çerçevesine aktarılmıştır.<br/>
   - `data_set.head(20)` ile veri çerçevesinin ilk 20 satırı görüntülenmiştir.<br/>
### *İşlem Kodları:*<br/>
import pandas as pd <br/>
import seaborn as sns <br/>
import numpy as np <br/>
import matplotlib.pyplot as plt <br/>
data_set=pd.read_csv('/content/drive/MyDrive/Adsız klasör/dataset.csv') <br/>
data_set.head(20)<br/>

2. **Eksik Verilerin Tespiti:**
   - Veri setindeki eksik veriler `data_set.isnull().sum()` komutuyla kontrol edilmiş ve her sütundaki eksik değer sayıları listelenmiştir.<br/>
### *İşlem Kodları:*<br/>
eksik_veriler = data_set.isnull().sum()<br/>
print("Eksik veriler:")<br/>
print(eksik_veriler[eksik_veriler > 0])<br/>

3. **Cinsiyet Dağılımı Analizi:**
   - Veri setinde yer alan müşterilerin cinsiyet dağılımı incelenmiş ve Seaborn kütüphanesi kullanılarak `data_set['Gender'].value_counts()` komutuyla görselleştirilmiştir.
### *İşlem Kodları:*<br/>
top_gender=data_set['Gender'].value_counts()<br/>
print(top_gender)<br/>

4. **En Çok Tekrar Eden Yaş ve Coğrafi Bölge Tespiti:**
   - Veri setinde en çok tekrar eden yaş grubu ve coğrafi bölge belirlenmiştir. Bu bilgiler veri setindeki sıklık analizleri ile elde edilmiştir.
   - Yaşı belirlemek için `data_set['Age'].value_counts().index[0]`, ülkeyi belirlemek için `data_set['Geography'].value_counts().index[0]` komutları kullanılmıştır.<br/>
### *İşlem Kodları:*<br/>
top_age=data_set['Age'].value_counts().index[0]<br/>
print(" listede en çok bulunan yaş:",top_age)<br/>
top_geography=data_set['Geography'].value_counts().index[0]<br/>
print("en çok yer alan ülke:",top_geography)<br/>

5. **İspanyol Müşterilerin Kredi Skor Ortalaması Analizi:**
   - Veri setindeki İspanya'da yaşayanların kredi skorlarının onlar basamağına göre ortalaması hesaplanmıştır. Skor ortalaması `np.floor(data_set[data_set['Geography'] == 'Spain']['CreditScore'] / 10) * 10`
 işlemi ile bulunmuş ve gruplanmıştır.<br/>
### *İşlem Kodları:*<br/>
ispanyollarr=data_set['ispanyollar'] = data_set['Geography'] == 'Spain'<br/>
print(ispanyollar)<br/>
data_set['onluk_skor'] = (np.floor(data_set['CreditScore'] / 10) * 10)<br/>
ispanyolların_skor_ortu = data_set.groupby('onluk_skor', as_index=False)['ispanyollar'].mean()<br/>
print(ispanyolların_skor_ortu)<br/>

6. **Kadın Müşterilerin Kredi Skor Analizi:**
   - Veri setindeki kadınların kredi skorlarının onlar basamağına göre ortalaması hesaplanmıştır. Skor ortalaması `np.floor(data_set[data_set['Gender'] == 'Female']['CreditScore'] / 10) * 10`
işlemi ile bulunmuş ve gruplanmıştır. Bu analizde NumPy ve Pandas kütüphaneleri kullanılmıştır.<br/>
### *İşlem Kodları:*<br/>
data_set['onluk_skor'] = (np.floor(data_set['CreditScore'] / 10) * 10)<br/>
skor_kadınlar = data_set['skor_kadınlar'] = data_set['Gender'] == 'Female'<br/>
skor_kadınlar_ortu = data_set.groupby(['onluk_skor', 'Age'], as_index=False)['skor_kadınlar'].mean()<br/>
print(skor_kadınlar.head(10))<br/>
print(f"\n kadınların ortalama skoru:",skor_kadınlar_ortu)<br/>

7. **En Az Süre Çalışan Kadın Müşterinin Belirlenmesi:**
   - Veri setinde en az süre çalışan kadının soyadı ve yaş bilgileri belirlenmiştir. İlk olarak kadınların filtrelendiği `data_set[data_set['Gender'] == 'Female']` ve ardından en az süre çalışan kadının soyadı
`ilk_deger['Surname'].values[0]` ve yaş bilgisi `ilk_deger['Age'].values[0]` olarak alınmıştır.<br/>
### *İşlem Kodları:*<br/>
skor_kadınlar = data_set['skor_kadınlar'] = data_set['Gender'] == 'Female'<br/>
ds_kadınlar = data_set[data_set['skor_kadınlar']]<br/>
ilk_deger = ds_kadınlar[ds_kadınlar['Tenure'] == ds_kadınlar['Tenure'].min()]<br/>
first_woman_sname = ilk_deger['Surname'].values[0]<br/>
first_woman_age = ilk_deger['Age'].values[0]<br/>
print(ds_kadınlar)<br/>
print("en az süre çalışan kadın:",first_woman_sname )<br/>
print("en az süre çalışan kadın yaşı:",first_woman_age)<br/>

8. **Soyadı En Az İki Kez Tekrar Eden Müşterilerin Tespiti:**
   - Veri setinde soyadı en az iki kez tekrar eden kişilerin listesi oluşturulmuştur. Tekrar eden soyadları belirlemek için `data_set['Surname'].value_counts()` komutu kullanılmış ve en az iki kez tekrar
edenler `tekrar_edenler` listesine eklenmiştir.<br/>
### *İşlem Kodları:*<br/>
deger = data_set['Surname'].value_counts()<br/>
tekrar_edenler = deger[deger >= 2].index<br/>
repeat_list = list(tekrar_edenler)<br/>
print(deger)<br/>
print(tekrar_edenler)<br/>
print("tekrar eden soyadlar  :", repeat_list)<br/>

9. **Cinsiyete Göre Müşteri Sayısı Grafiği**
   - `plt.figure(figsize=(10, 6))`: Bu satır, yeni bir figür oluşturur ve grafiğin boyutunu 10x6 inç olarak ayarlar.
   - `sns.countplot(x='Gender', data=data_set, palette=['red'])`: Bu satır, seaborn kütüphanesini kullanarak cinsiyete göre müşteri sayısını gösteren bir çubuk grafiği oluşturur.
'Gender' sütunundaki değerlere göre veri setindeki müşteri sayılarını sayar.
   - `plt.title('Cinsiyete Göre Müşteri Sayısı')`: Grafiğe bir başlık ekler.
   - `plt.xlabel('Cinsiyet')` ve `plt.ylabel('Müşteri Sayısı')`: X ekseni için 'Cinsiyet' ve y ekseni için 'Müşteri Sayısı' etiketleri ekler.
   - `plt.show()`: Oluşturulan grafiği ekranda gösterir.<br/>
### *İşlem Kodları:*<br/>
plt.figure(figsize=(10, 6))<br/>
sns.countplot(x='Gender', data=data_set, palette=['red'])<br/>
plt.title('Cinsiyete Göre Müşteri Sayısı')<br/>
plt.xlabel('Cinsiyet')<br/>
plt.ylabel('Müşteri Sayısı')<br/>
plt.show()<br/>
### *Grafik:*<br/>

![Cinsiyete Göre Müşteri Sayısı Grafiği](https://github.com/Zeynep981/staj_projesi/blob/main/images/Ekran%20g%C3%B6r%C3%BCnt%C3%BCs%C3%BC%202024-07-10%20145830.png)

10. **Yaş ve Kredi Skoru Dağılımı Grafiği**
    - `plt.figure(figsize=(10, 6))`: Bu satır, yeni bir figür oluşturur ve grafiğin boyutunu 10x6 inç olarak ayarlar.
    - `sns.scatterplot(x='Age', y='CreditScore', hue='Exited', data=data_set, palette='coolwarm', alpha=0.5)`:
Bu satır, seaborn kütüphanesini kullanarak yaş ve kredi skoru arasındaki ilişkiyi gösteren bir dağılım grafiği oluşturur. 'Age' ve 'CreditScore' sütunlarındaki verilere göre noktalar çizilir ve 'Exited' sütunundaki değerlere göre renklendirilir.
    - `plt.title('Yaş ve Kredi Skoru Arasındaki İlişki')`: Grafiğe bir başlık ekler.
    - `plt.xlabel('Yaş')` ve `plt.ylabel('Kredi Skoru')`: X ekseni için 'Yaş' ve y ekseni için 'Kredi Skoru' etiketleri ekler.
    - `plt.show()`: Oluşturulan grafiği ekranda gösterir.<br/>
### *İşlem Kodları:*<br/>
plt.figure(figsize=(10, 6))<br/>
sns.scatterplot(x='Age', y='CreditScore', hue='Exited', data=data_set, palette='coolwarm', alpha=0.5)<br/>
plt.title('Yaş ve Kredi Skoru Arasındaki İlişki')<br/>
plt.xlabel('Yaş')<br/>
plt.ylabel('Kredi Skoru')<br/>
plt.show()<br/>
### *Grafik:*<br/>

![Yaş ve Kredi Skoru Dağılımı Grafiği]()
## **Kodu Çalıştırma Talimatları**<br/>


