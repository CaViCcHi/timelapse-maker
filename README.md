# timelapse-maker
This is a beautiful wrapper written entirely in BASH, extending bash-tui, and allows you to grab remote/local snapshots and combine them in a timelapse with music and text.

All this then can be uploaded on different platforms: as of now Youtube and Facebook. Youtube uploading comes from a repository here on github, whereas the Facebook upload is builtin by me.


#### Some examples of functionality:
`timelapse-maker --date today --wrap sunset --facebook --fbvideo --music=3m --publish_at='9pm today'`

Will create a time lapse from the pictures of TODAY, the length will be left up to the software (24fps is the configured default, as youtube uses 24), wrapping specifically only the sunset time. Will add music from the sub-directory '3m', Will post on Facebook the full video. And all this will be published at 9pm today.


`timelapse-maker --datePatt="201901{19..22}" --length=90 --videoSize=820x458` (quotes are important for --datePatt)

Will create a 90 second time lapse from the pictures of the days between Jan 19th and Jan 22nd, and the video will be resized to 820x458.


##### That's not just 'it'
The functionalities of this software go beyond these couple of tests, I will be documenting more and more

This is an extract of the help so far:

````
# timelapse-maker --help


Help generated by bashparms automagically for file /usr/local/bin/timelapse-maker


    --astronomy
                Generate astronomy details in description
    --auth_creds
                authentication file: If this file doesn't exist you have to authenticate manually!
    --date
                The date to timelapse, supports format of 'date --date'
    --datePatt
                the pattern you want to parse, eg: --datePatt="201804{20..22}" takes a 3 day timelapse
    --description
                The video description on YouTube
    --dirFrames
                with --reuseFrames is the local directory where the images are already
    --downloadonly
                if you just want to copy over the frames from the remote/local server
    --dullFrames
                When enabled, the software will compare each frame with the next with an algorithm I wrote and will discard if nothing happens, Generates a variable FPS effect.
    --facebook
                Post on facebook, by itself will perform a text post only
    --fb_message
                The message to post on acebook.
    --fbvideo
                Post the video just made on Facebook
    --help
                If you need help
    --imgDir
                Directory where you want to grab the images from
    --imgServer
                Server host/ip where to get the images from
    --keep_writeln
                Do not discard the Text frames generated with this procedure (deletes by default)
    --length
                Output video length: 180 secs = 3mins : default will calculate at 24fps
    --music
                Directory where to get the music from
    --private
                Youtube: make video private
    --publish_at
                Schedule your upload/post for a future time, supports the date --date format (eg. tomorrow, last monday, next week 3pm... and so on)
    --qa
                IN DEVELOPMENT: run a check on the timelapse that will be created and only release it if it's up to standard (eg. don't publish a timelapse if it's all grey because there was bad weather)
    --reuseFrames
                Reuse the frames already downloaded in a previous operation, do not download new ones.
    --tags
                Comma separated list of Video Tags for youtube, eg: "one,two,three and four,five"
    --thumbnail
                Path of a thumbnail, otherwise I'll chose a random image
    --thumbType
                Type of thumbnail, for now day,week,month
    --timestamps
                If you want to timestamp the frames
    --title
                The title of the video on youtube
    --ts_left
                Timestamp margin from the left in px
    --ts_top
                Timestamp: margin from the top in px
    --unlisted
                Youtube: make video unlisted
    --videoSize
                Size of the output video WxH, eg: 1920x1080
    --volume
                TODO: BROKEN: Adjust the volume of the music
    --wrap
                You can wrap your date by sunset,sunrise,daylight,nightsky
    --writeln
                Write in the timelapse, syntax begin_secs:end_secs:TEXT[:#COLOR[:X[:Y[:F_size[:F_style]]]]]
    --youtube
                If you want to upload your video on youtube
    --youtube_playlist
                Name of the youtube playlist
````

##### --wrap
nightsky: will grab the time when the sun is already down
daylight: will grab the time when the sun is up
sunset: starts 1 hour* before the sun disappears in the horizon and the light dissipates.
sunrise: starts when light starts appearing at the horizon and ends 1 hour* after.

* 1 hour is set in the configuration `fun_sunrise` and `fun_sunset` and it's an estimate of how long the event of the sun rising/setting is interesting for. May differ depending on your longitude.

##### --youtube
I suggest you read the configuration directly from https://github.com/tokland/youtube-upload

##### --facebook --fbvideo
Since I saw that Facebook had a cute API for video uploading in chunks I went for it, didn't take long.
You have the ability to upload the video directly on your Facebook page or feed, all you need is to get a "Page access token" (https://developers.facebook.com/docs/pages/access-tokens/) and place the token in `/etc/timelapse-maker/auth/facebook-auth` as
````
PAGE_TOKEN=YOUR_TOKEN
PAGE_NAME=YOUR_PAGE_NAME
````

##### --writeln


##### --timestamps --ts_left --ts_top


##### --thumbnail --thumbType


##### --music


##### --length


##### --dullFrames



### You need to have installed on your system:
- ffmpeg : (https://www.ffmpeg.org/)
- ImageMagick : (https://www.imagemagick.org/)

### Requires these git repositories installed:
- Astronomicon: https://github.com/CaViCcHi/AstroNomicon.sh or the machine won't know when is sunset/sunrise and other times of day
- Bash-Tui: https://github.com/CaViCcHi/bash-tui using the basic libraries like say with its colors or bashparms
- Youtube-Upload: https://github.com/tokland/youtube-upload for uploading the youtube videos.

I might shed the `bash-tui` requirements later in time if anyone is interested in this project alone, so I might just combine what's needed.

### Spaces or Tabs?
2 spaces.

## Why Bash?
Everyone more or less "speaks" bash and can easily edit anything from this script for his personal use
