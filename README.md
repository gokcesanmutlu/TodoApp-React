1- json server ile kendi apini oluşturduğundan proejyi her açtığında;
önce npm run server ile server'i sonra npm run dev ile projeyi ayağa kaldırmalısın

App.jsx
2- Projede ilk yaptığımız şey server crud ekranı yüklendiğinde ekrana gelmesi için apiden axios ile
verileri çekip bu verileri bir state'te(todos) tuttuk

3- Sonra todos listesini mapleyerek ekrana bastık.

- veriler gelmeden b ir mapleme halinde undefined/null olanı mapleyemez hata alırız. bunu önlemek için map'in başına konulan ?'den yararlandık.
- Maplerken dikkat edilmesi gereken bir diğer konu da :
  Maple ve her bir todo için ekrana bir <listItem> bas derken reactın her bir elemanı ayırt etmesi için bir key vermeliydik. vermeseydik hangi elemanı güncellediğimizi anlayamaz ve tüm elemanları tekrardan render eder. bu da performans sıkıntısı demek. Vereceğimiz key'i ise key={todo.id} şeklinde gönderdik zira elimizde id vardı.

4- veriler gelene kadar ekran boş durmasın diye Loading ekranı yaptık

5- Sırada ListItemlarımızın nasıl görüneceğini düzenlemek var.

- önce listItema gerip todo prop'unu al
- listItem'ın önyüzünü düzenledik.
- badgelere important, daily vs oluşuna göre renk verdik bunu bir incele.
- tarih'i işlemek için helper.js açtık ve orada tarihi istediğimiz formata döndürdük, return ettik.

6-form jsxe geldik.

- formun gönderilişini izlemek için onsubmit={handlesubmit} verdik
- handleSubmiti düzenledik.
- handle submitte formdaki verilere eriştik
- bu verileri axios ile veritabanına göndereceğiz
- bu verileri veri tabanına gönderirken title, status, id, date ve isDone değeri oluşturup göndermeliyiz
- o halde önce handleSubmitte gönderilecek veriyi hazırlayalım. bunun öncesinde form boşken gönderildiğinde alert verelim.
- veritabanına gönderilecek veriyi hazırlama: 17. satırda bunu hazırlamışız

ikinci ders
7- artık yapılması gereken hazırlanan veriyi veritabanına eklemek (AXIOS POST).Post yaptık ekledik
8- Db.jsona bakarsan verinin veritabanına eklendiğini görürüz ancak ekranı yenilemeden bizim ekranımıza yansımaz. çünkü app jsx.'deki 13. satır civarındaki veri çekme isteğimizi boş dizi ile yapmıştık yani sadece sayfa ekrana ilk geldiği anda verileri çekecek ve öylece kalacak
-ikinci hata durumu ise şu: kullanıcı inputa bir şey yazdı ve ben veriyi ekrana bastım, ekranda değişikliği yaptım, değişikliği apiye göndermedim.
Bu durumda ise sayfayı yenileyince değişiklik kaybolacak

9-dolayısıyla değişikliği anında görmek için apiyi güncellemek yetmez
altın kural : api ile çalıştığımız projelerde api güncellendiği anda arayüzü de güncellemeliyiz.
Arayüz güncelleniyorsa api de güncellenecek.

10- burada yapmamız gereken şey şu formda verileri post ettikten sonra apinin yeni hali ile ekranı güncelleme. bunu da post isteğinin then kısmında yapıyoruz. orayı incele (form 30 gibi). formda set todos'u kullanabilmek için app jsx'e döndük settodosu prop olarak gönderdik

11 AXİOS İLE DEL Butonu aracılığıyla silme işlemi

- del butonuna onClick="handleDelete" ekle
- handleDelete fonksiyonunda önce axios ile veritabanına silme isteği at
- ardından then kısmında yani silme isteğinin başarılı olduğu noktada todosları filtreleyerek ekranı da güncelle (lisıtem 9.satır civarı)

12 AXIOS İLE EDİT butonu aracılığıyla güncelleme
ListItemdeyiz.
güncelleme yapacaksak güncelleme modunda mıyız? sorusunun cevabını içeren isEditMode'u state'te tutmamı lazım satır 6
sonrasında edit buttonunun içine bir arrow func. yazdık.
bu fonk is edit değerini click olduğunda true'ya cekti

- bizim yazılmış iş başlığı ve günlük önemli iş kısımlarımızı
  isEditMode' true ise şöyle yaz değil ise böyle yaz şeklinde güncelledik.
- edit dediğimiz anda buttonlar'da güncellenmeli, kaydet iptal et butonları cıkmalı
  yaklaşık 34. satır civarları
- iptal et butonuna tkladığımızda edit moddan çıkıyor.
- kayıt butonuna tıkladığımızda ise yeni verileri alıp apiye kaydetmeliyiz. Bu noktada ayrı bir fonk. çalışmalı(handleEdit).
- handle edit çalıştığında hem inputa hem yanındaki önem derecesi bilgisine erişmemiz lazım.
- bir form içinde olsaydık form bize event kısmında bilgileri verirdi
- 1.  yöntem form içinde olmadığımız için state'te tutmak
- 2. useref kullanarak input ve select'i almak
# TodoApp-React
