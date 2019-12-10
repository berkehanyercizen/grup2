# Appendix & MagPi Articles
## A.01 SonicPi için tavsiyeler
## A.02 Live coding
## A.03 coded beats
## A.04 Synth Riffs
## A.05 Acid Bass
## A.06 Musical Minecraft
## A.07 Bizet Beats
Minecraft'ı sonic Sonic Pi ile kodlayan fantastik dünyaya yaptığımız kısa geziden sonra tekrar müzikal yapalım. Bugün, kodun müthiş gücünü kullanarak doğruca 21. yüzyıla klasik bir operatif dans parçası getireceğiz.
## A.7 Çirkin ve Yıkıcı
1875 yılına dönen zaman makinesine atlayalım. Bizet adında bir besteci en son operası Carmen'i yeni bitirmişti. Ne yazık ki, birçok heyecan verici ve yıkıcı yeni müzik parçası gibi, insanlar başlangıçta hiç beğenmedi çünkü çok çirkin ve farklıydı. Ne yazık ki Bizet, operanın büyük uluslararası başarı kazanmasından on yıl önce öldü ve tüm zamanların en ünlü ve en sık yapılan operalarından biri oldu. Bu trajedi ile sempati duymak için Carmen'in ana temalarından birini ele alalım ve zamanımızdaki çoğu insan için çok çirkin ve farklı olan modern bir müzik biçimine dönüştürelim - canlı kodlanmış müzik!

## A.7 - Habanera'nın Kodunu Çözme
Kod çalıştırmaya çalışmak tüm opera bu eğitim için biraz zor olacak. Hadi en ünlü bölümlerden biri olan Habanera'ya giden bas çizgisine odaklanalım:
 
Henüz müzik notasyonu okumamışsanız, bu size okunaklı görünmeyebilir. Ancak, programcılar olarak müzik gösterimini başka bir kod biçimi olarak görüyoruz - yalnızca bilgisayar yerine bir müzisyenin talimatlarını temsil ediyor. Bu nedenle kod çözmenin bir yolunu bulmamız gerekiyor.

## A.7 - Notalar
Notalar, bu dergideki kelimeler gibi soldan sağa doğru düzenlenir, ancak farklı yüksekliklere de sahiptir. Skordaki yükseklik notun perdesini gösterir. Skordaki nota arttıkça, notanın adımı da artar.
Biz zaten Sonic Pi da notanın perdesinin nasıl değiştirileceğini biliyoruz. Biz play 75 ve play 80 gibi yüksek veya düşük numaraları kullanıyoruz. Ya da nota adlarını kullanıyoruz play :E ve play :F. Neyse ki müzikal puanın dikey konumlarının her biri belirli bir nota adını temsil eder. Bu kullanışlı arama masasına bir göz atın:
 
## A.7 - Rests
Müzik notaları, birçok şeyle iletişim kurabilen son derece zengin ve etkileyici bir kod türüdür. Bu nedenle, müzik notalarının yalnızca hangi notaları çalacağınızı değil, aynı zamanda notaları çalamayacağınızı da söyleyebilmesi sürpriz olmamalıdır . Programlamada bu, nil ya da null- bir değerin olmaması fikrine eşdeğerdir . Başka bir deyişle, nota çalmamak notanın olmaması gibidir.
Eğer skora yakından bakarsanız, gerçekte oyun oynamak için notaları temsil eden siyah noktaların ve diğerlerini temsil eden şeylerin dalgalanmalarının olduğunu göreceksiniz. Neyse ki Sonic Pi'nin dinlenmek için çok kullanışlı bir temsili var: :r yani kaçarsak: play :r aslında sessizlik oynuyor! Ayrıca play :rest, play nil ya play false da bunların hepsini temsil etmenin eşdeğer yolları olarak yazabiliriz .

## A.7 - Ritim
Son olarak, notasyonda kod çözmeyi öğrenecek son bir şey var: notaların zamanlaması. Orijinal gösterimde notaların kiriş adı verilen kalın çizgilerle bağlantılı olduğunu göreceksiniz. İkinci nota bu kirişlerden ikisine sahiptir, yani atımın 16'sına kadar devam eder. Diğer notaların tek bir ışını vardır, bu da bir vuruşun 8'i için devam ettiği anlamına gelir. Gerisi iki dalgalı kirişe sahiptir, yani aynı zamanda atımın 16'sını temsil eder.
Yeni şeyleri çözmeye ve keşfetmeye çalıştığımızda çok kullanışlı bir numara, her türlü ilişkiyi veya örüntüyü denemek ve görmek için her şeyi mümkün olduğunca benzer yapmaktır. Örneğin, notasyonumuzu yalnızca 16'lı yıllarda tekrar yazdığımızda, notasyonumuzun sadece güzel bir nota ve dinlenme dizisine dönüştüğünü görebilirsiniz.
 
## A.7 - Habanera'yı yeniden kodlamak
Şimdi bu bas çizgisini Sonic Pi'ye çevirmeye başlayacağız. Hadi bu notları kodlayalım ve bir halkada dinlenelim:
(ring :d, :r, :r, :a, :f5, :r, :a, :r)
Bunun neye benzediğini görelim. Canlı bir döngüde atın ve işaretleyin:
live_loop :habanera do
  play (ring :d, :r, :r, :a, :f5, :r, :a, :r).tick
  sleep 0.25
end

Muhteşem, bu anında tanınabilir riff hoparlörleriniz aracılığıyla canlanır. Buraya gelmek için çok çaba sarf etti, ama buna değdi - beşlik!

## A.7 - Moody Synths
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

## A.7 - Hepsini bir araya getirmek
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
 
## A.08 Become a Minecraft VJ
## A.09 Randomisation
## A.10 Control
## A.11 Tick Tock
## A.12 Sample Slicing
## A.13 Code a Probabilistic Sequencer
## A.14 Amplitude Modulation
## A.15 Five Live Coding Techniques
## A.16 How to Practice Live Coding
## A.17 Sample Stretching
## A.18 Sound Design - Additive Synthesis
## A.19 Sound Design - Substractive Synthesis
