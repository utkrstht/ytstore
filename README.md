# ytstore

A Youtube-Based Storage Service.

(being made for midnight.hackclub.com)

# Prototyping
I've made a prototype which can encode any file into a video (webm)  
I've successfully recovered a 2MB image from youtube, which you can see in [the prototype folder](/prototype)  

In the [videos](/prototype/videos), you'll notice that the webm file is astronomically large, 79MB for about 1 second, that's because of extremely high quality video, that's needed to survive re-encoding and compression, down to 23MB (check downloaded.mp4), the compression doesn't cause any major corruption.2

manifest.json contains the decoding metadata for decoding the video/frames, however it isn't exactly necessary for decoding.

All recovered files are slightly bigger than the original, I assumed it was because of corrupted bytes,  
however it was because the decoder was reading EVERYTHING, including the unused black area at the last page,

### Scripts
Usage of the scripts,

NOTE: encoder will only output a video if ffmpeg is on PATH, otherwise, it'll only generate the frames, same goes for decoder, it needs ffmpeg to decode a video

encoder: `python encoder.py cool.file output_dir` (you can modify the internal video format, by passing cli args, check the first docstring in encoder.py)  
decoder: `python decoder.py encoded.webm recovered.file` (if you modified the internal video format, you'll need to match it here as well)  
decoder (using frames directory): `python decoder.py frames_directory recovered.file` (this is incase you don't have ffmpeg)  

The encoder will always output a webm ("encoded.webm"), however the decoder will accept any video format.  
The encoder also outputs a /frames directory which contains each frame, you may/may not need this.

# How to store on youtube
Storing:
Step 1: Encode your file (check above on how to)
Step 2: Upload your webm to Youtube as Unlisted or Public, Do not set to private.

Retrieving:
Step 1: Install yt-dlp (`pip install yt-dlp`)
Step 2: Run `yt-dlp -f "bv*" <URL>` (replace <URL> with your video url)
Step 3: Run the downloaded file through the decoder (check above on how to) 


# Disclamer and Warnings
This is a concept, you may store your files using this at your own risk.  
Your file *MAY* be corrupted.
Do not store any extremely sensitive data that can absolutely not be corrupted.
Youtube may at anytime remove your data, and there is nothing we can do. 

