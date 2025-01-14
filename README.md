# What is Craig?
Craig is a multi-track voice recorder for Discord. Craig is divided into three
components: The actual recording bot, the web page (for downloading
recordings), and the audio processing scripts.

The recording bot is craig.js. It is a Node.js application written with
the Eris Discord library. For historical reasons it uses the sharding manager
from discord.js. Its dependencies can be installed with `npm install`. In
principle the recording bot works fine without the other components, but the
audio files it produce aren't really usable without processing.

The web page is in PHP (yuck), but otherwise has essentially no dependencies.
The "other formats" feature, which performs audio processing in the browser,
requires ffmpeg.js. The patch for ffmpeg.js to build it with the required
modules is in ffmpeg-js-craig.diff. ffmpeg.js should be built to
ffmpeg-worker-craig.js.

The audio processing scripts require the following command-line tools:

- ffmpeg ( http://ffmpeg.org/ ) compiled with libopus support
- flac ( https://xiph.org/flac/ )
- oggenc ( https://xiph.org/vorbis/ )
- opusenc ( http://opus-codec.org/ )
- fdkaac ( https://github.com/nu774/fdkaac )
- zip and unzip ( http://infozip.org/ )

Various components of the audio processing scripts require compilation or
translation:
```sh
cd cook
for i in *.c; do gcc -O3 -o ${i%.c} $i; done
for i in *.svg; do inkscape -o ${i%.svg}.png $i; done
```

The self extractors require compilation if you want them:
```sh
cd windows; make
cd macosx; make
```

Finally, the avatar stuff requires ImageMagick.  
  
If you want EnnuiCastr (browser-based recording) support, you must set  
config.ennuicastr to the web address, which must be on the same host as Craig.  
EnnuiCastr requires no further modification to work with Craig.  
  
If you want Ennuizel (browser-based processing) support, you must make it  
available at the location linked from the downloader (dl.php), and run ces.sh  
in ennuicastr/server.  
  
More information on Craig can be found at  
https://craig.chat/  
  
  
Craig can integrate with other tools (largely also by Yahweasel) to provide  
improved functionality.  
  
EnnuiCastr ( https://github.com/Yahweasel/ennuicastr/ ) is a browser-based  
audio capture tool which records more reliably than Discord, and can be used to  
get higher-quality audio if config.ennuicastr is set to an appropriate URL.  
  
Ennuizel ( https://github.com/Yahweasel/ennuizel/ ) is a browser-based audio  
editor which can provide audio processing features too heavy to put on the  
server. The 'ennuizel' directory here is the associated client plugin for  
Ennuizel as well as the server component, only required when combining Ennuizel  
with Craig.  
  
  
No documentation is provided for running your own instances of Craig. A user  
has kindly added an installation guide to the wiki on github at  
https://github.com/Yahweasel/craig/wiki , but note that this is not maintained  
by the author of Craig.  
  
RUNNING CRAIG IS NOT LIKE RUNNING ANY OTHER BOT. MOST OF THE COMPLEXITY OF  
CRAIG IS NOT IN THE BOT ITSELF, BUT IN THE AUDIO PROCESSING.  
  
IF YOU ARE NOT FAMILIAR WITH C AND UNIX, DO NOT WASTE YOUR TIME OR MINE. IF YOU  
DELUDE YOURSELF INTO THINKING YOU WILL HOST CRAIG ON WINDOWS, DO NOT WASTE YOUR  
TIME OR MINE. CRAIG IS NOT MERELY BUILT FOR UNIX, CRAIG IS BUILT ON THE UNIX  
PHILOSOPHY.  
  
"THIS ONE TIME I RAN A LINUX VM" IS NOT SUFFICIENT. "I CAN USE PUTTY" WON'T CUT  
IT. IF THE WORD "WINDOWS" DOESN'T MAKE YOUR SKIN CRAWL, YOU ARE NOT THE KIND OF  
PERSON WHO WILL SUCCEED IN RUNNING CRAIG.  
  
If you're familiar with C and Unix, it shouldn't be too difficult to get your  
own Craig working. Yahweasel is generally happy to help if you have the  
requisite background.  
  