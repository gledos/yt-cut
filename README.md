# yt-cut

YouTube 较长的音乐专辑，往往会分章节，方便用户跳转到合适的部分欣赏音乐。但是从 YouTube 下载的高音质的 opus
音乐是一个整体，不利于欣赏，而 CUE 这种描述音轨的布局、信息和索引的章节格式，也不怎么支持 opus，就需要更好的方法了。

## 使用方法

现在大多数播放器都能播放 opus 编码，那么直接将高音质的 opus 音乐切片，不进行额外的转码，应该就是最好的方法了。

首先使用 yt-dlp 这款 CLI 工具下载音频：

```shell
yt-dlp -f "bestaudio/best" --write-description -ciw -o "%(title)s.%(ext)s" -v --extract-audio {% URL %}
```

`--write-description` 参数能够将章节信息保存为文件，以文本格式打开后，就能看到［章节号］［章节名］［开始时间］
这样的内容，将这部分内容复制到我让 GPT 编写的网页工具中转换，就能得到 ffmpeg 的切片命令。

最后将音乐复制一份，重命名为 test.opus，就能在 shell 中批量执行这些命令了（比如 Windows 里常用的 CMD），
单曲也就会出现。

工具在线链接是：<https://gledos.science/yt-cut/>

附言：重命名为 test.opus，可以防止名称过长，如果切片时出现错误，就能较容易找到问题，并且复制一份也是保险，
防止刚下好的文件被意外覆盖。
