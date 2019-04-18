# 题目描述

实现 strStr() 函数。
给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

### 说明:

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。
对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

### 示例

``` bash
输入: haystack = "hello", needle = "ll"
输出: 2

输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

# 思路1

转换成数组进行匹配，第一个匹配成功后开始循环输入的字符串。

``` bash
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
   if(!needle){
       return 0
   }
    haystack=haystack.split("")
    needle=needle.split("")
    for(let i=0;i<haystack.length;i++){
        if(haystack[i]==needle[0]){
            for(let j=0;j<needle.length;j++){
                if(haystack[i+j] != needle[j]){
                    break
                }
                if(j==needle.length - 1){
                    return i
                }
            }
        }
    }
    return -1
};
```

### 提交记录
执行用时 : 4948 ms, 在Implement strStr()的JavaScript提交中击败了6.17% 的用户
内存消耗 : 35.1 MB, 在Implement strStr()的JavaScript提交中击败了22.77% 的用户

# 思路2

优化一下循环，大大降低了执行时间

``` bash
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
   if(!needle){
       return 0
   }
    haystack=haystack.split("")
    needle=needle.split("")
    var i = 0,j=0
    while(i<haystack.length && j<needle.length){
        if(haystack[i]==needle[j]){
            i++
            j++
        }else{
            i = i+1-j
            j=0
        }
    }
    if(j == needle.length){
        return i-j
    }else{
        return -1
    }
};
```
