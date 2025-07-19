# HDR to SDR .cube LUTs for HDR video uploads to YouTube

I created this GitHub repo mainly for my own reference, but decided to make it public in case it helps someone else.

## Why is this needed?
The SDR variant of HDR videos uploaded to YouTube have raised near black tones and poor contrast because of incorrect gamma/tonemapping by default, however, YouTube allows you to change its tonemapping behavior if you attach an appropriate LUT file to your HDR video before uploading.

This repo contains some pre-configured LUTs which I generated using DaVinci Resolve. These can be attached to your final video export before upload to significantly improve the SDR variant's presentation, bringing it closer to the intended look. 

The LUT files can be attached using mkvmerge.exe by running a command in Windows' command prompt/Terminal. This should work on Linux and Mac as well, but I haven't tested them.

## How To Use
1. Download and install [MKVToolNix](https://mkvtoolnix.download/downloads.html#windows).
2. Download and extract the latest release from the releases page, or alternatively directly download it [with this link](https://github.com/Animesh-Does-Code/HDR-to-SDR-LUTs_YouTube/releases/latest/download/HDR-to-SDR-LUTs_YouTube.zip).
3. Move your final exported video to the folder you extracted the .zip's files to.
4. Open mkvmerge_command.txt and find & replace all instances of `1000` with the nits value of one of the available LUT files, if needed. For best results, this should correspond with the peak nits that your video was mastered at.
5. Rename `input.mkv` in mkvmerge_command.txt to your video's file name.
6. Open command prompt/Windows Terminal with the path set to the current folder (Right click blank space in explorer -> Open in Windows Terminal)
7. Copy and paste the mkvmerge command into the terminal and press enter. An `output.mkv` file will be created in the folder with the LUT file attached, as well as added HDR metadata.

<hr/>

## Settings used in DaVinci Resolve for LUT generation
Color Space Transform filter settings:
* Input Color Space: Rec.2100
* Input Gamma: Rec.2100 ST2084
* Output Color Space: Rec.709
* Output Gamma: Gamma 2.4
* HDR 203 Nits Diffuse White: Enabled
* Tone Mapping Method: Saturation Preserving
* Custom Max. Input: Set to LUT specific nits
* Everything else: Default

## Side-by-side comparison
Below is a comparison of the SDR variant of two HDR videos uploaded to YouTube. One had the LUT attached while the other didn't. To my eyes, the one that has the LUT applied looks much closer to the overall look of the actual [HDR video](https://youtu.be/vQVwkyn3-F8) (Skip to 2:00).
![*Credit to Jacob + Katie Schwarz on YouTube*](./LUT-comparison.png)|
|--------------------------------------------------------------------|
|_Credit to Jacob + Katie Schwarz on [YouTube](https://youtu.be/vQVwkyn3-F8) for their amazing HDR videos._|

## Extra Information
* Using mkvmerge on some video formats (DNxHR) may strip the video's framerate metadata, resulting in a choppy looking video when uploaded to YouTube. Adding the parameter `--default-duration` to the mkvmerge command will fix this issue. Example: `--default-duration 0:60p` for a 60 fps video. Refer to mkvmerge's [documentation](https://mkvtoolnix.download/doc/mkvmerge.html#mkvmerge.description.default_duration) for more information.
* The mkvmerge command I've provided is based on the command found in YouTube's own [HDR metadata tool repository](https://github.com/youtubehdr/hdr_metadata). Unfortunately, that repository has not been updated in quite some time, and therefore contains outdated mkvmerge builds and broken links to MKVToolNix.
