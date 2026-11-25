# largeFiles

个人网站 [fanyu-meng.github.io](https://fanyu-meng.github.io/) 的大文件。它们不进网站仓库的 git 历史，网站部署时才合并发布，和网站同域名，网站通过站点根路径 `/largeFiles/…` 引用这里的文件。

## 发布方式

本仓库不单独开启 GitHub Pages。个人网站仓库的部署工作流（`.github/workflows/deploy.yml`）每次部署时检出本仓库的 `main` 分支，放在网站的 `/largeFiles/` 下一起发布。文件地址是：

```
https://fanyu-meng.github.io/largeFiles/<路径>
```

只改了本仓库时，到个人网站仓库的 Actions 里手动运行 Deploy to GitHub Pages，新文件才会上线。仓库改名或换分支时，要同步改那个部署工作流。

## acoustics-media/

子鱼声学科普文章里的视频。每篇文章一个文件夹，名字就是网站上的作品 ID（见个人网站仓库 `public/content/acoustics-index.json`）。

- `video-N.mp4`：第 N 个视频，按它在正文里出现的顺序编号。H.264 + AAC，画面最高 480p，音轨保留原始码率；原片本来就小的保持原样。
- `video-N.webp`：这个视频的封面图，用作播放器的 `poster`。
- `xiaohongshu.mp4`、`xiaohongshu.webp`：由这篇文章改编的小红书视频和它的封面，显示在网站文章标题下方。用个人网站仓库的 `scripts/publish-xhs-video.py` 生成，做法见那边的《小红书视频上站》。

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
2. 提交并推送到 `main`。
3. 在个人网站文章 JSON 的 `html` 里加上面的 `<video>`，推送网站后随部署上线。

## 容量

GitHub Pages 每个站点的发布上限约 1 GB，本仓库和个人网站共用这一份：目前网站约 106 MB，本仓库约 540 MB。接近上限时，可以给本仓库单独开启 Pages（Settings → Pages → Deploy from a branch → `main` / root，会发布到同一个 `/largeFiles/` 地址，拥有自己的 1 GB），再从个人网站的部署工作流里去掉检出本仓库的那一步。
