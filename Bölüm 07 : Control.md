# 7 Kontrol:
## Çalmakta Olan Sesleri Kontrol Etme:
Şu ana kadar synthleri ve sampleları nasıl tetikleyebileceğinizi öğrendik ve ayrıca bu seslerin amplitude, pan, envelope gibi ayarlarını nasıl değiştireceğimizi gördük. Tetiklenen her ses çaldığı süre boyunca kendine özgü sesine ve ayarlarına sahiptir.

Peki ya ses çalarken özelliklerini değiştirebilseydiniz? Tıpkı bir gitarın teline vurduktan sonra tel hala titreşirken teli sıkıştırmak gibi. Çok havalı olmaz mıydı? 

Çok şanslısın – bu kısım sana tam olarak bunu nasıl yapacağını öğretecek.

## 7.1 Çalmakta Olan Synthleri Kontrol Etme:
Şu ana kadar yalnızca yeni sesler ve FX’ler tetiklemekle ilgilendik. Ancak, Sonic Pi bize halihazırda çalmakta olan sesleri manipüle ve kontrol etme imkânı sunar. Bunu bir synthe karşılık gelecek bir değişken kullanarak yapıyoruz:
```
s = play 60, release: 5
```
Here, we have a run-local variable s which represents the synth playing note 60. Note that this is run-local - you can’t access it from other runs like functions.

Artık “s” değişkenimizi “control” fonksiyonunu kullanarak kontrol edebiliriz:
```
s = play 60, release: 5
sleep 0.5
control s, note : 65
sleep 0.5
control s, note: 67
sleep 0.5
control s, note: 72
```
Sizin de fark edebileceğiniz gibi burada 4 farklı synth tetiklemiyoruz – yalnızca bir synth tetikleyip sonrasında o ses oynarken tonunu 3 kere değiştiriyoruz.

Biz her standart seçeneği “control” fonksiyonuna aktarabiliriz, bu da demek oluyor ki amp:, cutoff:, pan: gibi değerleri de bu fonksiyonu kullanarak çalma esnasında kontrol edebiliriz.

## Konrol Edilemeyen Ayarlar:
Bazı ayarlar synth bir kere başladıktan sonra kontrol edilemez. Bu durum bütün ADSR envelope değişkenleri için geçerlidir. Hangi ayarların değiştirilebildiğine yardım sisteminden ulaşabilirsiniz.

## 7.2 FX’leri Kontrol Etme:
Biraz farklı bir yolla yapılsa da FX’leri de kontrol etmek mümkündür:
```
with_fx :reverb do |r|
  play 50
  sleep 0.5
  control r, mix: 0.7
  play 55
  sleep 1
  control r, mix: 0.9
  sleep 1
  play 62
end
```
Bir değişken kullanmak yerine, burada do/end bloğunu kullanıyoruz. “|” barlarının içine çalmakta olan FX’e karşılık gelen bir isim belirtmeliyiz. Bu ismi do/end bloğumuzun ilerleyen kısımlarında kullanacağız. Bu yaptığımız şey bir önceki bölümde yaptığımızın tamamen aynısı.

Şimdi gidin ve biraz synth ve FX kontrol edin!


	

