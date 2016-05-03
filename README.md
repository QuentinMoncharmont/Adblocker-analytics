# At Internet solution + Adblocker (v 1.0)

How to measure an adblocker on your website with AT Internet analytics Solution

# Valid on

- Google Chrome
- Mozilla Firefox
- Internet Explorer (8+)
- Safari
- Opera

# Requierement

- Download the "fuckadblock.js" library : https://github.com/sitexw/FuckAdBlock
- Download the "smarttag.js" library : https://apps.atinternet-solutions.com/TagComposer/#/javascript

## Code example - Method 1 : Publisher impression

    <head>
      <script src="./js/smarttag.js"></script>
      <script src="./js/adblock/fuckadblock.js"></script>
    </head>
    
    //Footer
    //At Internet tracker initialization
    var tag = new ATInternet.Tracker.Tag();
    
    function AtInternet_Adblock_Impression() {
      tag.selfPromotion.send({
        impression:{
        adId : '1' }
      });
    }
		
    //Function from the "fuckadblock.js" library
    function adBlockDetected() {
        AtInternet_Adblock_Impression();
    }
		
    if(typeof fuckAdBlock === 'undefined') {
        adBlockDetected();
    }else{
        fuckAdBlock.onDetected(adBlockDetected).onNotDetected(adBlockNotDetected);
    }


# Analysis

## Method 1

If a visitor is navigating on your website with an adblocker, the "adBlockDetected();" function sends a publisher impression.

Benefits:
- The hit sent is independent of the page hit
- You could use a segment on this value
