# encoder

Encode information into videos

(being made for midnight.hackclub.com)

# Prototyping
This was originally meant to be used to store files on youtube, however the compression and re-encoding from youtube absolutely destroyed it.

### Scripts
Usage of the scripts,  

NOTE: You NEED ffmpeg on path, otherwise encoder and decoder won't work!!!  

encoder: `python encoder.py <cool_file> <output_dir>`
decoder: `python decoder.py <video_file> <file_output>`  

The encoder will always output a webm ("encoded.webm") and a frames/ directory with the frames of the video

### Features added/tried
1. Different Codecs for faster encoding/decoding, This only matters for encoding, as youtube re-encodes it into it's own av1/vp9 format.  
I tried using both vp9 and av1, as vp9 is faster to encode, but it's bigger and also slower to decode, and av1 is much much slower to encode, but smaller and faster to decode. This is unnecessary unless you're encoding a local video.

2. zstd Input Compression, This is for faster encoding/decoding, as there is less information to process, We compress the input file, this really only works for text/binary files, something like an image or video won't have a big change. You can use this with `--compress` (use this on both encoder and decoder), but it's not recommended currently for youtube videos. 

3. Diskless Pipeline, This is way too complicated for what it's worth, this is only implemented in the frame to video stage so we don't store any frames, I tried implementing this to directly upload the video to the fastapi server, but it was unnecessary, and deleting the file after uploading it had the same effect.




