A fix for the iOS orientationchange zoom bug.
=======================

Authored by @scottjehl, rebounded by @wilto.
MIT / GPLv2 License.

Demo: http://scottjehl.github.com/iOS-Orientationchange-Fix/

Minified src:

	/*! A fix for the iOS orientationchange zoom bug. Script by @scottjehl, rebound by @wilto. MIT / GPLv2 License.*/(function(w){var ua=navigator.userAgent;if(!(/iPhone|iPad|iPod/.test(navigator.platform)&&/OS [1-5]_[0-9_]* like Mac OS X/i.test(ua)&&ua.indexOf("AppleWebKit")>-1)){return;}var doc=w.document;if(!doc.querySelector){return;}var meta=doc.querySelector("meta[name=viewport]"),initialContent=meta&&meta.getAttribute("content"),enabled=true,x,y,z,aig;if(!meta){return;}function restoreZoom(){meta.setAttribute("content",initialContent.replace(/minimum\-scale[ =0-9\.]*/gi,"minimum-scale=.25").replace(/maximum\-scale[ =0-9\.]*/gi,"maximum-scale=10").replace(/user\-scalable[ =]*no/gi,"user-scalable=1"));enabled=true;}function disableZoom(){meta.setAttribute("content",initialContent.replace(/minimum\-scale[ =0-9\.]*/gi,"minimum-scale=1").replace(/maximum\-scale[ =0-9\.]*/gi,"maximum-scale=1").replace(/user\-scalable[ =]*no/gi,"user-scalable=0"));enabled=false;}function checkTilt(e){aig=e.accelerationIncludingGravity;x=Math.abs(aig.x);y=Math.abs(aig.y);z=Math.abs(aig.z);if((!w.orientation||w.orientation===180)&&(x>7||((z>6&&y<8||z<8&&y>6)&&x>5))){if(enabled){disableZoom();}}else if(!enabled){restoreZoom();}}w.addEventListener("orientationchange",restoreZoom,false);w.addEventListener("devicemotion",checkTilt,false);})(this);
Instructions: 
Include the script, enable your zooms. (I'll fill that out more later...).

How it works:
This fix works by listening to the device's accelerometer to predict when an orientation change is about to occur. When it deems an orientation change imminent, the script disables user zooming, allowing the orientation change to occur properly, with zooming disabled. The script restores zoom again once the device is either oriented close to upright, or after its orientation has changed. This way, user zooming is never disabled while the page is in use.
