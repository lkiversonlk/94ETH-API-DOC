
# Authentication 
The authentication of 94ETH API.

## 1.  Account Id
please register in https://www.94eth.com/api to get an Account id.
### Notes
Currently we only support QQ Oauth, Will support Github soon.

## 2. Key & Secret
After login, click to generate a new API key & secret.
### Notes
The secret will only show when it's created, please keep it in a safe place.
Generating new Key&Secret will deprecate the previous one.

## 3. API Auth
Use AccountId, Key and Secret to encrypt API request

**URL** : `ANY`

**URL Parameters** : `account=[account id]&timestamp=[UTC timeoffset]&key=[public key]&encrypt=[encrypted part]&uniq=[uniq number]` 

**Method** : `ANY`

**Example**: `https://www.94eth.com/api/api/gen_order?token=0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6&amount=400000000&sender=0xc713Ad7305Ec2EB9d8D7654190ac359293A22968&secret=test1&account=1&timestamp=1559622161&key=fedd9a91-3bc3-44b1-85f6-d4d315acac28&encrypt=027a1dea4ea1f066662f526d15a9a674&uniq=8074`

### Steps

for example, try to call `https://www.94eth.com/api/api/gen_order`

1. The host is https://www.94eth.com/api

2.  The **path** to encrypt is /api/gen_order   **prev /api excluded**

3. The query parameter required by Auth is:
	* account: `accoun id`
	* timestamp: `currrent UTC timestamp`
	* key: `the public key`
	* encrypt: `fill in the secret at first`
	* uniq: `an uniq number that should repeat in api calls within 10 minutes`
	
4.  Append the auth parameters to the parameters that required by the API itself (sequence doesn't matter)

5. The original content to encrypted it **[path][queries]**:
        example: 
        `/api/gen_ordertoken=0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6&amount=400000000&sender=0xc713Ad7305Ec2EB9d8D7654190ac359293A22968&secret=test1&account=1&timestamp=1559626144&key=fedd9a91-3bc3-44b1-85f6-d4d315acac28&encrypt=[secret]&uniq=6502`

6. **MD5(original content)** to get encrypted data: `027a1dea4ea1f066662f526d15a9a674`

7. Replace the [encrypt] in the `Auth Parameters` with **encrypted data**

8. Now you can call the API by
   `https://www.94eth.com/api/api/gen_order?token=0x255Aa6DF07540Cb5d3d297f0D0D4D84cb52bc8e6&amount=400000000&sender=0xc713Ad7305Ec2EB9d8D7654190ac359293A22968&secret=test1&account=1&timestamp=1559626144&key=fedd9a91-3bc3-44b1-85f6-d4d315acac28&encrypt=0670777ca4d02806f24df310a138c71a&uniq=6502`