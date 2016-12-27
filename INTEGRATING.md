#Integrating to Monetary's Credit Gateway

###Submit the following transactions with the specified parameters:

####1. Sale Transaction
 * Track2: `4012000098765439=20121011796251900000`
 * Amount: `1.01` 

####2. Void Sale Transaction
 * RefNo: _`[Last Transaction Response RefNo]`_
 * Token: _`[Last Transaction Response Token]`_

####3. Sale Transaction
  * Account: `4012000098765439`
  * Expiration: `12/20`
  * Amount: `1.02`

####4. Adjust Transaction <sup>1</sup>
  * RefNo: _`[Last Transaction Response RefNo]`_
  * Token: _`[Last Transaction Response Token]`_

####5. Return Transaction
  * Account: `4012000098765439`
  * Expiration: `12/20`
  * Amount: `1.03`

####6. Void Return Transaction
  * RefNo: _`[Last Transaction Response RefNo]`_
  * Token: _`[Last Transaction Response Token]`_

####7. PreAuth Transaction <sup>2</sup>
  * Account: `4012000098765439`
  * Expiration: `12/20`
  * Amount: `1.03`
  
####8. Capture Transaction <sup>2</sup>
  * RefNo: _`[Last Transaction Response RefNo]`_
  * Token: _`[Last Transaction Response Token]`_
  * Amount: `1.03`
  * Tip: `1.00`

####9. AuthOnly Transaction
  * Account: `4012000098765439`
  * Expiration: `12/20`
  * Amount: `1.04`

<sup>1</sup> For merchant accounts supporting Sale/Adjust transactions.<br />
<sup>2</sup> For merchant accounts supporting PreAuth/Capture transactions. 
