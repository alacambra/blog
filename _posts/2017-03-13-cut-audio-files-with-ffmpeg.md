---
ID: 88
post_title: cut audio files with ffmpeg
author: alacambra
post_date: 2017-03-13 19:38:27
post_excerpt: ""
layout: post
permalink: >
  http://blog.lacambra.de/wordpress/2017/03/13/cut-audio-files-with-ffmpeg/
published: true
---
To create an mp3 file of the first 30s of an existent mp3 file, just use the following command.

ffmpeg -t 30 -i inputfile.mp3 -acodec copy outputfile.mp3

In case the original format is not mp3 you can use instead

ffmpeg -t 30 -i inputfile.webm -acodec libmp3lame -aq 4  outputfile.mp3