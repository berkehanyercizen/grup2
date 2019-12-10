***En İyi Beş İpucu***

**1. Hata Yok**

Sonic Pi ile öğrenmek için en önemli ders gerçekten hata olmamasıdır. Öğrenmenin en iyi yolu, sadece denemek ve denemek. Birçok farklı şeyi deneyin, kodunuzun iyi görünüp görünmediğinden endişelenmeyi bırakın ve mümkün olduğunca çok farklı sentezleyici, nota, FX ve opst ile denemeye başlayın. Sizi güldüren birçok şey keşfedeceksiniz çünkü sesleri çok kötü geliyor ve gerçekten şaşırtıcı görünen bazı gerçek taşlar. Sadece sevmediğiniz şeyleri bırakın ve yaptığınız şeyleri saklayın. “Hatalar” ne kadar çok öğrenirseniz, kişisel kodlama sesini de öğrenir ve keşfedersiniz.

**2.FX’I kullanın**

Örnek sesle ses yapmanın Sonic Pi'nin temelleri konusunda ustalaştınız. Oyun oynadınız mı? Sıradaki ne? Sonic Pi'nin, kodunuzun sesini değiştirmek için 27'den fazla stüdyo FX'i desteklediğini biliyor muydunuz? FX, çizim programlarındaki fantezi görüntü filtreleri gibidir; bunun dışında siyah beyaz bir şeyi bulanıklaştırmak yerine, sesinize yankı, bozulma gibi şeyler ekleyebilirsiniz. Kabloyu gitarınızdan seçtiğiniz bir efekt pedalına ve daha sonra amplifikatöre yapıştırmak gibi düşünün. Neyse ki, Sonic Pi FX'i kullanmayı gerçekten kolaylaştırıyor ve kablo gerektirmiyor! Yapmanız gereken tek şey, kodunuzun hangi bölümüne FX'in eklenmesini istediğinizi seçmek ve bunu FX koduna sarmaktır. Bir örneğe bakalım. Aşağıdaki koda sahip olduğunuzu söyleyin:
sample :loop_garzul

16.times do
  sample :bd_haus
  sleep 0.5
end 
FX'i: loop_garzul örneğine eklemek istiyorsanız, bunu böyle bir with_fx bloğunun içine sokmanız yeterlidir: 
with_fx :flanger do
  sample :loop_garzul
end

16.times do
  sample :bd_haus
  sleep 0.5
end 
Şimdi, bas davuluna FX eklemek istiyorsanız, onu da with_fx ile sarın:
with_fx :flanger do
  sample :loop_garzul
end

with_fx :echo do
  16.times do
    sample :bd_haus
    sleep 0.5
  end
end 
Unutmayın, with_fx içindeki herhangi bir kodu sarabilirsiniz ve oluşturulan sesler bu FX'ten geçer.

**3.  Sentezlerinizi Parametrelendirin**

Kodlama sesini gerçekten keşfetmek için yakında sentezleyici ve FX'in nasıl değiştirileceğini ve kontrol edileceğini bilmek isteyeceksiniz. Örneğin, bir notanın süresini değiştirmek, daha fazla yankı eklemek veya yankılar arasındaki süreyi değiştirmek isteyebilirsiniz. Neyse ki, Sonic Pi size opsiyonel parametreler veya kısa süreliğine seçtikleri özel şeylerle tam olarak yapmanız için inanılmaz bir kontrol seviyesi sunar. Hızlıca bir göz atalım. Bu kodu bir çalışma alanına kopyalayın ve çalıştır tuşuna basın:
sample :guit_em9 
Ooh, güzel bir gitar sesi! Şimdi, onunla oynamaya başlayalım. Oranını değiştirmeye ne dersiniz?
sample :guit_em9, rate: 0.5 
Hey, bu oran ne: Sonunda eklediğim 0,5 bit. Buna opt denir. Tüm Sonic Pi’lerin sentezleyici ve FX’leri onları destekliyor ve birlikte oynayabileceğiniz çok şey var. Ayrıca FX için de kullanılabilirler. Bunu dene:
with_fx :flanger, feedback: 0.6 do
  sample :guit_em9
end 
Şimdi, bu çılgınca sesleri duymak için bu geri bildirimi 1'e yükseltmeyi deneyin! Size sunulan birçok seçenek hakkında ayrıntılı bilgi için belgeleri okuyun.

**4. Canlı Kod**

Hızlı bir şekilde Sonic Pi'yi denemenin ve keşfetmenin en iyi yolu canlı koddur. Bu, önceden kodları başlatılabilir ve hala çalarken sürekli olarak değiştirmenizi ve düzenlemenizi sağlar. Onları, kesim parametresinin bir örneğe ne yaptığını bilmiyorsanız, sadece oynayın. Bir deneyelim! Bu kod Sonic Pi çalışma alanlarınızdan kopyalayın:

live_loop :experiment do
  sample :loop_amen, cutoff: 70
  sleep 1.75
end 
Şimdi, çalıştırmaya başla ve biraz boğuk bir davul molası duyacaksın. Şimdi, kesme: değerini 80 olarak değiştir ve tekrar çalıştırmaya başla. Farkı duyabiliyor musun? 90, 100, 110'u deneyin.
Live_loops'u kullanmaya başladığınızda, geri dönemezsiniz. Ne zaman bir canlı kodlama konseri yaparsam, davulcuların çubuklarına dayandığı kadar live_loop'a güveniyorum. Canlı kodlama hakkında daha fazla bilgi için dahili eğitimin 9. Bölümüne bakın.

**5. Rastgele Akışlarda Gezinin**

Sonunda, yapmayı sevdiğim bir şeyde, Sonic Pi'nin benim için bir şeyler hazırlamasını sağlayarak hile yapmak. Bunu yapmanın gerçekten harika bir yolu randomizasyon kullanmaktır. Kulağa karmaşık gelebilir ama gerçekten değil. Hadi bir bakalım. Bunu boş bir çalışma alanına kopyalayın:

live_loop :rand_surfer do
  use_synth :dsaw
  notes = (scale :e2, :minor_pentatonic, num_octaves: 2)
  16.times do
    play notes.choose, release: 0.1, cutoff: rrand(70, 120)
    sleep 0.125
  end
end 
Şimdi, bunu oynadığınızda, şu ölçekten sürekli bir rasgele nota akışı duyacaksınız: e2: minor_pentatonic: dsaw synth. "Bekleyin bekleyin! Bu bir melodi değil ”, bağırdığını duydum! İşte sihir numarasının ilk kısmı. Live_loop'ta her tur yaptığımızda Sonic Pi'ye rastgele akışı bilinen bir noktaya getirmesini söyleyebiliriz. Bu biraz da TARDIS’te Doktor ile birlikte zaman ve uzayda belirli bir noktaya geri dönmek gibi. Bir deneyelim - use_random_seed 1 satırını live_loop'a ekleyin:

live_loop :rand_surfer do
  use_random_seed 1
  use_synth :dsaw
  notes = (scale :e2, :minor_pentatonic, num_octaves: 2)
  16.times do
    play notes.choose, release: 0.1, cutoff: rrand(70, 120)
    sleep 0.125
  end
end 
Şimdi, live_loop her döngüde dönerse, rastgele akış sıfırlanır. Bu, her seferinde aynı 16 notayı seçtiği anlamına gelir. Hey! Çabuk! Anlık bir melodi. Şimdi, işte gerçekten heyecan verici bir parça. Tohum değerini 1'den başka bir numaraya değiştirin. 4923 deyin. Vay! Başka bir melodi! Yani, sadece bir sayıyı değiştirerek hayal edebileceğiniz kadar melodik kombinasyonları keşfedebilirsiniz! Şimdi, bu kodun büyüsü.

***Canlı Kodlama*** 

Subwoofer kalabalığın derinliklerine bas basarken, lazer ışınları dumanın içinde dilimlenmiş. Atmosfer, karma bir sentezleyici ve dans karışımıyla olgunlaşmıştı. Ancak bu gece kulübünde bir şey tam olarak doğru değildi. DJ kabininin üstündeki parlak renklerle yansıtılan fütüristik bir yazıydı, hareket ediyor, dans ediyor, yanıp sönüyordu. Bu, fantezi görseller değildi, sadece bir Raspberry Pi ile çalışan Sonic Pi'nin bir yansımasıydı. DJ kabininin kullanıcısı dönen disk değildi, kod yazıyor, düzenliyor ve değerlendiriyordu. Canlı. Bu Canlı Kodlama.
 
Bu, fütüristik bir gece kulübünden çok uzaktaki bir hikaye gibi gelebilir, ancak müziği bu şekilde kodlamak gittikçe artan bir eğilimdir ve genellikle Canlı Kodlama (http://toplap.org) olarak tanımlanır. Bu müzik yapımcılığına atılan son yönelimlerden biri Algorave'dir (http://algorave.com) - benim gibi sanatçıların insanların dans etmesi için müzik kodladığı etkinlikler. Ancak, bir gece kulübünde Live Code'a girmenize gerek yoktur - Sonic Pi v2.6 + ile Raspberry Pi'nizi ve bir çift kulaklık veya bazı hoparlörleri alabileceğiniz her yerde yapabilirsiniz. Bu makalenin sonuna gelindiğinde, kendi vuruşlarınızı programlayacak ve canlı olarak değiştireceksiniz. Daha sonra nereye gideceğiniz sadece hayal gücünüzle kısıtlanacaktır.
Canlı Döngü
Sonic Pi ile kodlama yapmanın anahtarı live_loop'ta ustalaşmaktır. Şuna bir bakalım:
live_loop :beats do
  sample :bd_haus
  sleep 0.5
end 
Bir live_loop için 4 temel bileşen var. İlk adı. Yukarıdaki live_loop fonksiyonumuz: atım. Live_loop'unuzu istediğiniz herhangi bir şeyi aramakta özgürsünüz. Delirmek. Yaratıcı ol. Sık sık izleyicilere yaptıkları müzikle ilgili bir şeyler ileten isimler kullanırım. İkinci bileşen, live_loop'un başladığı yeri işaretleyen do kelimesidir. Üçüncüsü, live_loop'un nerede biteceğini belirten son kelimedir ve nihayetinde, döngünün tekrarlanacağını tanımlayan live_loop'un gövdesi vardır - bu, do ve end arasındaki bit. Bu durumda, art arda bas davul çalıyor ve yarım ritmi bekliyoruz. Bu güzel bir düzenli bas ritmi üretir. Devam et, boş bir Sonic Pi tamponuna kopyala ve kaç. Boom, Boom, Boom!
Anında Yeniden Tanımlama
Tamam, live_loop hakkında bu kadar özel olan ne? Şimdiye kadar sadece yüceltilmiş bir döngü gibi görünüyor! Şey, live_loops'un güzelliği, onları anında yeniden tanımlayabilmen. Bu, hala koşarken, ne yaptıklarını değiştirebileceğiniz anlamına gelir. Bu Sonic Pi ile kodlama yaşamanın sırrı budur. Bir oyun oynayalım:

live_loop :choral_drone do
  sample :ambi_choir, rate: 0.4
  sleep 1
end 
Şimdi Çalıştır düğmesine basın veya alt-r tuşuna basın. Şimdi bazı harika koro seslerini dinliyorsunuz. Şimdi, hala çalarken, oranı 0,4'ten 0,38'e değiştirin. Yine koş. Vay! Koro değişim notunu duydun mu? Nasıl olduğuna geri dönmek için 0.4'a kadar değiştirin. Şimdi, onu 0,2'ye, 0,19'a düşürün ve tekrar 0,4'e düşürün. Anında sadece bir parametrenin değiştirilmesinin müziğin gerçek kontrolünü size nasıl verebileceğini anlayın. Şimdi kendi kendinize oranla oynayın - kendi değerlerinizi seçin. Negatif sayıları, gerçekten küçük sayıları ve büyük sayıları deneyin. İyi eğlenceler!
Uyumak Önemlidir
Live_loops ile ilgili en önemli derslerden biri dinlenmeye ihtiyaç duymalarıdır. Aşağıdaki live_loop düşünün:

live_loop :infinite_impossibilities do
  sample :ambi_choir
end 
Bu kodu çalıştırmayı denerseniz, derhal Sonic Pi'nin live_loop'un uyumadığından şikayet ettiğini göreceksiniz. Bu devreye giren bir güvenlik sistemi! Bu kodun bilgisayardan ne yapmasını istediğini düşünmek için bir dakikanızı ayırın. Bu doğru, bilgisayardan sıfır zamanda sonsuz miktarda koro örneği çalmasını istiyor. Güvenlik sistemi olmadan, fakir bilgisayar bunu deneyecek ve yapmaya çalışacak, çarpışma ve yanma sürecinde. Bu yüzden unutmayın, live_loops'unuz bir uyku içermelidir.
Sesleri Birleştirmek
Müzik aynı anda olan şeylerle doludur. Gitarla aynı anda vokallerle aynı anda bas gitar çalmak ... Davullarda eşzamanlılık diyoruz ve Sonic Pi bize aynı anda inanılmaz basit bir şekilde çalma imkanı sunuyor. Birden fazla live_loop kullanın!

live_loop :beats do
  sample :bd_tek
  with_fx :echo, phase: 0.125, mix: 0.4 do
    sample  :drum_cymbal_soft, sustain: 0, release: 0.1
    sleep 0.5
  end
end

live_loop :bass do
  use_synth :tb303
  synth :tb303, note: :e1, release: 4, cutoff: 120, cutoff_attack: 1
  sleep 4
end 
Burada, iki hızlı döngü var, biri hızlı bir şekilde atıyor, diğeri yavaşça çılgınca bir bas sesi çıkarıyor.
Birden fazla live_loops kullanmakla ilgili ilginç şeylerden biri, her birinin kendi zamanını yönetmesidir. Bu, ilginç çok yönlü ritmik yapılar yaratmanın ve hatta aşamalı Steve Reich stiliyle oynamanın gerçekten kolay olduğu anlamına gelir. Şuna bir bak:

*# Steve Reich's Piano Phase*

notes = (ring :E4, :Fs4, :B4, :Cs5, :D5, :Fs4, :E4, :Cs5, :B4, :Fs4, :D5, :Cs5)

live_loop :slow do
  play notes.tick, release: 0.1
  sleep 0.3
end

live_loop :faster do
  play notes.tick, release: 0.1
  sleep 0.295
end 
Hepsini Bir Araya Getirmek
Bu eğitimlerin her birinde, sunulan tüm fikirlerden çıkan yeni bir müzik parçası şeklinde son bir örnekle son bulacağız. Bu kodu okuyun ve ne yaptığını hayal edip edemediğinizi görün. Ardından, taze bir Sonic Pi tamponuna kopyalayın ve Çalıştır'a basın ve aslında nasıl bir ses olduğunu duyun. Son olarak, sayılardan birini değiştirin ya da yorum ve yorumdakileri rahatsız edin. Bunu yeni bir performans için bir başlangıç noktası olarak kullanıp kullanamayacağınıza bakın ve çoğu zaman eğlenin! Bir dahaki sefere görüşürüz…

with_fx :reverb, room: 1 do
  live_loop :time do
    synth :prophet, release: 8, note: :e1, cutoff: 90, amp: 3
    sleep 8
  end
end

live_loop :machine do
  sample :loop_garzul, rate: 0.5, finish: 0.25
  sample :loop_industrial, beat_stretch: 4, amp: 1
  sleep 4
end

live_loop :kik do
  sample :bd_haus, amp: 2
  sleep 0.5
end

with_fx :echo do
  live_loop :vortex do
    # use_random_seed 800
    notes = (scale :e3, :minor_pentatonic, num_octaves: 3)
    16.times do
      play notes.choose, release: 0.1, amp: 1.5
      sleep 0.125
    end
  end
end

***Kodlu Beats***

Modern müzikteki en heyecan verici ve rahatsız edici teknik gelişmelerden biri örnekleyicilerin icadıydı. Bunlar, içine herhangi bir ses kaydetmenize ve daha sonra bu sesleri birçok ilginç şekilde değiştirmenize ve oynatmanıza izin veren kutulardı. Örneğin, eski bir rekor çekebilir, bir davul solo (veya mola) bulabilir, örnekleyicinize kaydedebilir ve ardından en son atımlarınızın temelini oluşturmak için yarı hızda tekrarla tekrar oynatabilirsiniz. Hip-hop müziğinin bu şekilde doğması işte budur ve bugün bir çeşit örnek içermeyen elektronik müzik bulmak neredeyse imkansızdır. Örnekleri kullanmak, canlı kodlanmış performanslarınıza kolayca yeni ve ilginç öğeler eklemenin harika bir yoludur.
Peki bir örnekleyiciyi nereden bulabilirsin? Zaten bir tane var - bu senin Raspberry Pi! Dahili canlı kodlama uygulaması Sonic Pi, çekirdeğinde yerleşik son derece güçlü bir örnekleyiciye sahiptir. Haydi onunla oynayalım!

**Amen Arası**

En klasik ve tanınabilir davul kırma örneklerinden biri Amen Kırması olarak adlandırılır. İlk defa 1969'da Winstons tarafından davul aralığının bir parçası olarak “Amen Brother” şarkısında yapıldı. Bununla birlikte, 80'li yılların başlarında hip-hop müzisyenleri tarafından keşfedildiğinde ve örnekleyicide kullanıldığında, davul ve bas, breakbeat, hardcore tekno ve breakcore gibi çok çeşitli diğer stillerde yoğun bir şekilde kullanılmaya başlandığı zamandı.
Sonic Pi'ye de yerleştirildiğini duymaktan heyecan duyduğuna eminim. Bir tamponu temizleyin ve aşağıdaki kodu girin:
sample :loop_amen 
Çalıştır ve bomba vur! Dans müziği tarihinin en etkili davul çalmalarından birini dinliyorsunuz. Ancak, bu örnek tek seferlik oynanmasıyla ünlüydü, ilmek almak için yapıldı.
Gerilmiş Vuruş 
Eski dostumuzu geçen ay bu derste tanıtılan live_loop'u kullanarak Amen Break'i geri alalım:
live_loop :amen_break do
  sample :loop_amen
  sleep 2
end 
Tamam, bu yüzden döngü, ama her zaman sinir bozucu bir duraklama var. Bunun nedeni 2 vuruş için uyumasını istedik ve 60'lık varsayılan BPM ile: loop_amen örneği yalnızca 1.753 atış için sürüyor. Bu nedenle 2 - 1.753 = 0.247 atış sessizliğine sahibiz. Kısa olmasına rağmen, hala farkedilir. Bu sorunu düzeltmek için beat_stretch'i kullanabiliriz: Sonic Pi'den numuneyi belirtilen vuruş sayısı ile eşleştirmesini (veya daralmasını) isteyin.
Sonic Pi’nin örnek ve sentezi, amp :, cutoff: ve release: gibi isteğe bağlı parametreler ile size çok fazla kontrol sağlar. Bununla birlikte, isteğe bağlı parametre terimi gerçek bir ağız doludur, bu yüzden işleri güzel ve basit tutmak için sadece opts diyoruz.
live_loop :amen_break do
  sample :loop_amen, beat_stretch: 2
  sleep 2
end   
Şimdi dans ediyoruz! Yine de, belki de havanıza uyması için hızlandırmak veya yavaşlatmak istiyoruz.
Zamanla Oynamak 
Tamam, peki ya stilleri eski okul hip hop ya da breakcore olarak değiştirmek istiyorsak? Bunu yapmanın basit bir yolu zamanla oynamaktır - ya da başka bir deyişle tempoyla uğraşmaktır. Bu Sonic Pi’de süper kolaydır - sadece use_bpm’yi canlı döngünüze atın:

live_loop :amen_break do
  use_bpm 30
  sample :loop_amen, beat_stretch: 2
  sleep 2
end  

Bu yavaş vuruşların üstüne atlarken, 2 için hala uyuduğumuzu ve BPM'mizin 30 olduğunu, ancak her şeyin zaman içinde olduğunu unutmayın. Beat_stretch opt, her şeyin sadece çalıştığından emin olmak için mevcut BPM ile çalışır.
Şimdi, işte eğlenceli kısım. Döngü hala canlıyken, use_bpm 30 satırındaki 30 değerini 50 olarak değiştirin. Hop, her şey daha hızlı, ancak zaman içinde tutuldu! Daha hızlı gitmeyi deneyin - 80'e, 120'ye kadar, şimdi çıldırın ve 200'e yumruk atın!
Filtreleme
Şimdi döngü örnekleri yaşayabiliriz, örnek synth tarafından sağlanan en eğlenceli seçeneklerden bazılarına bakalım. İlk önce kesim: örnekleyicinin kesim filtresini kontrol eder. Varsayılan olarak bu devre dışı bırakılmıştır, ancak kolayca açabilirsiniz:

live_loop :amen_break do
  use_bpm 50
  sample :loop_amen, beat_stretch: 2, cutoff: 70
  sleep 2
end   
Devam et ve keseni değiştir: seç. Örneğin, 100'e yükseltin, Çalıştır'a basın ve sesin değişimini duymak için döngünün dönmesini bekleyin. 50 sağlam ve bassy gibi düşük değerlerin ve 100 ve 120 gibi yüksek değerlerin daha tam sesli ve raspy olduğuna dikkat edin. Bunun nedeni, kesme: opt'in, çim biçme makinesinin çimlerin tepesinden kesildiği gibi, sesin yüksek frekanslı kısımlarını kesmesidir. Kesim: opt uzunluk ayarı gibidir - ne kadar çim bırakılacağını belirler.

**Dilimleme**

Oynamak için bir diğer harika araç dilimleyici FX. Bu sesi kesecek (dilimleyecek). Örnek satırı, FX kodu ile şu şekilde sarın:

live_loop :amen_break do
  use_bpm 50
  with_fx :slicer, phase: 0.25, wave: 0, mix: 1 do
    sample :loop_amen, beat_stretch: 2, cutoff: 100
  end
  sleep 2
end 
Sesin biraz yukarı ve aşağı nasıl sıçradığına dikkat edin. (Karışımı değiştirerek orijinal sesi FX olmadan duyabilirsiniz: opt. 0). Şimdi, phase: opt. Bu, dilimleme etkisinin oranıdır (atış olarak). 0.125 gibi daha küçük bir değer daha hızlı dilimleyecek ve 0.5 gibi daha büyük değerler daha yavaş dilimleyecektir. Aşamayı art arda yarıya indiren ya da ikiye katlayanlara dikkat edin: opt val, her zaman iyi görünme eğilimindedir. Son olarak, dalgayı değiştirin: 0, 1 veya 2'den birini seçin ve sesi nasıl değiştirdiğini duyun. Bunlar çeşitli dalga şekilleridir. 0 bir testere dalgasıdır (sert içeri, solma) 1, kare bir dalgalıdır (sert içeri, sert dışarı) ve 2, üçgen bir dalgalıdır (solmaya, solmaya).
Hepsini Bir Araya Getirmek
Son olarak, zaman içinde geri dönelim ve bu ayın örneğiyle Bristol davul ve bas sahnesini tekrar ziyaret edelim. Tüm bunların ne anlama geldiği hakkında çok fazla endişelenmeyin, sadece yazın, Çalıştır'a basın, sonra opt numaralarını değiştirerek canlı kodlamaya başlayın ve nereye götürebileceğinizi görün. Lütfen yarattıklarınızı paylaşın! Bir dahaki sefere görüşürüz…

use_bpm 100

live_loop :amen_break do
  p = [0.125, 0.25, 0.5].choose
  with_fx :slicer, phase: p, wave: 0, mix: rrand(0.7, 1) do
    r = [1, 1, 1, -1].choose
    sample :loop_amen, beat_stretch: 2, rate: r, amp: 2
  end
  sleep 2
end

live_loop :bass_drum do
  sample :bd_haus, cutoff: 70, amp: 1.5
  sleep 0.5
end

live_loop :landing do
  bass_line = (knit :e1, 3, [:c1, :c2].choose, 1)
  with_fx :slicer, phase: [0.25, 0.5].choose, invert_wave: 1, wave: 0 do
    s = synth :square, note: bass_line.tick, sustain: 4, cutoff: 60
    control s, cutoff_slide: 4, cutoff: 120
  end
  sleep 4
end

***Beş Canlı Kodlama Tekniği***

Bu ayki Sonic Pi eğitiminde, Sonic Pi'ye gerçek bir enstrüman gibi nasıl davranmaya başlayacağınıza bir göz atacağız. Bu nedenle, kodu tamamen farklı bir şekilde düşünmeye başlamamız gerekir. Canlı kodlayıcılar, kodu kemancıların yaylarını nasıl düşündüklerine benzer şekilde düşünür. Aslında, aynı kemancı gibi, farklı sesler (uzun yavaş hareketler ve kısa hızlı vuruşlar) oluşturmak için çeşitli yay tekniklerini uygulayabilir, Sonic Pi'nin sunduğu temel canlı kodlama tekniklerinden beşini keşfedeceğiz. Bu makalenin sonunda, kendi canlı kodlanmış performanslarınız için pratik yapmaya başlayabilirsiniz.

**1. Kısa Yolları Ezberlemek**

Sonic Pi ile kodlamayı yaşayan ilk ipucu kısayolları kullanmaya başlamaktır. Örneğin, fareye ulaşmak için değerli zamanınızı boşa harcamak, Çalıştır düğmesine taşımak ve tıklamak yerine, yalnızca alt ve r tuşlarına aynı anda basabilirsiniz; bu daha hızlıdır ve klavyede parmaklarınızı bir sonraki düzenlemeye hazır tutar. . Üstteki ana düğmelerin kısayollarını, fareyi üzerlerine getirerek bulabilirsiniz. Kısayolların tam listesi için yerleşik öğretici bölüm 10.2'ye bakın.
Gerçekleştirirken, yapılacak eğlenceli bir şey, kısayollara basarken kol hareketinize biraz yetenek katmaktır. Örneğin, bir değişiklik yapmak üzereyken izleyiciyle iletişim kurmak çoğu zaman iyidir - bu nedenle büyük bir güç akoruna çarptığında yaptığınız gibi bir gitaristin üstüne vurduğunuzda hareketlerinizi süsleyin.

**2. Seslerinizi Manuel Olarak Tetikleyin** 
Artık klavyeyle anında kodu tetikleyebilirsiniz, bu beceriyi seslerinizi elle katmanlamak olan ikinci tekniğimiz için hemen uygulayabilirsiniz. Oynamak için çok sayıda çağrı kullanmak ve uykuyla yapılan çağrılarla ayrılmış örnekleri kullanmak yerine, alt-r komutunu kullanarak manuel olarak tetikleyeceğimiz bir çağrı yapacağız. Hadi deneyelim. Aşağıdaki kodu yeni bir belleğe yazın:

synth :tb303, note: :e2 - 0, release: 12, cutoff: 90

Şimdi, Çalıştır tuşuna basın ve ses çalarken, dört notayı aşağıya doğru değiştirerek bırakmak için kodu değiştirin:

synth :tb303, note: :e2 - 4, release: 12, cutoff: 90

Şimdi, her iki sesin de aynı anda çalındığını duymak için Yeniden Çalıştır düğmesine basın. Bunun nedeni, Sonic Pi’nin Çalıştır düğmesinin önceki bir kodun bitmesini beklememesi, ancak aynı anda çalışan kodu başlatmasıdır. Bu, her tetikleyici arasında küçük veya büyük değişikliklerle çok sayıda sesi kolayca katmanlaştırabileceğiniz anlamına gelir. Örneğin, hem notu hem de kesmeyi değiştirmeyi deneyin: opts ve ardından yeniden tetikleyin.
Bu tekniği uzun soyut örneklerle de deneyebilirsiniz. Örneğin:
sample :ambi_lunar_land, rate: 1 
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
set_mixer_control! lpf_slide: 16, lpf: 30 
Daha sonra aşağıdakilerle hızlı bir şekilde yüksek bir değere geri dönebilirsiniz:

set_mixer_control! lpf_slide: 1, lpf: 130 
Bunu yaparken, böyle bir karıştırıcı ile çalışmak için bir tamponu boş tutmak genellikle yararlıdır.

**5. Uygulama**

Canlı kodlama için en önemli teknik pratiktir. Her çeşit profesyonel müzisyenler arasında en yaygın özellik, enstrümanları ile çalmayı pratik etmeleridir - genellikle günde saatlerce. Uygulama, bir gitarist kadar canlı bir kodlayıcı için de önemlidir. Alıştırma parmaklarınızın belirli kalıpları ve genel düzenlemeleri ezberlemesine izin verir, böylece daha akıcı bir şekilde yazabilir ve onlarla çalışabilirsiniz. Alıştırma ayrıca yeni sesleri ve kod yapılarını keşfetme fırsatları sunar.
Gösteri yaparken, ne kadar çok uygulama yaparsanız, konserde rahatlamanız o kadar kolay olacaktır. Alıştırma ayrıca size çekilecek bir deneyim hazinesi verecektir. Bu, hangi değişiklik türlerinin ilginç olacağını ve mevcut seslerle iyi çalışacağını anlamanıza yardımcı olabilir.
Hepsini Bir Araya Getirmek 

Bu ay, tartışılan her şeyi birleştiren son bir örnek vermek yerine, bir meydan okuma belirleyelim. Her gün bu fikirlerden birini uygulamak için bir hafta geçirebilecek misiniz bir bakın. Örneğin, bir gün pratik el ile tetikleyiciler, ertesi gün bazı temel live_loop çalışmaları yapılır ve ertesi gün ana karıştırıcı ile oynanır. Ardından tekrarlayın. İlk başta işler yavaş ve tıkalı hissediyorsa endişelenmeyin - pratik yapmaya devam edin ve gerçek bir izleyici için canlı kodlama yapacağınızı bilmeden önce.

***Canlı Kodlama Uygulaması İçin 8 İpucu***

Geçen ay, canlı kodlamada uzmanlaşmak için beş önemli tekniğe göz attık - diğer bir deyişle, Sonic Pi'yi bir müzik aletine yaklaşırken yaptığımız gibi kod yaklaşımı için nasıl kullanabileceğimizi araştırdık. Tartıştığımız önemli kavramlardan biri pratikti. Bu ay, canlı kodlama uygulamasının neden önemli olduğunu ve nasıl başlayabileceğinizi anlamak için daha derin bir dalış yapacağız.
Düzenli Olarak Pratik Yapın
En önemli öneri, düzenli olarak pratik yapmanızdır. Kural olarak, genellikle günde 1-2 saat pratik yapıyorum, ancak başladığınızda 20 dakika gayet iyi. Küçük ama çoğu zaman hedeflediğiniz şeydir - yani sadece 10 dakikayı yönetebiliyorsanız, bu harika bir başlangıç.
Alıştırma ipucu # 1 - Bir alıştırma rutini geliştirmeye başlayın. Sizin için uygun olan günde güzel bir zaman geçirin ve haftanın birçok günü olabildiğince çok çalışın. Çok geçmeden normal oturumunuzu dört gözle bekliyor olacaksınız.
Dokunma Tipini Öğrenin 
Sahnede sahne alan profesyonel bir müzisyeni izlerseniz, muhtemelen birkaç şeyi fark edeceksiniz. Öncelikle, oyun oynadıklarında aletlerine bakmazlar. Parmakları, kolları ve vücutları, hangi tuşlara basılacağını, kopacak dizeleri veya çok fazla düşünmek zorunda kalmadan vurmak için davulları biliyorlar. Bu “kas hafızası” olarak bilinir ve yalnızca profesyonellerin yapabileceği bir şey gibi görünse de, bu sadece tekrarlamayı pratik yaparak - bisiklete binmeyi ilk öğrendiğinizde olduğu gibi. Canlı kodlayıcılar, zihinlerini nerede hareket ettireceklerini düşünmek zorunda kalmamak için kas hafızasını kullanır, böylece müziğe odaklanabilirler. Buna dokunmatik yazma denir - klavyeye bakmak zorunda kalmadan yazma.
Pratik ipucu # 2 - tipe dokunmayı öğrenin. Bunu başarmanıza yardımcı olacak birçok uygulama, web sitesi ve hatta oyun var. Görünümünden hoşlandığınızı bulun ve aşağıya bakmadan kod yazana kadar devam edin.

**Dururken Kod**

Bir müzisyenin vücudu enstrümanlarını çalmak için koşullanmıştır. Örneğin, bir trompet çaların sert bir şekilde üfleyebilmesi gerekir, bir gitaristin klavyeyi güçlü bir şekilde tutabilmesi ve bir davulcunun davullara uzun süre boyunca sürekli olarak vurabilmesi gerekir. Öyleyse, canlı kodlamada fiziksel olan nedir? Tıpkı DJ'ler gibi, canlı kodlayıcılar tipik olarak ayakta dururken performans sergiliyor ve bazıları kod yaparken bile dans ediyor! Bir masada otururken canlı kodlama pratiği yapıyorsanız ve ardından bir konserde kalkıp durmak zorunda kalırsanız, muhtemelen farkı çok zor ve sinir bozucu bulursunuz.
Pratik ipucu # 3 - pratik yaparken ayakta durun. Bunu yapmanın en kolay yolu, bir yükseklik masasını kullanmaktır. Ancak, benim gibi evde biri yoksa, birkaç tane düşük-fi seçeneği var. Aldığım yaklaşım, oldukça iyi çalışan bir ütü masası kullanmak. Bir diğeri de bazı kutuları veya büyük kitapları normal bir masaya koymak ve klavyenizi bunun üzerine koymak. Ayrıca, uygulamaya başlamadan önce biraz gerindiğinizden ve seans boyunca biraz dans ettiğinden emin olun. Unutma, kimse seni izlemiyor, o yüzden eğlen ve sahnede kendini daha doğal hissedeceksin.
Uygulama Kurma 
Çoğu enstrüman çalınmadan önce bir miktar montaj ve ayar gerektirir. Kâğıtlarla dolu bir otobüsü olan bir rock yıldızı olmadıkça, işinden önce kendi enstrümanını kurman gerekecek. Bu genellikle stresli bir zamandır ve sorunların ortaya çıkması kolaydır. Buna yardımcı olmanın bir yolu, kurulum sürecini uygulama oturumlarına dahil etmektir.
Uygulama ipucu # 4 - kurulumunuzu uygulamanızın önemli bir parçası olarak kabul edin. Örneğin, Raspberry Pi'nizi ve klavyenizi içeride tutabileceğiniz bir kutu veya çantaya sahip olun. Her bir uygulama seansından önce, tüm parçaları çıkarın, her şeyi bağlayın ve Sonic Pi çalışana ve ses gelene kadar önyükleme işlemi boyunca çalışın . Çalışmayı tamamladığınızda, daha sonra her şeyi dikkatlice paketlemek için zaman ayırın. Bu ilk başta biraz zaman alabilir, ancak çok geçmeden düşünmeden, her şeyi inanılmaz hızlı bir şekilde kurup paketleyebileceksiniz.
Müziksel Olarak Deneme 
Bir kere kurduğunuzda ve müzik yapmaya başlamak için hazır olduğunuzda, nereden başlayacağınızı bilmek için kendinizi zorlukla karşılaşabilirsiniz. Birçok insanın karşılaştığı sorunlardan biri, yapmak istedikleri ses türleri hakkında iyi bir fikir sahibi olmaları, ancak üretemedikleri için hayal kırıklığına uğramalarıdır. Bazı insanlar ne tür sesler yapmak istediklerini bile bilmiyorlar! Yapılacak ilk şey, endişelenmek değil - bu çok yaygındır ve her müzisyenin başına gelir - uzun süredir çalışıyor olsalar bile. Hiç sevmediğiniz sesler yapmak, hiç ses çıkarmamaktan çok daha önemlidir.
Pratik ipucu # 5 - sevmediğiniz sesler ve müzik yapmak için zaman harcayın. Yeni sesleri ve fikirleri keşfetmek için zaman ayırmaya çalışın. Aradığınız tarz değilse, kulağa korkunç gelebileceğinden endişe etmeyin. Böyle bir deney yaparken, bir sese ya da sevdiğiniz bir ses kombinasyonuna tökezleme şansını arttırırsınız! Yaptığınız seslerin% 99'u kötü olsa bile,% 1'i yeni parçanıza riff ya da giriş olabilir. Sevmediğiniz şeyleri unutun ve yaptığınız parçaları hatırlayın. Kodla müzik yaparken bu daha da kolay - sadece kaydet düğmesine tıklayın!

**Kodu Duy**

Birçok müzisyen müzikal nota bakabilir ve çalmak zorunda kalmadan kafasındaki müziği duyabilir. Bu çok faydalı bir beceridir ve canlı kodlama alıştırma seanslarınıza katılmaya değer. Değersiz nokta, kodun neye benzeyeceğini biraz anlayabilmektir. Tam olarak kafanızdan duyabiliyor olmanıza gerek yok, ancak bunun yerine kodun hızlı, yavaş, yüksek, ritmik, melodik, rastgele, vb. Olup olmadığını bilmek faydalı olacaktır. Bu işlemi tersine çevirebilme - kafanızdaki müziği duyabilme ve bunu yapmak için hangi kodu yazacağınızı bilme. Bu konuda ustalaşmanız uzun zaman alabilir, ancak bir kez yaparsanız, sahnede doğaçlama yapabilir ve fikirlerinizi akıcı bir şekilde ifade edebilirsiniz.
Pratik ipucu # 6 - Sonic Pi'ye bir kod yazın, ancak Çalıştır düğmesine basmayın. Bunun yerine, hangi sesi üreteceğini hayal etmeye çalışın. Sonra, Çalıştır, dinle, dinle ve neyin doğru olduğunu ve neyin yapmadığını düşün. Kodlama işleminizin doğal bir parçası haline gelinceye kadar bunu tekrarlamaya devam edin. Pratik yaparken normalde kodun neye benzeyeceği konusunda iyi bir fikrim var. Ancak, yine de şaşırdım ve sonra neden yanıldığımı düşünerek biraz zaman geçirip duracağım. Bu her olduğunda, kendimi yeni yollarla ifade etmeme izin veren yeni numaralar öğreniyorum.
Tüm Dikkat Dağıtıcaları Kaldır 
Pratik yaparken sık karşılaşılan bir sorun, diğer şeylerle dikkatinizi dağıtmaktır. Alıştırma yapmak zordur ve yaptığınız müzik türünden bağımsız olarak gerçek bir disiplin gerektirir - cazdan klasik ve EDM'ye. Başlamak veya ilerlemek için mücadele ediyorsanız, sosyal medyada dolaşmak veya internette bir şeyler aramak çok kolaydır. Kendinizi 20 dakikalık bir uygulama hedefi olarak belirlediyseniz, denemek önemlidir. Tüm bu zamanı mümkün olduğunca üretken olarak geçirin.
Pratik ipucu # 7 - Uygulamaya başlamadan önce mümkün olduğunca fazla dikkat dağıtıcıyı kaldırın. Örneğin, internet bağlantısını kesin, telefonunuzu başka bir odaya koyun ve rahatsız edilmeyeceğiniz sessiz bir yerde pratik yapmaya çalışın. Müzik kodlamaya odaklanmaya çalışın ve işiniz bittiğinde dikkatinizin dağılmasına geri dönebilirsiniz.
Alıştırma Günlüğü Tut 
Pratik yaparken, zihninizi sık sık yeni heyecan verici fikirlerle dolu bulacaksınız - yeni müzik yönleri, denemek için yeni sesler, yazmak için yeni işlevler, vb. Bu fikirler genellikle ne yaptığınızı durduracak kadar ilginç yapıyorum ve fikir üzerinde çalışmaya başlayın. Bu başka bir dikkat dağıtma şekli!
Alıştırma ipucu # 8 - klavyenizdeki alıştırma günlüğünü tutun. Heyecan verici yeni bir fikir edindiğinizde, uygulama oturumunuzu geçici olarak duraklatın, fikri hemen not edin, sonra unutun ve uygulamaya devam edin. Uygulamayı tamamladıktan sonra fikirlerinizi düşünerek ve üzerinde çalışarak kaliteli zaman geçirebilirsiniz.

**Hepsini Bir Araya Getirmek**

Bu fikirlerin mümkün olduğunca çoğunu içeren bir uygulama rutini oluşturmaya çalışın. Seansları olabildiğince eğlenceli tutmaya çalışın, ancak bazı uygulama seanslarının zor olacağına ve biraz kendinize iş hissedeceğine dikkat edin. Ancak, ilk parçanızı yarattıktan veya ilk performansınızı verdikten sonra hepsi buna değecektir. Unutma, pratik başarının anahtarıdır!

**Örnek Germe**

İnsanlar Sonic Pi'yi keşfettiğinde, öğrendikleri ilk şeylerden biri, örnek işlevi kullanarak önceden kaydedilmiş sesleri çalmanın ne kadar basit olduğu. Örneğin, endüstriyel bir davul döngüsünü çalabilir, bir koronun sesini duyabilir veya hatta tek bir kod satırı üzerinden bir vinil çizik dinleyebilirsiniz. Bununla birlikte, birçok insan, bazı güçlü efektler için örneğin oynatılma hızını ve kaydedilen sesler üzerinde yepyeni bir kontrol seviyesi için gerçekte değişiklik yapabileceğinizi fark etmiyor. Öyleyse, Sonic Pi'nin bir kopyasını çıkartın ve bazı örnekleri esnetmeye başlayalım!
Örneklerin Yavaşlatılması
Bir örneğin oynatma oranını değiştirmek için hızı kullanmamız gerekir: opt:
sample :guit_em9, rate: 1 
1'lik bir oran belirlersek, örnek normal hızda oynatılır. Eğer yarı hızda oynatmak istiyorsak, sadece 0,5:
sample :guit_em9, rate: 0.5 
Bunun ses üzerinde iki etkisi olduğuna dikkat edin. Öncelikle, örnek adımda daha az ses çıkarır ve ikincisi oynatmak için iki kez uzun sürer (bunun neden böyle olduğunu açıklamak için kenar çubuğuna bakın). 0'a doğru hareket eden daha düşük ve daha düşük hızları bile seçebiliriz, bu nedenle: 0,25'lik bir çeyrek hızdır, 0,1 hızın onda biridir, vb. Bazı düşük oranlarla çalmayı deneyin ve sesi düşük seviyeye getirip getiremeyeceğinizi görün gürle.

**Yukarı Yönlü Hızlandırma Örnekleri**

Küçük bir oran kullanarak sesi daha uzun ve daha düşük hale getirmenin yanı sıra, sesi daha kısa ve daha yüksek yapmak için daha yüksek oranları kullanabiliriz. Bu sefer davul döngüsüyle oynayalım. İlk önce, varsayılan 1'de nasıl ses geldiğini dinleyin:
sample :loop_amen, rate: 1 
Şimdi biraz hızlandıralım:

Örnek: loop_amen, oran: 1.5

Ha! Müzik türlerini eski skool teknodan ormana taşıdık. Her bir davul vuruşunun perdesinin ne kadar yüksek olduğuna ve tüm ritmin nasıl hızlandığına dikkat edin. Şimdi daha da yüksek oranlar deneyin ve tambur döngüsünü ne kadar yüksek ve kısa yapabileceğinizi görün. Örneğin, 100'lük bir oran kullanırsanız, bateri döngüsü bir tıklamaya dönüşür!
Geri Vites
Şimdi, çoğunuzun aynı şeyi düşündüğünden eminim… “oran için negatif bir sayı kullanırsanız?”. Harika soru! Bir an için bunu düşünelim. Hızımız: opt, örneğin oynatıldığı hızı, 1'i normal hız, 2'si çift hız, 0,5'i yarı hız, 1'i geriye doğru anlamalıdır! Hadi bir tuzakta deneyelim. İlk önce normal hızda oynatın:

sample :elec_filt_snare, rate: 1 
Şimdi geriye doğru oynat:

sample :elec_filt_snare, rate: -1 
Tabii ki, -2 ile iki kat daha hızlı ya da yarı hızda -0.5 ile geriye doğru oynayabilirsiniz. Şimdi, farklı negatif oranlarla oynayın ve eğlenin. Özellikle: misc_burp örneği ile eğlenceli.

***Örnek, Hız ve Adım [Kenar Çubuğu]***

Hız modifikasyonunun numuneler üzerindeki etkilerinden biri, daha hızlı oranların numunenin ziftte daha yüksek çıkmasına ve daha yavaş hızların numunenin ziftte daha düşük olmasına neden olmasıdır. Her gün yaşamda bu etkiyi duymuş olabileceğiniz bir başka yer de bisiklete binerken ya da bip yaya geçidinden geçerken - ses kaynağına doğru ilerlerken ses perdesinden uzaklaştığınızdan daha yüksektir - sözde Doppler etkisi. Bu neden?
Bir sinüs dalgası ile temsil edilen basit bir bip sesi düşünelim. Bir bip işaretlemek için bir osiloskop kullanırsak, Şekil A gibi bir şey göreceğiz. Bir bip yüksek ok sesi çıkarırsak, Şekil B'yi göreceğiz ve alt oktav Şekil C'ye benzeyecektir. notlar daha küçüktür ve alt notaların dalgaları daha yayılır.
Bir bip sesi örneği, bir grafiğe çizildiğinde orijinal eğrileri yeniden çizecek birçok sayıdan (x, y, koordinatlardan) başka bir şey değildir. Her dairenin bir koordinatı temsil ettiği şekil D'ye bakınız. Koordinatları sese geri döndürmek için, bilgisayar her x değerinde çalışır ve karşılık gelen y değerini hoparlörlere gönderir. Buradaki hile, bilgisayarın x sayılarıyla çalışma hızının kaydedildikleri oranla aynı olması gerekmediğidir. Başka bir deyişle, her daire arasındaki boşluk (bir zamanı temsil eden) gerilebilir veya sıkıştırılabilir. Bu nedenle, bilgisayar x değerlerini orijinal hızdan daha hızlı bir şekilde geçirirse, daha yakın bir bip sesiyle sonuçlanacak şekilde daireleri birbirine daha yakın ezme etkisi olacaktır. Ayrıca tüm çevrelerde daha hızlı çalışacağımızdan bip sesini kısaltacaktır. Bu, Şekil E'de gösterilmiştir.
Son olarak, bilinmesi gereken son şey, Fourier adlı bir matematikçinin, herhangi bir sesin aslında bir araya geldiğini ve çok sayıda sinüs dalgası olduğunu kanıtlamasıdır. Bu nedenle, kaydedilmiş herhangi bir sesi sıkıştırıp uzattığımızda, aslında aynı anda birçok sinüs dalgasını aynı anda gerer ve sıkıştırırız.

**Adım Bükme**

Görüldüğü gibi, daha hızlı bir hız kullanmak ses tonunu yükseltir ve daha yavaş bir hız ses tonunu düşürür. Çok basit ve kullanışlı bir püf noktası, oranın iki katına çıkmasının aslında ziftin oktav kadar yükselmesine neden olduğunu bilmek ve hız sonuçlarının ters yönde yarıya inmesinin ziftin oktav kadar düşük olmasıyla sonuçlanmasıdır. Bu, melodik numuneler için, çift / yarı oranlarda kendisiyle birlikte çalmak, aslında kulağa hoş geliyor:

sample :bass_trance_c, rate: 1
sample :bass_trance_c, rate: 2
sample :bass_trance_c, rate: 0.5 
Ancak, sadece perdenin bir yarı ton (piyanoda bir nota kadar) yükseleceği şekilde oranı değiştirmek istiyorsak ne olur? Sonic Pi bunu rpitch ile çok kolaylaştırıyor: opt:

sample :bass_trance_c
sample :bass_trance_c, rpitch: 3
sample :bass_trance_c, rpitch: 7 

Sağdaki kayıt defterine bakarsanız, 3'lük bir rpitchin gerçekte 1.1892 oranına, 7'nin bir rpitch'in 1.4983 oranına karşılık geldiğini fark edeceksiniz. Son olarak, hızı birleştirebiliriz: ve rpitch: opts:

sample :ambi_choir, rate: 0.25, rpitch: 3
sleep 3
sample :ambi_choir, rate: 0.25, rpitch: 5
sleep 2
sample :ambi_choir, rate: 0.25, rpitch: 6
sleep 1
sample :ambi_choir, rate: 0.25, rpitch: 1 
Hepsini Bir Araya Getirmek 
Bu fikirleri birleştiren basit bir parçaya göz atalım. Boş bir Sonic Pi tamponuna kopyalayın, oyuna basın, bir süre dinleyin ve sonra kendi parçanız için bir başlangıç noktası olarak kullanın. Örneklerin oynatma hızını değiştirmenin ne kadar eğlenceli olduğunu görün. Ek bir alıştırma olarak kendi seslerinizi kaydetmeyi deneyin ve çılgınca hangi sesleri çıkartabileceğinizi görün.

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

