# JavaScript

## Articles

- [How to Make Uploading 10x Faster](https://blog.daftcode.pl/how-to-make-uploading-10x-faster-f5b3f9cfcd52)

## Documentation

- [Einführung in JavaScript](https://molily.de/js)
- [The Modern JavaScript Tutorial](https://javascript.info)
  - [Coordinates](https://javascript.info/coordinates)

## Libraries

- [Day.js](https://day.js.org) uses the API of [Moment.js](https://momentjs.com/)
- [pako](https://github.com/nodeca/pako) (compression, zlib)
- [Vanilla JS](http://vanilla-js.com)

## Snippets

### Date & Time

```js
let today = new Date();
let date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
let time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
let dateTime = date+' '+time;
```

```js
let buildYMDHIS = function () {
    let date = new Date();

    let year = date.getFullYear();
    let month = date.getMonth() + 1;
    let day = date.getDate();
    let hours = date.getHours();
    let minutes = date.getMinutes();
    let seconds = date.getSeconds();

    return year
        + "-" + (month < 10 ? 0 : '') + month
        + "-" + (day < 10 ? 0 : '') + day
        + " " + (hours < 10 ? 0 : '') + hours
        + ":" + (minutes < 10 ? 0 : '') + minutes
        + ":" + (seconds < 10 ? 0 : '') + seconds;
};
```
