---
title:  mp3 download from choralia.net
categories:
- bash
- mp3
- choir
author: Oliver Gaida
version: 3
---

here i show, how to download 117 learning mp3 files from choralia.net. the songs are the choral-songs of "J.S. BACH - ST. JOHN PASSION BWV245"
This script downloads 117 mp3 = 4 voices (satb) and 29 times (choral-songs). I take the solo version without metronom. After downloading i create special mp3 versions
where the solo voice is on the left channel and all other voices are on the right channel. This is done with the help of ffmpeg. therefor i have reduced the volume of the right channel a bit, so it is not 
to loud.

```bash
#!/usr/bin/env bash
for i in {1..20} {22..29}
do 
    wget https://mp3.choralia.net/mp3player.php?mp3file=bh03mp3/bh03-${i}ss.mp3 -O bh03-${i}ss.mp3
    wget https://mp3.choralia.net/mp3player.php?mp3file=bh03mp3/bh03-${i}as.mp3 -O bh03-${i}as.mp3
    wget https://mp3.choralia.net/mp3player.php?mp3file=bh03mp3/bh03-${i}ts.mp3 -O bh03-${i}ts.mp3
    wget https://mp3.choralia.net/mp3player.php?mp3file=bh03mp3/bh03-${i}bs.mp3 -O bh03-${i}bs.mp3

    # Sopran
    ffmpeg -i bh03-${i}ss.mp3 -i bh03-${i}as.mp3 -i bh03-${i}ts.mp3 -i bh03-${i}bs.mp3 \
        -filter_complex \
        "[0:a]volume=0.8[left]; \
        [1:a][2:a][3:a]amix=inputs=3:normalize=0,volume=0.3[right]; \
        [left][right]amerge=inputs=2,pan=stereo|FL=c0|FR=c1[out]" \
        -map "[out]" -c:a libmp3lame -q:a 2 bh03-${i}ss-left.mp3

    # Alt
    ffmpeg -i bh03-${i}as.mp3 -i bh03-${i}ss.mp3 -i bh03-${i}ts.mp3 -i bh03-${i}bs.mp3 \
        -filter_complex \
        "[0:a]volume=0.8[left]; \
        [1:a][2:a][3:a]amix=inputs=3:normalize=0,volume=0.3[right]; \
        [left][right]amerge=inputs=2,pan=stereo|FL=c0|FR=c1[out]" \
        -map "[out]" -c:a libmp3lame -q:a 2 bh03-${i}as-left.mp3

    # Tenor
    ffmpeg -i bh03-${i}ts.mp3 -i bh03-${i}as.mp3 -i bh03-${i}ss.mp3 -i bh03-${i}bs.mp3 \
        -filter_complex \
        "[0:a]volume=0.8[left]; \
        [1:a][2:a][3:a]amix=inputs=3:normalize=0,volume=0.3[right]; \
        [left][right]amerge=inputs=2,pan=stereo|FL=c0|FR=c1[out]" \
        -map "[out]" -c:a libmp3lame -q:a 2 bh03-${i}ts-left.mp3

    # Bass
    ffmpeg -i bh03-${i}bs.mp3 -i bh03-${i}as.mp3 -i bh03-${i}ts.mp3 -i bh03-${i}ss.mp3 \
        -filter_complex \
        "[0:a]volume=0.8[left]; \
        [1:a][2:a][3:a]amix=inputs=3:normalize=0,volume=0.3[right]; \
        [left][right]amerge=inputs=2,pan=stereo|FL=c0|FR=c1[out]" \
        -map "[out]" -c:a libmp3lame -q:a 2 bh03-${i}bs-left.mp3
    
    rm bh03-${i}{s,a,t,b}s.mp3
    for a in s a t b
    do 
        mv bh03-${i}${a}s{-left,}.mp3
    done
done

# track21 has no bass voice ....

i=21
wget https://mp3.choralia.net/mp3player.php?mp3file=bh03mp3/bh03-${i}ss.mp3 -O bh03-${i}ss.mp3
wget https://mp3.choralia.net/mp3player.php?mp3file=bh03mp3/bh03-${i}as.mp3 -O bh03-${i}as.mp3
wget https://mp3.choralia.net/mp3player.php?mp3file=bh03mp3/bh03-${i}ts.mp3 -O bh03-${i}ts.mp3
# Sopran
ffmpeg -i bh03-${i}ss.mp3 -i bh03-${i}as.mp3 -i bh03-${i}ts.mp3 \
    -filter_complex \
    "[0:a]volume=0.8[left]; \
    [1:a][2:a]amix=inputs=2:normalize=0,volume=0.4[right]; \
    [left][right]amerge=inputs=2,pan=stereo|FL=c0|FR=c1[out]" \
    -map "[out]" -c:a libmp3lame -q:a 2 bh03-${i}ss-left.mp3

# Alt
ffmpeg -i bh03-${i}as.mp3 -i bh03-${i}ss.mp3 -i bh03-${i}ts.mp3 \
    -filter_complex \
    "[0:a]volume=0.8[left]; \
    [1:a][2:a]amix=inputs=2:normalize=0,volume=0.4[right]; \
    [left][right]amerge=inputs=2,pan=stereo|FL=c0|FR=c1[out]" \
    -map "[out]" -c:a libmp3lame -q:a 2 bh03-${i}as-left.mp3

# Tenor
ffmpeg -i bh03-${i}ts.mp3 -i bh03-${i}as.mp3 -i bh03-${i}ss.mp3 \
    -filter_complex \
    "[0:a]volume=0.8[left]; \
    [1:a][2:a]amix=inputs=2:normalize=0,volume=0.4[right]; \
    [left][right]amerge=inputs=2,pan=stereo|FL=c0|FR=c1[out]" \
    -map "[out]" -c:a libmp3lame -q:a 2 bh03-${i}ts-left.mp3

rm bh03-${i}{s,a,t}s.mp3
for a in s a t
do 
    mv bh03-${i}${a}s{-left,}.mp3
done
```