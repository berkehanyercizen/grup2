# 3 Samples

Kendi müziğini yaratmanın başka bir yolu da önceden kaydedilmiş sesleri kullanmak olabilir. Hip-hop geleneğinde bu sesler samples olarak adlandırılır. Daha anlaşılır kılmak gerekirse yağmur damlalarının oluşturduğu sesi kaydetmek bir sample olarak gösterilebilir.
Bu sample’lae sayesinde SonicPi üzerinde oldukça eğlenceli şeyler yapılabilir. SonicPi’da kolayca erişebileceğiniz 90 dan fazla örneğin yanı sıra kendiniz de smaplelar yaratabilir ve hazır bulunanlar üzerinde oynamalar gerçekleştirebilirsiniz. Haydi nasıl olduklarına bakalım...

## 3.1 Triggering Samples

‘Beep’leri kullanmak SonicPi’ın yalnızca başlangıcı. Önceden kaydedilmiş sampleları çalıştırarak farklı şekillerde de müzikler yaratabiliriz. Hadi aşağıdaki satırı deneyelim:
```
sample :ambi_lunar_land
```
Önceden de belirttiğimiz gibi SonicPi içerisinde bir çok sample mevcut. Bu sample’ları  ‘play’ komutunun kullandığımız gibi kullanabiliriz. Notalarla ve sample’larla oynamak için alt alta yazmamız yeterli:
```
play 36
play 48
sample :ambi_lunar_land sample :ambi_drone
```
Eğer notalarımızın ya da sample’larımızın arasında zaman boşlukları istiyorsak ‘sleep(milisaniye)’ komutunu kullanabiliriz:
```
sample :ambi_lunar_land sleep 1
play 48
sleep 0.5
play 36
sample :ambi_drone sleep 1
play 
```
  SonicPi’ın başka bir sesi başlatmak için öncekinin bitmesini beklemediğini farkettiniz mi?  ‘sleep’ komutu yalnızca satırlarda yazan komutların başlatılması arasında bekleme yapar. Bu durum da bize sesleri üzt üste oynatarak ilginç efektler yaratmamız konusunda yardımcı olur. İlerleyen aşamalarda seslerin zamanlamalarının nasıl kontrol edildiği konusuna da değineceğiz.
  
### Discovering Samples
SonicPi üzerinde hazırda bulunan sample’ları keşfetmenin iki yolu mevcut. Öncelikle programın yardım sistemi bir seçenek olarak değerlendirilebilir. Solda dikey olarak bulunan menüde ‘samples’ a tıkladıktan sonra kategorinizi seçin ve işte karşınızda kullanabileceğiniz sample’ların bir listesi.

Alternatif olarak da program yazarken size yardımcı olacak otomatik-tamamlama sistemini kullanabilirsiniz. Kodunuzu yazarken yazdığınız komutlara uygun seçenekler SonicPi tarafından size göterilecektir. Örneğin, programda sample :ambi_ yazdığınız zaman aşağıda göreceğiniz seçenekler liste olarak karşınıza çıkacaktır.

- :ambi_
- :bass_
- :elec_
- :perc_
- :guit_
- :drum_
- :misc_
- :bd_
Artık ‘sample’ları çalışmalarımızda kullanmaya başlayabiliriz.

## 3.2 Sample Parameters Amp and Pan
‘synth’ methodunda da gördüğümüz üzere sesleri parametreler sayesinde kolayca kontrol edebiliyoruz. ‘sample’lar aynı parametreleri kullanmamıza izin vermektedir. Haydi *amp:* ve *pan:* parametrelerimizi hatırlayalım.
### Amping Samples
‘synth’ methodunda kullandığımız şekilde ‘sample’ların ses yüksekliği ile oynayabiliriz:
```
sample :ambi_lunar_land, amp: 0.5
```
### Panning Samples
Ayrıca  pan: methodunu da bir diğer parametre olarak kullanma şansına sahibiz. Örneğin, aşağıdaki örnekte :loop_amen ssample’ını sol hoperlörden başlatıp yarısında sağ hoperlöre döndürdük.
```
sample :loop_amen, pan: -1 sleep 0.877
sample :loop_amen, pan: 1
```
Burada ‘sleep’ methodunda 0.877 yazmamzın sebebinin kullanılan sample’ın yarı süresine denk geldiğini belirtmekte fayda var.
Son olarak eğer programda önceden use_synth_defaults kullanarak  (daha sonradan bunun ne olduğuna değineceğiz) ‘synth’ methodu için bazı özellikleri ayarladıysanız bile bunların ‘sample’ tarafından gözardı edileceğini hatırlatalım.

## 3.3 Streching Samples
Artık müziğimizi yaratmak için çeşit çeşit synth ve sample kullanabiliriz. Bunun için şimdi ikisini birlikte nasıl kullanacağımızı daha iyi anlayarak daha eşsiz parçalar yaratmaya çalışmalıyız. İlk olarak *stretch* ve *squash* örnekleri ile başlayalım.
### Sample Representation
‘Sample’lar hoperlörün sesi nasıl çıkarması gerektiğini gösteren, öncededen kaydedilmiş ve sayılar olarak sbilgisayarın hafızasında saklanan seslerdir. Sample içindeki sayılar hoperlörün zarının her birim zamanda ne kadar içeri dışarı hareket etmesi gerektiğini gösterirler. Düzgün bir sample üretebilmek için bilgisayarın genellikle bir saniye için binlerce sayıyı kaydetmesi gerekebilir. SonicPi bu sayılar listesini alır ve bilgisayarın hoperlörünü listeye uygun şekilde hareket ettirerek doğru seslerim oluşmasını sağlar. Bu listedeki sayıları ve zamanlamaları değiştirmek eğlenceli ve ilginç sonuçlar da yaratabilir. 
### Changing Rate
*:ambi_choir* ortam sesini deneyelim. Bunun için sample satırını yazdıktan sonra virgül koymalı ve ardından rate: methodunu eklemeliyiz.
```
sample :ambi_choir, rate: 1
```
‘rate’imiz şu anda 1 olduğu için kendi hızında ve normal bir şekilde çalmakta. Peki ya ‘rate’imiz 1 yerıne farklı bir sayı olursa?
```
sample :ambi_choir, rate: 0.5
```
Ups, neler oldu öyle? Öncelikle ‘sample’ımızın çalma süresi iki katına çıktı ve ikinci olarak da sesimiz bir okta alçaldı. Biraz daha detaya girerek inceleyelim...
### Lets's Stretch
*:loop_amen* sıkıştırarak ve uzatarak oynaması eğlenceli olan bir sample. Normal koşullarda bass bir arkaplan beklenebilir:
```
sample :loop_amen
```
‘rate’i değiştirmek parçanın türünde de değişikliğe sebep olabilir. Yarım hızı deneyip nasıl bir tarz oluştuğuna bakalım:
```
sample :loop_amen, rate: 0.5
```
Aynı şekilde yavaşlatmak yerine hızlandırdığımızda da parçanın türünde değişikliğe sebep olabilirz:
```
sample :loop_amen, rate: 1.5
```
Peki ya negatif bir sayı yazarsak ne olur?
```
sample :loop_amen, rate: -1
```
Tersten çalmaya başladığını fark ettiniz mi? Şimdi farklı negatif değerlerle deneyerek parçanın tersten farkı türlerde nasıl çaldığını deneyebilirsiniz.
### Simple Explanation of Sample Rate
Sample’ları kolayca anlamak için yay dalgalarına benzetmek yardımcı olabilir. Bu noktada sıkışıp genleşen yay dalgalarını düşünebilirz. Parçanın hızı iki katına çıkartıldığında normal dalga boyunun içerisine iki parça sığdırmış oluruz. Bu da dalgayı sıkıştırdığımızı ve normal zamanın yarıs kadar zamanda çalacağını gösterir. Benzer şekilde hızımızı yarıya düşürdüğümüzde parçanın iki kere çalabileceği zaman aralığında yalnızca bir parça çalabiliriz. Sonuç olarak hızımız arttıkça parça kısalacak, düştükçe parça yavaşlayacaktır.  
Bir dalgayı sıkıştırmak dalganın yoğunluğunu arttıracağından ses daha yüksek duyulacaktır. Parça yavaşlatıldığında da benzer olarak sesin daha düşük geldiğini göreceğiz.
### The Maths Behind Sample Rate
(Bu kısım merak edenler için açıklayıcı olması adına eklenmiştir. İsterseniz atlayıp devam edebilirsiniz.)
Öncesinde bahsettiğimiz üzere parçamız hoparlörün zarının zaman içerisinde olması gereken konumunu belirten sayılardan oluşmakta. Bu sayıları liste şeklinde alıp grafiğe dönüştürdüğümüzde aşağıdakine benzer bir şekil ile karşılaşacağız.
***here we have wave pic***
Daha önceden benzer bir grafik ile karşılaşmış olabilirsiniz. Bu grafik dalga gösterimi olarak adlandırılmakta. Bu tarz bir dalga gösterimi her saniye için 44100 adet sayı içerebilmekte. Parçamızı çalarken ‘rate’ değerimiz ile oynadığımızda buradaki veri akış hızını etkilemiş olmaktayız. Daha açık olmak gerekirse parçanın normal hızda çalması için saniyede 44100 adet sayının hoparlöre iletilmesi gerekirken bu sayıyı bölüyor ve çarpıyoruz. Sonucunda da hızı iki katına çıkardığımızda saniyede 88200 adet sayı iletilirken hızı yarıya düşürdüğümüzde de 22050 adet sayı iletiliyor.
Parçamızın çalma süresinin hızı (rate) ile ilişkisini şu şekilde özetleyebiliriz : 
* Hızımızı iki katına çıkarmak çalma süresini yarıya düşürecektir. 
* Hızımızı yarıya düşürmek çalma süresini iki katına çıkartacaktır. 
* Hızımız dörtte birine düştüğünde çalma süresi de dört katına çıkacaktır. 
* Hızımız on katına çıktığında parça normalin 1/10’u sğresinde tamamlanacaktır.
Bu durumu aşağıdaki formül ile de gösterebiliriz:
`Çalma_süresi = (1 / hız(rate)) * parçanın_normal_süresi`
Parçanın hızını değiştirmek parçanın ses yüksekliğini de etkileyecektir. Bir dalganın frekansı ne kadar hızlı aşağı yukarı hareket ettiği gibi düşünülebilir. Parçamız hızlandığında dalganın aşağı yukarı hareketi hızlanacak ve bu durum sesi daha yüksek algılamamıza sebep olacaktır. Benzer şekilde yavaşlatıldığında da sesi daha düşük bir şekilde duyacağız.

## 3.4 Enveloped Samples
Synth  kullanırken çaldığımız notanın zamanlamasını ve ses yüksekliğini ayarlamak mümkün olsa da sample’larda bu durum kısıtlanmakta. Parçamızın zamanını ve ses yüksekliğini azaltabiliyoruz ancak arttırmamız mümkün değil. Ayrıca çaldığımız parçamız hangi durum önce gerçekleşirse ona bağlı olarak çalmayı sonlandıracak: ya parçamızın sonuna geleceğiz ya da *release:* methodumuzun parçayı bitirmesi durumuyla karşılaşacağız. Bir örnekle açıklayacak olursak, eğer *release:* süresini uzun tutarsanız ve parça öncesinde biterse r nin bir anlamı kalmayacak ve parça otomatik olarak sonlandırılacaktır.
### Amen Envelopes
Daha önceden kullandığımız parçamız ile denemeye başlayalım:
```
sample :loop_amen
```
Parçamız normal bir şekilde çaldı. Şimdi parçanın en başından itibaren yükselerek çalmasını sağlamaya çalışalım:
```
sample :loop_amen, attack: 1
```
Daha kısa bir çıkış süresi için değerimizi küçültebilir daha uzun bir çıkış süresi için bu değeri arttırabiliriz:
```
sample :loop_amen, attack: 0.3
```
### Auto Sustain
Parçamızda iniş ve çıkışları kullanırken SonicPi kendi içerisinde hesaplama yapar. (???) ***gotta check this part***
### Fade Outs
Biraz daha iyi anlayabilmek için önceki denemelerde kulladığımız parçamızı tekrardan kullanalım ve SonicPi’dan parçamızın çalma süresini bize çıktı olarak vermesini isteyelim:
```
print sample_duration :loop_amen
```
SonicPi çıktı olarak parçanın süresi için 1.753310657596372 çıktısını verecektir. Hesaplamamızı kolaylaştırmak için bu sayıyı 1.75 olarak ele alabiliriz. Şimdi *release:* parametresini 0.75 olarak ayarladığımızda ilginç bir sonuç ile karşılaşacağız.
```
sample :loop_amen, release: 0.75
```
Parçanın ilk bir saniyelik kısmı seste alçalma olmadan çalacaktır. Bu durum bize SonicPi’ın bir özelliği olan otomatik sustain’in nasıl çalıştığını göstermektedir. SonicPi parçanın release: dışında kalan kısımlarının hepsini sustain: olarak otomatik şekilde ayarlamıştır. Eğer parçamız 10.75 saniye olsaydı ilk 10 saniye normal seviyede çalacak ve son 0.75 saniye ses alçalacaktı.
### Fade In and Out
*attack:* ve *release:* parametlerini SonicPi’ın otomatik sustain modu ile kolayca sustain: parametresini girmek zorunda kalmadan kullanabiliriz.
```
sample :loop_amen, attack: 0.75, release: 0.75
```
Parçamızın normal uzunluğu 1.75 saniye iken attack: ve release: parametrelerini 0.75 saniye olarak ayarladığımızda 0.25 saniyelik tanımsız bir boşluk oluşacaktır. Bu boşluk parçanın ortasında olduğundan SonicPi sustain: parametresini otomatik olarak 0.25 saniye olarak ayarlamaktadır.
### Explicit Sustain
Normalde sistem tarafından kullanılan ayarlara dönmek için sustain: 0 yapmamız yeterli olacaktır.
```
sample :loop_amen, sustain: 0, release: 0.75
```
Bu durumda parçamız eski haline deöndü ve 0.75 saniye çalıyor. attack: ve decay: değerleri de 0 olarak ayarlandığı için parça normal ses yüksekliğinde ve başlangıcından itibaren alçalan bir sesle 0.75 saniye çalıyor.
### Percussive Cymbals
Bu methodu uzun bir parçamızı kısaltmak ve daha vurucu yapmak için kullanabailiriz:
```
:drum_cymbal_open:
sample :drum_cymbal_open
```
Denediğimizde parçanın içindeki periodik vuruşları farkedeceğiz. Buna ek olarak zamanlamaları da ekleyerek daha etkileyici vuruşlar çalmasını sağlayabiliriz.
```
sample :drum_cymbal_open, attack: 0.01, sustain: 0, release: 0.1
```
‘Cymbal’ kullanarak parçamıza vuruşları ekledikten sonra *sustain:* değerini arttırarak vuruşların sönümlenmesini sağlayabiliriz.
```
sample :drum_cymbal_open, attack: 0.01, sustain: 0.3, release: 0.1
```
Haydi şimdi öğrendiklerimizi bir arada kullanarak oluşan farklı sonuçları gözlemleyelim.
## 3.5 Partial Samples
Bu kısımda SonicPi sample methodunda öğrendiklerimizi derleyeceğiz. SonicPi içerisinde kayıtlı olan sample’ları nasıl çaldığımızı öğrenmiştik:
```
sample :loop_amen
```
Ardından bu sample’lar üzerinde hız değişikliği yaparak nasıl bir etki yaratabileceğimizi gözlemledik:
```
sample :loop_amen, rate: 0.5, attack: 1
```
Ayrıca sample kullanırken çalma esnasındaki zamanlamanın  detayına inerek attack:, sustain:, release: parametreleri ile neler yapabileceğimizi gördük:
```
sample :loop_amen, rate: 2, attack: 0.01, sustain: 0, release: 0.35
```
Bunlara ek olarak bir sample çalarken parçanın en başından başlamak zorunda olmasak güzel olmaz mıydı? Peki ya istediğimiz noktada bitirmek istesek?
### Choosing a Starting Point
Parçanın başını 0 değeri sonunu da 1 değeri olarak düşünerek başlangıç ve bitiş noktasını belirtmemiz mümkün:
```
sample :loop_amen, start: 0.5
```
Parçanın son çeyreğine göz atalım:
```
sample :loop_amen, start: 0.75
```
### Choosing a Finish Point
Benzer şekilde *finish:* parametresine 0 ile 1 arasında bir değer verilerek parçanın bu noktada sonlanması ayarlanabilir:
```
sample :loop_amen, finish: 0.5
```
### Specifying Start and Finish
Bahsettiğimiz başlangıç ve bitiş parametrelerini aşağıda gösterildiği gibi aynı satır içerisinde de kullanabiliriz:
```
sample :loop_amen, start: 0.4, finish: 0.6
```
Peki ya başlangıç parametremiz bitiş parametremizden büyükse?
```
sample :loop_amen, start: 0.6, finish: 0.4
```
Ve evet, parçamız tersten çalmaya başlar.
### Combining with Rate
Başlangıç ve bitiş parametrelerinin yanına rate: parametremizi de eklememiz ve parçamızın küçük bir bölümünü yavaş veya hızlı çalmamız mümkün:
```
sample :loop_amen, start: 0.5, finish: 0.7, rate: 0.2
```
### Combining with Envelopes
Son olarak parçanın iniş ve çıkışlarını da parametreler ile belirtip eşsiz bir parça oluşmasını sağlayabilriz:
```
sample :loop_amen, start: 0.5, finish: 0.8, rate: -0.2, attack: 0.3, release: 1
```
Hadi şimdi SonicPi üzerinde hepsini kullanarak farklı şeyler deneyelim.

## 3.6 External Samples
SonicPi’ın içinde bulunan ‘sample’lar hızlı bir şekilde müzik yapmaya başlamana yardımcı olabilmesine rağmen kendi kaydettiğin sesleri ve müzikleri de eklemek isteyebilirsin. SonicPi içerisinde bu tamamen mümkün. Öncelikle dışardan ekleyeceğin bu parçaların taşınabilirliğine bakalım.
### Portability
SonicPi içerisinde bulunan synth’lerle ve sample’larla hazırlanan bir kod çalıştırıldığında bilgisayar yazılanları çalmaya başlar. Mesajla birisine gönderebileceğin bir yazı bilgisayar sayesinde hoş bir müziğe dönüşebilir. Arkadaşlarınla bu müziği yalnızca yazdığın kodu onlara göndererek kolayca paylaşabilirsin.
Ne yazık ki koduna dışarıdan bir müzik parçası eklediğinde kolay bir şekilde paylaşma durumu rafa kalkmak zorunda. Kodunu paylaştığın diğer insanların, yazılan kodun yanısıra bilgisayarındaki örnek müzik dosyasına da ihtiyaçları olmakta. Her ne kadar bu durum kodunu paylaşmanı zorlaştırsa da farklı şeyler deneme arzusunun önüne geçmemeli. Yalnızca olası sonuçları akılda tutarak hareket etmekte fayda var.
### Local Samples
Peki .WAV veya .AIFF dosyasını programımıza nasıl eklemeliyiz?  Yapmamız gereken tek şey dosya uzantısını aşağıda olduğu gibi eklemek.
```
# Raspberry Pi, Mac, Linux
sample "/Users/sam/Desktop/my-sound.wav" # Windows
sample "C:/Users/sam/Desktop/my-sound.wav"
```
SonicPi otomatik olarak dosyayı çalacaktır. Ek olarak öncesinde bahsi geçen bütün parametreler bu durumda da kullanılabilmektedir.
```
# Raspberry Pi, Mac, Linux
sample "/Users/sam/Desktop/my-sound.wav", rate: 0.5, amp: 0.3 # Windows
sample "C:/Users/sam/Desktop/my-sound.wav", rate: 0.5, amp: 0.3
```
