# Music Player Model

### Frontend challenge #01

- Vue.js 3
- Vite
- Typescript

`$ npx vite`

`$ npm run build`

---

This model was created inspired by
https://www.figma.com/community/file/1195050524500542670

![demo](https://github.com/ovictorpereira/vue-music-player-model/blob/main/public/demo.png?raw=true 'demo')

```html
<MusicPlayer :playlist="playlist" />
```

The component MusicPlayer gets an Array of songs as a prop:

```js
const playlist = [
  {
    id: 1,
    albumCover:
      'https://cdns-images.dzcdn.net/images/cover/de9496f611d6d7391fa57401bac99d5b/0x1900-000000-80-0-0.jpg',
    musicName: 'Born to die',
    artistName: 'Lana del Rey',
    duration: 192,
  },
  {
    id: 2,
    albumCover: 'https://pure-music.co.uk/wp-content/uploads/2019/04/Thriller-Album-Cover.png',
    musicName: 'Thriller',
    artistName: 'Michael Jackson',
    duration: 210,
  },
]
```

There is a ProgressBar component imported inside MusicPlayer component that responds to drag and click events.

TODO:

- Load real music from an API service;
