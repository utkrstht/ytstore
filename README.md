# ytstore

A Youtube-Based Storage Service.

(being made for midnight.hackclub.com)

# Prototyping
The videos generated are extremely big, as the video needs to be very high quality to survive re-encoding and compression  

manifest.json has been shifted to the video description.

Do note, this is not a very fast process, encoding and decoding takes a decent bit of time, and the ratio is quite bad (latest prototype 214mb:2mb), however that doesn't matter since youtube is the one storing it :3

### Scripts
Usage of the scripts,  

NOTE: You NEED ffmpeg on path, otherwise encoder and decoder won't work!!!  
NOTE2: Your file needs to be ATLEAST 1MB, it's recommended to have 2MB, as if the video is too short, youtube abandons processing it  

encoder: `python encoder.py <cool_file> <output_dir>`, <cool.file> should be in the same folder as the encoder. as when decoding, it'll resolve to that input filename, you can set output_dir as .  
decoder (using link): `python decoder.py --youtube <youtube_link>`, you don't need to provide the cli args, as the manifest is linked with the video  
decoder (using video): `python decoder.py <video_file> <file_output>`  

The encoder will always output a webm ("encoded.webm") which will be deleted after uploading successfully, this however does not account for abandoning processing (video too short).  

The decoder when using a youtube link, it first queries to download the video in the highest video quality available using yt-dlp, then, it queries for it's title (filename) and description (manifest), then it uses that to decode it and output the file.  

### Features added/tried
1. Different Codecs for faster encoding/decoding, This only matters for encoding, as youtube re-encodes it into it's own av1/vp9 format.  
I tried using both vp9 and av1, as vp9 is faster to encode, but it's bigger and also slower to decode, and av1 is much much slower to encode, but smaller and faster to decode. This is unnecessary unless you're encoding a local video.

2. zstd Input Compression, This is for faster encoding/decoding, as there is less information to process, We compress the input file, this really only works for text/binary files, something like an image or video won't have a big change. You can use this with --compress, but it's not recommended currently for youtube videos. 

3. Diskless Pipeline, This is way too complicated for what it's worth, this is only implemented in the frame to video stage so we don't store any frames, I tried implementing this to directly upload the video to the fastapi server, but it was unnecessary, and deleting the file after uploading it had the same effect.

# Disclamer and Warnings
This is a concept, you may store your files using this at your own risk.  
Your file *MAY* be corrupted.  
Do not store any extremely sensitive data that can absolutely not be corrupted.  
Youtube may at anytime remove your data, and there is nothing we can do.  

