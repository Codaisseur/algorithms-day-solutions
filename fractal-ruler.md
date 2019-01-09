A recursive solution always has an stop-condition. In this case, the problem describes the smallest ruler at length **1**. The definition of ruler is already recursive. So, we can translate the English definition to code like this:

```js
function ruler(n) {
    if (n === 1) {
        return '-'
    }
    return ruler(n-1) + '\n' + '-'.repeat(n) + '\n' + ruler(n-1)
}
```