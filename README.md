# Investec Open API 
Investecs open-banking API gives users and services the ability to automate banking processes otherwise left to requiring manual interaction. The Investec open banking API is under active development and users may experience bugs or service interruptions at times.

## Installation

Requires python 3.7 or above. Available via pypi package manager 
```shell
pip install investec-open-api
```

## Usage

```python
from investec_open_api import InvestecClient
client = InvestecClient('client_id', 'secret')
```

### get_accounts
Lists the users accounts.

```python
client.get_accounts()
```
Example Response
```json
[
  {
    "accountId": "xxxxxxxxxxxxxxxxxxxxx", 
    "accountNumber": "100xxxxxxxxxx", 
    "accountName": "Mr J Smith", 
    "referenceName": "Mr J Smith", 
    "productName": "Private Bank Account"
  }, 
]
```
### get_account_balance
Get the accounts current balance.

```python
client.get_balance('account_id')
```
Example Response
```json
{
  "accountId": "xxxxxxxxxxxxxxxxxxxxx", 
  "currentBalance": -2269.8, 
  "availableBalance": 639.2, 
  "currency": "ZAR"
}
```

### get_account_transactions
Lists all transactions associated with the account in a given time period. 

```python
client.get_account_transactions('account_id')
```
Example Response
```json
[
  {
    "accountId": "xxxxxxxxxxxxxxxxxxxxx", 
    "type": "DEBIT",  // Debit or credit
    "transactionType": "DebitOrders", 
    "status": "POSTED", 
    "description": "COMPANY XXXXXXXXX", 
    "cardNumber": "",     // the cc number if a cc was used
    "postedOrder": 1116, // the transaction order
    "postingDate": "2022-10-03", // date interest is credited or debted or when deposits are spendable
    "valueDate": "2022-10-03", 
    "actionDate": "2022-10-03", 
    "transactionDate": "2022-10-03", // date the transaction took place
    "amount": 205.05, 
    "runningBalance": -2269.8 // account balance after transaction is posted
  },
]
```
### transfer
Transfer funds between two internal accounts. The accounts can be retrieved using get_accounts.

```python
client.transfer('account_id', 'beneficiary_account_id', 5)
```

### get_countries
Gets a list of countries.

```python
client.get_countries()
```
Example Response
```json
[
  {
    "Code": "ZA", 
    "Name": "South Africa"
  }, 
  {
    "Code": "GB", 
    "Name": "United Kingdom of Great Britain and Northern Ireland (the)"
  }
]
```
### get_currencies
Gets a list of currencies.

```python
client.get_currencies()
```
Example Result
```json
[
  {
    "Code": "ZAR", 
    "Name": "South African Rand"
  }, 
  {
    "Code": "GBP",
    "Name": "British Pound"
  }
]
```

### get_merchants
Fetches a list of mcc codes, these merchant codes can be used to determine what the transaction can be classified as.

```python
client.get_merchants()
```
Example Result
```json
[
  {
    "Code": "7623", 
    "Name": "A/C, Refrigeration Repair"
  }, 
  {
    "Code": "8931", 
    "Name": "Accounting/Bookkeeping Services"
  }
]
```

## Build pypi package

```shell
python -m build
python -m twine upload dist/*
```