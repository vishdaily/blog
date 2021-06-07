---
id: 607
title: Video Or Audio Format Conversion Using ffmpeg
date: 2018-10-07T17:37:41+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=607
permalink: /index.php/computers/bash-scripting/video-audio-format-conversion-using-ffmpeg/
categories:
  - bash-scripting
tags:
  - audio-video
---

Recommended resolution & aspect ratios
For the default 16:9 aspect ratio, encode at these resolutions:

```bash
2160p: 3840x2160
1440p: 2560x1440
1080p: 1920x1080
720p: 1280x720
480p: 854x480
360p: 640x360
240p: 426x240
```

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


# cut mp3 from hh:mm:ss to hh:mm:ss
ffmpeg -ss 00:00:14 -t 00:04:04 -i "input.mp3" -acodec copy outputfile.mp3

# to cut a part of the video
## output cut video re-encoded
ffmpeg -i input.mp4 -ss 1:12 -t 2:50 output-cut-reencoded.mp4
## output cut video streams just copied
ffmpeg -i input.mp4 -c:v copy -c:a copy -ss 1:12 -t 2:50 output-cut.mp4
# working
ffmpeg -i "input.mp4" -ss 29:30 -to 01:31:20 -codec copy "output.mp4"


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


# Change resolution of video file
ffmpeg -i input.mp4 -filter:v scale=1280:720 -c:a copy output.mp4 OR
ffmpeg -i input.mp4 -s 1280x720 -c:a copy output.mp4
ffmpeg -i input.mp4 -filter:v scale=640:480 -c:a copy output.mp4 OR
ffmpeg -i input.mp4 -s 640x480 -c:a copy output.mp4
ffmpeg -i test.mp4 -filter:v scale=640x480 -c:a copy test1.mp4
# Convert video to audio
ffmpeg -i input.mp4 -vn -ab 320 output.mp3
ffmpeg -i input.webm -qscale 0 output.mp4
# compress video file
ffmpeg -i input.mp4 -vf scale=1280:-1 -c:v libx264 -preset veryslow -crf 24 output.mp4

Please note that you will lose the quality if you try to reduce the video file size. You can lower that crf value to 23 or lower if 24 is too aggressive.
You could also transcode the audio down a bit and make it stereo to reduce the size by including the following options.

-ac 2 -c:a aac -strict -2 -b:a 128k
# Removing audio stream from a media file
ffmpeg -i input.mp4 -an output.mp4
# Extracting images from the video
ffmpeg -i input.mp4 -r 1 -f image2 image-%2d.png
# convert the first 50 seconds of given video.mp4 file to video.avi format
ffmpeg -i input.mp4  -t 50 output.avi 
# Set the aspect ratio to video
ffmpeg -i input.mp4 -aspect 16:9 output.mp4
# Trim a media file using start and stop times
ffmpeg -i audio.mp3 -ss 00:01:54 -to 00:06:53 -c copy output.mp3
ffmpeg -i input.mp4 -ss 00:00:50 -codec copy -t 50 output.mp4
ffmpeg -i st.mp4 -s 00:00:00 -to 00:58:40 -codec copy st_output.mp4
# to cut media from middle to somewhere -to isn't working but -t is..
ffmpeg -i "input.mp4" -ss 37:00 -t 01:16:00 -codec copy "output.mp4"
# join files
ffmpeg -f concat -i join.txt -c copy output.mp4
fmpeg -i input.mp4 -i subtitle.srt -map 0 -map 1 -c copy -c:v libx264 -crf 23 -preset veryfast output.mp4
# map audio coming from left to both left and right
ffmpeg -i "input.mp4" -map_channel 0.1.0 -maap_channel 0.1.0 output.mp4
# convert part of video to different output
ffmpeg -i input.mp4  -t 50 output.avi

https://unix.stackexchange.com/questions/28803/how-can-i-reduce-a-videos-size-with-ffmpeg

ffmpeg -i $infile -vf "scale=iw/2:ih/2" $outfile 

# The command to just stream it to a new container (mp4) needed by some applications like Adobe Premiere Pro without encoding (fast) is:
ffmpeg -i input.mov -qscale 0 output.mp4

# Alternative as mentioned in the comments, which re-encodes with best quaility (-qscale 0):
ffmpeg -i input.mov -q:v 0 output.mp4

# Reduce size by reducing size of the video
ffmpeg -i IMG_0709.MOV -filter:v scale=720:-1 -c:a copy IMG_0709.mp4

# Sometimes i had problems with the above command  where it was complaining about 
# maybe incorrect parameters such as bit_rate, rate, width or height
# as the recording (since they were recorced as screen recording) width and hight were wierd width=750, height=1334 
ffmpeg -i RPReplay_Final1610878476_compress.MP4 -vf scale=-1:1280 -acodec copy -threads 12 output/RPReplay_Final1610878476_compress.MP4
```


## script to reduce file size of the video files given the path and the regex


```bash
#!/bin/bash
# ./reduce_video_size.sh ~/Pictures/personal_photos_processing/vedith/ "*.mov" ~/Pictures/personal_photos_processing/vedith/output/ 1280 720 mp4

SOURCE_DIR="$1"
NAME_FILTER="$2"
OUTPUT_DIR="$3"
TARGET_WIDTH="$4"
TARGET_HEIGHT="$5"
OUTPUT_FILE_FORMAT="$6"

if [ $# -ne 6 ]; then
echo "number of params passed $#"
echo "pass all required params"
echo "$0 SOURCE_DIR NAME_FILTER(*.mp4) OUTPUT_DIR TARGET_WIDTH(1280) TARGET_HEIGHT(720) OUTPUT_FILE_FORMAT(mp4)"
exit 1
fi

if [ ! -d "$SOURCE_DIR" ]; then
	echo "source_dir $SOURCE_DIR doesnt exist"
	exit 1
fi

find "$SOURCE_DIR" -iname "$NAME_FILTER" -print | while read -r line; do
echo "processing"
du -h "$line"
W=$( ffprobe "$line" -show_streams 2>1 | grep -E '^width=' )
W=${W#width=}

H=$( ffprobe "$line" -show_streams 2>1 | grep -E '^height=' )
H=${H#height=}
echo "width=$H - height=$W"
DURATION=$( ffprobe "$line" -show_streams 2>1 | grep -E '^duration=' | head -n 1  )
DURATION=${DURATION#duration=}
echo "duration = $DURATION seconds which is around $(echo "($DURATION/60)" | bc) minute(s)"

# Target a 1920x1080 output video.
TARGETW=1280
TARGETH=720

if [ $(( $W * $TARGETH )) -gt $(( $H * $TARGETW )) ]; then
    # The width is larger, use that
    SCALEPARAM="scale=-1:$TARGETW"
else
    # The height is larger, use that
    SCALEPARAM="scale=$TARGETH:-1"
fi

OUTPUT_FILE_NAME="$(basename "$line")"
OUTPUT_PATH="${OUTPUT_DIR}/${OUTPUT_FILE_NAME}.${OUTPUT_FILE_FORMAT}"
echo ffmpeg -i $line -vf $SCALEPARAM $OUTPUT_PATH

done
```