---
title: Javascript | Generate a product key.
description: Javascript | Generate a product key.
header: Javascript | Generate a product key.
---
Generating a product key in JavaScript is a matter of creating random segments from a given string.

This is solution helpful to you. We can implement the following solution:

``` javascript
(function() {
	function getRandomInt( min, max ) {
         return Math.floor( Math.random() * ( max - min + 1 ) ) + min;
    }
    
	function generateProductKey() {
		var tokens = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789",
			chars = 5,
			segments = 4,
			keyString = "";
			
		for( var i = 0; i < segments; i++ ) {
			var segment = "";
			
			for( var j = 0; j < chars; j++ ) {
			    var k = getRandomInt( 0, 35 );
				segment += tokens[ k ];
			}
			
			keyString += segment;
			
			if( i < ( segments - 1 ) ) {
				keyString += "-";
			}
		}
		
		return keyString;

	}
})();

```
## How to use??

``` javascript
console.log( generateProductKey() );
	
//Output: GHT78-L2H2M-9U3WF-CYBF2

```