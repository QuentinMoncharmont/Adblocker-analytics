# AT Internet solution + Adblocker (v 1.0)

How to measure an adblocker on your website with AT Internet Analytics Solution

# Valid on

- Google Chrome
- Mozilla Firefox
- Internet Explorer (8+)
- Safari
- Opera

# Requierements

- Download the "fuckadblock.js" library : https://github.com/sitexw/FuckAdBlock
- Download the "smarttag.js" library : https://apps.atinternet-solutions.com/TagComposer/#/javascript

## Code example

### 1 - Initialization

    <head>
      <script src="./js/smarttag.js"></script>
      <script src="./js/adblock/fuckadblock.js"></script>
    </head>
    
    //Footer
    //At Internet tracker initialization
    var tag = new ATInternet.Tracker.Tag();
    
### 2 - Method 1 : Publisher impression function

    function AtInternet_Adblock_hit() {
      tag.publisher.send({
		impression:{
			campaignId : '[adblock]',
			creation : '[detection]',
			url : '[/tests/detection-adblock.html]'
		}
	});
    }
    
### 2 - Method 2 : Click function
    
     function AtInternet_Adblock_hit(value) {
     
     	return tag.click.send({
     		elem:element, // DOM element given
     		name:'adblock', 
     		chapter1:'adblock', 
     		chapter2:"'" + value + "'", 
     		level2:'1', //Your level 2 click
      		type:'action', 
      	});
    }

### 3 - "fuckadblock.js" functions
		
    //Function from the "fuckadblock.js" library
    function adBlockDetected() {
    	//Method 2.1 - Publisher impression function
        AtInternet_Adblock_hit();
        
        //or Method 2.2 - Click
        AtInternet_Adblock_hit("detected");
    }
    
    function adBlockNotDetected() {
	//Method 2.2 - Click
        AtInternet_Adblock_hit("not_detected");
    }
		
    if(typeof fuckAdBlock === 'undefined') {
        adBlockDetected();
    }else{
        fuckAdBlock.onDetected(adBlockDetected).onNotDetected(adBlockNotDetected);
    }


# Analysis

### Method 1

If a visitor is navigating on your website with an adblocker, the "adBlockDetected();" function sends a publisher impression.

Benefits:
- Automatic campaign (no need to declare this campaign).
- The impression hit sent is independent from the page hit (no risk of losing some page data).
- Possibility to apply a specific segment based on this campaign (to understand the different behaviour of these visitors).


### More explanation

See the .pdf file : AT-Internet-results.pdf (https://github.com/QuentinMoncharmont/Adblocker-analytics/blob/master/AT-Internet-results.pdf)

Or example files : Example.zip (https://github.com/QuentinMoncharmont/Adblocker-analytics/blob/master/example.zip)


### Method 2

With a click function it is possible to know if the visitor is navigating with or without an adblocker. In comparaison to the first method, "AtInternet_Adblock_hit(value)" method (which send a hit click) waits one parameter (value "detected" or "not_detected").

Benefits:
- Event click (no setting requiered).
- The impression hit sent is independent from the page hit (no risk of losing some page data).
- Possibility to apply a specific segment based on this campaign (to understand the different behaviour of these visitors).


