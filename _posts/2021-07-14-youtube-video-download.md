---
title: Youtube Video Download
categories:
  - bash
  - youtube
author: Oliver Gaida
version: 3
---

# {{ page.title }}

## Installation youtube-dl

### Installation unter Linux bzw. Windows WSL

siehe [https://github.com/ytdl-org/youtube-dl](https://github.com/ytdl-org/youtube-dl)

Letztlich einfach nur herunterladen und ausführbar machen:

```bash
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```

### Installation unter MacOS

```bash
brew install youtube-dl
```


## Verwendung

Mit folgenden Kommandos könnte man nun ein Video herunterladen, wenn man es unbedingt offline benötigt. Das Herunterladen von Videos ist anscheinend legal, siehe [https://www.futurezone.de/digital-life/article211244737/futurezone-hilft-Ist-der-Download-von-YouTube-Videos-legal.html](https://www.futurezone.de/digital-life/article211244737/futurezone-hilft-Ist-der-Download-von-YouTube-Videos-legal.html). Verbreiten, womöglich noch kommerziell ist wahrscheinlich keine gute Idee.


### Video Download - Best Quality

Wenn man ein gefundenes Video in der bestmöglichen Qualität herunterladen will, empfiehlt sich folgendes Kommando:

```bash
youtube-dl -f bestvideo[ext=mp4]+bestaudio[ext=m4a] https://www.youtube.com/watch?v=VIDEO-ID
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
youtube-dl -x --audio-format mp3 https://www.youtube.com/watch?v=<VIDEO-ID>
```