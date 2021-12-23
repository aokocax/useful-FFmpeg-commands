<b>Türkçe</b>

Herhangi bir video formatını diğer formata çevirme. 

ffmpeg -i source.avi  source.mp4

ffmpeg -i source.mov source.mp4

Videonun framerate'ini arttırma/azaltmak (Twitter ve bazı platformlar 30FPS video istemekteler)

ffmpeg -i source.mp4 -framerate 30 source30fps.mp4

Videoyu kısaltmak

İlk üç saniyesini almak
ffmpeg -i source.mp4 -t 3 source3seconds.mp4
ya da 
ffmpeg -i source.mp4 -t 00:00:03 source3seconds.mp4

Videonun belirli bir aralığını almak
3. saniyeden başlayarak sonraki 3 saniye alınıyor
ffmpeg ffmpeg -i source.mp4 -ss 3 -t 3 source3seconds.mp4
Belirli bir saniyeden videonun sonuna kadar videoyu kesmek

ffmpeg ffmpeg -i source.mp4 -ss 3 source3seconds.mp4




