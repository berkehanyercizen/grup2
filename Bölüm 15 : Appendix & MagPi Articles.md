# Appendix & MagPi Articles
## A.01 SonicPi için tavsiyeler
## A.02 Live coding
## A.03 coded beats
## A.04 Synth Riffs
## A.05 Acid Bass
## A.06 Musical Minecraft
## A.07 Bizet Beats
## A.08 Become a Minecraft VJ
## A.09 Randomisation
## A.10 Control
## A.11 Tick Tock
## A.12 Sample Slicing
## A.13 Code a Probabilistic Sequencer
## A.14 Amplitude Modulation
## A.15 Five Live Coding Techniques
***Beş Canlı Kodlama Tekniği***
Bu ayki Sonic Pi eğitiminde, Sonic Pi'ye gerçek bir enstrüman gibi nasıl davranmaya başlayacağınıza bir göz atacağız. Bu nedenle, kodu tamamen farklı bir şekilde düşünmeye başlamamız gerekir. Canlı kodlayıcılar, kodu kemancıların yaylarını nasıl düşündüklerine benzer şekilde düşünür. Aslında, aynı kemancı gibi, farklı sesler (uzun yavaş hareketler ve kısa hızlı vuruşlar) oluşturmak için çeşitli yay tekniklerini uygulayabilir, Sonic Pi'nin sunduğu temel canlı kodlama tekniklerinden beşini keşfedeceğiz. Bu makalenin sonunda, kendi canlı kodlanmış performanslarınız için pratik yapmaya başlayabilirsiniz.
**1. Kısa Yolları Ezberlemek**
Sonic Pi ile kodlamayı yaşayan ilk ipucu kısayolları kullanmaya başlamaktır. Örneğin, fareye ulaşmak için değerli zamanınızı boşa harcamak, Çalıştır düğmesine taşımak ve tıklamak yerine, yalnızca alt ve r tuşlarına aynı anda basabilirsiniz; bu daha hızlıdır ve klavyede parmaklarınızı bir sonraki düzenlemeye hazır tutar. . Üstteki ana düğmelerin kısayollarını, fareyi üzerlerine getirerek bulabilirsiniz. Kısayolların tam listesi için yerleşik öğretici bölüm 10.2'ye bakın.
Gerçekleştirirken, yapılacak eğlenceli bir şey, kısayollara basarken kol hareketinize biraz yetenek katmaktır. Örneğin, bir değişiklik yapmak üzereyken izleyiciyle iletişim kurmak çoğu zaman iyidir - bu nedenle büyük bir güç akoruna çarptığında yaptığınız gibi bir gitaristin üstüne vurduğunuzda hareketlerinizi süsleyin.
**2. Seslerinizi Manuel Olarak Tetikleyin**
Artık klavyeyle anında kodu tetikleyebilirsiniz, bu beceriyi seslerinizi elle katmanlamak olan ikinci tekniğimiz için hemen uygulayabilirsiniz. Oynamak için çok sayıda çağrı kullanmak ve uykuyla yapılan çağrılarla ayrılmış örnekleri kullanmak yerine, alt-r komutunu kullanarak manuel olarak tetikleyeceğimiz bir çağrı yapacağız. Hadi deneyelim. Aşağıdaki kodu yeni bir belleğe yazın:

'''
synth :tb303, note: :e2 - 0, release: 12, cutoff: 90
'''
Şimdi, Çalıştır tuşuna basın ve ses çalarken, dört notayı aşağıya doğru değiştirerek bırakmak için kodu değiştirin:
'''
synth :tb303, note: :e2 - 4, release: 12, cutoff: 90
'''
Şimdi, her iki sesin de aynı anda çalındığını duymak için Yeniden Çalıştır düğmesine basın. Bunun nedeni, Sonic Pi’nin Çalıştır düğmesinin önceki bir kodun bitmesini beklememesi, ancak aynı anda çalışan kodu başlatmasıdır. Bu, her tetikleyici arasında küçük veya büyük değişikliklerle çok sayıda sesi kolayca katmanlaştırabileceğiniz anlamına gelir. Örneğin, hem notu hem de kesmeyi değiştirmeyi deneyin: opts ve ardından yeniden tetikleyin.
Bu tekniği uzun soyut örneklerle de deneyebilirsiniz. Örneğin:
'''
sample :ambi_lunar_land, rate: 1 
'''
Örneği başlatmayı deneyin ve ardından aşamalı olarak oranı yarıya indirin: Vuruş arasında koşmayı deneyin 1'den 0.5'e 0.25'den 0.125'e koşun ve sonra -0.5 gibi bazı negatif değerleri deneyin. Sesleri bir araya getirin ve nereye götürebileceğinizi görün. Son olarak, biraz FX eklemeyi deneyin.
Bu şekilde basit kod satırlarıyla çalışmak, Sonic Pi'ye yeni gelen bir izleyicinin, yaptığınız şeyi takip etme ve duydukları seslerle okuyabilecekleri kodla ilişkilendirme konusunda iyi bir şansı olduğu anlamına gelir.
**3. Master Canlı Döngüler** 
Daha ritmik bir müzikle çalışırken, her şeyi elle tetiklemek ve iyi zaman geçirmek çoğu zaman zor olabilir. Bunun yerine, bir live_loop kullanmak genellikle daha iyidir. Bu, kodunuz için tekrarlama sağlarken, bir sonraki döngüde kodu düzenleme olanağı sağlar. Ayrıca diğer live_loops'lar ile aynı anda çalışacaklar, bu da onları birbirleriyle ve manüel kod tetikleyicilerle birlikte katmanlandırabileceğiniz anlamına gelir. Canlı döngülerle çalışma hakkında daha fazla bilgi için yerleşik eğitimin 9.2 bölümüne bakın.
Gerçekleştirirken, live_loop’un senkronizasyonundan yararlanmayı unutmayın: bir hata nedeniyle canlı döngünün çalışmasını durduran yanlışlıkla çalışma zamanı hatalarından kurtulmanızı sağlar. Senkronizasyona zaten sahipseniz: geçerli bir başka live_loop'a işaret etmeyi seçtiyseniz, hatayı hızlı bir şekilde düzeltebilir ve bir ritmi kaçırmadan işleri yeniden başlatmak için kodu yeniden çalıştırabilirsiniz.
**4. Master Mikserini kullanın**
Sonic Pi’nin en iyi saklanan sırlarından biri, içinden tüm seslerin aktığı bir ana miksere sahip olmasıdır. Bu mikser, hem düşük geçişli bir filtreye hem de yüksek geçişli bir filtreye sahiptir, böylece seste kolayca genel değişiklikler yapabilirsiniz. Master mikserin işlevselliğine fn set_mixer_control! Aracılığıyla erişilebilir. Örneğin, bazı kodlar çalışırken ve ses çıkarırken, bunu boş bir ara belleğe girin ve Çalıştır düğmesine basın:
set_mixer_control! lpf: 50
Bu kodu çalıştırdıktan sonra, mevcut ve tüm yeni sesler kendilerine uygulanan düşük geçişli bir filtreye sahip olacak ve bu nedenle daha fazla boğulacaktır. Bunun, yeni karıştırıcı değerlerinin tekrar değiştirilinceye kadar yapışacağı anlamına geldiğine dikkat edin. Ancak, isterseniz, reset_mixer! İle karıştırıcıyı her zaman varsayılan durumuna sıfırlayabilirsiniz. Şu anda desteklenen seçeneklerden bazıları: pre_amp :, lpf: hpf :, ve amp :. Listenin tamamı için set_mixer_control!
Zaman içinde bir veya daha fazla opt değerini kaydırmak için karıştırıcının * _slide opts özelliğini kullanın. Örneğin, karıştırıcının düşük geçiş filtresini geçerli değerden 30'a yavaşça kaydırmak için aşağıdakileri kullanın:
'''
set_mixer_control! lpf_slide: 16, lpf: 30 
'''
Daha sonra aşağıdakilerle hızlı bir şekilde yüksek bir değere geri dönebilirsiniz:
'''
set_mixer_control! lpf_slide: 1, lpf: 130 
'''
Bunu yaparken, böyle bir karıştırıcı ile çalışmak için bir tamponu boş tutmak genellikle yararlıdır.
**5. Uygulama**
Canlı kodlama için en önemli teknik pratiktir. Her çeşit profesyonel müzisyenler arasında en yaygın özellik, enstrümanları ile çalmayı pratik etmeleridir - genellikle günde saatlerce. Uygulama, bir gitarist kadar canlı bir kodlayıcı için de önemlidir. Alıştırma parmaklarınızın belirli kalıpları ve genel düzenlemeleri ezberlemesine izin verir, böylece daha akıcı bir şekilde yazabilir ve onlarla çalışabilirsiniz. Alıştırma ayrıca yeni sesleri ve kod yapılarını keşfetme fırsatları sunar.
Gösteri yaparken, ne kadar çok uygulama yaparsanız, konserde rahatlamanız o kadar kolay olacaktır. Alıştırma ayrıca size çekilecek bir deneyim hazinesi verecektir. Bu, hangi değişiklik türlerinin ilginç olacağını ve mevcut seslerle iyi çalışacağını anlamanıza yardımcı olabilir.
**Hepsini Bir Araya Getirmek **

Bu ay, tartışılan her şeyi birleştiren son bir örnek vermek yerine, bir meydan okuma belirleyelim. Her gün bu fikirlerden birini uygulamak için bir hafta geçirebilecek misiniz bir bakın. Örneğin, bir gün pratik el ile tetikleyiciler, ertesi gün bazı temel live_loop çalışmaları yapılır ve ertesi gün ana karıştırıcı ile oynanır. Ardından tekrarlayın. İlk başta işler yavaş ve tıkalı hissediyorsa endişelenmeyin - pratik yapmaya devam edin ve gerçek bir izleyici için canlı kodlama yapacağınızı bilmeden önce.


## A.16 How to Practice Live Coding
***Canlı Kodlama Uygulaması İçin 8 İpucu***
Geçen ay, canlı kodlamada uzmanlaşmak için beş önemli tekniğe göz attık - diğer bir deyişle, Sonic Pi'yi bir müzik aletine yaklaşırken yaptığımız gibi kod yaklaşımı için nasıl kullanabileceğimizi araştırdık. Tartıştığımız önemli kavramlardan biri pratikti. Bu ay, canlı kodlama uygulamasının neden önemli olduğunu ve nasıl başlayabileceğinizi anlamak için daha derin bir dalış yapacağız.
**Düzenli Olarak Pratik Yapın**
En önemli öneri, düzenli olarak pratik yapmanızdır. Kural olarak, genellikle günde 1-2 saat pratik yapıyorum, ancak başladığınızda 20 dakika gayet iyi. Küçük ama çoğu zaman hedeflediğiniz şeydir - yani sadece 10 dakikayı yönetebiliyorsanız, bu harika bir başlangıç.
Alıştırma ipucu # 1 - Bir alıştırma rutini geliştirmeye başlayın. Sizin için uygun olan günde güzel bir zaman geçirin ve haftanın birçok günü olabildiğince çok çalışın. Çok geçmeden normal oturumunuzu dört gözle bekliyor olacaksınız.
**Dokunma Tipini Öğrenin**
Sahnede sahne alan profesyonel bir müzisyeni izlerseniz, muhtemelen birkaç şeyi fark edeceksiniz. Öncelikle, oyun oynadıklarında aletlerine bakmazlar. Parmakları, kolları ve vücutları, hangi tuşlara basılacağını, kopacak dizeleri veya çok fazla düşünmek zorunda kalmadan vurmak için davulları biliyorlar. Bu “kas hafızası” olarak bilinir ve yalnızca profesyonellerin yapabileceği bir şey gibi görünse de, bu sadece tekrarlamayı pratik yaparak - bisiklete binmeyi ilk öğrendiğinizde olduğu gibi. Canlı kodlayıcılar, zihinlerini nerede hareket ettireceklerini düşünmek zorunda kalmamak için kas hafızasını kullanır, böylece müziğe odaklanabilirler. Buna dokunmatik yazma denir - klavyeye bakmak zorunda kalmadan yazma.
Pratik ipucu # 2 - tipe dokunmayı öğrenin. Bunu başarmanıza yardımcı olacak birçok uygulama, web sitesi ve hatta oyun var. Görünümünden hoşlandığınızı bulun ve aşağıya bakmadan kod yazana kadar devam edin.
**Dururken Kod**
Bir müzisyenin vücudu enstrümanlarını çalmak için koşullanmıştır. Örneğin, bir trompet çaların sert bir şekilde üfleyebilmesi gerekir, bir gitaristin klavyeyi güçlü bir şekilde tutabilmesi ve bir davulcunun davullara uzun süre boyunca sürekli olarak vurabilmesi gerekir. Öyleyse, canlı kodlamada fiziksel olan nedir? Tıpkı DJ'ler gibi, canlı kodlayıcılar tipik olarak ayakta dururken performans sergiliyor ve bazıları kod yaparken bile dans ediyor! Bir masada otururken canlı kodlama pratiği yapıyorsanız ve ardından bir konserde kalkıp durmak zorunda kalırsanız, muhtemelen farkı çok zor ve sinir bozucu bulursunuz.
Pratik ipucu # 3 - pratik yaparken ayakta durun. Bunu yapmanın en kolay yolu, bir yükseklik masasını kullanmaktır. Ancak, benim gibi evde biri yoksa, birkaç tane düşük-fi seçeneği var. Aldığım yaklaşım, oldukça iyi çalışan bir ütü masası kullanmak. Bir diğeri de bazı kutuları veya büyük kitapları normal bir masaya koymak ve klavyenizi bunun üzerine koymak. Ayrıca, uygulamaya başlamadan önce biraz gerindiğinizden ve seans boyunca biraz dans ettiğinden emin olun. Unutma, kimse seni izlemiyor, o yüzden eğlen ve sahnede kendini daha doğal hissedeceksin.
**Uygulama Kurma**
Çoğu enstrüman çalınmadan önce bir miktar montaj ve ayar gerektirir. Kâğıtlarla dolu bir otobüsü olan bir rock yıldızı olmadıkça, işinden önce kendi enstrümanını kurman gerekecek. Bu genellikle stresli bir zamandır ve sorunların ortaya çıkması kolaydır. Buna yardımcı olmanın bir yolu, kurulum sürecini uygulama oturumlarına dahil etmektir.
Uygulama ipucu # 4 - kurulumunuzu uygulamanızın önemli bir parçası olarak kabul edin. Örneğin, Raspberry Pi'nizi ve klavyenizi içeride tutabileceğiniz bir kutu veya çantaya sahip olun. Her bir uygulama seansından önce, tüm parçaları çıkarın, her şeyi bağlayın ve Sonic Pi çalışana ve ses gelene kadar önyükleme işlemi boyunca çalışın . Çalışmayı tamamladığınızda, daha sonra her şeyi dikkatlice paketlemek için zaman ayırın. Bu ilk başta biraz zaman alabilir, ancak çok geçmeden düşünmeden, her şeyi inanılmaz hızlı bir şekilde kurup paketleyebileceksiniz.
**Müziksel Olarak Deneme**
Bir kere kurduğunuzda ve müzik yapmaya başlamak için hazır olduğunuzda, nereden başlayacağınızı bilmek için kendinizi zorlukla karşılaşabilirsiniz. Birçok insanın karşılaştığı sorunlardan biri, yapmak istedikleri ses türleri hakkında iyi bir fikir sahibi olmaları, ancak üretemedikleri için hayal kırıklığına uğramalarıdır. Bazı insanlar ne tür sesler yapmak istediklerini bile bilmiyorlar! Yapılacak ilk şey, endişelenmek değil - bu çok yaygındır ve her müzisyenin başına gelir - uzun süredir çalışıyor olsalar bile. Hiç sevmediğiniz sesler yapmak, hiç ses çıkarmamaktan çok daha önemlidir.
Pratik ipucu # 5 - sevmediğiniz sesler ve müzik yapmak için zaman harcayın. Yeni sesleri ve fikirleri keşfetmek için zaman ayırmaya çalışın. Aradığınız tarz değilse, kulağa korkunç gelebileceğinden endişe etmeyin. Böyle bir deney yaparken, bir sese ya da sevdiğiniz bir ses kombinasyonuna tökezleme şansını arttırırsınız! Yaptığınız seslerin% 99'u kötü olsa bile,% 1'i yeni parçanıza riff ya da giriş olabilir. Sevmediğiniz şeyleri unutun ve yaptığınız parçaları hatırlayın. Kodla müzik yaparken bu daha da kolay - sadece kaydet düğmesine tıklayın!
**Kodu Duy**
Birçok müzisyen müzikal nota bakabilir ve çalmak zorunda kalmadan kafasındaki müziği duyabilir. Bu çok faydalı bir beceridir ve canlı kodlama alıştırma seanslarınıza katılmaya değer. Değersiz nokta, kodun neye benzeyeceğini biraz anlayabilmektir. Tam olarak kafanızdan duyabiliyor olmanıza gerek yok, ancak bunun yerine kodun hızlı, yavaş, yüksek, ritmik, melodik, rastgele, vb. Olup olmadığını bilmek faydalı olacaktır. Bu işlemi tersine çevirebilme - kafanızdaki müziği duyabilme ve bunu yapmak için hangi kodu yazacağınızı bilme. Bu konuda ustalaşmanız uzun zaman alabilir, ancak bir kez yaparsanız, sahnede doğaçlama yapabilir ve fikirlerinizi akıcı bir şekilde ifade edebilirsiniz.
Pratik ipucu # 6 - Sonic Pi'ye bir kod yazın, ancak Çalıştır düğmesine basmayın. Bunun yerine, hangi sesi üreteceğini hayal etmeye çalışın. Sonra, Çalıştır, dinle, dinle ve neyin doğru olduğunu ve neyin yapmadığını düşün. Kodlama işleminizin doğal bir parçası haline gelinceye kadar bunu tekrarlamaya devam edin. Pratik yaparken normalde kodun neye benzeyeceği konusunda iyi bir fikrim var. Ancak, yine de şaşırdım ve sonra neden yanıldığımı düşünerek biraz zaman geçirip duracağım. Bu her olduğunda, kendimi yeni yollarla ifade etmeme izin veren yeni numaralar öğreniyorum.
**Tüm Dikkat Dağıtıcaları Kaldır**
Pratik yaparken sık karşılaşılan bir sorun, diğer şeylerle dikkatinizi dağıtmaktır. Alıştırma yapmak zordur ve yaptığınız müzik türünden bağımsız olarak gerçek bir disiplin gerektirir - cazdan klasik ve EDM'ye. Başlamak veya ilerlemek için mücadele ediyorsanız, sosyal medyada dolaşmak veya internette bir şeyler aramak çok kolaydır. Kendinizi 20 dakikalık bir uygulama hedefi olarak belirlediyseniz, denemek önemlidir. Tüm bu zamanı mümkün olduğunca üretken olarak geçirin.
Pratik ipucu # 7 - Uygulamaya başlamadan önce mümkün olduğunca fazla dikkat dağıtıcıyı kaldırın. Örneğin, internet bağlantısını kesin, telefonunuzu başka bir odaya koyun ve rahatsız edilmeyeceğiniz sessiz bir yerde pratik yapmaya çalışın. Müzik kodlamaya odaklanmaya çalışın ve işiniz bittiğinde dikkatinizin dağılmasına geri dönebilirsiniz.
**Alıştırma Günlüğü Tut**
Pratik yaparken, zihninizi sık sık yeni heyecan verici fikirlerle dolu bulacaksınız - yeni müzik yönleri, denemek için yeni sesler, yazmak için yeni işlevler, vb. Bu fikirler genellikle ne yaptığınızı durduracak kadar ilginç yapıyorum ve fikir üzerinde çalışmaya başlayın. Bu başka bir dikkat dağıtma şekli!
Alıştırma ipucu # 8 - klavyenizdeki alıştırma günlüğünü tutun. Heyecan verici yeni bir fikir edindiğinizde, uygulama oturumunuzu geçici olarak duraklatın, fikri hemen not edin, sonra unutun ve uygulamaya devam edin. Uygulamayı tamamladıktan sonra fikirlerinizi düşünerek ve üzerinde çalışarak kaliteli zaman geçirebilirsiniz.
**Hepsini Bir Araya Getirmek**
Bu fikirlerin mümkün olduğunca çoğunu içeren bir uygulama rutini oluşturmaya çalışın. Seansları olabildiğince eğlenceli tutmaya çalışın, ancak bazı uygulama seanslarının zor olacağına ve biraz kendinize iş hissedeceğine dikkat edin. Ancak, ilk parçanızı yarattıktan veya ilk performansınızı verdikten sonra hepsi buna değecektir. Unutma, pratik başarının anahtarıdır!

## A.17 Sample Stretching
***Örnek Germe***
İnsanlar Sonic Pi'yi keşfettiğinde, öğrendikleri ilk şeylerden biri, örnek işlevi kullanarak önceden kaydedilmiş sesleri çalmanın ne kadar basit olduğu. Örneğin, endüstriyel bir davul döngüsünü çalabilir, bir koronun sesini duyabilir veya hatta tek bir kod satırı üzerinden bir vinil çizik dinleyebilirsiniz. Bununla birlikte, birçok insan, bazı güçlü efektler için örneğin oynatılma hızını ve kaydedilen sesler üzerinde yepyeni bir kontrol seviyesi için gerçekte değişiklik yapabileceğinizi fark etmiyor. Öyleyse, Sonic Pi'nin bir kopyasını çıkartın ve bazı örnekleri esnetmeye başlayalım!
**Örneklerin Yavaşlatılması**
Bir örneğin oynatma oranını değiştirmek için hızı kullanmamız gerekir: opt:
'''
sample :guit_em9, rate: 1 
'''
1'lik bir oran belirlersek, örnek normal hızda oynatılır. Eğer yarı hızda oynatmak istiyorsak, sadece 0,5:
'''
sample :guit_em9, rate: 0.5 
'''
Bunun ses üzerinde iki etkisi olduğuna dikkat edin. Öncelikle, örnek adımda daha az ses çıkarır ve ikincisi oynatmak için iki kez uzun sürer (bunun neden böyle olduğunu açıklamak için kenar çubuğuna bakın). 0'a doğru hareket eden daha düşük ve daha düşük hızları bile seçebiliriz, bu nedenle: 0,25'lik bir çeyrek hızdır, 0,1 hızın onda biridir, vb. Bazı düşük oranlarla çalmayı deneyin ve sesi düşük seviyeye getirip getiremeyeceğinizi görün gürle.

**Yukarı Yönlü Hızlandırma Örnekleri**

Küçük bir oran kullanarak sesi daha uzun ve daha düşük hale getirmenin yanı sıra, sesi daha kısa ve daha yüksek yapmak için daha yüksek oranları kullanabiliriz. Bu sefer davul döngüsüyle oynayalım. İlk önce, varsayılan 1'de nasıl ses geldiğini dinleyin:
'''
sample :loop_amen, rate: 1 
'''
Şimdi biraz hızlandıralım:

Örnek: loop_amen, oran: 1.5

Ha! Müzik türlerini eski skool teknodan ormana taşıdık. Her bir davul vuruşunun perdesinin ne kadar yüksek olduğuna ve tüm ritmin nasıl hızlandığına dikkat edin. Şimdi daha da yüksek oranlar deneyin ve tambur döngüsünü ne kadar yüksek ve kısa yapabileceğinizi görün. Örneğin, 100'lük bir oran kullanırsanız, bateri döngüsü bir tıklamaya dönüşür!
**Geri Vites**
Şimdi, çoğunuzun aynı şeyi düşündüğünden eminim… “oran için negatif bir sayı kullanırsanız?”. Harika soru! Bir an için bunu düşünelim. Hızımız: opt, örneğin oynatıldığı hızı, 1'i normal hız, 2'si çift hız, 0,5'i yarı hız, 1'i geriye doğru anlamalıdır! Hadi bir tuzakta deneyelim. İlk önce normal hızda oynatın:
'''
sample :elec_filt_snare, rate: 1 
'''
Şimdi geriye doğru oynat:
'''
sample :elec_filt_snare, rate: -1 
'''
Tabii ki, -2 ile iki kat daha hızlı ya da yarı hızda -0.5 ile geriye doğru oynayabilirsiniz. Şimdi, farklı negatif oranlarla oynayın ve eğlenin. Özellikle: misc_burp örneği ile eğlenceli.

**Örnek, Hız ve Adım [Kenar Çubuğu]**
Hız modifikasyonunun numuneler üzerindeki etkilerinden biri, daha hızlı oranların numunenin ziftte daha yüksek çıkmasına ve daha yavaş hızların numunenin ziftte daha düşük olmasına neden olmasıdır. Her gün yaşamda bu etkiyi duymuş olabileceğiniz bir başka yer de bisiklete binerken ya da bip yaya geçidinden geçerken - ses kaynağına doğru ilerlerken ses perdesinden uzaklaştığınızdan daha yüksektir - sözde Doppler etkisi. Bu neden?
Bir sinüs dalgası ile temsil edilen basit bir bip sesi düşünelim. Bir bip işaretlemek için bir osiloskop kullanırsak, Şekil A gibi bir şey göreceğiz. Bir bip yüksek ok sesi çıkarırsak, Şekil B'yi göreceğiz ve alt oktav Şekil C'ye benzeyecektir. notlar daha küçüktür ve alt notaların dalgaları daha yayılır.
Bir bip sesi örneği, bir grafiğe çizildiğinde orijinal eğrileri yeniden çizecek birçok sayıdan (x, y, koordinatlardan) başka bir şey değildir. Her dairenin bir koordinatı temsil ettiği şekil D'ye bakınız. Koordinatları sese geri döndürmek için, bilgisayar her x değerinde çalışır ve karşılık gelen y değerini hoparlörlere gönderir. Buradaki hile, bilgisayarın x sayılarıyla çalışma hızının kaydedildikleri oranla aynı olması gerekmediğidir. Başka bir deyişle, her daire arasındaki boşluk (bir zamanı temsil eden) gerilebilir veya sıkıştırılabilir. Bu nedenle, bilgisayar x değerlerini orijinal hızdan daha hızlı bir şekilde geçirirse, daha yakın bir bip sesiyle sonuçlanacak şekilde daireleri birbirine daha yakın ezme etkisi olacaktır. Ayrıca tüm çevrelerde daha hızlı çalışacağımızdan bip sesini kısaltacaktır. Bu, Şekil E'de gösterilmiştir.
Son olarak, bilinmesi gereken son şey, Fourier adlı bir matematikçinin, herhangi bir sesin aslında bir araya geldiğini ve çok sayıda sinüs dalgası olduğunu kanıtlamasıdır. Bu nedenle, kaydedilmiş herhangi bir sesi sıkıştırıp uzattığımızda, aslında aynı anda birçok sinüs dalgasını aynı anda gerer ve sıkıştırırız.
**Adım Bükme**
Görüldüğü gibi, daha hızlı bir hız kullanmak ses tonunu yükseltir ve daha yavaş bir hız ses tonunu düşürür. Çok basit ve kullanışlı bir püf noktası, oranın iki katına çıkmasının aslında ziftin oktav kadar yükselmesine neden olduğunu bilmek ve hız sonuçlarının ters yönde yarıya inmesinin ziftin oktav kadar düşük olmasıyla sonuçlanmasıdır. Bu, melodik numuneler için, çift / yarı oranlarda kendisiyle birlikte çalmak, aslında kulağa hoş geliyor:
'''
sample :bass_trance_c, rate: 1
sample :bass_trance_c, rate: 2
sample :bass_trance_c, rate: 0.5 
'''
Ancak, sadece perdenin bir yarı ton (piyanoda bir nota kadar) yükseleceği şekilde oranı değiştirmek istiyorsak ne olur? Sonic Pi bunu rpitch ile çok kolaylaştırıyor: opt:
'''
sample :bass_trance_c
sample :bass_trance_c, rpitch: 3
sample :bass_trance_c, rpitch: 7 
'''
Sağdaki kayıt defterine bakarsanız, 3'lük bir rpitchin gerçekte 1.1892 oranına, 7'nin bir rpitch'in 1.4983 oranına karşılık geldiğini fark edeceksiniz. Son olarak, hızı birleştirebiliriz: ve rpitch: opts:
'''
sample :ambi_choir, rate: 0.25, rpitch: 3
sleep 3
sample :ambi_choir, rate: 0.25, rpitch: 5
sleep 2
sample :ambi_choir, rate: 0.25, rpitch: 6
sleep 1
sample :ambi_choir, rate: 0.25, rpitch: 1 
'''
**Hepsini Bir Araya Getirmek**
Bu fikirleri birleştiren basit bir parçaya göz atalım. Boş bir Sonic Pi tamponuna kopyalayın, oyuna basın, bir süre dinleyin ve sonra kendi parçanız için bir başlangıç noktası olarak kullanın. Örneklerin oynatma hızını değiştirmenin ne kadar eğlenceli olduğunu görün. Ek bir alıştırma olarak kendi seslerinizi kaydetmeyi deneyin ve çılgınca hangi sesleri çıkartabileceğinizi görün.
'''
live_loop :beats do
  sample :guit_em9, rate: [0.25, 0.5, -1].choose, amp: 2
  sample :loop_garzul, rate: [0.5, 1].choose
  sleep 8
end
 
live_loop :melody do
  oct = [-1, 1, 2].choose * 12
  with_fx :reverb, amp: 2 do
    16.times do
      n = (scale 0, :minor_pentatonic).choose
      sample :bass_voxy_hit_c, rpitch: n + 4 + oct
      sleep 0.125
    end
  end
end
'''

## A.18 Sound Design - Additive Synthesis
## A.19 Sound Design - Substractive Synthesis
