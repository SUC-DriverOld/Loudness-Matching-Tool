# Loudness Matching Tool

基于 PyQt5 写的一个音频响度匹配小工具，目前支持 ITU-R BS.1770 (LUFS), 平均响度 (dBFS), 最大峰值 (dBFS), 总计 RMS (dB), 四种匹配方式。

## 安装发行版

你可以直接前往 [releases](https://github.com/SUC-DriverOld/Loudness-Matching-Tool/releases) 下载安装程序或解压直用版。

## 从源码启动

1. 克隆本仓库

```bash
git clone https://github.com/SUC-DriverOld/Loudness-Matching-Tool.git
```

2. 安装依赖

```bash
pip install -r requirements.txt
```

3. 下载 [ffmpeg](https://ffmpeg.org/) 并将 `ffmpeg.exe` 放置到 `./ffmpeg` 目录下

4. 使用 `gui.py` 启动

```bash
python gui.py
```

## 一些说明

1. 目前支持的响度匹配有以下四种：

   - ITU-R BS.1770 (LUFS)
   - 平均响度 (dBFS)
   - 最大峰值 (dBFS)【不是最大 **实际** 峰值！】
   - 总计 RMS (dB)

2. 导出格式支持：

   - 支持的导出音频格式：`wav`, `mp3`, `flac`
   - 支持设置导出 mp3 比特率：`320k`, `256k`, `192k`, `128k`
   - 支持设置导出采样率：`32000Hz`, `44100Hz`, `48000Hz`
   - 支持设置导出位深度：`16bit`, `24bit`, `32 bit float`

## 存在的问题

**如果有佬能解决这些问题的话，欢迎提出 pull request，感激不尽！**

1. 因为 pydub 的导出无法指定 ffmpeg 路径并且打包出来的程序在运行时会有控制台窗口闪烁，所以当转换为其他格式时，采用的方法是先保存为 wav 格式，再调用 ffmpeg 进行格式转换。导出操作的部分代码如下。也有可能是我太菜了，轻喷。详情请见 [audio_processor.py#L35](https://github.com/SUC-DriverOld/Loudness-Matching-Tool/blob/main/audio_processor.py#L35)

2. pydub 只能计算 peak，无法计算 true peak，所以只能匹配最大峰值，实际最大峰值没法匹配。详情请见 [audio_processor.py#L96](https://github.com/SUC-DriverOld/Loudness-Matching-Tool/blob/main/audio_processor.py#L96)

3. 在实际测试中，部分电脑出现了控制台闪烁的情况。**但大部分情况下不会出现这个问题。**我暂时无法复现这个问题，所以暂时无法解决。
