#A.7 - Bizet Beats
Minecraft'ı sonic Sonic Pi ile kodlayan fantastik dünyaya yaptığımız kısa geziden sonra tekrar müzikal yapalım. Bugün, kodun müthiş gücünü kullanarak doğruca 21. yüzyıla klasik bir operatif dans parçası getireceğiz.
##Çirkin ve Yıkıcı
1875 yılına dönen zaman makinesine atlayalım. Bizet adında bir besteci en son operası Carmen'i yeni bitirmişti. Ne yazık ki, birçok heyecan verici ve yıkıcı yeni müzik parçası gibi, insanlar başlangıçta hiç beğenmedi çünkü çok çirkin ve farklıydı. Ne yazık ki Bizet, operanın büyük uluslararası başarı kazanmasından on yıl önce öldü ve tüm zamanların en ünlü ve en sık yapılan operalarından biri oldu. Bu trajedi ile sempati duymak için Carmen'in ana temalarından birini ele alalım ve zamanımızdaki çoğu insan için çok çirkin ve farklı olan modern bir müzik biçimine dönüştürelim - canlı kodlanmış müzik!

#A.7 - Habanera'nın Kodunu Çözme
Kod çalıştırmaya çalışmak tüm opera bu eğitim için biraz zor olacak. Hadi en ünlü bölümlerden biri olan Habanera'ya giden bas çizgisine odaklanalım:
 
Henüz müzik notasyonu okumamışsanız, bu size okunaklı görünmeyebilir. Ancak, programcılar olarak müzik gösterimini başka bir kod biçimi olarak görüyoruz - yalnızca bilgisayar yerine bir müzisyenin talimatlarını temsil ediyor. Bu nedenle kod çözmenin bir yolunu bulmamız gerekiyor.

#A.7 - Notalar
Notalar, bu dergideki kelimeler gibi soldan sağa doğru düzenlenir, ancak farklı yüksekliklere de sahiptir. Skordaki yükseklik notun perdesini gösterir. Skordaki nota arttıkça, notanın adımı da artar.
Biz zaten Sonic Pi da notanın perdesinin nasıl değiştirileceğini biliyoruz. Biz play 75 ve play 80 gibi yüksek veya düşük numaraları kullanıyoruz. Ya da nota adlarını kullanıyoruz play :E ve play :F. Neyse ki müzikal puanın dikey konumlarının her biri belirli bir nota adını temsil eder. Bu kullanışlı arama masasına bir göz atın:
 
#A.7 - Rests
Müzik notaları, birçok şeyle iletişim kurabilen son derece zengin ve etkileyici bir kod türüdür. Bu nedenle, müzik notalarının yalnızca hangi notaları çalacağınızı değil, aynı zamanda notaları çalamayacağınızı da söyleyebilmesi sürpriz olmamalıdır . Programlamada bu, nil ya da null- bir değerin olmaması fikrine eşdeğerdir . Başka bir deyişle, nota çalmamak notanın olmaması gibidir.
Eğer skora yakından bakarsanız, gerçekte oyun oynamak için notaları temsil eden siyah noktaların ve diğerlerini temsil eden şeylerin dalgalanmalarının olduğunu göreceksiniz. Neyse ki Sonic Pi'nin dinlenmek için çok kullanışlı bir temsili var: :r yani kaçarsak: play :r aslında sessizlik oynuyor! Ayrıca play :rest, play nil ya play false da bunların hepsini temsil etmenin eşdeğer yolları olarak yazabiliriz .

#A.7 - Ritim
Son olarak, notasyonda kod çözmeyi öğrenecek son bir şey var: notaların zamanlaması. Orijinal gösterimde notaların kiriş adı verilen kalın çizgilerle bağlantılı olduğunu göreceksiniz. İkinci nota bu kirişlerden ikisine sahiptir, yani atımın 16'sına kadar devam eder. Diğer notaların tek bir ışını vardır, bu da bir vuruşun 8'i için devam ettiği anlamına gelir. Gerisi iki dalgalı kirişe sahiptir, yani aynı zamanda atımın 16'sını temsil eder.
Yeni şeyleri çözmeye ve keşfetmeye çalıştığımızda çok kullanışlı bir numara, her türlü ilişkiyi veya örüntüyü denemek ve görmek için her şeyi mümkün olduğunca benzer yapmaktır. Örneğin, notasyonumuzu yalnızca 16'lı yıllarda tekrar yazdığımızda, notasyonumuzun sadece güzel bir nota ve dinlenme dizisine dönüştüğünü görebilirsiniz.
 
#A.7 - Habanera'yı yeniden kodlamak
Şimdi bu bas çizgisini Sonic Pi'ye çevirmeye başlayacağız. Hadi bu notları kodlayalım ve bir halkada dinlenelim:
(ring :d, :r, :r, :a, :f5, :r, :a, :r)
Bunun neye benzediğini görelim. Canlı bir döngüde atın ve işaretleyin:
live_loop :habanera do
  play (ring :d, :r, :r, :a, :f5, :r, :a, :r).tick
  sleep 0.25
end

Muhteşem, bu anında tanınabilir riff hoparlörleriniz aracılığıyla canlanır. Buraya gelmek için çok çaba sarf etti, ama buna değdi - beşlik!

#A.7 - Moody Synths
Şimdi bas hattımız var, hadi ameliyat sahnesinin ambiyansının bir kısmını yeniden yaratalım. Denemek :blade için bir synth, karamsar 80'ler tarzı:d Bir dilimleyici ve yankıdan geçen başlangıç notuyla deneyelim :

live_loop :habanera do
  use_synth :fm
  use_transpose -12
  play (ring :d, :r, :r, :a, :f5, :r, :a, :r).tick
  sleep 0.25
end

with_fx :reverb do
  live_loop :space_light do
    with_fx :slicer, phase: 0.25 do
      synth :blade, note: :d, release: 8, cutoff: 100, amp: 2
    end
    sleep 8
  end
end

Şimdi bas satırındaki diğer notları deneyin: :a ve :f5. Unutmayın, durdurma düğmesine basmanıza gerek yok, sadece müzik çalarken kodu değiştirip tekrar çalıştırmaya başladığınızda kodu değiştirin. Ayrıca, dilimleme makinesi en için farklı değerler deneyin phase: gibi opt 0.5, 0.75ve 1.

#A.7 - Hepsini bir araya getirmek
Son olarak, şimdiye kadar tüm fikirleri Habanera'nın yeni bir remiksinde birleştirelim. Bas çizgisinin başka bir bölümünü yorum olarak eklediğimi fark edebilirsiniz. Hepsini yeni bir tampon belleğe yazdıktan sonra, kompozisyonu duymak için Çalıştır'ı tıklayın. Şimdi, durmadan, ikinci çizgiyi ve tekrar tekrar koşarak çıkararak rahatsız et# - bu ne kadar muhteşem! Şimdi, etrafını karıştırmaya başla ve eğlen.

use_debug false
bizet_bass = (ring :d, :r, :r, :a, :f5, :r, :a, :r)
bizet_bass = (ring :d, :r, :r, :Bb, :g5, :r, :Bb, :r)

with_fx :reverb, room: 1, mix: 0.3 do
  live_loop :bizet do
    with_fx :slicer, phase: 0.125 do
      synth :blade, note: :d4, release: 8,
        cutoff: 100, amp: 1.5
    end
    16.times do
      tick
      play bizet_bass.look, release: 0.1
      play bizet_bass.look - 12, release: 0.3
      sleep 0.125
    end
  end
end

live_loop :ind do
  sample :loop_industrial, beat_stretch: 1,
    cutoff: 100, rate: 1
  sleep 1
end

live_loop :drums do
  sample :bd_haus, cutoff: 110
  synth :beep, note: 49, attack: 0,
    release: 0.1
  sleep 0.5
end
 
#A.8 - Bir Minecraft VJ Olun
 
Herkes Minecraft oynadı. Hepiniz inanılmaz yapılar inşa etmiş, kurnaz tuzaklar tasarlamış ve hatta redstone anahtarları tarafından kontrol edilen ayrıntılı araba hatları oluşturmuş olacaksınız. Kaçınız Minecraft ile performans sergilediniz? Profesyonel bir VJ gibi muhteşem görseller oluşturmak için Minecraft'ı kullanabileceğinizi bilmiyorduk.
Minecraft’i değiştirmenin tek yolu fare ile olsaydı, yeterince hızlı bir şekilde işleri değiştirmek için zor bir zaman geçirirsiniz. Neyse ki sizin için Raspberry Pi, kod ile kontrol edilebilir bir Minecraft sürümü ile birlikte geliyor. Ayrıca, Minecraft'ı sadece kolay değil aynı zamanda inanılmaz derecede eğlenceli hale getiren Sonic Pi adlı bir uygulama ile birlikte geliyor.
Günümüzün makalesinde, gece kulüplerinde ve dünyadaki müzik mekanlarında performans oluşturmak için kullandığımız bazı ipuçlarını ve püf noktalarını göstereceğiz.
Başlayalım…

##A.8 - Başlarken
Temel bilgilerle kendimizi yenilemek için basit bir ısınma egzersiziyle başlayalım. Öncelikle, Raspberry Pi'nizi açıp sonra hem Minecraft hem de Sonic Pi'yi ateşleyin. Minecraft'ta yeni bir dünya yaratın ve Sonic Pi'de yeni bir tampon seçin ve bu koda yazın:
mc_message "Let's get started..."
Çalıştır düğmesine basın, mesajı Minecraft penceresinde göreceksiniz. Tamam, başlamaya hazırız, haydi biraz eğlenelim ……

#A.8 - Kum Fırtınaları
Minecraft'ı görseller oluşturmak için kullanırken hem ilginç görünecek hem de koddan kolayca üretilebilecek şeyler hakkında düşünmeye çalışıyoruz. Güzel bir numara, gökten kum blokları düşürerek bir kum fırtınası yaratmaktır. Bunun için tek ihtiyacımız olan birkaç temel şey:
•	sleep - eylemler arasına gecikme eklemek için
•	mc_location - güncel konumumuzu bulmak için
•	mc_set_block- kum blokları belirli bir yere yerleştirmek için
•	rrand - bir aralıkta rasgele değerler oluşturmamıza izin vermek için
•	live_loop - sürekli olarak yağmur kumu yapmamıza izin vermek için

Herhangi bir yerleşik fn'e yabancıysanız rrand, kelimeyi tamponunuza yazmanız yeterlidir, üzerine tıklayın ve sonra Control-i dahili dokümantasyonu getirmek için klavyedeki combo'yu tıklayın . Alternatif olarak, Yardım sistemindeki dil sekmesine gidebilir ve daha sonra yapabileceğiniz diğer heyecan verici şeylerle birlikte doğrudan fns'a bakabilirsiniz.
Fırtınanın gücünü açığa çıkarmadan önce biraz yağmur yağdıralım. Bulunduğunuz yeri alın ve yakınlardaki gökyüzünde birkaç kum bloğu oluşturmak için kullanın:
x, y, z = mc_location
mc_set_block :sand, x, y + 20, z + 5
sleep 2
mc_set_block :sand, x, y + 20, z + 6
sleep 2
mc_set_block :sand, x, y + 20, z + 7
sleep 2
mc_set_block :sand, x, y + 20, z + 8

Çalıştır'a bastığınızda, şu anda hangi yöne baktığınıza bağlı olarak bloklar arkanıza düşmeye başladığından, biraz etrafa bakmanız gerekebilir. Endişelenmeyin, onları kaçırdıysanız, sadece bir kez daha yağmur yağması için tekrar koşun - sadece doğru yola baktığınızdan emin olun!
Burada neler olduğunu hızla gözden geçirelim. İlk satırda biz fn ile koordinatlar olarak Steve'in yerini kaptı mc_location ve değişkenler içine yerleştirilir x, y ve z. Sonra bir sonraki satırlarda mc_set_block fn'yi Steve ile aynı koordinatlara biraz kum koymak için ama bazı modifikasyonlar için kullandık. Aynı x koordinatını seçtik, ay koordinatı 20 blok daha yüksek ve ardından art arda daha büyük z koordinatları, böylece kum Steve'den uzak bir çizgide düştü.
Neden bu kodu alıp kendinle oynamaya başlamıyorsun? Uyku süreleri, daha satırları ekleyerek değiştirmeyi deneyin, karıştırma deneyin :sand ile :gravel ve farklı koordinat seçin. Sadece deney yap ve eğlen!

#A.8 – Canlı Döngüler
Tamam, fırtına gücünü artırma zamanı live_loop- Sonic Pi'nin canlı kodlamanın tüm gücünü açığa çıkaran sihirli yeteneği çalışırken kodunu değiştiriyor!

live_loop :sand_storm do
  x, y, z = mc_location
  xd = rrand(-10, 10)
  zd = rrand(-10, 10)
  co = rrand(70, 130)
  synth :cnoise, attack: 0, release: 0.125, cutoff: co
  mc_set_block :sand, x + xd, y+20, z+zd
  sleep 0.125
end

Ne komik! Oldukça hızlı bir şekilde dönüyoruz (saniyede 8 kez) ve her döngüde Steve'in yerini daha önce olduğu gibi buluyoruz ama sonra 3 rastgele değer üretiyoruz:
•	xd - fark x için -10 ile 10 arasında olacak
•	zd - fark z için de -10 ile 10 arasında olacak
•	co - Düşük geçiş filtresi için 70 ile 130 arasında bir kesme değeri

Daha sonra bu rasgele değerleri fns'de kullanıyoruz synth ve mc_set_block bize Steve etrafındaki rasgele yerlere düşen kum ve synth'den gelen şiddetli yağmur benzeri bir ses veriyoruz :cnoise.
Canlı döngülere yeni başlayanlar için - bu gerçekten eğlencenin Sonic Pi ile başladığı yer. Kod çalışırken ve kum aşağı doğru akarken, değerlerden birini, belki uyku saatini 0.25 veya :sandblok tipini değiştirmeyi deneyin :gravel. Şimdi tekrar koşmaya başla . Hey! Çabuk! Kod durmadan işler değişti. Bu, gerçek bir VJ gibi performans gösteren geçidiniz. Pratik yapmaya ve çevresinde bir şeyler değiştirmeye devam edin. Kodu durdurmadan görselleri ne kadar farklı yapabilirsiniz?

#A.8 - Epik Blok Kalıpları
 
Son olarak, ilginç görseller üretmenin başka bir harika yolu, yaklaşmak ve yaklaşmak için büyük desenli duvarlar oluşturmaktır. Bu etki için blokları rastgele yerleştirmekten, sıralı bir şekilde yerleştirmeye geçmemiz gerekir. Bunu, iki yineleme kümesini iç içe geçirerek yapabiliriz (Yardım düğmesine basın ve yineleme hakkında daha fazla bilgi için “Yineleme ve Döngüler” dersinin 5.2 bölümüne bakın). Yaptıktan |xd| sonra komik xd olan, yinelemenin her değeri için ayarlanacağı anlamına gelir. Bu yüzden ilk defa 0, sonra 1, sonra 2… vb. Olacak. İki lot yinelemeyi bu şekilde bir araya getirerek, bir kare için tüm koordinatları oluşturabiliriz. Daha sonra ilginç bir etki için blok halkalarından blok türlerini rastgele seçebiliriz:

x, y, z = mc_location
bs = (ring :gold, :diamond, :glass)
10.times do |xd|
  10.times do |yd|
    mc_set_block bs.choose, x + xd, y + yd, z
  end
end

Oldukça temiz. Burada eğleniyor iken bs.choose u bs.tick e değiştirmeyi deneyin. Blok tiplerini değiştirmeyi deneyin ve daha maceracılarınız live_loop, kalıpları otomatik olarak değişmeye devam edecek şekilde yapışmayı deneyebilirsiniz.
Şimdi, VJ finali için - ikisini 10.times değiştirin 100.times ve Run'a basın. Kabooom Rasgele yerleştirilmiş tuğlaların devasa devasa duvarı. Bunu farenizle manuel olarak yapmanın ne kadar süreceğini hayal edin! Sinek moduna girmek ve bazı harika görsel efektler için çekmeye başlamak için alana iki kez dokunun. Yine de burada durmayın - bazı harika fikirleri bir araya getirmek için hayal gücünüzü kullanın ve ardından Sonic Pi'nin kodlama gücünü kullanın. Yeterince pratik yaptığınız zaman ışıkları kısın ve arkadaşlarınız için bir VJ şovu hazırlayın!
 
#A.9 - Sörf Rasgele Akışları

Bu eğitici serinin 4. bölümünde, biraz cızırtılı synth riffleri kodlarken rastgeleleştirmeye kısa bir göz attık. Randomizasyonun canlı kodlama DJ setlerimin bu kadar önemli bir parçası olduğu göz önüne alındığında, temelleri çok daha ayrıntılı bir şekilde ele almanın faydalı olacağını düşündüm. Öyleyse, şanslı şapkanı tak ve biraz rasgele akıntıya gir!

#A.9 – Burada rastgele yok
Sonic Pi'nin randomizasyon fonksiyonları ile oynadığınızda sizi gerçekten şaşırtabilecek şeyleri öğrenecek ilk şey, gerçekten rastgele olmadıklarıdır. Bu aslında ne anlama geliyor? Peki, birkaç test deneyelim. Önce, kafanda 0 ile 1 arasında bir sayı hayal et. Orada kal ve bana söyleme. Şimdi tahmin edeyim ... öyleydi 0.321567? Yok hayır? Bak, açıkça bu konuda iyi değilim. Bir tane daha gideyim, ama Sonic Pi'den bu sefer bir numara seçmesini isteyelim. Sonic Pi v2.7 + 'yı ateşleyin ve rastgele bir numara isteyin ancak bir daha söyleme:
print rand
Şimdi ortaya çıkarmak için… öyle 0.75006103515625mi? Evet! Ha, biraz şüpheci olduğunu görebiliyorum. Belki de sadece şanslı bir tahmindi. Tekrar deneyelim. Çalıştır düğmesine tekrar basın ve ne aldığımızı görün… Ne? 0.75006103515625tekrar? Bu açıkça rastgele olamaz! Haklısın, değil.
Burada neler oluyor? Buradaki süslü bilgisayar bilimi kelimesi determinizmdir. Bu sadece hiçbir şeyin tesadüfen olmadığı ve her şeyin olması gerektiği anlamına gelir. Sonic Pi versiyonunuz daima 0.75006103515625yukarıdaki programa geri dönmeye mahkumdur. Bu oldukça işe yaramaz gelebilir, ancak sizi Sonic Pi'nin en güçlü parçalarından biri olduğuna dair temin ederim. Eğer buna sadık kalırsanız, Sonic Pi'nin randomizasyonunun deterministik doğasına, besteleriniz ve canlı kodlu DJ setleriniz için temel bir yapı taşı olarak nasıl güveneceğinizi öğreneceksiniz.

#A.9 - Rastgele Melodi
Sonic Pi önyükleme yaptığında aslında belleğe 441.000 önceden oluşturulmuş rastgele değerler dizisi yükler. Rand veya gibi rasgele bir işlev çağırdığınızda rrand, bu rasgele akış sonucunuzu üretmek için kullanılır. Rastgele bir işleve yapılan her çağrı, bu akıştan bir değer tüketir. Bu nedenle, rastgele bir işlev için 10. çağrı akıştaki 10. değeri kullanacaktır. Ayrıca, Çalıştır düğmesine her basışınızda, akış o çalışma için sıfırlanır. Bu yüzden sonucu tahmin edebildim rand ve 'rastgele' melodiinin neden her zaman aynı olduğunu belirleyebildim. Herkesin Sonic Pi sürümü, parçalarımızı birbirimizle paylaşmaya başladığımızda çok önemli olan aynı rastgele akışı kullanıyor.
Bu bilgiyi tekrarlanabilir bir rasgele melodi üretmek için kullanalım:
8.times do
 play rrand_i(50, 95)
 sleep 0.125
end

Bunu boş bir ara belleğe yazın ve Çalıştır düğmesine basın. 50 ile 95 arasında 'rasgele' notalardan oluşan bir melodi duyacaksınız. Tamamlandığında, aynı melodiyi tekrar dinlemek için tekrar Çalıştır'a basın.
##Handy Randomisation İşlevleri
Sonic Pi, rastgele akımla çalışmak için çeşitli faydalı işlevler sunar. İşte en yararlı bazılarının bir listesi:
-	rand - Basitçe rastgele akışta bir sonraki değeri döndürür
-	rrand - Bir aralıktaki rastgele bir değeri döndürür
-	rrand_i - Bir aralıktaki rastgele bir tam sayıyı döndürür
-	one_in - Verilen olasılıkla doğru veya yanlış döndürür
-	dice - Zar atmayı taklit eder ve 1 ile 6 arasında bir değer verir
-	choose - Listeden rastgele bir değer seçer
Ayrıntılı bilgi ve örnekler için Yardım sistemindeki belgelerine bakın.

#A.9 - Akışı Sıfırlama
Seçilen notaların bir dizisini tekrarlama kabiliyeti, dans pistinde bir riff oynatmanıza izin vermek için şart olsa da tam olarak istediğiniz riff olmayabilir. Bir dizi farklı riff deneyebilir ve en sevdiğimizi seçebilirsek harika olmaz mıydı? Gerçek sihrin başladığı yer burasıdır.
Akışı fn ile manuel olarak ayarlayabiliriz use_random_seed. Computer Science'ta rastgele bir tohum, yeni bir rastgele değerler akışının filizlenebileceği ve çiçek açabileceği başlangıç noktasıdır. Hadi deneyelim:
use_random_seed 0
3.times do
  play rrand_i(50, 95)
  sleep 0.125
end

Harika, yukarıdaki rastgele melodinin ilk üç notları almak: 84, 83ve 71. Ancak artık tohumu başka bir şeyle değiştirebiliriz. Buna ne dersin:

use_random_seed 1
3.times do
  play rrand_i(50, 95)
  sleep 0.125
end

İlginç, biz olsun 83, 71ve 61. Buradaki ilk iki sayının önceki son iki sayıyla aynı olduğunu fark edebilirsiniz - bu bir tesadüf değil.
Unutmayın ki rastgele akış, yalnızca 'önceden alınmış' değerlerin dev bir listesidir. Rasgele bir tohum kullanmak bizi sadece o listedeki bir noktaya atlar. Bunu düşünmenin bir başka yolu da karıştırılmış kartlardan oluşan büyük bir desteyi hayal etmek. Rasgele bir tohum kullanmak, güverteyi belirli bir noktada kesmektir. Bunun muhteşem kısmı, müzik yaparken bize büyük güç veren rastgele akımın etrafında atlamak için tam da bu yeteneğin olmasıdır.
Bu yeni dere sıfırlama gücü ile 8 notadaki rastgele melodimizi tekrar gözden geçirelim, ama aynı zamanda canlı bir döngüye geçelim;
live_loop :random_riff do
  use_random_seed 0
  8.times do
    play rrand_i(50, 95), release: 0.1
    sleep 0.125
  end
end

Şimdi, hala çalarken, tohum değerini 0 başka bir şeyle değiştirin. Dene 100, ne olmuş 999. Kendi değerlerinizi deneyin, deneyin ve oynayın - hangi tohumun en sevdiğiniz riff'i ürettiğini görün.

#A.9 - Hepsini bir araya getirmek

Bu ayki eğitici bilgiler Sonic Pi'nin randomizasyon işlevselliğinin çalışmalarına oldukça teknik bir dalış oldu. Umarım, nasıl çalıştığı ve müziğinizde tekrarlanabilir kalıplar oluşturmak için randomizasyonu nasıl güvenilir bir şekilde kullanmaya başlayabileceğinize dair bir fikir vermiştir. İstediğiniz her yerde tekrarlanabilir randomizasyon kullanabileceğinizi vurgulamak önemlidir. Örneğin, notların genliğini, ritmin zamanlamasını, reverb miktarını, mevcut sentezi, bir FX'in karışımını vb. Rasgele ayarlayabilirsiniz. Gelecekte bunlardan bazılarına yakından bakacağız. Başvurular, ancak şimdilik sizi kısa bir örnekle bırakmama izin verin.
Aşağıdakileri boş bir ara belleğe yazın, Çalıştır'a basın ve ardından tohumları değiştirmeye başlayın, tekrar Çalıştır'a (hala çalınırken) vurun ve yapabileceğiniz farklı sesleri, ritimleri ve melodileri keşfedin. Güzel bir tane bulduğunuzda, tohum numarasını hatırlayın, böylece geri dönebilirsiniz. Sonunda, hoşunuza giden birkaç tohum bulduğunuzda, tam bir parça oluşturmak için sevdiğiniz tohumlar arasında geçiş yaparak arkadaşlarınız için canlı kodlanmış bir performans sergileyin.
live_loop :random_riff do
  use_random_seed 10300
  use_synth :prophet
  s = [0.125, 0.25, 0.5].choose
  8.times do
    r = [0.125, 0.25, 1, 2].choose
    n = (scale :e3, :minor).choose
    co = rrand(30, 100)
    play n, release: r, cutoff: co
    sleep s
  end
end

live_loop :drums do
  use_random_seed 2001
  16.times do
    r = rrand(0.5, 10)
    sample :drum_bass_hard, rate: r, amp: rand
    sleep 0.125
  end
end
 
#A.10 - Sesinizi Kontrol Etme
Şimdiye kadar bu dizi sırasında sesleri tetiklemeye odaklandık. Sonic Pi’de yerleşik olan birçok sentezi play veya synth ile önceden kaydedilmiş örnekleri nasıl tetikleyeceğimizi keşfettik sample. Ayrıca, bu tetiklenen sesleri, with_fx komut kullanarak yankı ve çarpıtma gibi stüdyo FX içine nasıl sardığımızı da inceledik. Bunu Sonic Pi'nin inanılmaz derecede hassas zamanlama sistemi ile birleştirin ve çok çeşitli sesler, ritimler ve riffler üretebilirsiniz. Ancak, belirli bir sesin seçeneklerini dikkatlice seçtiğiniz ve tetikledikten sonra, doğru çalarken onunla uğraşmak mümkün değil mi? Yanlış! Bugün çok güçlü bir şey öğreneceksiniz - çalışan synth nasıl kontrol edilir.

##Temel Bir Ses
Güzel, basit bir ses yaratalım. Sonic Pi'yi kapatın ve yeni bir tamponda aşağıdakileri yazın:
synth :prophet, note: :e1, release: 8, cutoff: 100

Şimdi güzel bir gürleyen synth sesi duymak için sol üstteki Çalıştır düğmesine basın. Devam edin, hissetmek için birkaç kez tekrar basın. Tamam yapıldı? Kontrol etmeye başlayalım!

##Synth Düğümleri

Sonic Pi Biraz bilinen özelliği FNS olmasıdır play, synth ve sample, dönüş şey denen SynthNode bir koşu sesi temsil eder. Bunlardan birini SynthNode standart bir değişken kullanarak yakalayabilir ve daha sonra daha sonra kontrol edebilirsiniz . Örneğin, cutoff:1 vuruştan sonra opt'in değerini değiştirelim :
sn = synth :prophet, note: :e1, release: 8, cutoff: 100
sleep 1
control sn, cutoff: 130
Sırayla her satıra bakalım:
İlk önce :prophet fn'yi synth normal olarak kullanarak synth'i tetikleriz . Bununla birlikte sonucu ayrıca bir değişkende yakaladık sn. Bu değişkeni tamamen farklı bir şey olarak adlandırmış olabilirdik synth_node ya da jane- isim önemli değil. Ancak, performanslarınız ve kodunuzu okuyan insanlar için sizin için anlamlı bir ad seçmek önemlidir. Sn Synth düğümü için güzel bir kısa hatırlatıcı olarak seçtim .
2. satırda standart bir sleep komutumuz var. Bu özel bir şey yapmaz - bilgisayardan bir sonraki satıra geçmeden önce 1 atım beklemesini ister.
Satır 3, kontrol eğlencesinin başladığı yerdir. Burada, controlfn kullanarak koşu SynthNode değerimizi kesme değerini değiştirmesini söyleriz 130. Eğer vurursanız Çalıştır butonuna, siz duyarsınız :prophet önceki gibi synth başlangıç oynamaya, ancak 1 vuruştan sonra daha parlak bir ses çıkarır.
 
Ayarlanabilir Seçenekler
Sonic Pi'nin synth ve FX tercihlerinin çoğu tetiklendikten sonra değiştirilebilir. Ancak, hepsi için durum böyle değil. Örneğin, kaplama seçmesidir attack:, decay:, sustain: ve release: Synth tetiklerken sadece ayarlanabilir. Hangi seçeneklerin değiştirilebileceğini ve değiştirilemeyeceğini bulmak basittir - verilen bir synth veya FX belgesine gidin ve kişisel seçenek belgesine gidin ve "Oynarken değiştirilebilir" veya "Yapılamaz" ifadelerini arayın ayarlandıktan sonra değiştirilebilir ”. Örneğin, :beep synth’in tercihine ilişkin belgeler attack:, değiştirilmesinin mümkün olmadığını açıkça ortaya koyuyor:
-	Varsayılan: 0
-Sıfır veya daha büyük olmalı
-	Ayarlandıktan sonra değiştirilemez
-	Mevcut BPM değeri ile ölçeklendirildi

##Birden Çok Değişiklik
Bir synth çalışırken, yalnızca bir kez değiştirmekle sınırlı kalmazsınız -istediğiniz kadar değiştirmek için özgürsünüz. Örneğin :prophet, aşağıdakileri içeren mini bir arpejatöre dönüştürebiliriz:
notes = (scale :e3, :minor_pentatonic)
sn = synth :prophet, note: :e1, release: 8, cutoff: 100
sleep 1
16.times do
  control sn, note: notes.tick
  sleep 0.125
end

Bu kod snippet'inde az önce birkaç şey daha ekledik. Öncelikle notes, içinde dolaşmak istediğimiz notları içeren yeni bir değişken tanımladık (bir arpejör, sırayla bir not listesinde dolaşan bir şey için sadece süslü bir isimdir). İkincisi, tek aramamızı control 16 kez yinelemeyle değiştirdik. Her aramada control biz .tick bizim halkanın içinden bir notes biz sonuna (Sonic Pi'nin halkalarının muhteşem gücü sayesinde) bir kez hangi otomatik tekrar edecektir. Çeşitli biraz İçin değiştirmeyi deneyin .tick ile .choose ve farkı duymak görmek.
Birden fazla seçeneği aynı anda değiştirebileceğimizi unutmayın. Kontrol çizgisini aşağıdakine değiştirmeyi deneyin ve farkı dinleyin:
control sn, note: notes.tick, cutoff: rrand(70, 130)

##Kayma

A kontrol ettiğimizde SynthNode, tam zamanında yanıt verir ve anında bir düğmeye basmış ya da değişiklik isteyen bir düğmeye basmış gibi tercihinizi anında yenisiyle değiştirir. Bu ritmik ve vurmalı gelebilir - özellikle opt tınıların bir yönünü kontrol ederse cutoff:. Ancak, bazen değişimin anında gerçekleşmesini istemezsiniz. Bunun yerine, bir kaydırıcıyı veya kadranı oynatmışsınız gibi geçerli değerden yenisine sorunsuzca geçmek isteyebilirsiniz. Tabii ki, Sonic Pi bunu da _slide: tercihlerini kullanarak yapabilir.
Değiştirilebilecek her tercih, aynı zamanda _slide: bir slayt süresi belirlemenizi sağlayan özel bir ilgili seçeneğe de sahiptir . Örneğin, amp: vardır amp_slide:ve cutoff:vardır cutoff_slide:. Bu slayt seçenekleri, bir sonraki kontroller sırasında nasıl davranacaklarını bildirdikleri için diğer tüm seçeneklerden biraz daha farklı çalışır. Hadi bir bakalım:
sn = synth :prophet, note: :e1, release: 8, cutoff: 70, cutoff_slide: 2
sleep 1
control sn, cutoff: 130

Bu örneğin, eklenmesi dışında eskisi ile aynı olduğuna dikkat edin cutoff_slide:. Bu, bir dahaki sefere bu synth'in cutoff: kontrolünü ele geçirdiğinde, mevcut değerden yenisine geçmek için 2 vuruş alacağını söylüyor. Bu nedenle, kullandığımız control zaman kesme slaydı 70'den 130'a kadar olan sesleri duyabilirsiniz. Sese ilginç, dinamik bir his verir. Şimdi, cutoff_slide: sesi nasıl değiştirdiğini görmek için zamanı 0,5 gibi kısa bir değere veya 4 gibi daha uzun bir değere değiştirmeyi deneyin. Unutmayın, değiştirilebilir seçeneklerden herhangi birini tam olarak bu şekilde kaydırabilirsiniz ve her _slide: değer tamamen farklı olabilir, böylece kesimin yavaşça kaymasını, ampin hızlı kaymasını ve tava arasında istediğiniz yerde kaymasını sağlayabilirsiniz ...

##Hepsini bir araya getirmek
Haydi, tetiklendikten sonra synthleri kontrol etmenin gücünü gösteren kısa bir örneğe bakalım. Biraz farklı bir sözdizimine rağmen FX'i de tıpkı synth gibi kaydırabileceğinize dikkat edin. FX kontrolü hakkında daha fazla bilgi için yerleşik eğitimin 7.2 bölümüne bakın.
Kodu yedek bir belleğe kopyalayın ve dinleyin. Yine de orada bitmiyor- kodla oynayın. Slayt sürelerini değiştirin, notları, synth, FX ve uyku zamanlarını değiştirin ve tamamen farklı bir şeye dönüştürüp çeviremeyeceğinizi görün!
live_loop :moon_rise do
  with_fx :echo, mix: 0, mix_slide: 8 do |fx|
    control fx, mix: 1
    notes = (scale :e3, :minor_pentatonic, num_octaves: 2).shuffle
    sn = synth :prophet , sustain: 8, note: :e1, cutoff: 70, cutoff_slide: 8
    control sn, cutoff: 130
    sleep 2
    32.times do
      control sn, note: notes.tick, pan: rrand(-1, 1)
      sleep 0.125
    end
  end
end
 
#A.11 - Atışı İzleme
Bu seride geçen ay, Sonic Pi'nin temelini oluşturan randomizasyon sistemine derin bir teknik dalış yaptık. Kodumuz üzerinde belirleyici olarak yeni dinamik kontrol seviyeleri eklemek için bunu nasıl kullanabileceğimizi araştırdık. Bu ay teknik dalışa devam edeceğiz ve dikkatimizi Sonic Pi'nin benzersiz kene sistemine çevireceğiz. Bu makalenin sonunda, ritimler arasında yolunuzu geçiyor olacak ve canlı bir kodlayıcı DJ olma yolunda ilerleyeceksiniz.

#A.11 - Beat Sayımı
Müzik yaparken sıklıkla hangi ritmin olduğuna bağlı olarak farklı bir şey yapmak istiyoruz. Sonic Pi, bir tick ritmin gerçekten gerçekleştiği zaman size kesin kontrol sağlamanız ve hatta kendi temposuyla birden fazla ritmi desteklemeniz için adlandırılan özel bir ritme sayma sistemine sahiptir.
Bir oyun yapalım- aramamız gereken ritmi ilerletmek için tick. Yeni bir tampon açın, aşağıdakini yazın ve Çalıştır'a basın:
puts tick #=> 0

Bu akım yendi döndürür: 0. Çalıştır düğmesine birkaç kez bassanız bile, her zaman geri döneceğine dikkat edin 0. Bunun nedeni, her koşunun 0'dan itibaren sayılarıyla yeni bir vuruş başlatmasıdır. Ancak, koşu hala aktifken, atımı istediğimiz kadar ilerletebiliriz:

puts tick #=> 0
puts tick #=> 1
puts tick #=> 2

Bir #=> kod satırının sonunda sembolü gördüğünüzde, bu satır metni sağ tarafa kaydedecektir. Örneğin puts foo #=> 0, kod programdaki o noktadaki günlüğe puts foo yazdırıyor demektir 0.

#A.11 - Vuruşu Kontrol Etme
Bunun tick iki şey yaptığını gördük. Artar (bir tane ekler) ve mevcut atımı döndürür. Bazen şu anki ritmi, üzerinden yapabileceğimizi arttırmak zorunda kalmadan bakmak istiyoruz look:

puts tick #=> 0
puts tick #=> 1
puts look #=> 1
puts look #=> 1
Bu kodda, ritmi iki kez işaretledikten sonra look iki kere çağırıyoruz . Biz günlüğüne aşağıdaki değerleri görürsünüz: 0, 1, 1, 1. İlk iki ticks 0 sonra 1 beklendiği gibi geri döndü, sonra iki looks sadece iki kez son atım değerini döndürdü 1.

#A.11 - Yüzükler
Şimdi ritmi ilerletebilir ve ritmi tick kontrol edebiliriz look. Sıradaki ne? Geçecek bir şeye ihtiyacımız var. Sonic Pi, riffleri, melodileri ve ritimleri temsil etmek için halkalar kullanır ve kene sistemi özellikle onlarla yakın çalışmak üzere tasarlanmıştır. Aslında, halkaların kendi nokta sürümleri vardır tick ki bunlar iki şey yapar. İlk olarak, düzenli bir kene gibi davranır ve atışı artırır. İkincisi, atımı indeks olarak kullanarak halka değerini arar. Hadi bir bakalım:
puts (ring :a, :b, :c).tick #=> :a

.ticktick halkanın ilk değerini döndürecek özel bir nokta sürümüdür :a. Ringdeki değerlerin her birini .tickbirden çok kez arayarak alabiliriz :

puts (ring :a, :b, :c).tick #=> :a
puts (ring :a, :b, :c).tick #=> :b
puts (ring :a, :b, :c).tick #=> :c
puts (ring :a, :b, :c).tick #=> :a
puts look                   #=> 3
 
Günlüğüne bir göz atın ve göreceksiniz :a, :b, :cdaha sonra ve :a yine. Dikkat edin look döner 3. Aramalar için .tick için düzenli aramalar gibi hareket tick yerel ritmi artırmaz -.
#A.11 - Bir Canlı Döngü Arpejörü

Tick Halkalar ve s'lerle karıştırdığınızda gerçek güç gelir live_loop. Birleştirildiğinde, basit bir arpejörü oluşturmak ve anlamak için gereken tüm araçlara sahibiz. Sadece dört şeye ihtiyacımız var:
-1.	Döndürmek istediğimiz notları içeren bir yüzük.
-2.	Ritmi arttırma ve elde etme aracı.
-3.	Geçerli ritmi dayalı bir nota çalma yeteneği.
-4.	Arpejatörün tekrar etmesini sağlayan bir ilmek yapısı.
Bu kavramların tümü aşağıdaki kodda bulunabilir:
notes = (ring 57, 62, 55, 59, 64)

live_loop :arp do
  use_synth :dpulse
  play notes.tick, release: 0.2
  sleep 0.125
end

Bu çizgilerin her birine bakalım. Öncelikle, sürekli çalacağımız notalarımızı tanımlarız. Daha sonra bizim için yuvarlak olan bir live_loop çağrı yarattık :arp. Her seferinde live_loop synth'i ayarlıyoruz :dpulse ve sonra ringimizi kullanarak bir sonraki notayı çalıyoruz .tick. Bunun, atım sayacımızı artıracağını ve en son atım değerini bir not olarak kullanacağımızı unutmayın. Sonunda, tekrar döngü yapmadan önce sekizinci atışı bekleriz.
##A.11 - Birden Çok Eşzamanlı Atım
Bilmeniz gereken gerçekten önemli bir şey, bunun tick yerel olması live_loop. Bu, her live_loop birinin kendi bağımsız vuruş sayacına sahip olduğu anlamına gelir. Bu, küresel bir metronom ve dövmeden çok daha güçlü. Buna şu anda bakalım:

notes = (ring 57, 62, 55, 59, 64)

with_fx :reverb do
  live_loop :arp do
    use_synth :dpulse
    play notes.tick + 12, release: 0.1
    sleep 0.125
  end
end

live_loop :arp2 do
  use_synth :dsaw
  play notes.tick - 12, release: 0.2
  sleep 0.75
end
#A.11 - Çatışma Vuruşları

Sonic Pi'nin kene sistemi ile ilgili kafa karışıklığının büyük bir nedeni, insanların aynı anda birden fazla halkayı tıkamak istedikleri zaman live_loop:

use_bpm 300
use_synth :blade
live_loop :foo do
  play (ring :e1, :e2, :e3).tick
  play (scale :e3, :minor_pentatonic).tick
  sleep 1
end

Her birinin live_loop kendi bağımsız vuruş sayacı olmasına rağmen .tick, aynı şey için iki kez çağırıyoruz live_loop. Bu, atımın her seferinde iki kez artırılacağı anlamına gelir. Bu, bazı ilginç polidimler üretebilir ancak genellikle istediğiniz şey değildir. Bu sorunun iki çözümü var. Bir seçenek, tick başlangıcında elle arama yapmak live_loop ve ardından .look her birindeki geçerli ritmi aramak için kullanmaktır live_loop. İkinci çözelti, her çağrı için benzersiz ismi geçmektir .tickgibi .tick(:foo). Sonic Pi daha sonra kullandığınız her bir kene için ayrı bir vuruş sayacı oluşturacak ve izleyecektir. Böylece ihtiyaç duyduğunuz kadar atımla çalışabilirsiniz! Daha fazla bilgi için yerleşik eğitimin 9.4'ünde işaretli keneler bölümüne bakınız.

#A.11 - Hepsini bir araya getirmek
Tüm bu ticks, rings ve live_loops bilgilerini nihai eğlenceli bir örnek için bir araya getirelim. Her zamanki gibi, buna bitmiş bir parça olarak bakma. Bir şeyleri değiştirmeye başlayın ve onunla oynamaya başlayın ve onu neye dönüştürebileceğinizi görün. Bir dahaki sefere görüşürüz…
use_bpm 240
notes = (scale :e3, :minor_pentatonic).shuffle

live_loop :foo do
  use_synth :blade
  with_fx :reverb, reps: 8, room: 1 do
    tick
    co = (line 70, 130, steps: 32).tick(:cutoff)
    play (octs :e3, 3).look, cutoff: co, amp: 2
    play notes.look, amp: 4
    sleep 1
  end
end

live_loop :bar do
  tick
  sample :bd_ada if (spread 1, 4).look
  use_synth :tb303
  co = (line 70, 130, steps: 16).look
  r = (line 0.1, 0.5, steps: 64).mirror.look
  play notes.look, release: r, cutoff: co
  sleep 0.5
end

