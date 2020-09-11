---
layout: post
title: Video including closed captions, method 2
date: 2020-09-11
# description: 
img: Screenshot-2020-09-11-at-06.59.34.png
fig-caption: Screenshot
fig-attrib: Nick Hood
published: yes
tags:
- Education
- Digital Literacy
- Video
- Closed Caption
- OSX
- Transcription

# permalink:
---
Further to [this recent post](/video-cc-workflow) on capturing, processing and captioning video, my colleague, Dr. Audrey Cameron, advised me to try YouTube for capturing the `.srt` captions file more quickly. I am thankful to her for this, because although I was aware of YouTube's rapidly improving automatic captioning (I use it myself when I watch with sound off, for example), I didn't know that the `.srt` file can be downloaded. Here's a revised approach I am using today.

## Capturing the video and audio

For capturing an old-fashioned lecture-style talk using [KeyNote](https://www.apple.com/uk/keynote/), I use the facility to record a presentation (from the Play menu). The presentation can be exported as a `.m4v` video file with sound. **At the same time** as recording the presentation in KeyNote, I also record myself on my [Fuji X-T2 camera](https://fujifilm-x.com/global/products/cameras/x-t2/) and capture a high quality audio track separately on a [Zoom H-1](https://www.zoom.co.jp/products/handy-recorder/h1-handy-recorder) recorder. A "pro" tip to is to clap just before you start presenting -- it leaves a nice spike in the audio waveforms, making it easy to line up the separate tracks. You can also pretend to be Steven Spielberg or Alfred Hitchcock, according to your *genre*, by saying, "Action!" at the same time.

## Processing 

Import the video and audio tracks into [iMovie](https://www.apple.com/uk/imovie/), align them using the spike from your clap, and check that the audio is the same length as in the video track of the speaker. I found that for longer videos, over 15 minutes, they can be different. This difference produces an echo effect, eventually separating the video from the soundtrack, like a Swedish movie. Adjusting the audio to align properly can easily be done in iMovie using the speed adjustment. Once the clips are aligned, you can turn the audio level of the video clips down to zero, so only the high quality track remains.

The next thing I do is to change the video track of the presenter to "Picture in picture", so viewers can see me presenting within the slides: I think this is a bit of a substitute for one of the features I miss from live presenting, which is managing the attention of the viewer. I normally do this by blanking the display, which has the effect of moving the eyes in the room from the screen to my face -- a powerful way to add contrast to your talk. This "mini me" within the slides can be faded in or out, according to what you want the students to focus on at any point. Other effects are possible, like switching to embedding the presentation within the presenter video.

![](/assets/img/Screenshot 2020-09-11 at 07.53.03.png)

The finished project can be exported via the Share menu to a `.mp4` file.

## Getting the transcript 

The video can be uploaded to YouTube now: you'll need a verified account to upload clips longer than 15 minutes, which means giving Google your phone number. I baulked at this at first, but expedient is the slayer of principle, and in this case, privacy. Make sure you click "Private" when saving the clip. These lectures are not for public consumption.

![](/assets/img/Screenshot 2020-09-11 at 07.23.47.png)

After a while -- maybe 30 minutes, depending on the length of your video -- the automatically-generated captions file can be edited using a really nice editing interface in [YouTube Studio](https://studio.youtube.com/) designed for the purpose. You will need to add punctuation and if you wish, add comments to your own commentary. Once that has been done, the `.srt` file is ready to download.

## Media Hopper Create

Your video can now be used within your local VLE, in my case, Blackboard Learn, by uploading via the media manager, [Media Hopper](https://media.ed.ac.uk/). Once uploaded, you can then add closed captions by uploading the `.srt` file alongside it. Students then have a choice whether to access captions within the video sequences or not.

### Another Hitch
I was about to post this, all smug, like, as I uploaded the latest video made with this method, when I hit a "file too large" error when uploading to Media Hopper. The video I had made was just short of 18 minutes and had a file size of 1.2GB. Now, mp4 is an efficient container format so I maybe made too many "best quality" choices in making the video: high definition 1080p for the presenter, same for the KeyNote. Rather than go back and do it all again, I resorted to ffmpeg to make me a reduced bitrate version. I thought halving the bitrate might produce a file half the size.

```sh
$ ffmpeg -i mybigvideo.mp4 	# find out what the current bitrate is..
...
  Duration: 00:17:28.55, start: 0.000000, bitrate: 9978 kb/s
...
$ ffmpeg -i mybigvideo.mp4 -b 4489k mysmallervideo.mp4
```
This made (after thrashing my 5-year old MacBook Air for about 25 minutes) a file -- as hoped for -- half the size (673 MB).

## Deployment to a website

To use the video and captions file together within a webpage is straightfroward, except that the captions need to be in a different format. This format is **Web Video Text Tracks (VTT)**, and is easily obtained using ffmpeg:

```sh
$ ffmpeg -i srtfile.srt subtitlefile.vtt
```

The web page needs the following code (adapted to your own file paths, obviously):

```html
<p>  
<video width="640" height="360" controls="controls">
	<source src="https://www.learn.ed.ac.uk/path-to-video.mp4" type="video/mp4">  
	<track src="https://www.learn.ed.ac.uk/path-to-vtt-file.vtt" kind="captions" srclang="en" label="English" default>
	Your browser does not support the video tag.
</video>
</p>
```

## Conclusion
Video production for 'digital first' teaching strategies needed in response to COVID-19 measures or similar, is a non-trivial task. Including closed captions is an additional time multiplier. Personally, I don't like asynchronous teaching at all: it misses so many important aspects of good pedagogy, aspects which are easily ignored by administrators of education in the pursuit of apparent economies or easy fixes. I am at ease, however, with an established workflow.

I am thankful to my colleague, Audrey, for her patience and support in helping me get to this solution. We both have a lot of videos to make, and now it will not take me as long as it might have done.

<!--## Footnotes-->
