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
    
## **Projenin Adım Adım Özeti:**<br/>
1. **Veri Yükleme ve Görüntüleme:**
   - CSV dosyasındaki veriler `pandas` kütüphanesi kullanılarak okunmuş ve `data_set` adlı bir veri çerçevesine aktarılmıştır.<br/>
   - `data_set.head(20)` ile veri çerçevesinin ilk 20 satırı görüntülenmiştir.<br/>

2. **Eksik Verilerin Tespiti:**
   - Veri setindeki eksik veriler `data_set.isnull().sum()` komutuyla kontrol edilmiş ve her sütundaki eksik değer sayıları listelenmiştir.

3. **Cinsiyet Dağılımı Analizi:**
   - Veri setinde yer alan müşterilerin cinsiyet dağılımı incelenmiş ve Seaborn kütüphanesi kullanılarak `data_set['Gender'].value_counts()` komutuyla görselleştirilmiştir.

4. **En Çok Tekrar Eden Yaş ve Coğrafi Bölge Tespiti:**
   - Veri setinde en çok tekrar eden yaş grubu ve coğrafi bölge belirlenmiştir. Bu bilgiler veri setindeki sıklık analizleri ile elde edilmiştir.
   - Yaşı belirlemek için `data_set['Age'].value_counts().index[0]`, ülkeyi belirlemek için `data_set['Geography'].value_counts().index[0]` komutları kullanılmıştır.

5. **İspanyol Müşterilerin Kredi Skor Ortalaması Analizi:**
   - Veri setindeki İspanya'da yaşayanların kredi skorlarının onlar basamağına göre ortalaması hesaplanmıştır. Skor ortalaması `np.floor(data_set[data_set['Geography'] == 'Spain']['CreditScore'] / 10) * 10`
 işlemi ile bulunmuş ve gruplanmıştır.

6. **Kadın Müşterilerin Kredi Skor Analizi:**
   - Veri setindeki kadınların kredi skorlarının onlar basamağına göre ortalaması hesaplanmıştır. Skor ortalaması `np.floor(data_set[data_set['Gender'] == 'Female']['CreditScore'] / 10) * 10`
işlemi ile bulunmuş ve gruplanmıştır. Bu analizde NumPy ve Pandas kütüphaneleri kullanılmıştır.

7. **En Az Süre Çalışan Kadın Müşterinin Belirlenmesi:**
   - Veri setinde en az süre çalışan kadının soyadı ve yaş bilgileri belirlenmiştir. İlk olarak kadınların filtrelendiği `data_set[data_set['Gender'] == 'Female']` ve ardından en az süre çalışan kadının soyadı
`ilk_deger['Surname'].values[0]` ve yaş bilgisi `ilk_deger['Age'].values[0]` olarak alınmıştır.

8. **Soyadı En Az İki Kez Tekrar Eden Müşterilerin Tespiti:**
   - Veri setinde soyadı en az iki kez tekrar eden kişilerin listesi oluşturulmuştur. Tekrar eden soyadları belirlemek için `data_set['Surname'].value_counts()` komutu kullanılmış ve en az iki kez tekrar
edenler `tekrar_edenler` listesine eklenmiştir.

9. **Cinsiyete Göre Müşteri Sayısı Grafiği**
   - `plt.figure(figsize=(10, 6))`: Bu satır, yeni bir figür oluşturur ve grafiğin boyutunu 10x6 inç olarak ayarlar.
   - `sns.countplot(x='Gender', data=data_set, palette=['red'])`: Bu satır, seaborn kütüphanesini kullanarak cinsiyete göre müşteri sayısını gösteren bir çubuk grafiği oluşturur.
'Gender' sütunundaki değerlere göre veri setindeki müşteri sayılarını sayar.
   - `plt.title('Cinsiyete Göre Müşteri Sayısı')`: Grafiğe bir başlık ekler.
   - `plt.xlabel('Cinsiyet')` ve `plt.ylabel('Müşteri Sayısı')`: X ekseni için 'Cinsiyet' ve y ekseni için 'Müşteri Sayısı' etiketleri ekler.
   - `plt.show()`: Oluşturulan grafiği ekranda gösterir.
     
10. **Yaş ve Kredi Skoru Dağılımı Grafiği**
    - `plt.figure(figsize=(10, 6))`: Bu satır, yeni bir figür oluşturur ve grafiğin boyutunu 10x6 inç olarak ayarlar.
    - `sns.scatterplot(x='Age', y='CreditScore', hue='Exited', data=data_set, palette='coolwarm', alpha=0.5)`:
Bu satır, seaborn kütüphanesini kullanarak yaş ve kredi skoru arasındaki ilişkiyi gösteren bir dağılım grafiği oluşturur. 'Age' ve 'CreditScore' sütunlarındaki verilere göre noktalar çizilir ve 'Exited' sütunundaki değerlere göre renklendirilir.
    - `plt.title('Yaş ve Kredi Skoru Arasındaki İlişki')`: Grafiğe bir başlık ekler.
    - `plt.xlabel('Yaş')` ve `plt.ylabel('Kredi Skoru')`: X ekseni için 'Yaş' ve y ekseni için 'Kredi Skoru' etiketleri ekler.
    - `plt.show()`: Oluşturulan grafiği ekranda gösterir.
