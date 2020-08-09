## Video to audio

```bash
ffmpeg -i video.avi -ac 2 -acodec pcm_s16le sound.wav
```



wav to opus:

```bash
opusenc input.wav output.opus
```

if opusenc not fount, then:

```bash
apt install opus-tools
```

