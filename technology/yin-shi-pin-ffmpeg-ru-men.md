---
description: 音视频处理入门
---

# 音视频-FFmpeg入门

![&#x77E5;&#x8BC6;&#x6846;&#x67B6;](../.gitbook/assets/image%20%2821%29.png)

视频处理示例（移除某个视频文件里的音频）：  
首先运行`ffmpeg -i file.mp4`以查看文件中存在哪些流。您应该会看到以下内容：

```text
Stream #0.0: Video: mpeg4, yuv420p, 720x304 [PAR 1:1 DAR 45:19], 23.98 tbr, 23.98 tbn, 23.98 tbc
Stream #0.1: Audio: ac3, 48000 Hz, 5.1, s16, 384 kb/s
Stream #0.2: Audio: ac3, 48000 Hz, 5.1, s16, 384 kb/s
```

然后运行`ffmpeg -i file.mp4 -map 0:0 -map 0:2 -acodec copy -vcodec copy new_file.mp4`以将视频流和第二音频流复制到`new_file.mp4`。

{% embed url="http://www.ruanyifeng.com/blog/2020/01/ffmpeg.html" %}



