<b>Türkçe</b>
<ol>
  <li><h2>Herhangi bir video formatını diğer formata çevirme.</h2> </li>

`ffmpeg -i source.avi  output.mp4`

`ffmpeg -i source.mov output.mp4`

<li><h2>Videonun framerate'ini arttırma/azaltmak. (Twitter ve bazı platformlar 30FPS video istemekteler)</h2> </li>

`ffmpeg -i source.mp4 -framerate 30 output30fps.mp4`

<li><h2> Videoyu kısaltmak.</h2></li>

<ul><li><h3> İlk üç saniyesini almak.</h3></li></ul>
`ffmpeg -i source.mp4 -t 3 output3seconds.mp4`
> ya da 

`ffmpeg -i source.mp4 -t 00:00:03 output3seconds.mp4`

<ul><li><h3> Videonun belirli bir aralığını almak.</h3></li></ul>
> 3. saniyeden başlayarak sonraki 3 saniye alınıyor

`ffmpeg ffmpeg -i source.mp4 -ss 3 -t 3 source3seconds.mp4`

<ul><li><h3>  Belirli bir saniyeden videonun sonuna kadar videoyu kesmek.</h3></li></ul>

`ffmpeg ffmpeg -i source.mp4 -ss 3 output3seconds.mp4`

`ffmpeg ffmpeg -i source.mp4 -ss 00:00:03 output3seconds.mp4`

<li><h2> İki videoyu arka arkaya eklemek.</h2></li>


<li><h2> Videoyu animasyonu gife çevirme.</h2></li>

`ffmpeg -i source.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif`

> fps saniyelik frame sayısını belirtir scale ile çözünürlük belirtebilirsiniz
> loop tekrar sayısını belirtir

<li><h2>Videonun bir bölümünü animasyonlu gife çevirme</h2></li>
  
`ffmpeg -i source.mp4 -ss 1 -t2 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 tar.gif`

<li><h2>İki videoyu arka arkaya ekleme (audiosuz)</h2></li>
`ffmpeg -i source1.mp4 -i source2.mp4 -y -filter_complex "[0:v][1:v] concat=n=2:v=1:[v]" -map "[v]" output.mp4`

<li><h2> İki videoyu arka arkaya ekleme (audio ile)</h2></li>

'ffmpeg -i source1.mp4 -i source2.mp4 -y  -filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0] concat=n=2:v=1:a=1 [v] [a]" -map "[a]" -map "[v]" output.mp4'


<li><h2>Ekran ortasına watermark filigran ekleme</h2></li>
`ffmpeg.exe -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 `

<li><h2> Ekranın belirli bir noktasına watermark filigran ekleme</h2> </li>
`ffmpeg -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 `

<li><h2> Videodaki tüm frameleri resim olarak çıkarma</h2> </li>
`ffmpeg -i source.mp4  "%04d.png"`

<li><h2> Videodaki belirli bir karenin ekran görüntüsünü alma</h2> </li>
`ffmpeg -i wm.mp4 -ss 00:00:01.23 -vframes 1 -q:v 2 output.jpg`

<li><h2> Videodaki her 1 saniyeden ekran görüntüsü çıkarmak</h2> </li>
`ffmpeg.exe -i wm.mp4 -r 1  -f image2 screenshot-%03d.jpg`

<li><h2> İki ayrı ses doyasını birleştirme</h2> </li>
`ffmpeg -i sound1.wav -i sound2.wav -filter_complex "[0:0][1:0]concat=n=2:v=0:a=1[out]" -map "[out]" soundconcat.wav`

</ol>
