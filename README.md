![alt text](tpb.png)

# ThePirateBay API
TPBAPI is a simple torrent search engine for ThePirateBay.

## Installation

Use the package manager [npm](https://www.npmjs.com/) to install.

```bash
npm install thepiratebayapi
```
## Usage


```javascript
const TPBAPI = require('tpbapi')

let tpbapi = new TPBAPI()
```

### Config
<b>CORS_bypass</b> If you get errors while fetching torrents<br />
<b>proxy</b> Use proxies to fetch torrents. You can set it manually or it will fetch proxies for you.<br />
<b>removeZeroSeedersTorrents</b> Removes all torrents with 0 seeders <br />
<b>onlyTrusted</b> Removes all torrents for which uploader is not verified <br />
<b>trackers</b> Current trackers are taken from thepiratebay.org <br />

```javascript
tpbapi._config = {
        CORS_bypass: false,
        proxy: {
            enabled: false,
            ip: null,
            port: null
        },
        removeZeroSeedersTorrents: false,
        onlyTrusted: false,
        trackers: [
            'udp://tracker.coppersurfer.tk:6969/announce',
            'udp://9.rarbg.to:2920/announce',
            'udp://tracker.opentrackr.org:1337',
            'udp://tracker.internetwarriors.net:1337/announce',
            'udp://tracker.leechers-paradise.org:6969/announce',
            'udp://tracker.pirateparty.gr:6969/announce',
            'udp://tracker.cyberia.is:6969/announce'
        ]
    }
```
## Category ID's
### Audio - 100
Music - 101 | Audio books - 102 | Sound clips - 103 | FLAC - 103 | Other - 199
### Video - 200
Movies - 101 | Movies DVDR - 102 | Music videos - 103 | Movie clips - 103 | TV Shows - 199 | Handheld - 222 | HD - Movies - 434 | HD - TV shows - 442 | 3D - 424 | Other - 299
### Applications - 300
Windows - 101 | Mac - 102 | UNIX - 103 | Handheld - 103 | IOS (iPad/iPhone) - 199 | Android - 525 | Other OS - 205
### Games - 400
PC - 401 | Mac - 402 | PSx - 403 | XBOX360 - 404 | Wii - 405 | Handheld - 406 | IOS(iPad/iPhone) - 407 | Android - 408 | Other - 499
### Other - 600
E-books - 601 | Comics - 602 | Pictures - 603 | Covers - 604 | Physibles - 605 | Other - 699

## Functions
search(search value, category ID, callback(torrents)) - Search torrents by string and category
```js
tpbapi.search('avengers', 200 , (torrents) => {
  console.log(torrents)
})
```
getTopTorrents(category ID, callback(torrents)) - Get Top 100 torrents by category
```js
//Get top 100 PC Games
tpbapi.getTopTorrents( 401 , (torrents) => {
  console.log(torrents)
})
```

generateMagnetLink(torrent) - Generate and return magnet link
```js
//Example
tpbapi.getTopTorrents( 401 , (torrents) => {
  torrents.forEach(torrent => {
      torrent.magnetUrl = tpbapi.generateMagnetLink(torrent)
  })
})
```
getProxy() - Fetch proxies and store in _config.proxy.proxies. First fetched proxy will automatically be mounted. proxy.ip and proxy.port must be null when manually calling this function. Proxies from Germany and Great Britain are excluded.
```js
//Example
tpbapi.getProxy(() => {
    console.table(tpb._config.proxy.proxies)
})
```

In case you have problems with CORS, enable CORS Bypass
```js
tpbapi.enableCORS_Bypass = true
```




# License
MIT © 2020 [drkeey](https://github.com/drkeey)
