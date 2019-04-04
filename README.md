# lyric-parser

lyric-parser base on javascript

## Install

```js
  // 改变package.json里面该项的配置,自己修改之后的同学不要忘记build
  "lyric-parser": "git+git@github.com:Hhpon/lyric-parser.git"
```

## Usage

```
 import Lyric from 'lyric-parser'
 let lyric = new Lyric(lyricStr, handler)

 function hanlder({lineNum, txt}){
   // this hanlder called when lineNum change
 }
```

## API

#### play()

play the lyric

#### stop()

stop play

#### seek(startTime)

seek to correspond starTime

#### togglePlay()

toggle play state

可以兼容网易云音乐的歌词，原来不能兼容的原因是'网易云音乐接口拿到的歌词微秒位有三种情况(.100,.010,.10)，而原来使用的 QQ 音乐的歌词微秒位为(.10)格式,这里需要对 result[3]做处理。'

```js
time: result[1] * 60 * 1000 + result[2] * 1000 + (result[3] || 0) * 10;
// 原来是这种方式处理时间，但是对于.010这种微秒格式会把时间增大到原来的十倍
// 所以为了继续兼容原来的QQ音乐，可以把(result[3] || 0)截取前两位再乘以10
```
