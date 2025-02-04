# API payouts (ВЫПЛАТЫ)

### URL: ```https://m2cerber.pythonanywhere.com/bot_api/```
### TEST URL: ```https://testm2cerber.pythonanywhere.com/bot_api/```

## Signature: 
```
payment_sum = float(payment_sum)
signature = hashlib.sha256(str(payment_id).encode('utf-8') + str(secret_key).encode('utf-8') +
            str(status).encode('utf-8') + str(payment_sum).encode('utf-8')).hexdigest()
return signature
```

### 1. New payout
   ```payout/```
   
   Method: ```POST```
   
   Data:
   ```
   {
   "payment_id": req (str),
   "payment_sum": req (str),
   "wallet_number": req (str),
   "status": "pending",
   "callback_url": "https://webhook.com/...",
   "merch_id": "1",
   "create_time": "2024-09-28 14:30:00"
   }
   ```

   Headers:
   ```
   {
   "Signature": signature
   }
   ```

   Return
   ```
   {
   "payment_id": 3636363,
   "status": "pending"
   }
   ```

### 2. Get status
   ```get_status/```
   
   Method: ```GET```
   
   Data:
   ```
   {
   "payment_id": req (str)
   }
   ```

   Headers:
   ```
   {
   "Signature": signature
   }
   ```

   Return
   ```
   {
   "payment_id": 3636363,
   "status": "pending"/"accept"/"cancel"
   }
   ```

### 3. Get Balance
   ```get_balance/```
   
   Method: ```GET```
   
   Data:
   ```
   {
   "merch_id": 1,
   "callback_url": Optional
   }
   ```

   Headers:
   ```
   {
   "Signature": signature
   }
   ```

   Return
   ```
   {
   "canceled": 350,
   "confirm": 2000,
   "pending": 1500
   }
   ```


## My webhooks
### 1. New status
    ```Payment callback_url```
   
   Method: ```POST```
   
   Data:
   ```
   {
   "status": "confirm"/"cancel",
   "payment_id": "1234"
   }
   ```

   Headers:
   ```
   {
   "Signature": signature
   }
   ```
