# General

[https://en.wikipedia.org/wiki/Video_file_format](https://en.wikipedia.org/wiki/Video_file_format)

1. `HTML Video (Flash Video)`

2. `HTML5 Video`

# Browsers

- IE (Internet Explorer): IE (6, 7, 8, 9, 10, 11), Edge
- Firefox
- Chrome
- Opera
- Safari

# OS Devices
- Windows: Windows 2000, Windows XP, Windows Vista, Windows 7, Windows 8, Windows 10
- Mac/iOS: Mac, iPhone, iPad, iPod
- Android
- Unknown

```JS
// Check OS name
var checkOSname = function () {
    if (window.navigator.userAgent.indexOf("Windows NT 10.0") != -1)
        return "Windows 10";
    if (window.navigator.userAgent.indexOf("Windows NT 6.2") != -1)
        return "Windows 8";
    if (window.navigator.userAgent.indexOf("Windows NT 6.1") != -1)
        return "Windows 7";
    if (window.navigator.userAgent.indexOf("Windows NT 6.0") != -1)
        return "Windows Vista";
    if (window.navigator.userAgent.indexOf("Windows NT 5.1") != -1)
        return "Windows XP";
    if (window.navigator.userAgent.indexOf("Windows NT 5.0") != -1)
        return "Windows 2000";
    if (
        window.navigator.userAgent.indexOf("Mac") != -1 ||
        window.navigator.userAgent.indexOf("iPhone") != -1 ||
        window.navigator.userAgent.indexOf("iPad") != -1 ||
        window.navigator.userAgent.indexOf("iPod") != -1
    )
        return "Mac/iOS";
    if (window.navigator.userAgent.indexOf("Android") != -1) return "Android";
    
    return "Unknown";
};
````

```JS
// Check Browser
var checkBrowser = function() {
    // Return cached result if avalible, else get result then cache it.
    if (checkBrowser.prototype._cachedResult)
    return checkBrowser.prototype._cachedResult;

    // Opera 8.0+
    var isOpera =
        (!!window.opr && !!opr.addons) ||
        !!window.opera ||
        navigator.userAgent.indexOf(" OPR/") >= 0;

    // Firefox 1.0+
    var isFirefox = typeof InstallTrigger !== "undefined";

    // Safari 3.0+ "[object HTMLElementConstructor]"
    var isSafari =
        /constructor/i.test(window.HTMLElement) ||
        (function(p) {
        return p.toString() === "[object SafariRemoteNotification]";
        })(!window["safari"] || safari.pushNotification);

    // Internet Explorer 6-11
    var isIE = /*@cc_on!@*/ false || !!document.documentMode;

    // Edge 20+
    var isEdge = !isIE && !!window.StyleMedia;

    // Chrome 1+
    var isChrome = !!window.chrome;

    return (checkBrowser.prototype._cachedResult = isOpera ? "Opera" : isFirefox ? "Firefox" : isSafari ? "Safari" : isChrome ? "Chrome" : isIE ? "IE" : isEdge ? "Edge" : "Unknown");
};
```

```JS
// Check IE version
var checkVersionOfIE = function() {
    var sAgent = window.navigator.userAgent;
    var Idx = sAgent.indexOf("MSIE");

    // If IE, return version number.
    if (Idx > 0)
        return parseInt(sAgent.substring(Idx + 5, sAgent.indexOf(".", Idx)));
    // If IE 11 then look for Updated user agent string.
    else if (!!navigator.userAgent.match(/Trident\/7\./)) return 11;
    else return 0; //It is not IE
};
```

# Formats

### List formats
- .mp4
- .webm (WebM) - PV8, PV9
- .ogv (Ogg Video)
- .mov (QuickTime)
- .wmv (Windows Media Video)
- .flv (Flash Video)
- .avi (AVI)

__`HTML5 <video />:`__
- H.264 (.mp4, .mov) (type="video/mp4"): Supported by: IE 9, Safari 3.1, and Chrome (for now)
- VP8 (WebM) (.webm) (type="video/webm"): Supported by: Firefox 4.0, Chrome 6.0, Opera 10.6.
- Ogg Theora (.ogv) (type="video/ogg"): Supported by: Firefox 3.5, Chrome 4, Opera 10.5


# Video on Devices (Desktop/OS, Mobile) and Browser

### HTML (Adobe Flash)

- Many video hosting options: own server, YouTube, Vimeo, etc
- Support by all desktop browsers: Internet Explorer, Firefox, Chrome, Opera, Safari

- Flash plug-in is a must
- Constant plug-in updates
- Slow, high-load videos
- No video playback on mobiles like iPad and iPhone

### HTML5:

- Works on both desktop and mobile devices
- Flexible player settings: users can move and rotate web players

- Not supported by Internet Explorer 6, 7, 8
- Requires video conversion
