
  
    
# Cashier API Use Cashier API to create ERC20 token order.    
    
**cautions:** the parameters required for `Authentication` will not be displayed repeated in each api intro, and the `Success Response` only show the data of the `Result`.    
    
## 1. Create cashier address Create an cashier address to receive token.    
    
**URL**: `/api/api/gen_eth_bill_addr`  
  
 **URL Parameters** :      
    
**Method**: `GET`    

 **Auth required**: YES    
    
**Example**: `https://www.94eth.com/api/api/gen_eth_bill_addr?account=1&timestamp=1559623671&key=fedd9a91-3bc3-44b1-85f6-d4d315acac28&encrypt=fadcdd8fddeaa08b5852ef8b917e367b&uniq=4509`    

 ### Success Response    
 **Content example**    
 
 ```json 
 { 
 } 
 ``` 

### Notes
    
 ## 2. List current cashier address List current cashier addresses.    
    
**URL**: `/api/api/load_eth_bill_addr`    

 **URL Parameters** :      
    
**Method**: `GET`    

 **Auth required**: YES    
    
**Example**: `https://www.94eth.com/api/api/load_eth_bill_addr?account=1&timestamp=1559623671&key=fedd9a91-3bc3-44b1-85f6-d4d315acac28&encrypt=3d25e631c3482288ff885663d48721eb&uniq=4510`    

 ### Success Response    
 
 **Content example**    
 ```json 
 { 
 } 
 ``` 

### Notes    

 ## 3. Create Order Create an order specifying the sender, token and amount.    
    
**URL** : `/api/api/gen_order?`    

 **URL Parameters** : `token=[token addr]&amount=[amount in gwei]&sender=[sender addr]&urls=[notify urls]` **Method** : `GET`    
 
 **Auth required** : YES    
    
**Example**: `https://www.94eth.com/api/api/gen_order?token=0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6&amount=400000000&sender=0xc713Ad7305Ec2EB9d8D7654190ac359293A22968&secret=test1&account=1&timestamp=1559622161&key=fedd9a91-3bc3-44b1-85f6-d4d315acac28&encrypt=027a1dea4ea1f066662f526d15a9a674&uniq=8074&urls=%5B%22https%3A%2F%2Fwww.baidu.com%22%2C%22https%3A%2F%2Fwww.google.com%22%5D`   
  
### Success Response    

 **Content example**    
 ```json 
{  
    "id": 728, 
    "receiver": "0xab5ba34351cd3d0bae440998d5837347e6525e9a", 
    "start": 7891522, 
    "end": 9421522, 
    "status": 0, 
    "network": "main"
} 
 ```
 
### Notes 

* token : `the token you want to receive`  

* sender: `the sender address who will pay the order`  

* amount: `the amount of token in this order including the decimals, so it should be 10000 if the order is only 1 token and the decimals is 4`  

* secret: `any thing you want to mark this order`  

* urls: `a list of urls that need to be notified when the order is finished, use serialized json array format  and url encoded it`  

* the urls will not be guaranteed to be called (usually it will be called), not be guaranteed to be called only once.   

* successful order creation will return the order **id**,  then you can lead the user to page 

   * EN https://www.94eth.com/api/orderen/?o=[id]&r=[r]
   * ZH https://www.94eth.com/api/ordercn/?o=[id]&r=[r]
   
   in which **id** is the order id, **r** is the redirect page when order finished (make sure the **encodeURIComponent** the url)
   
* YOU MUST CALL **ORDER STATUS** TO MAKE SURE The order is finished, only just by the notifying url  
  
## 4. Order Info get the creation info of specified order    
    
**URL** : `/api/api/public_order_info`    

 **URL Parameters** : `order=[order_id]` **Method** : `GET`    
 
 **Auth required** : NO    
    
**Example**: `https://www.94eth.com/api/api/public_order_info?order=1`    

 ### Success Response    
 
 **Content example**    
 ```json 
{    
  "id": 1,    
  "token": "0x255aa6df07540cb5d3d297f0d0d4d84cb52bc8e6",    
  "gen_time": "2019-05-03T08:33:49.000Z",    
  "receiver": "0xab5ba34351cd3d0bae440998d5837347e6525e9a",    
  "amount": 400000000,    
  "filled": 10000000000000000,    
  "sender": "0xc713ad7305ec2eb9d8d7654190ac359293a22968",    
  "status": 1,    
  "account": 1,    
  "network": "main",    
  "tokenName": "RDN",    
  "decimals": "18" 
} 
``` 

### Notes 

Comparing to `Order Status`, `Order Info` get token name and token decimals from the chain, so it's a little bit slower than `Order Status`    

 ## 5. Order Status get the creation info of specified order    
    
**URL** : `/api/api/public_order_status` 
  
 **URL Parameters** : `order=[order_id]` **Method** : `GET`    
 
 **Auth required** : NO    
    
**Example**: `https://www.94eth.com/api/api/public_order_status?order=1`    

 ### Success Response    
 
 **Content example**    
 
 ```json 
 {    
  "id": 1,    
  "token": "0x255aa6df07540cb5d3d297f0d0d4d84cb52bc8e6",    
  "gen_time": "2019-05-03T08:33:49.000Z",    
  "receiver": "0xab5ba34351cd3d0bae440998d5837347e6525e9a",    
  "amount": 400000000,    
  "filled": 10000000000000000,    
  "sender": "0xc713ad7305ec2eb9d8d7654190ac359293a22968",    
  "status": 1,    
  "account": 1,    
  "network": "main",    
  "block": 7890816 
} 
``` 

### Notes    

 ## 5. Order Detail get the creation info of specified order    
    
**URL** : `/api/api/publicOrderDetails`  
  
 **URL Parameters** : `order=[order_id]` **Method** : `GET`    
 
 **Auth required** : NO    
    
**Example**: `https://www.94eth.com/api/api/publicOrderDetails?order=1`    

 ### Success Response    
 
 **Content example**    
 ```json 
 {    
 } 
 ``` 

### Notes 

not supported yet