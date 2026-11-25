# largeFiles

个人网站 [fanyu-meng.github.io](https://fanyu-meng.github.io/) 放不下的大文件。仓库用 GitHub Pages 发布，和个人网站同域名，网站通过站点根路径 `/largeFiles/…` 引用这里的文件。

## 发布方式

Settings → Pages → Deploy from a branch，选存放这些文件的分支，目录选 `/ (root)`。发布后文件地址是：

```
https://fanyu-meng.github.io/largeFiles/<路径>
```

仓库名必须保持 `largeFiles`（注意大小写），否则网站里的路径会失效。

## acoustics-media/

子鱼声学科普文章里的视频。每篇文章一个文件夹，名字就是网站上的作品 ID（见个人网站仓库 `public/content/acoustics-index.json`）。

- `video-N.mp4`：第 N 个视频，按它在正文里出现的顺序编号。H.264 + AAC，画面最高 480p，音轨保留原始码率；原片本来就小的保持原样。
- `video-N.webp`：这个视频的封面图，用作播放器的 `poster`。

地址形如：

```
https://fanyu-meng.github.io/largeFiles/acoustics-media/<作品ID>/video-N.mp4
```

文章里用站点根路径引用，不带域名：

```html
<video controls preload="none" playsinline
  poster="/largeFiles/acoustics-media/<作品ID>/video-N.webp"
  src="/largeFiles/acoustics-media/<作品ID>/video-N.mp4"
  width="…" height="…"></video>
```

音频（MP3）和图片不放在这里，仍在个人网站仓库的 `public/content/acoustics-media/`。

### 新增视频

1. 在 `acoustics-media/<作品ID>/` 下放 `video-N.mp4` 和同名的 `video-N.webp`。单个文件不要超过 100 MB。
2. 提交并推送，等 Pages 发布完成。
3. 在个人网站文章 JSON 的 `html` 里加上面的 `<video>`。

## 容量

GitHub Pages 站点上限约 1 GB，本仓库目前约 540 MB。接近上限时，再开一个同样结构的仓库，并在个人网站的 `WorksExplorer.tsx` 里加上它的路径。
