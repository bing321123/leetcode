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

### [268. 丢失的数字](https://leetcode.cn/problems/missing-number/)

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function (nums) {
    // 排序
    nums.sort((a, b) => a - b)
    // 数组从小到大没有漏一个数
    if (nums[nums.length - 1] === nums.length - 1) return nums.length
    // 数组中间漏一个数，|| 1 是特殊情况，数组为 [1]
    return (nums.find((item, index) => item - nums[index - 1] === 2) || 1) - 1
};
```

### [349. 两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/description/)

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    return nums1.reduce((prev, curr) => {
        // 结果数组里已经有的过滤掉
        // nums2 里有重复的进行 push
        if (!prev.includes(curr) && nums2.includes(curr)) {
            prev.push(curr)
        }
        return prev
    }, [])
};
```

### [496. 下一个更大元素 I](https://leetcode.cn/problems/next-greater-element-i/)

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var nextGreaterElement = function(nums1, nums2) {
    return nums1.reduce((prev, curr) => {
        const currIndex = nums2.findIndex(item => item === curr)
        const next = nums2.slice(currIndex + 1).find(item => item > curr)
        prev.push(next ? next : -1)
        return prev
    }, [])
};
```

### [350. 两个数组的交集 II](https://leetcode.cn/problems/intersection-of-two-arrays-ii/description/)

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersect = function(nums1, nums2) {
    nums1.sort((a, b) => a - b)
    nums2.sort((a, b) => a - b)
    const res = []
    let n1 = 0
    let n2 = 0
    while (n1 <= nums1.length - 1 && n2 <= nums2.length - 1) {
        if (nums1[n1] === nums2[n2]) {
            res.push(nums1[n1])
            n1++
            n2++
        } else if (nums1[n1] < nums2[n2]) {
            n1++
        } else {
            n2++
        }
    }
    return res
};
```

### [219. 存在重复元素 II](https://leetcode.cn/problems/contains-duplicate-ii/description/)

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
var containsNearbyDuplicate = function (nums, k) {
    const set = new Set()
    for (let i = 0; i < nums.length; i++) {
        if (set.has(nums[i])) {
            return true
        }
        set.add(nums[i])

        if (set.size > k) {
            set.delete(nums[i - k])
        }
    }
    return false
};
```

### [500. 键盘行](https://leetcode.cn/problems/keyboard-row/)

```js
/**
 * @param {string[]} words
 * @return {string[]}
 */
var findWords = function(words) {
    const firstSet = new Set('qwertyuiop'.split(''))
    const secondSet = new Set('asdfghjkl'.split(''))
    const thirdSet = new Set('zxcvbnm'.split(''))
    const sets = [firstSet, secondSet, thirdSet]

    const res = []

    words.forEach(item => {
        const cloneArr = item.toLowerCase().split('')
        const targetSet = sets.find(set => set.has(cloneArr[0]))
        const hasNotInTargetSet = cloneArr.find(str => !targetSet.has(str))
        
        if (!hasNotInTargetSet) {
            res.push(item)
        }
    })

    return res
};
```

### [506. 相对名次](https://leetcode.cn/problems/relative-ranks/description/)

```js
/**
 * @param {number[]} score
 * @return {string[]}
 */
const SSP = ["Gold Medal","Silver Medal","Bronze Medal"]
var findRelativeRanks = function(score) {
    const map = new Map(), ans = new Array(score.length);
    for(let i=0;i<score.length;i++)
        map.set(score[i], i)
    score = score.sort((a,b)=>b-a)
    for(let i=0;i<score.length;i++)
        ans[map.get(score[i])] = i <= 2 ? SSP[i] : (i + 1) + ""
    return ans
};

```

### [575. 分糖果](https://leetcode.cn/problems/distribute-candies/description/)

```js
/**
 * @param {number[]} candyType
 * @return {number}
 */
var distributeCandies = function(candyType) {
    const set = new Set(candyType)
    return set.size > candyType.length / 2 ? candyType.length / 2 : set.size
};
```

### [724. 寻找数组的中心下标](https://leetcode.cn/problems/find-pivot-index/description/)

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var pivotIndex = function(nums) {
    if (nums.length === 1) return 0

    let index = 0
    while (index < nums.length) {
        const leftSum = nums.slice(0, index).length ? nums.slice(0, index).reduce((prev, curr) => prev + curr) : 0
        const rightSum = nums.slice(index + 1).length ? nums.slice(index + 1).reduce((prev, curr) => prev + curr) : 0
        if (leftSum === rightSum) return index
        index++
    }
    return -1
};
```

### [744. 寻找比目标字母大的最小字母](https://leetcode.cn/problems/find-smallest-letter-greater-than-target/description/)

```js
/**
 * @param {character[]} letters
 * @param {character} target
 * @return {character}
 */
var nextGreatestLetter = function(letters, target) {
    const first = letters.find(item => item > target)
    return first ? first : letters[0]
};
```

### [747. 至少是其他数字两倍的最大数](https://leetcode.cn/problems/largest-number-at-least-twice-of-others/description/)

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var dominantIndex = function(nums) {
    if (nums.length <= 1) return -1
    const tempNums = [...nums].sort((a, b) => b - a)
    if (tempNums[0] >= tempNums[1] * 2) {
        return nums.findIndex(item => item === tempNums[0])
    }
    return -1
};
```