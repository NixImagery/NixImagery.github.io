---
layout: post
title: Video capture and production including closed captions 
date: 2020-08-30
# description: 
img: Screenshot-2020-08-30.png
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
## Introduction
{:.no_toc}

I am required to produce video resources for my students who are coming to the University very soon, either in person or digitally: our teaching under the COVID adjustments is "digital first". We are also particularly keen to support those students who might require captions on their videos. This isn't just those who might be hearing or visually impaired, it's all students who might like the ability sometimes to have the extra clarity provided by words on the screen that reflect the words spoken by the presenter.

Here's my take on a workflow model to make this work well. There are existing facilities to do this semi-automatically -- uploaded videos can have an automated transcription generated but this takes a lot of time, and requires the creator to go back on subsequent days to hand-edit any errors or make any other adjustments.

I like to do a task and complete it: I like to get it right and take my time over that. Once it's done, I like to move on to the next set of tasks. To that end, here is a way I have found of creating video, with quality captioning for those who need it, and the ability to switch it off for those who find it a distraction.

## Contents
{:.no_toc}

* table of contents 
{:toc}


## Subtitles vs. captions

Subtitles are embedded in DVD movies and the like for languages other than that on the audio. Multiple subtitle tracks can be embedded within a title, or switched off if the audio track is in the native language of the speaker. Captions, on the other hand, are a transcription of dialogue in the video. **Closed captions** are distinguished from **open captions** by being able to be switched off if required. Open captions are often embedded in the video and cannot be turned off. My intention in this workflow is to provide closed captions.

## Capturing the video and audio

I captured my video for the proof-of-concept using a [Fuji X-T2](https://fujifilm-x.com/global/products/cameras/x-t2/) APS-C digital mirrorless camera which takes 1080p (1920 x 1080) video. Although the camera records stereo audio, I prefer to capture audio separately using a [Zoom H-1](https://www.zoom.co.jp/products/handy-recorder/h1-handy-recorder) recorder. The quality is much better, not least because the mic is with the speaker, not the camera.

## Processing 

I import the video and audio tracks into [iMovie](https://www.apple.com/uk/imovie/), trim out the top and tail and make other edits, and remove the embedded audio track captured by the camera. This is replaced with the Zoom audio, which can be a bit of a fiddle to align well with the video. The audio waveform can help here but that depends on the recording environment. Depending on the exposure settings on the camera, you might want to "enhance" the video in iMovie for a contrastier image. Once you have added any title sequences (or credits) and  transitions, export the finished video (via the "share" menu) as an mp4 file.

## Getting the transcript 

Open the mp4 file in Quicktime and export as an audio file, the default m4a format is OK. This file can be uploaded to a blank Word document in Office 365 via the Dictate drop-down menu (select Transcribe). This will do a pretty decent job of turning your dialogue into text.

Save the .docx file and convert it to a plain text format - I prefer markdown, although this isn't necessary provided you can finish up with a plain text file. I do the conversion using pandoc:

```sh
$ pandoc transcript.docx -o transcript.md
```

This file can now be edited, correcting any errors in the transcription and chunking the dialogue to make it show at the right time during the video. This is easily done with the video window open on the desktop next to your editor. You should add section markers and timestamps for subtitles as you go through the video. A minimal example:

```sh
1
00:00:01,00 --> 00:00:01,30
Welcome to my interesting video.
```

Finally, you will need this transcript in the correct format for embedding into the video file. This is a simple matter of changing the filetype to .srt (which is a "SubRip Subtitle" file). 

## Add Closed Captions to the video file

The `ffmpeg` tool is best for this. This tool (and others you might need) can be installed simply using `brew` if it isn't already on your system. I don't propose to detail how to do this, but in essence, it's a matter of typing`$ brew install ffmpeg` in a terminal window. Once you have it, add the captions:

```sh
$ ffmpeg -i videofile.mp4 -i transcriptfile.srt -c:v copy -c:a copy  -c:s mov_text -metadata:s:s:0 language=eng output.mp4
```
The program accepts input files, which are you video and the srt file containing the captions and timings. Video and audio are merely copied to the output file.

## Finished, part one

The video file you have just created is now shareable: users can play it on their machines and opt to switch captioning on or off if they wish. Their computer may choose to control this behaviour automatically if local settings allow it.

I need to distribute this video using resources within the VLE (virtual learning environment, in my case, Blackboard Learn and [Media Hopper](https://media.ed.ac.uk/). This is where it gets sticky.

## Media Hopper Create

It's easy to upload a video to the Blackboard VLE by clicking on `Media Hopper Create` in the `Tools` menu. This is very nice but this process strips out the captions track. Embedding the uploaded video offer no CC option to viewers and no captions are visible. This is clearly a fault in the Media Hopper Create system.

You can ask for subtitles to be created for the uploaded video but this is an automated and low-quality service that isn't really any good. It creates, ironically, a CC track that is inferior to the one included in the uploaded file.

## A workaround

I have found a way of getting around this difficulty: within Learn, add a new item. This is effectively a webpage, and using the editing tools, you can upload two files. The first is the mp4 video file (it is not necessary for this file to have the embedded captions track).

The second file contains the captions and timing information in our `srt` file, but needs to be in a different format. This format is **Web Video Text Tracks (VTT)**, and is easily obtained using ffmpeg:

```sh
$ ffmpeg -i srtfile.srt subtitlefile.vtt
```

Having uploaded these two files to the Learn Item, it is necessary to edit the HTML using the built-in HTML editor (click the double chevron at the right end of the tool bar to reveal it). The item source should be edited to contain a `<video>` tag:

```html
<p>  
<video width="640" height="360" controls="controls">
	<source src="https://www.learn.ed.ac.uk/path-to-video" type="video/mp4" />  
	<track src="https://www.learn.ed.ac.uk/path-to-vtt-file" kind="captions" srclang="en" label="English" default />
	Your browser does not support the video tag.
</video>
</p>
```

Irrespective of what you type in the editor, Learn will try to close the `<track>` tags, even though they shouldn't be. It will result in user of older browsers not seeing the message about not supporting the video tag. I have little sympathy for them.

### Bizarre path changes

The path to video and the `vtt` files is available in the links to them put there by Learn when you uploaded the files. It is not necessary to keep these links, but there is another little feature you should be aware of. When you upload a file like this, it will be given a path that ends in something like "mp4" or "vtt". If you use this path in your `source` or `track` tags above, it will not work. This is because Learn **changes the url for embedded files after your edits are submitted.** This behaviour makes no sense to me, but what it means is that you will have to (1) upload the files and submit the edits to the item you are creating, then (2) edit it again and get the new paths to use in the `source` and `track` tags. Just another bizarre feature of Blackboard Learn, I suppose.

## Finished, part two

This is a workaround but we now have the facility to make and upload good quality video with closed captioning that can be viewed by students within their Learn course.

<!--## Footnotes-->
