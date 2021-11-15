title: ttygif
categories:
  - mac
date: 2021-11-15 17:08:10
---
### Mac终端录屏

```sh
https://github.com/icholy/ttygif
```

```sh
brew install ttygif
ttyrec myrecording

# On OSX optionally you can set a -f flag which will bypass cropping which is needed for terminal apps which aren't full screen. Both standard Terminal and iTerm apps are supported.
ttygif myrecording -f
```