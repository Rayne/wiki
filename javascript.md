# JavaScript
 
## Timestamp

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
