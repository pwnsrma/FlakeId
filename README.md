# FlakeId
Twittter Snowflake like unique id generator plugin for nodejs and browser implemented in js.

FlakeId takes 42 bit of timestamp, 10 bit of machine id (or any random number you provide), 12 bit of sequence number .  As javascript is limited to 53 bit integer precision, FlakeId generates id in string format like "285124269753503744", which can be easily type casted into 64 bit bigint in database.

# Installation

For Node
```js
npm install flakeid
```

For Browser
Include js file
```html
<script src="flakeid.js"></script>
```

# Usage
Initializtion
```js
var FlakeId = require('flakeid'); /* on node js only */

//initiate flake
var flake = new FlakeId({
	mid : 42, //optional, define machine id
    timeOffset : (2013-1970)*31536000*1000 //optional, define a offset time
});
```
Create a instance of flake as shown above which will be used to generate flake ids afterward.

Id generation
```js
var id1 = flake.gen(); \\returns something like 285124269753503744
var id2 = falke.gen(); \\returns something like 285124417543999488
```

# Options

mid : (Default to 1) A machine id or any random id. If you are generating id in distributed system, its highly advised to provide a proper mid which is unique to different machines.

timeOffset : (Defaults to 0) Time offset will be  subtracted from current time to get the first 42 bit of id. This help in generating smaller ids.

# Method
gen : Method to generate id from FlakeId instance.

------
As js have 53bit integer precision, Flake Id uses a smart solution by Dan Vanderkam (http://www.danvk.org/hex2dec.html) to convert hex to decimal without loosing precision. 
*Source code for converting hex to decimal is taken from http://www.danvk.org/hex2dec.html which have APACHE LICENCE*
