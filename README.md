# Card validation interview task

This is the starter for the card validation interview task. We'd like you to take this starter project and fulfil the requirements below. It's light-touch and so shouldn't take too long - we'd envisage no more than a few hours.

## Introduction

Create a web service written in Java, with a single endpoint, which validates a card number & associated billing address.

Please **do not use real card numbers to write or test your solution** - you can find fake ones in a variety of places (https://www.freeformatter.com/credit-card-number-generator-validator.html is one example).

## Specification

The service should:

 - Have a single endpoint at "/card/actions/validate".
 - Be JSON based (consume & return JSON)
 - Accept data in the following format:

```
POST /card/actions/validate

{
    "card_number" : "4242424242424242",
    "billing_address" : {
        "county" : "Kent",
        "postcode" : "DA1 3AT",
        "country" : "GB"
    }
}
```

...and return a response in the following format:

```
Response:

{
    "card": {
        "valid": true,
        "type": "Visa"
    },
    "billing_address_valid": true
}
```

## Request details

 - `card_number` should be a debit/credit card number (no spaces).
 - `billing_address.county` should be the name of a county.
 - `billing_address.postcode` should be a postcode.
 - `billing_address.country` should be the ISO country code ("GB" is the only one needed for this exercise.)
 - All inputs should be treated in a case-insensitive fashion.


## Response details

 - `card.valid` should be true only if the card number is at least 8 digits and passes the [luhn check](https://en.wikipedia.org/wiki/Luhn_algorithm).
 - `card.type` should return:
   - "Amex" if the card number starts with 34 or 37
   - "Visa" if the card number starts with 4
   - "Mastercard" if the card number starts with 22, 23, 24, 25, 26, 27, 51, 52, 53, 54 or 55
   - "Unknown" if none of the above conditions are met.
 - `billing_address_valid` should return true if the combination of `county`, `postcode` and `country` are valid:
   - For all countries other than "GB", return false.
   - For "GB", the [postcodes.io API](https://postcodes.io/) can be used.
     - The status will be 200 for any valid county
     - The county for the postcode will be contained in `result.admin_county`.
     
