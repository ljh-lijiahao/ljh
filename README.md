<head>
  <meta charset="utf-8">
 
  <title>召唤神龙</title>
 
  <!--http://www.html5rocks.com/en/mobile/mobifying/-->
  <meta name="viewport"
        content="width=device-width,user-scalable=no,initial-scale=1, minimum-scale=1,maximum-scale=1"/>
 
  <!--https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html-->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="format-detection" content="telephone=no">
 
  <!-- force webkit on 360 -->
  <meta name="renderer" content="webkit"/>
  <meta name="force-rendering" content="webkit"/>
  <!-- force edge on IE -->
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
  <meta name="msapplication-tap-highlight" content="no">
 
  <!-- force full screen on some browser -->
  <meta name="full-screen" content="yes"/>
  <meta name="x5-fullscreen" content="true"/>
  <meta name="360-fullscreen" content="true"/>
  
  <!-- force screen orientation on some browser -->
  <meta name="screen-orientation" content=""/>
  <meta name="x5-orientation" content="">
 
  <!--fix fireball/issues/3568 -->
  <!--<meta name="browsermode" content="application">-->
  <meta name="x5-page-mode" content="app">
 
  <!--<link rel="apple-touch-icon" href=".png" />-->
  <!--<link rel="apple-touch-icon-precomposed" href=".png" />-->
  
  
    <!-- <script>
        pushHistory();
        window.addEventListener("popstate", function(e) {
        }, false);
        function pushHistory() {
            var state = {
                title: "",
                url: window.location.href
            };
            window.history.pushState(state, state.title, state.url);
        }
    </script> -->
 
  <link rel="stylesheet" type="text/css" href="style-mobile.css"/>
 
</head>
<!-- <body style="margin: 0; background: #ddd;" align="center"> -->
  <div style="align:center;display: none">< img src="res/share.png" width="10%" /></div>
  
  <!-- <div id="canvasDiv" style="width:100%;height:100%;">
  </div>  -->
  <canvas id="GameCanvas" oncontextmenu="event.preventDefault()" tabindex="0" ></canvas>
 
  <video id="contentElement" style = "display:none;position: absolute;top:0px;left: 0px;">
            <!-- <source src="http://rmcdn.2mdn.net/Demo/vast_inspector/android.mp4"></source>
            <source src="http://rmcdn.2mdn.net/Demo/vast_inspector/android.webm"></source> -->
  </video> 
  <div id="block-Box" style="display:block;width:100%;height:100%;"></div>
  
  
 
 <div id="adContainer" style="display:none;position: absolute;top:0px;left: 0px;width:100%;height:100%;z-index:999;"></div> 
 <div id="loadingText"
 style="width:100%;display: none;text-align:center;position:absolute;top:45%;z-index:2;font-size:20px;color:#f99f0a">
 loading......0%
</div>
 
  <div id="splash">
      <!-- <div class="progress-bar stripes"> -->
        <!-- <span style="width: 0%"></span> -->
      <!-- </div> -->
   </div>
 
   <div id="loadingImg" style="top:45%;width: 100%;position:absolute; ">
    < img src="res/loading.gif" width="7%" height="7%" />
  </div>
  
     <!-- 判断浏览器是否屏蔽广告 -->
  <script src="http://demo.jb51.net/js/2015/adview_pic_cpc_cpm_cpa_guanggao_gg_ads_300x250.js" type="text/javascript"></script> 
 <script type="text/javascript">
 
  var killAdT = typeof(killads);
  // <!-- if (typeof(killads)=='undefined'){ -->
  //  <!-- alert('广告被过滤'); -->
  //  <!-- } -->
 </script>
   
  
  
  
<!--<div align="center" style="font-size: 10px;color: dimgrey">advertisement</div>-->
 
<script type="text/javascript" src="//imasdk.googleapis.com/js/sdkloader/ima3.js"></script>
<script type="text/javascript" src="ads.js"></script>
 
<script src="src/settings.js" charset="utf-8"></script>
 
<script type="text/javascript">
 
 var preloader;
    var adCompleteFlag = false;
    var resCompleteFlag = false;
 
    var adEndComplete = false;
    var resEndComplete = false;
 
 judgeLanTitle();
    function judgeLanTitle(){
 
//        console.log("window.navigator.language",window.navigator.language);
 
        if( window.navigator.language=="zh-CN" ||window.navigator.language=="zh-cn"){
            document.title = "召唤神龙";
        }else  if(window.navigator.language == "zh-TW" ){
            document.title = "召喚神龍";
        }else  if(window.navigator.language == "zh-HK" ){
            document.title = "召喚神龍";
        }else  if(window.navigator.language == "ko-KR"){
            document.title = "신용 소환";
        }else  if(window.navigator.language == "ja-JP"){
            document.title = "神竜を召喚する";
        }else  if(window.navigator.language == "th-TH"){
            document.title = "เรียกมังกร";
        }else{
            document.title = "Summon the Dragon";
        }
    }
 
    var loadintT = document.getElementById("loadingText");
    var loadintGif = document.getElementById("loadingImg")
    setTimeout(function () {
      loadintGif.remove();
      loadintT.style.display = ""
      updateLabView(0.1);
    }, 1 * 1000)
 
    window.timer = null;
    window.tempSeconds = 1;
    window.loadData = {};
    loadData.completedCount = 0;
    loadData.totalCount = 0;
 
  onload();
 function onload()  {
       var winHeight = document.documentElement.clientHeight;
       document.getElementById("canvasDiv").style.height = winHeight+"px";
  }; 
 window.onload =function() {
       document.getElementById("block-Box").style.display = "none";
 }
 
 function updateLabView(t) {
      if (timer != null) {
        clearInterval(timer);
      }
      timer = setInterval(function () {
        tempSeconds++;
        actualTotal();
        var loadintT = document.getElementById("loadingText")
        if(!loadintT){
          // clearInterval(timer);
          return;
        }
 
        loadintT.innerHTML = 'loading......' + parseInt(tempSeconds) + '%';
 
        switch (tempSeconds) {
          case 20:
            updateLabView(0.2);
            break;
          case 40:
            updateLabView(0.3);
            break;
          case 60:
            updateLabView(0.4);
            break;
          case 96:
            updateLabView(5);
            break;
          case 97:
            updateLabView(10);
            break;
          case 98:
            updateLabView(50);
            break;
          case 99:
            updateLabView(100);
            break;
          default:
            if (tempSeconds >= 80 && tempSeconds < 96) {
              updateLabView(t + 0.1);
            }
            break;
        }
        if (tempSeconds > 100) {
          clearInterval(timer);
          tempSeconds = 100
          loadintT.innerHTML = 'loading......' + parseInt(tempSeconds) + '%';
        }
      }, t * 1000);
    }
 
    function actualTotal() {
      var percent = parseInt(100 * loadData.completedCount / loadData.totalCount);
      if (percent > tempSeconds && loadData.totalCount > 1) {
        tempSeconds = percent;
      }
    }
 
 
</script>
  
  
  
  
  
<script src="src/settings.js" charset="utf-8"></script>
 
<script src="main.js" charset="utf-8"></script>
 
 
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<!-- 水工厂 -->
<!-- <ins class="adsbygoogle"
      style="position:absolute;border-top:5px #f0f0f1 solid;background:#f0f0f1;bottom:0px;z-index:1000;display:inline-block;min-width:320px;max-width:970px;width:100%;height:60px"
     data-ad-client="ca-pub-3932234672445376"
     data-ad-slot="1751302463"></ins>
<script>
      var ads = document.getElementsByClassName('adsbygoogle')[0];
      if (document.body.clientHeight > 700){
          ads.style.height = 80+'px';
      }else{
          ads.style.height = 60+'px';
      }
</script>
<script>
    function ShowBannerAD(){
      (adsbygoogle = window.adsbygoogle || []).push({});
    }
</script> -->
<!-- 果盘合合 -->
<script async
        data-ad-client="ca-pub-3932234672445376"
        data-ad-channel="1828757928"
      data-ad-frequency-hint="15s"
        src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js">
</script>
 
<script>window.adsbygoogle = window.adsbygoogle || [];
const adBreak =  function(o) {adsbygoogle.push(o);}
</script>
 
 
<script type="text/javascript">
 
(function () {
    // open web debugger console
    if (typeof VConsole !== 'undefined') {
        window.vConsole = new VConsole();
    }
 
    var debug = window._CCSettings.debug;
    var splash = document.getElementById('splash');
    splash.style.display = 'block';
 
    function loadScript (moduleName, cb) {
      function scriptLoaded () {
          document.body.removeChild(domScript);
          domScript.removeEventListener('load', scriptLoaded, false);
          cb && cb();
      };
      var domScript = document.createElement('script');
      domScript.async = true;
      domScript.src = moduleName;
      domScript.addEventListener('load', scriptLoaded, false);
      document.body.appendChild(domScript);
    }
 
    loadScript(debug ? 'cocos2d-js.js' : 'cocos2d-js-min.js', function () {
      if (CC_PHYSICS_BUILTIN || CC_PHYSICS_CANNON) {
        loadScript(debug ? 'physics.js' : 'physics-min.js', window.boot);
      }
      else {
        window.boot();
      }
    });
})();
 
 
</script>
</body>
