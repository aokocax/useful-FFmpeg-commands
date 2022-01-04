<h1>Useful FFmpeg commands</h1>

<a href="https://github.com/aokocax/useful-FFmpeg-commands/blob/main/readme.TR.md">Turkish</a>

The use of video in digital life is increasing exponentially day by day.
I prepared a document explaining how you can easily find answers to video solutions/problems that you will need in daily life with FFmpeg library.
I show you which commands to run for video solutions you will need with about 20 different scenarios in the file. 

Download FFmpeg to your computer for Windows => https://github.com/BtbN/FFmpeg-Builds/releases for Mac Os => https://evermeet.cx/ffmpeg/ After downloading from .cx/ffmpeg/ffmpeg-105012-gbb813ccb45.zip addresses, you can run ffmpeg as arguments by entering bin folder via terminal.

<ol>
  <li><h2>Convert any video format to other format.</h2> </li>

`ffmpeg -i source.avi  output.mp4`

`ffmpeg -i source.mov output.mp4`

<li><h2>Increasing/decreasing the framerate of the video. (Twitter and some platforms require 30FPS video)</h2> </li>

`ffmpeg -i source.mp4 -framerate 30 output30fps.mp4`

 <li><h2>Adding audio to video.</h2></li>
 
 > It will be as long as the video or audio, whichever is shorter.
  
`ffmpeg -i source.mp4 -i sound.mp3  -vcodec copy -map 0:v -map 1:a -map 1:a -shortest output.mp4`
  

<li><h2>Cutting the first three seconds of the video.</li></h2>
  
`ffmpeg -i source.mp4 -t 3 output3seconds.mp4`
  
> or 

`ffmpeg -i source.mp4 -t 00:00:03 output3seconds.mp4`

<li><h2>Cut a specific range of video.</li></h2>
  
> Getting next 3 seconds starting from 3 seconds

`ffmpeg -i source.mp4 -ss 3 -t 3 source3seconds.mp4`

<li><h2>Cut video from a specific second to the end of the video</li></h2>

`ffmpeg -i source.mp4 -ss 3 output3seconds.mp4`

`ffmpeg -i source.mp4 -ss 00:00:03 output3seconds.mp4`


<li><h2>Convert video to animated gif.</h2></li>

`ffmpeg -i source.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif`


<li><h2>Converting part of video to animated gif.</h2></li>
  
`ffmpeg -i source.mp4 -ss 1 -t2 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 tar.gif`

<li><h2>Concat two videos (without audio).</h2></li>
  
`ffmpeg -i source1.mp4 -i source2.mp4 -y -filter_complex "[0:v][1:v] concat=n=2:v=1:[v]" -map "[v]" output.mp4`

<li><h2> Concat two videos back-to-back (with audio).</h2></li>

`ffmpeg -i source1.mp4 -i source2.mp4 -y  -filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0] concat=n=2:v=1:a=1 [v] [a]" -map "[a]" -map "[v]" output.mp4`

<li><h2>Adding a watermark to the middle of the screen.</h2></li>
  
`ffmpeg -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 `

<li><h2>Adding a watermark to a specific point of the screen.</h2> </li>
  
`ffmpeg -i source.mp4 -i logo.png -filter_complex "overlay = (main_w - overlay_w)/2:(main_h - overlay_h) / 2" watermark.mp4 `

<li><h2>Extracting all the frames in the video as an image</h2> </li>
  
`ffmpeg -i source.mp4  "%04d.png"`

<li><h2>Take a screenshot of a specific frame in the video.</h2> </li>
  
`ffmpeg -i wm.mp4 -ss 00:00:01.23 -vframes 1 -q:v 2 output.jpg`

<li><h2>Take a screenshot from every 1 second of the video</h2> </li>
  
`ffmpeg -i wm.mp4 -r 1  -f image2 screenshot-%03d.jpg`

<li><h2>Merging two separate audio files.</h2> </li>
  
`ffmpeg -i sound1.wav -i sound2.wav -filter_complex "[0:0][1:0]concat=n=2:v=0:a=1[out]" -map "[out]" soundconcat.wav`

<li><h2>Extracting the audio file from the video as mp3.</h2></li>

`ffmpeg -i source.mp4 output.mp3`

<li><h2>To mute the video.</h2></li>

`ffmpeg -i source.mp4 -c copy -an sessiz.mp4`

<li><h2>Making video from photo gallery.</h2></li>

`ffmpeg -f concat -i filelist.txt -i audio.mp3 -c:a copy output.mp4`

filelist.txt sample file
<pre>
a1.jpg
a2.jpg
a3.jpg
</pre>
<li><h2>Writing text on the video with the desired font.</h2></li>

`ffmpeg -i source.mp4  -filter:v "drawtext=enable='between(t,0,2)':fontsize=30:fontfile=font.otf:fontcolor=yellow:text='my text':x = (w - text_w) / 2:y = (h - text_h - line_h) / 2" output.mp4`

> between(t,0,2) 0-2 seconds
 
> center the screen x = (w - text_w) / 2:y = (h - text_h - line_h) / 2

> You can make it output in the position you want by giving x and y values.
</ol>
