# 9 Canlı Kodlama
Sonic Pi’ın en heyecan verici özelliklerinden birisi de size canlı bir şekilde müzik yazdırabilmesi ve onu değiştirip geliştirmenize olanak sağlamasıdır. Tıpkı bir gitar çalmak gibi. Bunun avantajlarından biri de siz beste yaparken canlı bir şekilde geri dönüt alabilmenizdir (basitçe müziğinizi döngüye alın ve kulağınıza en hoş gelene ulaşana kadar onu değiştirin). Bunun dışında, asıl avantajı Sonic Pi ile sahne alıp ortalığı kasıp kavurabilme şansına sahip olmanızdır.

Bu kısımda statik kod bestelerinizi dinamik sahne performanslarına dönüştürebilmenin temellerini göreceksiniz.

Kemerlerinizi bağlayın…

## 9.1 Canlı Kodlama:
Şu ana dek öğrendiklerimiz biraz eğlenmemiz için yeterli. Bu bölümde önceki tüm bölümlerde öğrendiklerimizi kullanarak sizin canlı canlı beste yapmanızı ve bunu bir sahne performansına dönüştürmenize olanak sağlayacağız. Bunu yapabilmek için 3 ana içeriğe ihtiyacımız var:

-	Ses çıkarabilen kodlar yazmak – YAPILDI!
-	Fonksiyon yazabilmek – YAPILDI!
-	İsim verilmiş iş parçalarını kullanabilme – YAPILDI!

Pekâlâ, hadi başlayalım. Hadi ilk canlı kodlarımızı yazalım. İlk olarak çalmak istediğimiz kodu içeren bir fonksiyona ihtiyacımız var. Kolaydan başlayalım. Ayrıca bun fonksiyonun içindekileri döngüye almalıyız:
```
define :my_sound do
  play 50
  sleep 1
end

in_thread(name: :looper) do
  loop do
    my_sound
  end
end
```
Eğer bu size çok karmaşık geldiyse, geriye dönüp fonksiyonlar kısmını tekrardan okumanızı öneririm. Eğer yeterince kafa patlattıysanız bu size çok karışık gelmeyecektir.

Burada elimizde olan şey 50 notasını çalıp 1 vuruş susan bir fonksiyondur. Daha sonra :looper isimli bir kod parçası tanımlayıp my_sound’un tekrar tekrar çalmasını sağlıyoruz.

Eğer bu kodu çalıştırırsanız 50 notasını tekrar tekrar çaldığını duyacaksınız.

## İşleri değiştirmek:
İşte burası eğlencenin başladığı kısım. Kod halihazırda çalınırken 50 değerini başka bir sayıyla değiştirin, mesela 55, daha sonra yeniden çalıştır butonuna basın. İnanılmaz! Değişti! Hem de canlı olarak!

Çalmakta olanın üzerine yeni bir ses tabaksı eklemedi çünkü isimlendirilmiş kod parçalar kullandığımızdan bu ismi sadece eşsiz bir kod parçasına vermemize izin veriyor. Biz my_sound’a yeniden bir tanım verdik. :looper kodu döngüdeyken basitçe yeni bir tanım atandı.
```
define :my_sound do
  use_synth :tb303
  play 50, release: 0.3
  sleep 0.25
end
```
İşte şimdi işler ilginçleşmeye başladı, ama buna biraz daha tuz biber atabiliriz. Aynı notayı tekrar tekrar oynatmak yerine bir akoru oynatmayı deneyin:
```
define :my_sound do
  use_synth :tb303
  play chord(:e3, :minor), release: 0.3
  sleep 0.5
end
```
Akordan rastgele notaları çalmaya ne dersiniz:
```
define :my_sound do
  use_synth :tb303
  play choose(chord(:e3, :minor)), release: 0.3
  sleep 0.25
end
```
Ya da rastgele bir cutoff değeri kullanmaya:
```
define :my_sound do
  use_synth :tb303
  play choose(chord(:e3, :minor)), release: 0.2, cutoff: rrand(60, 130)
  sleep 0.25
end
```
Son olarak da biraz davul ekleyelim:
```
define :my_sound do
  use_synth :tb303
  sample :drum_bass_hard, rate: rrand(0.5, 2)
  play choose(chord(:e3, :minor)), release: 0.2, cutoff: rrand(60, 130)
  sleep 0.25
end
```
İşte asıl şimdi işler ilginçleşti!

Hemen koşup canlı kodlama yapmaya başlamadan önce yaptığınız şeyi bırakın ve sıradaki live_loop kısmını okuyun, bu kısım sizin Sonic Pi’da kodlama şeklinizi sonsuza dek değiştirecek…

## 9.2 Canlı Döngüler:
Tamam, bu kısım asıl ganimetin yattığı kısımdır. Eğer yalnızca tek bir kısım okuyabilseydiniz o bu olmalıdır. Eğer bir önceki Canlı Kodlamanın Temelleri bölümünü okuduysanız, live_loop fonksiyonu önceki bölümdekilerin tam olarak aynısını o kadar çok kod yazmanıza gerek kalmadan basit bir şekilde yapar.

Eğer önceki kısımları okumadıysanız da live_loop Sonic Pi da müzik yapmanın en iyi yoludur.

Haydi oynayalım. Yeni bir kanala aşağıdakileri yazın:
```
live_loop :foo do
  play 60
  sleep 1
end
```
Şimdi çalıştır butonuna basın. Her vuruşta basit bir bipleme duyacaksınız. Burada eğlenceli pek de bir şey yok. Ancak durdur tuşuna henüz basmayın. 60’ı 65 ile değiştirip yeniden oynat tuşuna basın.

İnanılmaz! Otomatik olarak hiç vuruş kaçırmadan değişti. İşte buna canlı kodlama denir.

Neden bu sesi biraz daha kalınlaştırmıyoruz? Kodunuzu çalarken değiştirin:
```
live_loop :foo do
  use_synth :prophet
  play :e1, release: 8
  sleep 8
end
```
Sonra oynat butonuna basın.

Hadi cutoff değerleriyle de biraz oynayalım:
```
live_loop :foo do
  use_synth :prophet
  play :e1, release: 8, cutoff: rrand(70, 130)
  sleep 8
end
```
Yeniden oynat butonuna basın.

Biraz da davul ekleyelim:
```
live_loop :foo do
  sample :loop_garzul
  use_synth :prophet
  play :e1, release: 8, cutoff: rrand(70, 130)
  sleep 8
end
```
Notayı e1’den c1’e değiştirin:
```
live_loop :foo do
  sample :loop_garzul
  use_synth :prophet
  play :c1, release: 8, cutoff: rrand(70, 130)
  sleep 8
end
```
Artık bu saatten sonra beni dinlemeyi bırakın ve kendiniz oynamaya başlayın! İyi eğlenceler!

## 9.3 Çoklu Canlı Döngü:
Aşağıdaki canlı döngüye bir göz atın:
```
live_loop :foo do
  play 50
  sleep 1
end
```
İsminin neden :foo oldğunu merak etmiş olabilirsiniz. Bu isim önemlidir, çünkü bu isim canlı döngüyü diğerlerinden ayıran şeydir.

İki canlı döngü asla aynı anda çalamaz.

Bu da demek oluyor ki, eğer iki döngüyü eşzamanlı olarak çalmak istiyorsak onlara farklı isimler vermeliyiz.
```
live_loop :foo do
  use_synth :prophet
  play :c1, release: 8, cutoff: rrand(70, 130)
  sleep 8
end

live_loop :bar do
  sample :bd_haus
  sleep 0.5
end
```
Artık iki ayrı canlı döngüyü de birbirinden bağımsız şeklide güncelleyip değiştirebilirsiniz.

## Canlı Döngüleri Eşzamanlı Hale Getirmek:
Fark etmiş olabileceğiniz şeylerden biri de canlı döngülerin önceden gördüğümüz cue mekanizmasıyla çalışıyor olması olabilir. Canlı döngü her başa döndüğünde yeni bir cue olayı oluşur. Buna da zaten canlı döngü diyoruz. Bizler de bu çalmakta olan döngülerimizi onları durdurmak zorunda kalmadan eşzamanlı hale hetirebiliriz.

Bu kötü zamanlandırılmış koda bir bakın:
```
live_loop :foo do
  play :e4, release: 0.5
  sleep 0.4
end

live_loop :bar do
  sample :bd_haus
  sleep 1
end
```
Hadi bakalım acaba bu zamanlama sıkıntısını çalmayı durdurmadan düzeltebilecek miyiz? Öncelikle, :foo döngüsünü düzeltelim. Bunu yapmak için sleep faktörünü 1 gibi bir şey yapmalıyız, 0.5 işimizi görür gibi:
```
live_loop :foo do
  play :e4, release: 0.5
  sleep 0.5
end

live_loop :bar do
  sample :bd_haus
  sleep 1
end
```
Henüz bitirmedik ama – fark edeceksiniz ki vuruşlar yine tam olarak oturmuş değil. Bunun nedeni ise döngülerin fazlarının uyuşmaması. Bu sorunu birini diğerine sync ile uydurarak çözelim:
```
live_loop :foo do
  play :e4, release: 0.5
  sleep 0.5
end

live_loop :bar do
  sync :foo
  sample :bd_haus
  sleep 1
end
```
Wow, artık her şey tamamen mükemmel bir zamanlamada, hem de bunların hepsi çalan sesi hiç durdurmadan gerçekleşti.

Şimdi, ilerleyin ve döngülerle canlı kodlama yapın.

## 9.4 Tıklama:
Kendinizi canlı kodlama esnasında yaparken halkaları döngülerken bulacaksınız.Notaları melodiler yaratabilmek için halkaların içine koyacaksınız, sleep fonksiyonlarını ritim ayarlaması için kullanacaksınız, akorları inceleyeceksiniz vs. vs.

## Halkaları Tıklama:
Sonic Pi içinde canlı döngüler varken halkaların içinde çalışabilmenizi sağlayan aşırı kullanışlı bir alete sahiptir. Buna da tıklama sistemi denir. Halkalarla ilgili olan kısımda devamlı artmakta olan bir sayaçtan bahsetmiştik, tıpkı vuruş sayısını anlık gösteren bir sayaç gibi. Tıklama da aynı bu mantığı uygular. Size, halkalar arasında tıklama yapma olanağı sunar. Hadi bir örnek görelim:
```
counter = 0
live_loop :arp do
  play (scale :e3, :minor_pentatonic)[counter], release: 0.1
  counter += 1
  sleep 0.125
end
```
Bu şuna eşittir:
```
live_loop :arp do
  play (scale :e3, :minor_pentatonic).tick, release: 0.1
  sleep 0.125
end
```
Burada, E3 minör beşli akorunun ölçüsünü alıp her eleman arasında tıklıyoruz. Bu ölçü deklarasyonunun sonuna .tick ekleyerek yapılabiliyor. Bu tıklamalar her canlı döngü için kişiseldir, yani her canlı döngü kendine özgü tıklamalara sahip olabilir:
```
live_loop :arp do
  play (scale :e3, :minor_pentatonic).tick, release: 0.1
  sleep 0.125
end

live_loop :arp2 do
  use_synth :dsaw
  play (scale :e2, :minor_pentatonic, num_octaves: 3).tick, release: 0.25
  sleep 0.25
end
```
## Tıklama:
Standart fn’lere tick diyebiliriz ve bu değerleri index numarası olarak kullanabiliriz:
```
live_loop :arp do
  idx = tick
  play (scale :e3, :minor_pentatonic)[idx], release: 0.1
  sleep 0.125
end
```
Ancak, her zaman sonuna .tick ibaresini koymak daha iyidir. Tick fn olayı eğer tıklama değeriyle gerçekten delice şeyler yapmak istiyorsanız ya da tıklamaları halka indexlemekten başka bir iş için kullanmak istiyorsanız işe yarayabilir.

## Bak:
Tıklamalar hakkındaki sihirli şey yalnızca yeni bir index vermesi (ya da halkada o indexte yer alan elemanı vermesi) değildir, asıl sihirli şey tıklamadan bir şey çağırdığınızda hiç aynı olmaz, her zaman bir sonraki şeyi verir. Tıklama örneklerine bakarak çalışma prensibini anlayabilirsiniz. Ancak, şimdilik, şunu bilmeniz önemlidir ki, bazen tıklamanın değerini öğrenmek istersiniz ve tıklama sayısının artmamasını istersiniz. Bunu da look fonksiyonuyla başarabilirsiniz. look standart bir fonksiyon gibi çağrılabilir ya da bir halkanın sonuna .look şeklinde eklenebilir.

## Tıklamalara İsim Vermek:
Sonuç olarak, bazen canlı döngüler için birden fazla tıklamaya ihtiyaç duyabilirsiniz. Bunu sağlamak için de tıklamanıza isim vermeniz gerekmektedir:
```
live_loop :arp do
  play (scale :e3, :minor_pentatonic).tick(:foo), release: 0.1
  sleep (ring 0.125, 0.25).tick(:bar)
end
```
İşte burada iki tıklama kullanıyoruz, bir tıklama çalacak olan notayı diğeri de uyku süresini belirliyor. Bu iki tıklama aynı canlı döngü içinde bulundukları için onları birbirinden ayırmalı ve farklı şekilde isimlendirmeliyiz. Bu canlı döngülerdeki olayın aynısı – öncesinde : ile belirtilmiş bir sembolü isim olarak belirleyebiliyoruz. Yukarıdaki örnekte bu tıklamanın adı :foo idi ve diğerininki ise :bar idi. Eğer bunlar üzerinde look fonksiyonunu kullanmak istersek tıklamanın adını look fonksiyonuna vermemiz gerekiyor.

## Fazla Karışıklığa Gerek Yok:
Tıklama sistemindeki en güçlü yanını yeni başladığınızda kullanamazsınız. Bu kısımdaki her şeyi birdenbire deneyip hepsini aynı anda öğrenmeye çalışmayın. Tek bir halka üzerinde tıklama üzerine odaklanın. Bu size canlı döngülerinizde halkalarınız içindeki değerleri tıklamanın zevkini verecektir.

Tıklama dökümanlarına bir göz atın, orada birçok işe yarar örnek bulabilirsiniz. Mutlu tıklamalar!


