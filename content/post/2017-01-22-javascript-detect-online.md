---
title: "JavaScript: How to detect online status in browser"
date: 2017-01-22
draft: false
tags: [JavaScript]
---

Sometimes we need to check whether the user is online. In today's world, more than billion people are online, but not everyone has a better internet connection; so there is a nice feature in modern browsers that we can cache the data in the browser's local storage so next time the user visits, there is no need to download the data again.


> The browsers provide `navigator` property that will help us to find the
> online status of the user.

The `navigator.onLine` property return a Boolean value with respect of whether or not the user is connected to the internet.

``` javascript
    if(navigator.onLine) {
        // do your operation
    }
```


The browser provides events too, means the the event is triggerd as soon as the browser detects that the user is online.

``` javascript
    window.addEventListener('online',  takeOnlineAction);
    window.addEventListener('offline', takeOfflineAction);
```

The `takeOnlineAction` function executes when the browser detect internet connection and same for `takeOfflineAction`.

Here is a demo

<iframe
  style="width: 100%; height: 300px"
  frameborder="0"
  src="https://jsfiddle.net/vikramcse/wuL4pffr/embedded/">
</iframe>
