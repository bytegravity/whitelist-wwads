#### [万维广告](https://wwads.cn) 网站流量主专用

![image](https://user-images.githubusercontent.com/4530539/126099207-04e4add7-4a71-4721-8f3f-750b33bfcc36.png)

以下 Javascript 代码（可放置在广告加载页面底部的 script 标签中）会检测万维广告的广告请求（函数名为“_AdBlockInit”）是否被 AdBlockPlus 等广告拦截器拦截，如果被拦截，则向访客展示页面顶部的提示加入广告拦截器白名单的通知条（如上图），查看 [示例站点](https://zhaodao.ai)（需要先开启广告拦截器查看效果）。你也可以根据需要自行修改代码。


```
// function called if wwads is blocked
function ABDetected() {
  var adBlockDetected_div = document.createElement("div");
  adBlockDetected_div.style.cssText = "position: absolute; top: 0; left: 0; width: 100%; background: #fc6600; color: #fff; z-index: 9999999999; font-size: 14px; text-align: center; line-height: 1.5; font-weight: bold; padding-top: 6px; padding-bottom: 6px;";
  adBlockDetected_div.innerHTML = "我们的广告服务商 <a style='color:#fff;text-decoration:underline' target='_blank' href='https://wwads.cn/page/end-user-privacy'>并不跟踪您的隐私</a>，为了支持本站的长期运营，请将我们的网站 <a style='color: #fff;text-decoration:underline' target='_blank' href='https://wwads.cn/page/whitelist-wwads'>加入广告拦截器的白名单</a>。";
  document.getElementsByTagName("body")[0].appendChild(adBlockDetected_div);
  // add a close button to the right side of the div
  var adBlockDetected_close = document.createElement("div");
  adBlockDetected_close.style.cssText = "position: absolute; top: 0; right: 10px; width: 30px; height: 30px; background: #fc6600; color: #fff; z-index: 9999999999; line-height: 30px; cursor: pointer;";
  adBlockDetected_close.innerHTML = "×";
  adBlockDetected_div.appendChild(adBlockDetected_close);
  // add a click event to the close button
  adBlockDetected_close.onclick = function() {
  this.parentNode.parentNode.removeChild(this.parentNode);
  };
};

function docReady(t) {
    "complete" === document.readyState ||
    "interactive" === document.readyState
      ? setTimeout(t, 1)
      : document.addEventListener("DOMContentLoaded", t);
}

//check if wwads' fire function was blocked after document is ready with 3s timeout (waiting the ad loading)
docReady(function () {
  setTimeout(function () {
    if( window._AdBlockInit === undefined ){
        ABDetected();
    }
  }, 3000);
});

```

