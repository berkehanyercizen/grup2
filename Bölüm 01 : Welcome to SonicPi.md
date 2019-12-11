## 1 Hoşgeldin arkadaşım:-)
Sonic Pi'a hoşgeldin.

Umarım sen de benim sana bu platformda göstermek istediğim çılgın sesleri çıkarmaya başlamak için benim olduğum kadar heyecanlısındır.

Müzikle ilgili bir çok şeyden başlayıp; sentezleme, programlama, besteleme, performans ve çok daha fazlasına uzanan çok eğlenceli bir yolculuk olacak.

Ah durun! Ne kadar kabayım.-Ben Sam Aaron- Sonic Pi'ın yaratıcısıyım. 
  Beni Twitter üzerinden @samaaron ismiyle bulabilirsiniz, size merhaba demekten fazlasıyla mutluluk duyacağım.
  Seyirciler önünde yaptığım canlı kodlama performanslarımı merak ederseniz Live Coding Performances adresiniziyaret edebilirsiniz.

Sonic Pi'ı iyileştireceğini ya da geliştireceğini düşündüğün fikirlerin varsa duymak isterim, kullanıcı yorumları bize çok yardımcı oluyor.

Asla bilemezsin! Belki de aklındaki fikir Sonic Pi'ın yeni özelliği olur!

Bu yönerge bölümlere ve kategorilere bölünmüştür. Bu yönergeleri yazarken baştan sona kolay öğrenmebasamaklarını dikkate alarak yazdım, kendinize uygun bir başlık gördüğünüzde okumaktan çekinmeyin.
  Eksik bir şey olduğunu düşünürseniz beni bilgilendirin lütfen belki de yeni gelecek versiyonlarda eklenebilir.
  Son olarak, başkalarını canlı bir şekilde kodlarken izlemek öğremek için gerçekten harika bir yoldur. Genellikle  http://youtube.com/samaaron adresinden canlı yayınlar yapıyorum lütfen uğrayın, bana birmerhaba diyin ve birçok soru sorun :-)
TAMAMDIR, hadi başlayalım...
  
## 1.1 Canlı Kodlama:
Sonic Pi'ın en heyecan verici yönlerinden biri de size kodunuzu canlı calı yazma ve düzenleme imkanı sunmasıdır, tıpkı canlı bir gitar performansında olduğu gibi.

Bu da demek oluyor ki biraz pratik yaptıktan sonra siz de Sonic Pi ile sahneye çıkıp ortalığı 
kasıp kavurabilirsiniz.

## Zihninizi Boşaltın:
Bu yönergenin geri kalanında Sonic Pi'ın çalışması ile ilgili derin deraylara girmeden önce size canlı kodlama deneyimini vermek isterim.
  Eğer bunlardan pek (ya da hiç) bir şey anlamazsanız endişhelenmeyin.
  Yalnızca arkanıza yaslanın ve tadını çıkarın...
## Canlı Tekrar:
Hadi başlayalım, bu kodu kopyalayıp boş kanallardan birine yapıştırın:
``` 
live_loop :flibble do
  sample :bd_haus, rate: 1
  sleep 0.5
end
```
Şimdi "çalıştır" butonuna basın, hızlıca çalan güzel bir davul bası duyacaksınız.
 
 Eğer durdurmak isterseniz "dur" butonuna basın. Bence daha durdura basmayın... Onun yerine aşağıdaki adımları takip edin:
  
1.Bas davulunuzun çalmaya devam ettiğinden emin olun
2.sleep değerini 0.5 den 1 e değiştirin
3.çalıştır butouna yeniden basın
4.Davulun hızının nasıl değiştiğine dikkat edin.
5.Son olarak, /bu anı hatırlayın/, bu sizin Sonic Pi kullanarak ilk canlı kodlayışınız, son olacak gibi de durmuyor...
  
Tamam, bu yeterince basitti. Şimdi miximize başka şeyler de ekleyelim.
  sample :bd_haus kodunun üzerine  sample :ambi_choir, rate: 0.3 satırını ekleyin. Kodunuz şunun gibi olmalı:
 ``` 
live_loop :flibble do
  sample :ambi_choir, rate: 0.3
  sample :bd_haus, rate: 1
  sleep 1
end
```
Şimdi bununla biraz oynayın. Değerleri değiştirin- daha yüksek değerler kullandığınızda, daha düşük değerler kullandıpınızda ya da negatif değerler kullandığınızda oluşan değişimlere dikkat edin. Rate: değerini, :ambi_choir sample'ını çok az değiştirdiğinizde ne olduğuna bakın(mesela 0.29).

Peki çok küçük bir sleep değeri seçerseniz ne olur? Onu bilgisayarınıza hata verdirecek kadar hızlandırıp hızlandıramayacağınızı görün.(Bazen bilgisayarlar Sonic Pi'a yetişemiyor, eğer bu olursa 
sleep değerini biraz büyütmeyi deneyin ve "çalıştır" tuşuna yeniden basın.)

Bazı sample satırlarını # kullanarak yorum haline getirmeyi deneyin.
```
live_loop :flibble do
  sample :ambi_choir, rate: 0.3
  #  sample :bd_haus, rate: 1
  sleep 1
end
```
Bilgisayarınıza onu görmezden gelmesini söylediğini fark ettiniz mi? Bu yüzden o satırı duyamıyoruz.

Buna yorum adı veriliyor. Sonic Pi'da yorumları miximize bir şeyler ekleyip çıkarmak için kullanıyoruz.

Son olarak, size oynayacak bir şeyler bırakmama izin verin. Aşağıdaki kodu kopyalayın ve boş kanallardan birine yapıştırın.
Şuanlık yalnızca iki loop olduğunu görmek dışında çok fazla anlamaya çalışmayın - yani iki şey aynı anda oynatılıyor.
Şimdi de en iyi yaptığınız şeyi yapın - denemeler yapın ve kodları biraz kurcalayın. İşte sizin için birkaç öneri:

*Mavi rate: değelerini değiştirin ve sample ın nasıl değiştiğine göz atın.
*sleep zaman aralıklarını değiştirmeyi deneyin ve iki loop un farklı hızlarda döndüğünü görün.
*Yorum halinde olan sample satırını mixinize ekleyin ce arkada çalan gitar sesinin tadını çıkarın.(başındaki # sembolünü silmelisiniz)
*Mavi mix: değerini 0 (mixe dahil değil) ile 1 (tamamen mixin içinde) değerler vermeyi deneyin.

Her seferinde "çalıştır" butonuna basmayı unutmayın, değişikleri loop başa döndüğünde fark edeceksiniz.

Eğer işleri mahvettiğinizi düşünürseniz dert etmeyin, sadece "durdur" tuşuna basın ve kodları silip yerine buradaki kodu yeniden yapıştırıp eğlencenize devam edin. Ne kadar hata yaparsanız o kadar hızlı öğrenirsiniz...
```
live_loop :guit do
  with_fx :echo, mix: 0.3, phase: 0.25 do
    sample :guit_em9, rate: 0.5
  end
#  sample :guit_em9, rate: -0.5
  sleep 8
end

live_loop :boom do
  with_fx :reverb, room: 1 do
    sample :bd_boom, amp: 10, rate: 1
  end
  sleep 8
end 
```
Denemelerinize Sonic Pi ile neler yapabileceğinizi öğrenmeyi merak kadar devam edin. Artık yönergelerin geri kalanı için hazırsınız.

E hadi o zaman ne bekliyorsunuz...

## 1.2 Sonic Pi Arayüzü:
Sonic Pi gayet basit bir kodlama arayüzüne sahiptir. Hadi keşfetmek için biraz vakit ayıralım.

- **A-Oynatma Kontrolleri**
- **B-Editör Kontrolleri**
- **C-Bilgi ve Yardım**
- **D-Kodlama Editörü**
- **E-Tercih paneli**
- **F-Jurnal Gösterimi**
- **G-Yardım Sistemi**
- **H-Dalga Gösterimi**

###### A. Oynatma Kontrolleri:
Bu pembe butonlar sesleri başlatıp durdurmak için ana kontrollerdir. Kod Editöründeki kodu oynatmak için bir 
"çalıştır" butonu var, kaydetmek için "kaydet" ve çalan sesin bir kayıdını(WAV dosyası olarak) almak için de "kayıt" tuşunu kullanabilirsiniz.

###### B. Editör Kontrolleri:
Bu turuncu tuşlar kod editörünü manipüle etmenizi sağlar. Size+ ve Size- butonları kodunuzdaki yazıları büyütüp küçültmeye yarar.

###### C. Bilgi ve Yardım:
Bu mavi tuşlar sizin bilgi, yardım ve tercihler menülerine girmenizi sağlar. Info tuşu Sonic Pi' ın kendisiyle ilgili bilgiler içeren bir pencere açar - çekirdek kadro, tarihçe, *contibutors* ve topluluğumuz.
  Help tuşu yardım sistemini(G) *toggle*lar ve Prefs tuşu da tercihler penceresini *toggle*lar, bu da sizin bazı basit sistem parametreleriyle oynamanıza izin verir.
  
###### D. Kodlama Editörü:
Bu alan sizin kodlarınızı yazacağınız, besteleme/yorumlama yapacağınız ana alandır. Kodlarınızı yazıp silebileceğiniz, kesip yapıştırabileceğiniz ve benzeri işleri yapabileceğiniz basit bir yazı editörüdür.
  Burayı Word'ün ya da Google Docs'un basit haliymiş gibi düşünebilirsiniz. Editör kelimelerin kod içindeki anlamlarına göre renklerini otomatik olarak değiştirecektir.
  Bu ilk başlarda garip gelebilir ancak çok geçmeden yararını görmeye başlayacaksınız. Örneğin bir şeyin sayı olduğunu mavi olmasından anlayabileceksiniz.
  
###### E. Tercih paneli:
*Buraya yardım*

###### F. Jurnal Gösterimi:
Kodunuzu çalıltırdığınızda programın ne yaptığıyla ilgili bilgiler log viewer'da gösterilir. Otomatik olarak, yarattığınız sesi, bilgisayar sesi ortama verdiği anda burada bir mesaj olarak görürsünüz. Bu sizin kodlarınızdaki sıkıntıları fark etmeniz ve çözmeniz için çok işe yarar bir şeydir, ayrıca kodunuzun ne yaptığını görebilmek kodunuzu anlamak için güzel bir yoldur.

###### G. Yardım Sistemi:
Sonic Pi Arayüzü'nün en önemli parçalarından biri olan yardım sistemi ekranın alt kısmında belirir. Bu mavi "yardım" butonuna tıklayarak açıp kapatılabilir. Yardım sistemi Sonic Pi hakkında derinlemesine bilgi içerir (bu yönergeler, kullanabileceğiniz bir *synths* listesi, örnek müzikler, efektler ve kullanılabilecek olan fonksiyonların tam listesini size sunar.

###### H. Dalga Gösterimi:
Dalga gösterimi size duyduğunuz sesi görmenizde yardımcı olur. Bir saw dalgasının testere şeklinde olduğunu ve basit bir bip sesinin de kıvrımlı bir sinüs dalgasına benzediğini görebilirsiniz. Yüksek ve düşük seslerin dalganın boy farkını nasıl değiştirdiğini görebilirsiniz. Kullanabileceğiniz 3 dalga gösterimi var – varsayılan dalga gösterimi sol ve sağ kanalların birleşiminden oluşur, stereo dalga göstericisi her bir kanal için dalgalar çizer. Son olarak da Lissajous curve dalga gösterimi vardır bu gösterge de size sol ve sağ kanallardaki seslerin aşamalı olarak ilişkisini gösterir bu dalga göstericisi ile güzel resimler yapabilirsiniz (https://en.wikipedia.org/wiki/Lissajous_curve).

## 1.3 Çalarak Öğrenme:
Sonic Pi sizi hem hesaplama hem de müzik yaparken deneysel bir şekilde öğrenmeniz için güzel bir ortamdır. En önemlisi ise eğleniyor olmanız, eğer eğlenirseniz siz daha farkına varmadan kodlamayı ve beste yapmayı öğrenmiş olacaksınız.

## HATA YOK
Hazır bu konuya gelmişken size bir öneride bulunmama izin verin, benim yıllar boyu süren canlı müzik kodlama deneyimimden öğrendiğim şey: hatalarının değil, olanakların olduğudur. Bu jazz aleminde daha çok duyduğum bir cümle ancak canlı kodlayarak müzik yapmak için de eşit derecede geçerlidir. Ne kadar deneyimli olduğunuz hiç önemli değildir – daha yeni başlamış kişilerden bu işi uzun süredir yapan kişilere, ikiniz de beklenmedik sonuçları doğuran aynı kodları çalıştıracaksınız. Çok havalı gözüküyor – siz de kendinizi dalgaya kaptırın. Bununla birlikte, tamamen zır ve yersiz görünebilir ancak önemli olan bir şeyin olmuş olması değil, sizin onunla daha sonra ne yapacağınızdır. Sesi alın, oni işleyin ve harika bir şeye dönüştürün. Kalabalık çıldıracaktır.

## BASİTTEN BAŞLAYIN
Siz öğreniyorken harika şeyleri hemen şimdi yapmak isteyeceksiniz ancak bu isteğinizi tutn ve onu gelecekte ulaşılacak bir hedef haline getirin. Şimdilik, yazabileceğiniz en basit şeyleri düşünün, bu sizin kafanızda düşündüğünüz o harika fikre ulaşmanız için attığınız küçük ve çok iyi hissettiren bir adım olacaktır. Küçük adımları öğrendikten sonra bun adımları uç uca ekleyip yürümeye çalışın, bu adımlarda oynamalar ve değişiklikler yaparak sizi nerelere götüreceğini ve size hangi yeni fikirleri vereceğini görün. Çok geçmeden eğlenmekle ve gerçekten gelişim göstermekle meşgul olacaksınız.

Kendi yaptıklarınızı başkalarıyla paylaşmayı unutmayın!




