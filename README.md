**# Wombo-Dream-Web-Resizer**

Tampermonkey boilerplate script that resizes the image in the preview as a 16x9 resolution aspect ratio instead of being smushed together assuming it's a phone resolution on the web. 

**Without Script:**

![image](https://github.com/lofihippo/Wombo-Dream-Web-Resizer/assets/130268671/1093f769-4b60-4013-a34d-bee1e109e86c)

**With Script:**

![image](https://github.com/lofihippo/Wombo-Dream-Web-Resizer/assets/130268671/658ab10d-7084-46b6-82a8-d0562cb51c20)

To run, download the Firefox extension Tampermonkey (or comporable alternative that allows for user scripting)
Location on Firefox Add-Ons: https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/

Once installed in Firefox, click on the Tampermonkey extension icon, and click on "Create a new script..."

Once you have the Editor open, paste the script: 
(You can also copy the script from the Nekobin here https://nekobin.com/gewibalote or in the userscript.txt file in this GitHub repository)

```javascript
// ==UserScript==
// @name        DreamAI Image Resizer
// @namespace   https://www.dream.ai/
// @description This script resizes images to their natural dimensions on DreamAI websites.
// @match     *://*.dream.ai/listing*
// @version     1.0
// @grant       none
// @run-at      document-start
// ==/UserScript==

(function() {
    let aspectRatio = 1920 / 1080;

    // function to resize the trading_card image
    function resizeImage() {
        let img = document.querySelector('img[alt="trading_card"]');
        if (img) {
            let container = img.parentElement; // assuming image is wrapped in a container
            container.style.maxWidth = '100%';
            container.style.height = (container.offsetWidth / aspectRatio) + 'px';
        }
    }

    // create a MutationObserver instance to watch for changes in the DOM
    let observer = new MutationObserver(function(mutations) {
        mutations.forEach(function(mutation) {
            if (mutation.type === 'childList') {
                resizeImage();
            }
        });
    });

    // start observing the document with the configured parameters
    observer.observe(document.body, { attributes: true, childList: true, subtree: true });
})();
```
**Future suggestions or possible changes**

This is just a boilerplate script that shows it can be resized. I'm not experienced enough with scripting/css to accurately change it so the bounding box around the resized image, is properly scaled up to make the overall image shown larger. 

If someone wants to modify it and also support other aspect ratios and image sizes than 16x9 and 1920x1080p, that would be awesome. 
