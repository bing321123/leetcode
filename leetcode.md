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

### [35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/description//)

```js
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function(nums) {
    let start = 0
    let end = 0
    let arr = []
    for (let i = 0; i < nums.length; i++) {
        if (nums[i +1] - nums[i] !== 1) {
            arr.push([nums[start], nums[end]])
            start = i + 1
            end = i + 1
        } else {
            end = i + 1
        }
    }
    return arr.map(item => item[0] === item[1] ? `${item[0]}` : `${item[0]}->${item[1]}`)
};
```


### [228. 汇总区间](https://leetcode.cn/problems/summary-ranges/description/)
```js
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function(nums) {
    let start = 0
    let end = 0
    let arr = []
    for (let i = 0; i < nums.length; i++) {
        if (nums[i +1] - nums[i] !== 1) {
            arr.push([nums[start], nums[end]])
            start = i + 1
            end = i + 1
        } else {
            end = i + 1
        }
    }
    return arr.map(item => item[0] === item[1] ? `${item[0]}` : `${item[0]}->${item[1]}`)
};
```