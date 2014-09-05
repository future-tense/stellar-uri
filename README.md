stellar-uri
===========

A quick proposal for a URI protocol for Stellar

#Short bakground

In order to facilitate commerce, we need an easier way to deal with transactions without having to manually enter all the details.
Wen need something that works all the way from the "Pay with Stellar"-button, to the wallet.

My proposal is to look at what others are doing using URI handlers.

    https://electrum.org/bitcoin_URIs.html
    https://wiki.ripple.com/Ripple_URIs

The benefit of URI handlers is that it's a mechanism that is supported on all relevant platform.
You click on a stellar URI, and you get transported to the wallet of your choice, no matter if you are on your phone or your desktop pc.


#Proposal

Sending currency to a user

```
stellar: send? address = <address> &
                dt = <destination tag> &
                amount = <amount> &
                signature = <signed hash>
```

Extending trust to a gateway (or other user)

```
stellar: trust? address = <address> &
                amount = <100/USD> &
                signature = <signed hash>
```

##Fields

Address (MANDATORY)

```
address = <account ID> / <federated username>

address=gaQJKTG5spdnRdDd9gwxg11DkkvHTeiad7
address=dzhambulat
address=dzhambulat@stellar.org
```

DT (for send only, OPTIONAL)
 
```
dt=1337
dt=64738
dt=14215469
```

Amount (MANDATORY)
```
amount = <value> ["/" <currency_code> ["/" <issuer>]]
```
100 STR:
```
amount=100
```
1 USD:
```
amount=1/USD
```
1 USD.justcoin:
```
amount=1/USD/gnhPFpbYXcYGMkGxfWdQGFfuKEdJoEThVo
```
Signature (OPTIONAL)

The signing hash is the sha512half of all of the URI up until signature.
Hash is signed by the secret key of the merchant, and can be validated by the client.
Result is base58-encoded.

NB:
Signatures would be nice to have, but for widespread usage they depend of being able to disable the master key.
You disable the master key, and use the regular key to sign all TX, and use the master key only for URI signing.
In case of a breach, the master key is of no use to the intruder.

