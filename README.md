# API paymetns (ПРИЕМ)

### URL: ```https://m2cerber.pythonanywhere.com/bot_api/```
### TEST URL: ```https://testm2cerber.pythonanywhere.com/bot_api/```

### 1. Get wallet
   ```get_wallet/```
   
   Method: ```POST```
   
   Data:
   ```
   {
   "payment_id": req (str),
   "user_wallet": req (str),
   "sum": req (str),
   "status": "pending",
   "callback_url": req,
   "merch_id": req (str),
   "create_time": req (str)
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
   "wallet_link": "https://m10.com/...",
   "image": b"...",
   "wallet_number": "9378238289"
   }
   ```


### 2. Update status
   ```update_status/```

   If user send money status = "accept", else status = "cancel"

   Method: ```POST```
   
   Data:
   ```
   {
   "payment_id": req (str),
   "status": red (str)
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
   "paymnet_id": 3636363,
   "status": "confirming"
   }
```

### 3. Get status
   ```get_status/```

   Method: ```GET```
   
   Data:
   ```
   {
   "payment_id": req (str),
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
   "status": "confirming"/"pending"/"accept"/"cancel"
   }
```

### 4. Get balance
   ```get_balance/```

   If start_date and end_date is null - you will get balance for all time.

   Method: ```GET```
   
   Data:
   ```
   {
   "merch_id": req (str),
   "start_date": optional (str),
   "end_date": optional (str),
   "callback_url": Optional
   }
```

   Headers:
   ```
   {
   "Signature": signature_balance
   }
```

   Return
   ```
   {
   "canceled_sum": 350,
   "confirm_sum": 2000,
   "pending_sum": 1500
   }
```


## My webhooks
### 1. Accept payment

   Method: ```POST```
   
   Data:
   ```
   {
   'status': 'confirm',
   'payment_id': '3636363',
   'confirm_sum': '500'
   }
```

   Headers:
   ```
   {
   "Signature": signature
   }
```

### 2. Cancel payment

   Method: ```POST```
   
   Data:
   ```
   {
   'status': 'cancel',
   'payment_id': '3636363',
   'confirm_sum': '0'
   }
```
   Headers:
   ```
   {
   "Signature": signature
   }
```

### 3. Change sum

   If the first payment came for 200, and the second for 300, then a webhook will come only for 200, then a webhook will come that the payment is confirmed automatically 

   Method: ```POST```
   
   Data:
   ```
   {
   "payment_id": 3636363,
   "confirm_sum": '200',
   "payment_sum": '500'
   }
```
