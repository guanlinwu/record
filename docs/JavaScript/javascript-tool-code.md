#

## 获取url参数(hash 或者 search后的都能拿到)

```javascript
/**
 *  * {a:1,b:2,c:3} -> params(...) -> a=1&b=2&c=3
 * hash 或者 search后的都能拿到
 */
const toParams = () => {
  var url = window.location.search // 获取url中"?"符后的字串
  var hash = window.location.hash
  var queryIndex = hash.indexOf('?')
  if (queryIndex >= 0 && hash.slice(queryIndex + 1)) {
    url === ''
      ? (url += '?' + hash.slice(queryIndex + 1))
      : (url += '&' + hash.slice(queryIndex + 1))
  }
  var query = {}

  url && url.replace(/([^?&=]+)=([^&]+)/g, (_, k, v) => query[k] = v)
  return query
}
```

## 睡眠
```javascript
sleep (timeout) {
  return new Promise((resolve) => setTimeout(resolve, timeout))
}
```