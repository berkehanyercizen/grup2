#4 - Rastgeleleştirme
Bazı rasgele sayılar kullanmak müziğinize ilgi eklemeyi sağlayan harika yollardan biridir. Sonic Pi, müziğinize rastgelelik katmak için harika bir işlevselliğe sahiptir. Ancak başlamadan önce şok edici bir gerçeği öğrenmemiz gerekir: Sonic
Pi’de rastgelelik tamamen rastgelelik değildir. Bu ne demek oluyor? Hadi, görelim bakalım.
Tekrarlanabilirlik
Gerçekten kullanışlı bir rastgele işlev olan rrand size iki sayı arasında rastgele bir değer verecektir:bir minimum ve bir maksimum . (rrand belli bir aralıktaki rastgelede kısadır.). Rasgele bir nota çalmayı deneyelim:

play rrand(50, 95)

Rastgele bir nota çaldı. 83.7527 notası çaldı. Bu nota 50 ile 95 arasında rastgele bir notadır. Bekle, ben de tam olarak rastgele bir nota aldığını tahmin ettim mi? Burada şüpheli bir şey oluyor. Kodu tekrar çalıştırmayı deneyin. Ne? Yine 83.7527 yi mi seçti? Bu rastgele olamaz!
Cevap gerçekten rastgele değil, sahte rastgelelik. Sonic Pi, tekrarlanabilir bir şekilde rasgele benzeri sayılar verecektir. Makinenizde oluşturduğunuz müziğin kompozisyonunuzda biraz rastgelelik kullansanız bile, herkesin makinesinde aynı gibi görünmesini sağlamak için çok
kullanışlıdır.
Elbette, belirli bir müzik parçasında, 83.7527 her seferinde 'rastgele' seçerse o zaman çok ilginç olmaz. Ancak, öyle değil. Aşağıdaki örneğe göz at:

loop do
play rrand(50, 95) sleep 0.5
end

Evet! Sonunda rastgele geliyor. Belirli bir run içinde rastgele işlevlere yapılan sonraki çağrılar rastgele değerler döndürür. Bununla birlikte, bir sonraki çalıştırma tamamen aynı rasgele değerler dizisini üretecek ve tamamen aynı şekilde ses çıkaracaktır. Sanki tüm Sonic Pi kodları, Run
 düğmesine her basıldığında tam olarak aynı noktaya geri döndü. Groundhog Müzik sentezi günü!
##Perili Çanlar
Eylemdeki randomizasyonun güzel bir örneği :perc_bell çan sesleri arasında rastgele bir hız ve uyku süresi ile örneği dolaştıran perili çan örneğidir :

loop do
sample :perc_bell, rate: (rrand 0.125, 1.5) sleep rrand(0.2, 2)
end


 ##Rastgele kesme
 Başka bir eğlenceli randomizasyon örneği de bir sentezin kesmesini rastgele değiştirmektir. Bunu denemek için harika bir örnek:tb303

loop do
play 50, release: 0.1, cutoff: rrand(60, 120) sleep 0.125
end

##Rastgele tohumlar
 Peki, Sonic Pi'nin sağladığı bu rasgele sayılar dizisini sevmiyorsanız ne olacak? Üzerinden farklı bir başlangıç noktası seçmek tamamen mümkün :use_random_seed. Varsayılan tohum 0 olur. Farklı bir rastgele deneyim için farklı bir tohum seçebilirsiniz.
Aşağıdakileri göz önünde bulundur:

5.times do
play rrand(50, 100) sleep 0.5
end

 Bu kodu her çalıştırdığınızda, aynı 5 nota dizisini duyacaksınız. Farklı bir dizi elde etmek için sadece tohumu değiştirin:

use_random_seed 40 5.times do
play rrand(50, 100)
sleep 0.5 end

 Bu, 5 notadan oluşan farklı bir sekans üretecektir. Tohumu değiştirerek ve sonuçları dinleyerek sevdiğiniz bir şeyi bulabilirsiniz. Başkalarıyla
 paylaştığınızda, tam olarak ne duyduğunuzu duyacaklar. Diğer yararlı rastgele işlevlere bir göz atalım.

##Seçmek
 Yapılacak çok yaygın bir şey, bilinen öğelerin listesinden rastgele bir öğe seçmektir. Örneğin, aşağıdakilerden bir nota çalmak isteyebilirim: 60, 65 veya 72. Bir listeden bir öğe seçmeme izin veren choose ile bunu başarabilirim. Öncelikle, sayılarımı köşeli parantez içine alarak ve virgüllerle ayırarak yapılan bir listeye koymam gerekiyor [60, 65, 72]. Sonra sadece onları seçmek için choose u kullan:

Bunun neye benzediğini duyalım:
choose ([60, 65, 72])
loop do
play choose([60, 65, 72]) sleep 1
end
 

##rrand
 Daha önce rrand ı gördük, ama hadi tekrar deneyelim. Sadece iki değer arasında rastgele bir sayı döndürür. Bu, asla üst veya alt sayıyı döndürmeyeceği anlamına gelir. Her zaman bu ikisi arasında bir

 şeydir. Sayı daima bir virgüllü sayı olacak - yani bir tam sayı değil. Döndürülen örnekler: rrand(20, 110):
 - 87,5054931640625 
 -86,05255126953125 
 -61,77825927734375
 
 ##rrand_i
 Bazen, rastgele bir tam sayı isteyeceksiniz, virgüllü sayı değil. Tam bu noktada rrand_i yardımınıza geliyor. rrand minimum ve maximum
 değerlerini potansiyel rastgele değerler olarak döndürebilmesi haricinde benzer şekilde çalışır (aralığın dışında olmaktan ziyade kapsayıcı anlamına gelir). Tarafından döndürülen sayı
örnekleri rrand_i(20, 110):
 - 88 
 -86 
 - 62
 
 ##Rand
 Bu, 0 (dahil) ile belirttiğiniz maksimum değer (özel) arasında rastgele bir değişken döndürür. Varsayılan olarak 0 ile bir arasında bir değer döndürür. Bu nedenle amp rastgele değerler seçmek için kullanışlıdır :
loop do
play 60, amp: rand sleep 0.25
end

##rand_i
 rrand_ive rrand arasındaki ilişkiye benzer , rand_i,0 ile belirttiğiniz maksimum değer arasında rastgele bir tam sayı döndürür.
 
 ##Dice
 Bazen bir zar atışını taklit etmek istersiniz. Bu rrand_i nin değerin her zaman 1 olduğu özel bir durumudur. Bir dice kullanımı, zardaki taraf sayısını belirlemenizi gerektirir. Standart bir zarın 6 tarafı
vardır. dice(6) buna çok benzer davranır - 1, 2, 3, 4, 5 veya 6

değerlerini döndürürler. Ancak değerleri 12 taraflı bir zar veya 20 taraflı bir zar belki de 120 taraflı bir zar gibi bulabilirsiniz.

##one_in
Son olarak, standart bir zardaki 6 gibi bir zarın en yüksek puanını atmaya benzetebilirsiniz.
Bu nedenle 6'da 1'lik bir olasılıkla doğru, aksi takdirde yanlış olarak geri döner. Doğru ve yanlış değerler, bu yazının sonraki bir bölümünde ele alacağımız if li ifadeler için çok kullanışlıdır.
Şimdi git ve kodunu biraz rastgelelikle karıştır!
