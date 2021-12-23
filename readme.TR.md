<b>Türkçe</b>

Herhangi bir video formatını diğer formata çevirme. 

ffmpeg -i source.avi  output.mp4

ffmpeg -i source.mov output.mp4

Videonun framerate'ini arttırma/azaltmak (Twitter ve bazı platformlar 30FPS video istemekteler)

ffmpeg -i source.mp4 -framerate 30 output30fps.mp4

Videoyu kısaltmak

İlk üç saniyesini almak
ffmpeg -i source.mp4 -t 3 output3seconds.mp4
ya da 
ffmpeg -i source.mp4 -t 00:00:03 output3seconds.mp4

Videonun belirli bir aralığını almak
3. saniyeden başlayarak sonraki 3 saniye alınıyor
ffmpeg ffmpeg -i source.mp4 -ss 3 -t 3 source3seconds.mp4
Belirli bir saniyeden videonun sonuna kadar videoyu kesmek

ffmpeg ffmpeg -i source.mp4 -ss 3 output3seconds.mp4
ffmpeg ffmpeg -i source.mp4 -ss 00:00:03 output3seconds.mp4

++İki videoyu arka arkaya eklemek


Videoyu animasyonu gife çevirme
ffmpeg -i source.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif

// fps saniyelik frame sayısını belirtir scale ile çözünürlük belirtebilirsiniz
//loop tekrar sayısını belirtir

Videonun bir bölümünü animasyonlu gife çevirme
ffmpeg -i source.mp4 -ss 1 -t2 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 tar.gif

İki videoyu arka arkaya ekleme //audio'suz
ffmpeg -i source1.mp4 -i source2.mp4 -y -filter_complex "[0:v][1:v] concat=n=2:v=1:[v]" -map "[v]" output.mp4

İki videoyu arka arkaya ekleme //audio ile
<pre>
ffmpeg -i source1.mp4 -i source2.mp4 -y  -filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0] concat=n=2:v=1:a=1 [v] [a]" -map "[a]" -map "[v]" output.mp4
</pre>

Ekran ortasına watermark filigran ekleme
ffmpeg.exe -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 

Ekranın belirli bir noktasına watermark filigran ekleme
ffmpeg -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 

Videodaki tüm frameleri resim olarak çıkarma
ffmpeg -i source.mp4  "%04d.png"

Videodaki belirli bir karenin ekran görüntüsünü alma
ffmpeg -i wm.mp4 -ss 00:00:01.23 -vframes 1 -q:v 2 output.jpg

Videodaki her 1 saniyeden ekran görüntüsü çıkarmak
ffmpeg.exe -i wm.mp4 -r 1  -f image2 screenshot-%03d.jpg

İki ayrı ses doyasını birleştirme
ffmpeg -i sound1.wav -i sound2.wav -filter_complex "[0:0][1:0]concat=n=2:v=0:a=1[out]" -map "[out]" soundconcat.wav
