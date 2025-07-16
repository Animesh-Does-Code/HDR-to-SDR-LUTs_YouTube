# HDR to SDR .cube LUTs for HDR video uploads to YouTube

I created this GitHub repo mainly for my own reference, but decided to make it public in case it helps someone else.

## What is this for?
The SDR variant of HDR videos uploaded to YouTube have raised near black tones and poor contrast because of incorrect gamma/tonemapping by default, however, YouTube allows you to change its tonemapping behavior if you attach an appropriate LUT file to your HDR video before uploading.

This repo contains some pre-configured LUTs which I generated using DaVinci Resolve. These can be attached to your final video export before upload to significantly improve the SDR variant's presentation, bringing it closer to the intended look. 

The LUT files can be attached using mkvmerge.exe by running a command in Windows' command prompt/Terminal. This should work on Linux and Mac as well, but I haven't tested them.

## How To Use
1. Download and install [MKVToolNix](https://mkvtoolnix.download/downloads.html#windows).
2. Download and extract the files of this repository by clicking the green `Code` button and then `Download ZIP`, or alternatively directly download it [with this link](https://github.com/Animesh-Does-Code/HDR-to-SDR-LUTs_YouTube/archive/refs/heads/main.zip).
3. Move your final exported video to the folder you extracted the repository's files to.
4. Open mkvmerge_command.txt and find & replace all instances of `1000` with the nits value of one of the available LUT files, if needed. For best results, this should correspond with the peak nits that your video was mastered at.
5. Rename `input.mkv` in mkvmerge_command.txt to your video's file name.
6. Open command prompt/Windows Terminal with the path set to the current folder (Right click blank space in explorer -> Open in Windows Terminal)
7. Copy and paste the mkvmerge command and press enter. An `output.mkv` file will be created with the LUT file attached.

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

## Extra Information
Using mkvmerge on some video formats (DNxHR) may strip the video's framerate metadata, resulting in a choppy looking video when uploaded to YouTube. Adding the parameter `--default-duration` to the mkvmerge command will fix this issue. Example: `--default-duration 0:60p` for a 60 fps video. Refer to mkvmerge's [documentation](https://mkvtoolnix.download/doc/mkvmerge.html#mkvmerge.description.default_duration) for more information.
