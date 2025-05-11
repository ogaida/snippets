---
title: Youtube Video Download
categories:
  - bash
  - youtube
author: Oliver Gaida
version: 4
---

# {{ page.title }}

## Installation youtube-dl

### Installation unter Linux bzw. Windows WSL

siehe [https://github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp)

Letztlich einfach nur herunterladen und ausführbar machen:

```bash
mkdir ~/.local/bin
curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o ~/.local/bin/yt-dlp
chmod a+rx ~/.local/bin/yt-dlp
[[ $PATH =~ ~/.local/bin ]] || export PATH=${PATH}:~/.local/bin
```

um die PATH Einstellungen zu persistieren, bietet sich an den PATH-Aufruf an das Ende der `~/.bashrc` anzuhängen:

```bash
echo '[[ $PATH =~ ~/.local/bin ]] || export PATH=${PATH}:~/.local/bin' >> ~/.bashrc
```

## Verwendung

### Video Download - Best Quality

Wenn man ein gefundenes Video in der bestmöglichen Qualität herunterladen will, empfiehlt sich folgendes Kommando:

```bash
yt-dlp -f bestvideo[ext=mp4]+bestaudio[ext=m4a] https://www.youtube.com/watch?v=VIDEO-ID
```

dabei bitte den String VIDEO-ID entsprechend ersetzen. Eventuell erfordert dieses Kommando noch die Installation von ffmpeg:

```bash
sudo apt install ffmpeg
```

Die Zieldatei erhält einen geeigneten Namen mit der Endung mp4.

Happy watching!

### Audio only

Falls man nur ein mp3 aus dem Video erstellen will, genügt folgender Aufruf:

```
yt-dlp -x --audio-format mp3 https://www.youtube.com/watch?v=<VIDEO-ID>
```