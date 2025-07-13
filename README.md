# README

## Prerequisites

1. Exit node-red
2. Install xterm

```bash
cd ~/.node-red
npm install @xterm/xterm
```

3. Allow xterm to be accessed by node-red frontend system. To do that edit your `settings.js`

```bash
cd ~/.node-red
nano settings.js
```

Find `httpAdminMiddleware`. 

> Do not uncomment

paste this below:

```js
httpAdminMiddleware: function(req, res, next) {
    if (req.url.startsWith('/xterm/')) {
        const path = require('path');
        const filePath = path.join(__dirname, 'node_modules/@xterm/xterm', req.url.replace('/xterm/', ''));
        res.sendFile(filePath);
    } else {
        next();
    }
},
```

4. Restart node-red
5. Drag a `dashboard template (ui)` in your workspace. Place it under a group, under a tab with suitable size. 
6. Copy paste the values of [console.html]( console.html) in there. 

> [!TIP]
> There's example usage flow file ([node-red-dashboard-console-example.json](node-red-dashboard-console-example.json)) to get started easily


### msg types 

For console interaction

| msg params | value | type | behavior
| --- | --- | --- | --- |
`msg.showLevels` | `true` | bool | Enables debug LEVELs in msg prefix. _Enabled by default_ |
`msg.showLevels` | `false` | bool | Disables debug LEVELs as msg prefix. |
`msg.timestamp` | `true` | bool | Enables time-stamp in msg prefix. _Enabled by default_ |
`msg.timestamp` | `false` | bool | Disables time-stamp LEVELs as msg prefix. |
`msg.payload` | string, json and array | could be string, json, js object or arrays  | can accept these as inputs to display in the console, neatly! |
`msg.level` | `info`, `warn`, `debug`, `error`, `white` | string  | Sets the warning levels adn this color of the console prints. Default is GREEN, if `msg.level` is not sent with `msg.payload` |

---

## LICENSE

[MIT](LICENSE)

---

```txt
Saurabh Datta
Berlin, Germnay
July 2025
```

