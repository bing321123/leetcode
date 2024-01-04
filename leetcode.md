## 数组
### [66. 加一](https://leetcode.cn/problems/plus-one/description/)
```js
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    let stop = false;
    for(let i = digits.length - 1; i >= 0 && !stop; i--) {
        // 如果当前数字不是9
        if (digits[i] !== 9) {
            digits[i] = digits[i] + 1
            stop = true
        } else {
            // 如果当前数字是9
            digits[i] = 0
            if (i === 0) {
                digits.unshift(1)
            }

        }
    }
    return digits
};
```