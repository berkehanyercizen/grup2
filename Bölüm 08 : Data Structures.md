# 8 Veri Yapıları:
Bir programlamacının alet çantasındaki en kullanışlı alet veri yapılarıdır.

Bazen birden çok şeyi kullanmak ya da sunmak istersiniz. Örneğin, birtakım notaların birbiri ardına çalmasını isteyebilirsiniz. Programlama dilleri de sizin tam olarak bunu yapabilmeniz için veri yapılarına sahiptir.

Programcıların elinin altında birçok enteresan ve egzotik veri yapıları vardır – ve insanlar her geçen gün yenilerini icat ediyorlar. Ancak şimdilik bizim uğraşmamız gereken tek veri yapısı basit bir veri yapısı olan listelerdir.

Hadi biraz daha detaya inelim. Basitçe yapısını inceleyip daha sonra listeleri nasıl ölçekler ve akorlar için kullanabileceğimize bakacağız. 
## 8.1 Listeler:
Bu kısımda çok işimize yarayacak olan bir veri yapısını ele alacağız – listeler. Bu veri yapısıyla daha önceden rastgelelik kısmında bir listeden seçilen rastgele bir notayı çalarken yüzeysel bir şekilde tanışmıştık:

play choose([50, 55, 62])

Bu kısımda listelerin akorları ve ölçüleri de temsil edebildiğini keşfedeceğiz. Öncelikle bir akoru nasıl oynatacağımızı yeniden hatırlayalım. Hatırlayacağınız üzere eğer sleep fonksiyonunu kullanmazsak bütün sesler aynı anda oynatılır:

play 52

play 55

play 59

Hadi bu kodu nasıl başka bir şekilde temsil edeceğimizi görelim.

	Bir Listeyi Çalmak:
Seçeneklerden biri, bütün notaları bir listeye koymaktır: [52, 55, 59]. Bizim akıllı play fonksiyonumuz bir listedeki notaları nasıl çalması gerektiğini bilebilecek kadar zekidir. Hadi dene:

play [52, 55, 59]

Ooh, Böyle yapmak şimdiden okumayı daha da kolaylaştırdı. Bir listeyi çalıyor olmanız sizin herhangi bir parametreyi normaldeki gibi kullanmanıza bir engel oluşturmaz:

play [52, 55, 59], amp: 0.3

Eğer isterseniz MIDI sayıları yerine geleneksel nota isimlerini de bu listelerde kullanabilirsiniz.

play [:E3, :G3, :B3]

Eğer daha önce müzik teorisi eğitimi alma şansına erişmiş biriyseniz bu akorun E Minör ün 3. oktavdan çalınışı olduğunu fark edeceksinizdir.

	Listelere Erişim:
Listelerin bir diğer kullanışlı özelliği de içinden bilgi alabilmenizdir. Bu kulağa biraz garip gelebilir, ama bunu birisinin size bir kitabın 23. sayfasını açmanızı söylemesinden bir farkı yoktur. Sizin de bir liste kullanırken programınızda söyleyeceğiniz şey “23. indexteki eleman nedir?” olacaktır. Bunu tek farklı yanı ise programlamada indexler genellikle 1 yerine 0’dan başlar.

Bir listede indexleri 1, 2, 3… olarak saymak yerine; 0, 1, 2… olarak sayarız.

Hadi biraz daha detaya girelim. Aşağıdaki listeye bakın:

[52, 55, 59]

Bunda korkulacak bir şey yok. Şimdi, bu listedeki 2. eleman nedir? Evet, tabii ki 55. Bu kolaydı. Hadi bakalım şimdi bilgisayara bunun cevabını verdirip verdiremeyeceğimize bakalım:

Puts [52, 55, 59] [1]

Tamam, bu eğer daha önce buna benzer bir şey görmediyseniz size garip gelebilir. Ama bana güvenin, o kadar da zor değil. Yukarıdaki satırda temel olarak 3 parça bulunmakta: “puts“ kelimesi, listemiz “[52, 55, 59]” ve indeximiz olan [1]. İlk olarak “puts” diyoruz, çünkü Sonic Pi’ın bizim için cevabını sağ tarafta yazdırmasını istiyoruz. Sonra, ona listemizi veriyoruz, ve son olarak da indeximiz ondan 2. elemanı istiyor. İndexi köşeli parantez içine almalıyız ve sayma işlemi 0’dan başladığı için 2. Elemanın indexi 1 oluyor. Bakın:

#indexler:   0    1    2
	     [52, 55, 59]

“puts [52, 55, 59] [1]” kodunu çalıştırdığınızda sağ taraftaki log kısmında 55 in listeden alındığını göreceksiniz. 1 indexini diğer indexlerle değiştirin, daha uzun listeleri deneyin ve bu kısımda listelerle ilgili öğrendiklerinizi bir sonraki kodlamanızda nasıl kullanacağınızı düşünün. Mesela, hangi müzik yapıları bir liste halinde ifade edilebilir…

	8.2 Akorlar:
Sonic Pi içinde önceden yüklü bir şekilde listelerinizde kullanabileceğiniz akor isimleriyle gelir. Kendiniz deneyin:

play chord(:E3, :minor)

İşte şimdi bir şeyler yapmaya başladık. Bu şekilde yalın bir listeden daha iyi gözüküyor (ve kodunuzu okumak isteyen insanların da işini kolaylaştırıyor.). Sonic Pi başka hangi akorları destekliyor diye soracak olursanız size cevabım yeterinden fazlasını olacaktır. Bunlardan bazılarını deneyin:

	chord(:E3, :m7)
	chord(:E3, :minor)
	chord(:E3, :dim7)
	chord(:E3, :dom7)

Arpejler:
play_pattern fonksiyonunu kullanarak akorları kolayca arpejlere çevirebiliriz:

play_pattern chord(:3, :m7)

Tamam, biliyorum, bu çok da eğlenceli değil- gerçekten de yavaş bir şekilde çaldı. play_pattern bir liste içindeki her notayı sleep 1 aralığıyla her çalmak istediğinizde çalacaktır. Bir başka fonksiyon olan play_pattern_timed fonksiyonunu kullanarak zamanlamaları özelleştirerek işleri biraz hızlandırabiliriz.

play_pattern_timed chord(:E3, :m7), 0.25

Bir zaman listesi verip zamanın burdan sırayla seçilmesini de sağlayabiliriz:

 play_pattern_timed chord(:E3, :m13), [0.25, 0.5]

Bu aşağıdakine eşit olacaktır:

play 52
sleep 0.25
play 55
sleep 0.5
play 59
sleep 0.25
play 62
sleep 0.5
play 66
sleep 0.25
play 69
sleep 0.5
play 73

Siz olsanız hangisini yazmayı tercih ederdiniz?

	8.3 Ölçekler:
Sonic Pi geniş bir ölçek aralığını destekler. C3 akorunu majör ölçekte çalmaya ne dersiniz?

play_pattern_timed scale(:c3, :majör), 0.125, release: 0.1

Daha çok oktav ekleyebiliriz:

play_pattern_timed scale(:c3, :majör, num_octaves: 3), 0.125, release: 0.1

Bütün notaları 5 tonluk bir ölçüde çalmaya ne dersiniz?

play_pattern_timed (scale :c3, :major_pentatonic, num_octaves: 3), 0.125,
  release: 0.1

	Rastgele Notalar:
Akorlar ve ölçüler rastgele bir seçimi anlamlaştırmak için harika seçimlerdir. E3 minor akorundan rastgele notalar alıp çalan bu örneği çalın:

use_synth :tb303
loop do
  play choose(chord(:E3, :minor)), release: 0.3, cutoff: rrand(60, 120)
  sleep 0.25
end

Farklı akorlar ve cutoff değerlerini deneyin.

	Akorlar ve Ölçüleri Keşfetmek:
Sonic Pi tarafından hangi akorların ve ölçülerin desteklendiğini görmek için bu öğreticinin en solunda bulunan “Lang” ibaresine tıklayın ve çıkan listeden akor veya ölçü kısmını seçin. Ana panelin içindeki bilgilerden aşağı indiğinizde uzun bir akor veya ölçü listesi göreceksiniz (hangisini seçtiyseniz o listelenir).

Eğlenin ve şunu hatırlayın, hata diye bir şey yoktur, yalnızca fırsatlar vardır.

	8.4 Halkalar:
Standart listelerin ilginç bir kısmı da halkalardır. Eğer biraz programlama biliyorsanız, daha önceden halka arabelleği veya halka dizilişleri ile karşılaşmış olabilirsiniz. İşte, hemen bir halka oluşturacağız – kısa ve basit bir tane olacak.

Listelerin bir önceki kısmında index mekanizmasıyla bir listeden nasıl eleman çekebileceğimizi gördük:

puts [52, 55, 59] [1]

Peki eğer ya 100 indexini yazarsak? Görüldüğü üzere bu listede yalnızca 3 eleman olduğu için 100 numaralı indexte hiçbir eleman yok. Bundan dolayı Sonic Pi size hiçbir şey anlamına gelen nil ibaresini yazdıracaktır.

Diyelim ki sürekli artan bir vuruş sayacınız var ve bu sayaç sürekli artıyor. Sayacımızı ve listemizi yazalım:

counter = 0
notes =[52, 55, 59] 

Artık sayacımızı liste içindeki bir notaya erişmek için kullanabiliriz.

puts notes[counter]

Harika, işte 52’yi çektik. Şimdi ise sayacımızı 1 arttıralım ve listeden başka bir nota çekelim:

counter = (inc counter)
puts notes[counter]

Süper, şimdi ise 55’i çektik ve bunu yeniden yaparsak listeden 59’u çekebiliriz. Ancak, bunu yeniden yapmak istersek, elemanımız bittiği için nil almış oluruz. Peki ya eğer bunun yerine listenin başına dönüp yeniden başlamasını isteseydik? İşte bu kısımda halkalar edvreye giriyor. 

	Halka Oluşturmak:
Halkaları iki şekilde oluşturabiliriz. Ya ring fonksiyonunu kullanıp ringin değişkenlerini de halkanın elemanları olarak atayacağız:

(ring 52, 55, 59)

Ya da normal bir listeyi alıp bunu bir halkaya dönüştürmek için sonuna .ring ibaresini ekleyebiliriz:

[52, 55, 59].ring

	Halkaları İndexlemek:
Bir halka oluşturduysanız, onu normal bir listeyi kullanıyormuş gibi kullanabilirsiniz. Ayrıca, halkaların içinden negatif indexleri çekebilirsiniz. Bir halkadan çekmek istediğiniz index, halkadaki eleman sayısından büyük olabilir. İndex sayısı, halkadaki elemanlar bittikçe başa sarar ve size o halkadaki elemanlardan birini mutlaka verir:

(ring 52, 55, 59)[0] #=> 52
(ring 52, 55, 59)[1] #=> 55
(ring 52, 55, 59)[2] #=> 59
(ring 52, 55, 59)[3] #=> 52
(ring 52, 55, 59)[-1] #=> 59

	Halkaları Kullanmak:
Farz edelim ki vuruş sayısını temsil eden bir değişkenimiz var. Biz bunu halkamızın içindeki notaları çaldırırken index numarası, release zamanı ya da bize kullanışlı gelen her şey için olarak kullanabiliriz.

	Halkalar Ölçüler ve Akorlardır:
Ölçü ve akor tarafından döndürülen listeler bizim uygun gördüğümüzde ulaşabileceğimiz birer halkadır.

	Halka Oluşumu:
ring fonksiyonuna ek olarak bizim için halka oluşturabilecek birkaç tane daha fonksiyonumuz var.

	range: başlangıçve bitiş noktaları ile adım büyüklüğü girmenizi gerektirir.
	bools: sizin 1’leri ve 0’ları bilgisayar mantığı ile temsil ettirmenizi sağlar.
	knit: sizin tekrar eden bir dizi örmenizi sağlar.
	spread: Öklit dağılımına göre 1 ve 0’lardan oluşan bir halka yaratmanızı sağlar.

Daha fazla bilgi için onların dosyalarına bakabilirsiniz.

	8.5 Halka Zincirleri:
Bunu keşfetmek için basit bir halka alıyoruz:

(ring 10, 20, 30, 40, 50)

Ya bunu tersten dizmek isteseydik? İşte o zaman bir zincir komutu olan .reverse komutunu kullanırdık:

(ring 10, 20, 30, 40, 50).reverse  #=> (ring 50, 40, 30, 20, 10)

Peki ya ilk 3 değeri istiyorsak?

(ring 10, 20, 30, 40, 50).take(3)  #=> (ring 10, 20, 30)

Son olarak, ya bu halkayı karıştırmak istersek?

(ring 10, 20, 30, 40, 50).shuffle  #=> (ring 40, 30, 10, 50, 20)

	Çoklu Zincirler:
Bu halihazırda yeni halkalar oluşturmanın güçlü bir yolu. Ancak gerçek güç, bu komutların birkaç tanesini uç uca ekleyebildiğinizde açığa çıkıyor.

Halkayı önce karıştırıp, sonra 1 element atıp sıradaki 3 elemanı almaya ne dersiniz?

Bunu adım adım yapalım:

1.	(ring 10, 20, 30, 40, 50) - our initial ring
2.	(ring 10, 20, 30, 40, 50).shuffle - shuffles - (ring 40, 30, 10, 50, 20)
3.	(ring 10, 20, 30, 40, 50).shuffle.drop(1) - drop 1 - (ring 30, 10, 50, 20)
4.	(ring 10, 20, 30, 40, 50).shuffle.drop(1).take(3) - take 3 - (ring 30, 10, 50)

Bu şekilde uç uca ekleyerek oluşturduğumuz zincirleri nasıl oluşturduğumuzu görüyor musunuz? Bu komutları istediğimiz sırada uç uca ekleyerek mevcut zincirlerden yenilerini çok zengin ve güçlü bir yoldan oluşturabiliriz.

	Değişmezlik:
Bu halkaların güçlü ve önemli bir özelliği vardır, değiştirilemezler. Bu da demek oluyor ki bu kısımda gösterilen metodlar mevcut halkaları değiştirmez, onun yerine yeni halkalar oluştururlar. Bu da demek oluyor ki ana halkanızı gönül rahatlığıyla bu metodlara maruz bırakabilirsiniz, çünkü değişmeme özelliğine sahiptirler.

	Kullanılabilecek Zincir Yöntemleri:

İşte oynayabileceğiniz zincir metodlarının bir listesi:

- reverse – halkanın ters çevrilmiş halini verir
- sort – halkanın sıralanmış halini verir
- shuffle – halkanın karıştırılmış halini verir
- pick(3) - .choose metodunu 3 kere uygular
- pick - .pick(3) metoduna benzer ama bunun boyutu orijinal halka kadardır
- take(5) – ilk 5 elemanı içeren bir halka verir
- drop(3) ilk 3 eleman dışındakileri içeren bir halka verir
- butlast – son eleman haricindeki bir halka oluşturur
- drop_last(3) – son 3 elemanı eksik olan bir halka verir
- take_last(6) – sadece son 6 elemanı içeren bir halka verir
- stretch(2) – halka içindeki her elemanı 2 kere tekrar eder
- repeat(3) – tüm halkayı 3 kere tekrarlar
- mirror – halkayı kendisinin ters çevrilmiş haline ekleyip veirir
- reflect – mirror methodunun aynısıdır ancak ortadaki elemanı tekrarlamaz
- scale(2) – halkadaki her elemanı 2 ile çarpar(halkadaki elemanların sayı olduğunu varsayar)

Sayı gerektiren metodlar tabii ki de başka sayıları da alabilir!

