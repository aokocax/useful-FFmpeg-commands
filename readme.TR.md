<a href="https://github.com/aokocax/useful-FFmpeg-commands/blob/main/README.md">=>English</a>

Bant genişliklerinin artmasıyla dijital hayatta video kullanımı her geçen gün katlanarak artıyor. Ücretsiz FFmpeg programı ve kütüphanelerini kullanarak gündelik hayatta sıkça ihtiyaç duyacağınız video çözümlerine/sorunlarına bu kütüphane ile nasıl kolaylıkla cevap bulacağınızı anlatan bir doküman hazırladım. Dosyada 20 kadar farklı senaryo ile ihtiyaç duyacağınız video çözümleri için hangi komutları çalıştırmanız gerektiğini gösteriyorum. Doküman hakkındaki soru/sorularınızı Issues bölümünden iletebilirsiniz.

FFmpeg programını bilgisayarınıza
Windows için => https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-latest-win64-gpl-shared-4.4.zip 
Mac Os için => https://evermeet.cx/ffmpeg/ffmpeg-105012-gbb813ccb45.zip
Adreslerinden indirdikten sonra terminal üzerinden bin klasörüne girerek `ffmpeg argümanlar` şeklinde çalıştırabilirsiniz

<ol>
  <li><h2>Herhangi bir video formatını diğer formata çevirmek.</h2> </li>

`ffmpeg -i source.avi  output.mp4`

`ffmpeg -i source.mov output.mp4`

<li><h2>Videonun framerate'ini arttırma/azaltmak. (Twitter ve bazı platformlar 30FPS video istemekteler)</h2> </li>

`ffmpeg -i source.mp4 -framerate 30 output30fps.mp4`

 <li><h2> Videoya ses eklemek.</h2></li>
 
 > Video veya görüntüden kısa olanın süresinde video biter.
  
`ffmpeg -i source.mp4 -i sound.mp3  -vcodec copy -map 0:v -map 1:a -map 1:a -shortest output.mp4`
  

<li><h2> Videonun ilk üç saniyesini almak/kesmek.</li></h2>
  
`ffmpeg -i source.mp4 -t 3 output3seconds.mp4`
  
> ya da 

`ffmpeg -i source.mp4 -t 00:00:03 output3seconds.mp4`

<li><h2> Videonun belirli bir aralığını almak.</li></h2>
  
> 3. saniyeden başlayarak sonraki 3 saniye alınıyor

`ffmpeg -i source.mp4 -ss 3 -t 3 source3seconds.mp4`

<li><h2>  Belirli bir saniyeden videonun sonuna kadar videoyu kesmek.</li></h2>

`ffmpeg -i source.mp4 -ss 3 output3seconds.mp4`

`ffmpeg -i source.mp4 -ss 00:00:03 output3seconds.mp4`


<li><h2> Videoyu animasyonlu gife çevirmek.</h2></li>

`ffmpeg -i source.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif`

> fps saniyelik frame sayısını belirtir scale ile çözünürlük belirtebilirsiniz
  
> loop tekrar sayısını belirtir

<li><h2>Videonun bir bölümünü animasyonlu gife çevirmek.</h2></li>
  
`ffmpeg -i source.mp4 -ss 1 -t2 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 tar.gif`

<li><h2>İki videoyu arka arkaya eklemek (audiosuz).</h2></li>
  
`ffmpeg -i source1.mp4 -i source2.mp4 -y -filter_complex "[0:v][1:v] concat=n=2:v=1:[v]" -map "[v]" output.mp4`

<li><h2> İki videoyu arka arkaya eklemek (audio ile).</h2></li>

`ffmpeg -i source1.mp4 -i source2.mp4 -y  -filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0] concat=n=2:v=1:a=1 [v] [a]" -map "[a]" -map "[v]" output.mp4`

<li><h2>Ekran ortasına watermark filigran eklemek.</h2></li>
  
`ffmpeg -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 `

<li><h2> Ekranın belirli bir noktasına watermark filigran eklemek.</h2> </li>
  
`ffmpeg -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 `

<li><h2> Videodaki tüm frameleri resim olarak çıkarma</h2> </li>
  
`ffmpeg -i source.mp4  "%04d.png"`

<li><h2> Videodaki belirli bir karenin ekran görüntüsünü almak.</h2> </li>
  
`ffmpeg -i wm.mp4 -ss 00:00:01.23 -vframes 1 -q:v 2 output.jpg`

<li><h2> Videodaki her 1 saniyeden ekran görüntüsü çıkarmak</h2> </li>
  
`ffmpeg -i wm.mp4 -r 1  -f image2 screenshot-%03d.jpg`

<li><h2> İki ayrı ses dosyasını birleştirmek.</h2> </li>
  
`ffmpeg -i sound1.wav -i sound2.wav -filter_complex "[0:0][1:0]concat=n=2:v=0:a=1[out]" -map "[out]" soundconcat.wav`

<li><h2> Videodaki ses dosyasını mp3 olarak çıkarmak.</h2></li>

`ffmpeg -i source.mp4 output.mp3`

<li><h2> Videoyu sessiz hale getirmek.</h2></li>

`ffmpeg -i source.mp4 -c copy -an sessiz.mp4`

<li><h2> Fotoğraf galerisinden video yapmak. </h2></li>

`ffmpeg -f concat -i filelist.txt -i audio.mp3 -c:a copy output.mp4`

filelist.txt örneği
<pre>
a1.jpg
a2.jpg
a3.jpg
</pre>
<li><h2>Video üzerine istenilen yazı fontu ile yazı yazmak.</h2></li>

`ffmpeg -i source.mp4  -filter:v "drawtext=enable='between(t,0,2)':fontsize=30:fontfile=font.otf:fontcolor=yellow:text='my text':x = (w - text_w) / 2:y = (h - text_h - line_h) / 2" output.mp4`

> between(t,0,2) 0-2 saniye arasında gözüküyor
 
> ekranı ortalıyoruz x = (w - text_w) / 2:y = (h - text_h - line_h) / 2

> x ve y değeri vererek istediğiniz pozisyonda çıkmasını sağlayabilirsiniz.

<li><h2>Videoyu segmentlere ayırma</h2></li>

`ffmpeg -i input.mp4  -c copy -map 0 -segment_time 4 -f segment -segment_list list.txt output_video%03d.mp4`

<li><h2>Segmentlere ayrılmış videoyu birleştirme</h2></li>

`ffmpeg -y -v error -i list.txt -map 0 -c copy output.mp4`
</ol>
