---
id: 607
title: Video Or Audio Format Conversion Using ffmpeg
date: 2018-10-07T17:37:41+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=607
permalink: /index.php/computers/bash-scripting/video-audio-format-conversion-using-ffmpeg/
categories:
  - Bash Scripting
tags:
  - audio video conversion
---
```bash
# get file info
ffmpeg -i input.mp4

# mkv -> mp3
 ffmpeg -i "movie.mkv" -vn -c:a libmp3lame -y "sound.mp3"

 # cut video from hh:mm:ss.0 -> +t 2064 seconds 
# from 22 minutes to 54.40 minutes which is 22 minutes + 2064 seconds (34.40 minutes)
 ffmpeg -ss 00:22:00.0 -i input.mp4 -c copy -t 2064  output.mp4

# Split mp3 in to parts where each part is 60 minutes (3600 seconds) file name as out000.mp3, out001.mp3, out002.mp3 etc
ffmpeg -i 2019_09_24_09_22_44.mp3 -f segment -segment_time 3600 -c copy out%03d.mp3

# to cut a part of the video
## output cut video re-encoded
ffmpeg -i input.mp4 -ss 1:12 -t 2:50 output-cut-reencoded.mp4
## output cut video streams just copied
ffmpeg -i input.mp4 -c:v copy -c:a copy -ss 1:12 -t 2:50 output-cut.mp4

# input-list contails files to be appended. one file per line.
ffmpeg -f concat -i input-list.txt -c copy tank-mix.mp4

# Extract audio
ffmpeg -i input.ogv -vn -acodec libmp3lame -ar 44100 -b:a 96k output.mp3

# rotate the video or transpose the video. transpose=1 means 90 degrees. transpose=2 (90x2 = 180)
ffmpeg -i tank.mp4 -vf transpose=1output-video-rotated.mp4

# resize video
ffmpeg -i input.mp4 -vf scale=320:240 output.mp4

# add audio to video
ffmpeg -i sound.wav -i original_video.avi final_video.mpg

# subtitles to video
ffmpeg -i input.mp4 -i subtitles.srt -c copy -c:s mov_text output.mp4

# add an image to video
ffmpeg -i input.mp4 -i image.png -filter_complex "[0:v][1:v] overlay=25:25:enable='between(t,0,20)'" -pix_fmt yuv420p -c:a copy output.mp4

# crop: out_w = width of output, out_h = height of output, x:y specifies top left corner
ffmpeg -i input.mp4 -filter:v "crop=out_w:out_h:x:y" output.mp4

# resize image
ffmpeg -i input.jpg -vf scale=320:240 output_320x240.png

# images to video
ffmpeg -f image2 -i input%d.jpg output.mpg

# video to images
ffmpeg -i input.mpg output%d.jpg


```