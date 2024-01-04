# 数组
HJ3 明明的随机数

[链接](https://www.nowcoder.com/practice/3245215fffb84b7b81285493eae92ff0?tpId=37&tqId=21226&rp=1&ru=/exam/oj/ta&qru=/exam/oj/ta&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=)

```js
const rl = require("readline").createInterface({ input: process.stdin });
var iter = rl[Symbol.asyncIterator]();
const readline = async () => (await iter.next()).value;

void (async function () {
    let lines = [];
    // Write your code here
    while ((line = await readline())) {
        lines.push(parseInt(line));
    }
    const count = lines[0];
    lines.shift();
    [...new Set(lines.slice(0, count).sort((a, b) => a - b))].forEach((item) =>
        console.log(item)
    );
})();
```

