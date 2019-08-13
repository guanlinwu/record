
# 页面返回

## 针对IOS，页面返回后，不刷新的解决方案
```javascript
 var isPageHide = false
  window.addEventListener('pageshow', function () {
    if (isPageHide) {
      console.log('pageshow')
      window.location.reload()
    }
  })
  window.addEventListener('pagehide', function () {
    isPageHide = true
  })
```