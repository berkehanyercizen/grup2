## 10. Zaman Durumu
 Genelde iş parçaları ve canlı döngüler hakkında bilgi sahibi olmak kullanışlı olur. Örneğin kullandığın anahtar için bir gösterge kullanmak isteyebilirsin, BPM ya da daha soyut bir konsept aynı şu anki “karışıklık” (muhtemelen farklı iş parçalarında farklı değerlendireceksin). Aynı zamanda bunu yaparken var olan kaçınılmaz garantilerimiz de kaybetmek istemeyiz. Başka bir dille, başkalarıyla hala kod paylaşıp tam olarak ne duyacaklarından emin olmak isteriz. 5.6’ncı bölümde size neden iş parçaları arasında bilgi paylaşırken değişken kullanmamamız gerektiğini ve bununla beraber determinizimde kayıp olduğundan açıkça bahsettik. 

 Sonic Pi’yın bu konudaki çözümü şudur ki küresel değişkenlerle deterministik bir şekilde çalışmanın yolu yeni sistem olan Zaman Durumundan geçer. Bu kulağa biraz karışık ve zor görünebilir (hatta Birleşik Krallık’ta çoklu iş parçalarıyla programlama ve paylaşılan hafızayı programlama üniversite düzeyi bir iştir). Fakat, gördüğünüz gibi, aynı ilk notanızı çalmak gibi, Sonic Pi iş parçalarını eyaletler arası paylaşımını çok basit tutarken aynı zamanda sizin programlarınızı güvenli ve determenist tutar. 

 Şimdi başlayalım…

## 10.1-Hazırlan ve Başla
 Sonic Pi küresel bir hafıza deposu olan, Zaman Durumu’na sahiptir. Onunla yapabileceğiniz iki temel şey ise bilgi koymak ve bilgi almaktır. Şimdi daha derinlere dalalım…
Kurmak
 Zaman Durumunda bilgi depolamak için iki şeye ihtiyacımız vardır:
1.	Depolamak istediğimiz bilgi,
2.	Bilgi için eşsiz (anahtar) isim.
Örneğin 3000 sayısını bir anahtar kelime olan :intensity ile depolamak istiyoruz. Bunun için set fonksiyonunu kullanmak geçerli olabilir.
set :intensity, 3000

Anahtar kelimemiz için istediğimiz kelimeyi kullanabiliriz. Eğer bilgimiz çoktan anahtar kelime ile depolandıysa yeni set’imiz onu geçersiz kılar. 
set :intensity, 1000
set :intensity, 3000
Yukarıdaki örnekte gördüğünüz gibi iki tane bilgiyi aynı kelimeye depolamaya çalışıyoruz, bu durumda son kurulan bilgi kazanır yani :intensity 3000 sayısına eşit olur.


Almak
Zaman Durumumuzdan bilgi almak için sadece kurduğumuz anahtar kelimeye ihtiyacımız var ki şu anki durumumuzda kelimemiz :intensity. Daha sonra get[:intensity] yazmamız gerek ki zaten biz bunu satırımızda yazdırabiliriz. 
print get[:intensity] #=> prints 3000

Fark ettiğiniz üzere eskiden yazdığımız kurulu bilgi şimdi yazdığımız bilgi alma kısmında ortaya çıktı. Bir kere olsun bir bilgiyi kurduğumuzda o bilgi başka bir bilgi tarafından geçersiz kılınana kadar ya da Sonic Pi tarafından kapatılana kadar orda kalır. 

Çoklu iş parçaları
Zaman Durumunun en büyük yararı da güvenli bir şekilde iş parçaları ve canlı döngüleri üzerinden kullanılabilir. Örneğin, bir tane canlı döngünüz bilgiyi kurarken diğeri de onu alabilir. 
live_loop :setter do
  set :foo, rrand(70, 130)
  sleep 1
end

live_loop :getter do
  puts get[:foo]
  sleep 0.5
end
Kurma ve almanın en güzel kısmı ise bunun gibi iş parçaları üstünden bile her oynatışınızda her zaman aynı sonucu üretir. Hadi, deneyin. Aşağıdaki bölgeye bakın:
{run: 0, time: 0.0}
 └─ 125.72265625

{run: 0, time: 0.5}
 └─ 125.72265625

{run: 0, time: 1.0}
 └─ 76.26220703125

{run: 0, time: 1.5}
 └─ 76.26220703125

{run: 0, time: 2.0}
 └─ 114.93408203125

{run: 0, time: 2.5}
 └─ 114.93408203125

{run: 0, time: 3.0}
 └─ 75.6048583984375

{run: 0, time: 3.5}
 └─ 75.6048583984375
Birkaç kez çalıştırmayı deneyin, her seferinde aynı. İşte biz buna deterministik davranış diyoruz ve müzik olarak paylaştığımız kodları insanlar çaldığında bizim onlardan ne duymalarını beklediğimiz şeyleri duymaları bizim için çok önemli.

Basit deterministik durum sistemi
5.6 bölümde size iş parçaları arası değişkenlerin garip davranışlara yol açacağını söylemiştik. Bu bizi şu kodlar gibi yapmaktan alıkoyar:
```

## An Example of Non-Deterministic Behaviour
## (due to race conditions caused by multiple
## live loops manipulating the same variable
## at the same time).
##
## If you run this code you'll notice
## that the list that's printed is
## not always sorted!
a = (ring 6, 5, 4, 3, 2, 1)

live_loop :shuffled do
  a = a.shuffle
  sleep 0.5
end

live_loop :sorted do
  a = a.sort
  sleep 0.5
  puts "sorted: ", a
end
Şimdi kurma ve alma işlemleri yaparsak nasıl durur ona bir bakalım. 
## An Example of Deterministic Behaviour
## (despite concurrent access of shared state)
## using Sonic Pi's new Time State system.
##
## When this code is executed, the list that's
## printed is always sorted!
set :a, (ring 6, 5, 4, 3, 2, 1)

live_loop :shuffled do
  set :a, get[:a].shuffle
  sleep 0.5
end

live_loop :sorted do
  set :a, get[:a].sort
  sleep 0.5
  puts "sorted: ", get[:a]
end
```

Fark edin bu kodun değişken kullanımlı haline ne kadar çok benziyor. Fakat kodu çalıştırdığınızda ondan tam olarak neyi beklediğiniz bir Sonic Pi kodu gibi çalışıyor – Zaman Durumuna teşekkürler, her çaldığımızda aynı çalıyor. 
Senkronizasyon
5.7 bölümde senkronizasyon tehlikeleri ile karşılaşınca size cue ve sync fonksiyonları ile tanıştırdık. Orda bahsedilmeyen kısımda tüm bu fonksiyonların çalışmasını sağlayan Zaman Durumuydu. Aslında set ve cue aynı temel fonksiyon üzerine kurulu ve bu da Zaman Durumu sistemine bilgi aktarma. Ekstra olarak da sync öyle bir tasarlandı ki Zaman Durumuyla hatasız çalışıyor – Zaman Durumuna aktarmayı düşündüğümüz her hangi bir bilgiyi senkronize edebiliyoruz. Başka bir deyişle henüz Zaman Durumuna eklenmemiş olan olayları senkronize ediyoruz. 

Etkinlikler için bekleme
Zaman Durumuna yeni etkinlikler eklenmesini beklemek için senkronizasyonun nasıl kullanılacağına hızlıca göz atalım:
in_thread do
  sync :foo
  sample :ambi_lunar_land
end

sleep 2

set :foo, 1
İlk önce bu örnekte, Zaman Durumuna eklenecek bir :foo olayını bekleyen bir iş parçacığı oluşturuyoruz. Bu iş parçacığı bildirimi sonra 2 vuruş için uyur ve sonra ayarlanır :foo 1 olur. Bu daha sonra bir sonraki satıra hareket eden senkronizasyonu serbest bırakır :ambi_lunar_land örnek. Senkronizasyonun her zaman gelecekteki olayları beklediğini ve yeni bir olayı bekleyen mevcut parçayı engelleyeceğini unutmayın. Ayrıca, set veya cue ile tetikleyen çizgiyi mantıksal zamanını devralır, böylece zamanı senkronize etmek için de kullanılabilir. 
Değerleri geleceğe taşımak
Yukarıdaki örnekte :foo fonksiyonuna 1 değerini verdik ve hiçbir şey yapmadık. Aslında bu değeri :sync denilen çizgiden alabiliriz. 
in_thread do
  amp = sync :foo
  sample :ambi_lunar_land, amp: amp
end

sleep 2

set :foo, 0.5
Küme ve işaretten geçen değerlerin iş parçacığı için güvenli olması gerektiğine dikkat edin. Zaman Durumunda kaydetmeye çalıştığınız değer geçerli değilse, Sonic Pi bir hata atar.
Örüntü uyuşması
Zaman Durumuna bilgi alırken ve ayarlarken, :foo ve :bar gibi temel sembollerden daha karmaşık anahtarlar kullanmak mümkündür. "/ Foo / bar / baz" gibi yollar adı verilen URL stil dizelerini de kullanabilirsiniz. Yollarla çalışmaya başladığımızda, Sonic Pi’nin ‘benzer’ yollarından ziyade ‘tıpatıp’ ile senkronize etmek için sofistike kalıp eşleştirme sisteminden yararlanmaya başlayabiliriz. Hadi bir bakalım.
Herhangi bir yol parçasını eşleştir
Üç yol segmenti olan bir sonraki etkinliği beklemek istediğimizi varsayalım:
sync "/*/*/*"
Bu, herhangi bir Zaman Durumu olayı, adlarına bakılmaksızın tam olarak üç yol kesimi ile eşleşir. Örneğin:
•	cue "/foo/bar/baz"
•	cue "/foo/baz/quux"
•	cue "/eggs/beans/toast"
•	cue "/moog/synths/rule"
Ancak, daha az veya daha fazla yol parçası olan yolları eşleştirmez. Aşağıdakiler eşleşmeyecek:
•	cue "/foo/bar"
•	cue "/foo/baz/quux/quaax"
•	cue "/eggs"
Her * herhangi bir içerik anlamına gelir. Böylece, / * olan tek bir parçayla yolları eşleştirebiliriz /*/*/*/*/*
Kısmi bölümleri eşleştirme
Segmentin ne ile başlayacağını veya biteceğini biliyorsak, kısmi segment adına ek olarak * kullanabilirsiniz. Örneğin: "/ foo / b * / baz", ilk foo, son baz ve orta segment b ile başlayan herhangi bir şey olabilir, üç segmenti olan herhangi bir yolla eşleşir. Yani, eşleşecek: 
•	cue "/foo/bar/baz"
•	cue "/foo/baz/baz"
•	cue "/foo/beans/baz"
Ancak, aşağıdakilerle eşleşmez:
•	 cue "/foo/flibble/baz"
•	cue "/foo/abaz/baz"
•	cue "/foo/beans/baz/eggs"
Bir bölümün son karakterlerini belirtmek için * bölümün başına da yerleştirebilirsiniz: "/ foo / * zz / baz", herhangi bir 3 bölüm işaretiyle eşleşir veya ilk bölümün foo, son bölüm baz olduğu ve orta segment "cue" / foo / whiz / baz "gibi zz ile biter.
Yuvalanmış Yol Segmentlerini Eşleştirme
 Bazen kaç tane yol parçasını eşleştirmek istediğinizi bilmiyorsunuz. Bu durumlarda güçlü çift yıldızı kullanabilirsiniz: ** eşleşecek olan "/ foo / ** / baz" gibi:
•	cue "/foo/bar/baz"
•	cue "/foo/bar/beans/baz"
•	cue "/foo/baz"
•	cue "/foo/a/b/c/d/e/f/baz"
Tek Harfleri Eşleştirme
? karakterini tek bir görevle eşleştirmek için kullanabilirsiniz "/?oo/bar/baz" gibi.
•	cue "/foo/bar/baz"
•	cue "/goo/bar/baz"
•	cue "/too/bar/baz"
•	cue "/woo/bar/baz"
Birden Çok Kelimenin Eşleştirilmesi
Bir segmentin belirli bir kelime sayısından biri olabileceğini biliyorsanız, "ve foo / {bar, fasulye, yumurta} / quux" gibi yalnızca bir eşleşecek seçeneklerin listesini belirlemek için {ve} eşleştiricileri kullanabilirsiniz. Aşağıdaki gibi:
•	cue "/foo/bar/quux"
•	cue "/foo/beans/quux"
•	cue "/foo/eggs/quux"
 Birden Çok Harfin Eşleştirilmesi
Son olarak, "/ foo / [abc] ux / baz" gibi, yalnızca eşleşecek seçeneklerin bir listesini belirlemek için [ve] eşleştiricileri kullanırsanız, harf seçimine karşı eşleştirebilirsiniz:
•	 cue "/foo/aux/baz"
•	cue "/foo/bux/baz"
•	cue "/foo/cux/baz"

Harf aralıklarını belirtmek için - karakterini de kullanabilirsiniz. Örneğin, yalnızca eşleşecek olan "/ foo / [a-e] ux / baz":
•	cue "/foo/aux/baz"
•	cue "/foo/bux/baz"
•	cue "/foo/cux/baz"
•	cue "/foo/dux/baz"
•	cue "/foo/eux/baz"
Eşleştiricileri Birleştirme
Senkronizasyonu çağırırken veya elde ederken, eşleştiricileri, cue veya set tarafından oluşturulan herhangi bir Zaman Durumu olayıyla güçlü şekilde eşleşmesi için uygun gördüğünüz herhangi bir sırayla birleştirmekte serbestsiniz. Çılgın bir örneğe bakalım:
in_thread do
  sync "/?oo/[a-z]*/**/ba*/{quux,quaax}/"
  sample :loop_amen
end

sleep 1

cue "/foo/beans/a/b/c/d/e/bark/quux/"
OSC Örüntü Eşleştirme
Merak edenler için, bu eşleştirme kuralları, burada ayrıntılı olarak açıklanan Açık Ses Kontrolü deseni eşleştirme özelliğine dayanmaktadır: http://opensoundcontrol.org/spec-1_0

