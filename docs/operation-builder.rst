Using Operation Builder
=============================

* Digest API has Operation Builder to help write operation messages.
* Operation Builder makes it possible to generate operation messages through api without using sdk.
  
Get operation fact template
-------------------------------------------------

* By requesting an Operation fact template, you can receive a template for each operation type.
* You can create a fact message by changing the field value of the template.

| method : GET
| path : /builder/operation/fact/template/{fact}
| response examples

.. code-block::

    {
        "_hint": "a016:0.0.1",
        "hint": {
            "name": "mitum-currency-create-accounts-operation-fact",
            "hint": "a005:0.0.1"
        },
        "_embedded": {
            "_hint": "a005:0.0.1",
            "hash": "7F2RyyTAJAoNV7JFAz89Hdsy11Yo8iAnnAVd1TLkTHMt",
            "token": "cmFpc2VkIGJ5",
            "sender": "mother-a000:0.0.1",
            "items": [
                {
                    "_hint": "a025:0.0.1",
                    "keys": {
                        "_hint": "a004:0.0.1",
                        "hash": "8KRcsJkkeBCzePx7BnDoNYxioxijwRSabbWZDtLPkBGo",
                        "keys": [
                            {
                                "_hint": "a003:0.0.1",
                                "weight": 100,
                                "key": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H-0113:0.0.1"
                            }
                        ],
                        "threshold": 100
                    },
                    "amounts": [
                        {
                            "_hint": "a022:0.0.1",
                            "amount": "-333",
                            "currency": "xXx"
                        }
                    ]
                }
            ]
        },
        "_links": {
            "self": {
                "href": "/builder/operation/fact/template/create-accounts"
            }
        },
        "_extra": {
            "default": {
                "items.keys.keys.key": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H-0113:0.0.1",
                "items.big": "-333",
                "currency": "xXx",
                "token": "cmFpc2VkIGJ5",
                "sender": "mother-a000:0.0.1"
            }
        }
    }

* The _embedded object among the contents of the template responded represents the fact.
* Edit the contents of the fact json object and use it in ``Build operation message``.
* create-accounts fact example.

.. code-block::

    {
        "_hint": "a005:0.0.1",
        "hash": "7F2RyyTAJAoNV7JFAz89Hdsy11Yo8iAnnAVd1TLkTHMt",
        "token": "cmFpc2VkIGJ5",
        "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
        "items": [
            {
                "_hint": "a025:0.0.1",
                "keys": {
                    "_hint": "a004:0.0.1",
                    "keys": [
                        {
                            "_hint": "a003:0.0.1",
                            "weight": 100,
                            "key": "mymMwqm6g9M3WAmexJQbwu52j6hK5MJrhSZQboAavP5D-0113:0.0.1"
                        }
                    ],
                    "threshold": 100
                },
                "amounts": [
                    {
                        "_hint": "a022:0.0.1",
                        "amount": "333",
                        "currency": "MCC"
                    }
                ]
            }
        ]
    }

* The hash value is automatically completed by the builder. You don't have to edit it.
* token is a base64 encoded value.
* Please check :ref:`create keypair` for the details of key registration of accounts related to keys.
* Use the _hint item as it is.

Build operation message
-------------------------------

* The created fact message is sent to the request body in json format and the completed fact message is received.

| method : POST
| path : /builder/operation/fact
| request body

.. code-block::json

    {
        "_hint": "a005:0.0.1",
        "hash": "7F2RyyTAJAoNV7JFAz89Hdsy11Yo8iAnnAVd1TLkTHMt",
        "token": "cmFpc2VkIGJ5",
        "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
        "items": [
            {
                "_hint": "a025:0.0.1",
                "keys": {
                    "_hint": "a004:0.0.1",
                    "keys": [
                        {
                            "_hint": "a003:0.0.1",
                            "weight": 100,
                            "key": "mymMwqm6g9M3WAmexJQbwu52j6hK5MJrhSZQboAavP5D-0113:0.0.1"
                        }
                    ],
                    "threshold": 100
                },
                "amounts": [
                    {
                        "_hint": "a022:0.0.1",
                        "amount": "333",
                        "currency": "MCC"
                    }
                ]
            }
        ]
    }


| Response Example

.. code-block::

    HTTP/1.1 200 OK
    Content-Type: application/hal+json

    {
        "_hint": "a016:0.0.1",
        "hint": {
            "name": "mitum-currency-create-accounts-operation",
            "hint": "a006:0.0.1"
        },
        "_embedded": {
            "_hint": "a006:0.0.1",
            "hash": "DKLe7URcrA6UWeuxVBWqksqsQJvr1YbSwLuDM8BU9XFB",
            "fact": {
                "_hint": "a005:0.0.1",
                "hash": "HDKTNjH3Nd7WgPu9USUpn16kfAcQQKJZqzJfD4wYcL42",
                "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
                "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
                "items": [
                    {
                        "_hint": "a025:0.0.1",
                        "keys": {
                            "_hint": "a004:0.0.1",
                            "hash": "9tfc572ohjGC2kRuLxXynP68WrhAunkdWDweUpuwsDsB",
                            "keys": [
                                {
                                    "_hint": "a003:0.0.1",
                                    "weight": 100,
                                    "key": "mymMwqm6g9M3WAmexJQbwu52j6hK5MJrhSZQboAavP5D-0113:0.0.1"
                                }
                            ],
                            "threshold": 100
                        },
                        "amounts": [
                            {
                                "_hint": "a022:0.0.1",
                                "amount": "333",
                                "currency": "MCC"
                            }
                        ]
                    }
                ]
            },
            "fact_signs": [
                {
                    "_hint": "0150:0.0.1",
                    "signer": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H-0113:0.0.1",
                    "signature": "22UZo26eN",
                    "signed_at": "2020-10-08T07:53:26Z"
                }
            ],
            "memo": ""
        },
        "_links": {
            "self": {
                "href": "/builder/operation/fact"
            }
        },
        "_extra": {
            "default": {
                "fact_signs.signer": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H-0113:0.0.1",
                "fact_signs.signature": "22UZo26eN"
            },
            "signature_base": "8OLTzkLxkh63bK5XxG6xpYkY7Kmn6T/YReNHXX6Zh0NtaXR1bQ=="
        }
    }

* Check the fact.hash value of the response data.
* Uses the fact.hash value as data to complete the value of the fact_sign object.
* The signer is the publickey of the keypair used to create the signature.
* The signature is generated by the signer.
* signed_at is the datetime at which the signature was generated.

Sign operation message
----------------------------

* A signature is created using the hash of the received fact and the fact_sign is added.
* When the created fact message is transmitted to the request body in json format, the completed Operation message is received.

| method : POST
| path : /builder/operation/sign
| request body example

.. code-block:: 

    {
        "_hint": "a006:0.0.1",
        "hash": "DKLe7URcrA6UWeuxVBWqksqsQJvr1YbSwLuDM8BU9XFB",
        "fact": {
            "_hint": "a005:0.0.1",
            "hash": "HDKTNjH3Nd7WgPu9USUpn16kfAcQQKJZqzJfD4wYcL42",
            "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
            "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
            "items": [
                {
                    "_hint": "a025:0.0.1",
                    "keys": {
                        "_hint": "a004:0.0.1",
                        "hash": "9tfc572ohjGC2kRuLxXynP68WrhAunkdWDweUpuwsDsB",
                        "keys": [
                            {
                                "_hint": "a003:0.0.1",
                                "weight": 100,
                                "key": "mymMwqm6g9M3WAmexJQbwu52j6hK5MJrhSZQboAavP5D-0113:0.0.1"
                            }
                        ],
                        "threshold": 100
                    },
                    "amounts": [
                        {
                            "_hint": "a022:0.0.1",
                            "amount": "333",
                            "currency": "MCC"
                        }
                    ]
                }
            ]
        },
        "fact_signs": [
            {
                "_hint": "0150:0.0.1",
                "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1",
                "signature": "381yXYu9Decnkhj4oA796Fn64Wc12Az3P3uQaFJzCkwxxbDTcFYJtJFWSW9v4YAKmfuzd2gWtriQysgcnWde6wbb4gsSxyjq",
                "signed_at": "2021-03-24T05:25:26Z"
            }
        ],
        "memo": ""
    }

response example

.. code-block::

    {
        "_hint": "a016:0.0.1",
        "hint": {
            "name": "mitum-currency-create-accounts-operation",
            "hint": "a006:0.0.1"
        },
        "_embedded": {
            "memo": "",
            "_hint": "a006:0.0.1",
            "hash": "AvvWmq7vZmBuCjXLVRitHAdDzZcd2udSzcDxpRPREVEN",
            "fact": {
                "_hint": "a005:0.0.1",
                "hash": "HDKTNjH3Nd7WgPu9USUpn16kfAcQQKJZqzJfD4wYcL42",
                "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
                "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
                "items": [
                    {
                        "_hint": "a025:0.0.1",
                        "keys": {
                            "_hint": "a004:0.0.1",
                            "hash": "9tfc572ohjGC2kRuLxXynP68WrhAunkdWDweUpuwsDsB",
                            "keys": [
                                {
                                    "_hint": "a003:0.0.1",
                                    "weight": 100,
                                    "key": "mymMwqm6g9M3WAmexJQbwu52j6hK5MJrhSZQboAavP5D-0113:0.0.1"
                                }
                            ],
                            "threshold": 100
                        },
                        "amounts": [
                            {
                                "_hint": "a022:0.0.1",
                                "amount": "333",
                                "currency": "MCC"
                            }
                        ]
                    }
                ]
            },
            "fact_signs": [
                {
                    "_hint": "0150:0.0.1",
                    "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1",
                    "signature": "381yXYu9Decnkhj4oA796Fn64Wc12Az3P3uQaFJzCkwxxbDTcFYJtJFWSW9v4YAKmfuzd2gWtriQysgcnWde6wbb4gsSxyjq",
                    "signed_at": "2021-03-24T05:25:26Z"
                }
            ]
        },
        "_links": {
            "self": {
                "href": "/builder/operation/sign"
            }
        }
    }

Broadcast message to network
--------------------------------------

* By requesting an Operation or Seal message as the request body, you can broadcast it to the network.
* In this case, the signer of the seal becomes the digest node.
* If the request body is operation, a new seal is created and the digest node signs.
* If the request body is a seal, the seal is signed by the digest node.

| method : POST
| path : /builder/send
| request body example

.. code-block::

    {
        "memo": "",
        "_hint": "a006:0.0.1",
        "hash": "AvvWmq7vZmBuCjXLVRitHAdDzZcd2udSzcDxpRPREVEN",
        "fact": {
            "_hint": "a005:0.0.1",
            "hash": "HDKTNjH3Nd7WgPu9USUpn16kfAcQQKJZqzJfD4wYcL42",
            "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
            "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
            "items": [
                {
                    "_hint": "a025:0.0.1",
                    "keys": {
                        "_hint": "a004:0.0.1",
                        "hash": "9tfc572ohjGC2kRuLxXynP68WrhAunkdWDweUpuwsDsB",
                        "keys": [
                            {
                                "_hint": "a003:0.0.1",
                                "weight": 100,
                                "key": "mymMwqm6g9M3WAmexJQbwu52j6hK5MJrhSZQboAavP5D-0113:0.0.1"
                            }
                        ],
                        "threshold": 100
                    },
                    "amounts": [
                        {
                            "_hint": "a022:0.0.1",
                            "amount": "333",
                            "currency": "MCC"
                        }
                    ]
                }
            ]
        },
        "fact_signs": [
            {
                "_hint": "0150:0.0.1",
                "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1",
                "signature": "381yXYu9Decnkhj4oA796Fn64Wc12Az3P3uQaFJzCkwxxbDTcFYJtJFWSW9v4YAKmfuzd2gWtriQysgcnWde6wbb4gsSxyjq",
                "signed_at": "2021-03-24T05:25:26Z"
            }
        ]
    }

response example

.. code-block::

    {
        "_hint": "a016:0.0.1",
        "hint": {
            "hint": "0151:0.0.1",
            "name": "seal"
        },
        "_embedded": {
            "_hint": "0151:0.0.1",
            "hash": "Cj9Vc8fEE2RkjamMnKWbJL4EbygMZmdDxtQJsJjYURyz",
            "body_hash": "6khGv1TNyUT1MbPf1DhcgR6SMZaLDEoi2kwaVH2zssbj",
            "signer": "ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM-0113:0.0.1",
            "signature": "381yXYmPpzZpN4LiyHTMBvYH1vC9gCSJzwT87au7hLUxtqptwgHy3jNHMS7z9ByXqa4AJSUUdFMMcJUvEXvSxfHGU1FWXCSw",
            "signed_at": "2021-03-24T06:50:19.608375163Z",
            "operations": [
                {
                    "memo": "",
                    "_hint": "a006:0.0.1",
                    "hash": "AvvWmq7vZmBuCjXLVRitHAdDzZcd2udSzcDxpRPREVEN",
                    "fact": {
                        "_hint": "a005:0.0.1",
                        "hash": "HDKTNjH3Nd7WgPu9USUpn16kfAcQQKJZqzJfD4wYcL42",
                        "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
                        "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
                        "items": [
                            {
                                "_hint": "a025:0.0.1",
                                "keys": {
                                    "_hint": "a004:0.0.1",
                                    "hash": "9tfc572ohjGC2kRuLxXynP68WrhAunkdWDweUpuwsDsB",
                                    "keys": [
                                        {
                                            "_hint": "a003:0.0.1",
                                            "weight": 100,
                                            "key": "mymMwqm6g9M3WAmexJQbwu52j6hK5MJrhSZQboAavP5D-0113:0.0.1"
                                        }
                                    ],
                                    "threshold": 100
                                },
                                "amounts": [
                                    {
                                        "_hint": "a022:0.0.1",
                                        "amount": "333",
                                        "currency": "MCC"
                                    }
                                ]
                            }
                        ]
                    },
                    "fact_signs": [
                        {
                            "_hint": "0150:0.0.1",
                            "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1",
                            "signature": "381yXYu9Decnkhj4oA796Fn64Wc12Az3P3uQaFJzCkwxxbDTcFYJtJFWSW9v4YAKmfuzd2gWtriQysgcnWde6wbb4gsSxyjq",
                            "signed_at": "2021-03-24T05:25:26Z"
                        }
                    ]
                }
            ]
        },
        "_links": {
            "self": {
                "href": ""
            },
            "operation:0": {
                "href": "/block/operation/HDKTNjH3Nd7WgPu9USUpn16kfAcQQKJZqzJfD4wYcL42"
            }
        }
    }

.. _Operation Reason:

Confirming the success of the operation
-------------------------------------------

* Whether the operation is successfully processed can be checked by querying the operation with the fact hash value in the api.
* GET https://api_url/block/operation/{operation_fact_hash}
* If the ``_embedded.in_state`` value is ``true`` in the response message, the operation is saved in the block.
* If the value of ``_embedded.in_state`` is ``false``, the operation was not saved in the block.
* If the operation fails, the reason may be as follows.
* In case of insufficient balance of sender when sending money, incorrect signature, creation-account, amount less than new-account-min-balance, etc.
* You can check the reason for failure in ``_embedded.reason.msg`` in the response message.


.. code-block:: json

    {
      "_hint": "a016:0.0.1",
      "hint": {
        "name": "mitum-currency-operation-value",
        "hint": "a019:0.0.1"
      },
      "_embedded": {
        "_hint": "a019:0.0.1",
        "hash": "H2GGTYERy88Feh11Vrd5CrjGiWYZ41nXWaRdrTgjRYeC",
        "operation": {
          "fact_signs": [
            {
              "_hint": "0150:0.0.1",
              "signer": "rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1",
              "signature": "AN1rKvt9JBs9jUYgvoiiRLnuEtMADiLNpsPbgZReEuSTjboY3h9trj9HMpBVQZcyrzzxBvAS8ATW6z4gBLGT2TziGaMV71VHD",
              "signed_at": "2021-05-04T07:58:23.998Z"
            }
          ],
          "memo": "",
          "_hint": "a002:0.0.1",
          "hash": "Bk7vMjzFs1LFDAETgGn6mnQZv6EPQ8RX95PydirBE5hA",
          "fact": {
            "_hint": "a001:0.0.1",
            "hash": "H2GGTYERy88Feh11Vrd5CrjGiWYZ41nXWaRdrTgjRYeC",
            "token": "MjAyMS0wNS0wNFQwNzo1ODoyMy45OTc3MjZa",
            "sender": "4UM4CN8MZNyv26TK84486CX5X8bu9EUYbsWz5ovRsp1M-a000:0.0.1",
            "items": [
              {
                "_hint": "a027:0.0.1",
                "receiver": "5terLZQX4fTPpjmBsjPjvwBLMY78qRWhKZ6j1kEiDNeV-a000:0.0.1",
                "amounts": [
                  {
                    "_hint": "a022:0.0.1",
                    "amount": "10000000000000000000",
                    "currency": "MCC"
                  }
                ]
              }
            ]
          }
        },
        "height": 24324,
        "confirmed_at": "2021-05-04T07:58:38.75Z",
        "reason": {
          "_hint": "0158:0.0.1",
          "msg": "insufficient balance of sender, 4UM4CN8MZNyv26TK84486CX5X8bu9EUYbsWz5ovRsp1M-a000:0.0.1; 5554455 !> 10000000000000000000",
          "data": null
        },
        "in_state": false,
        "index": 0
      },
      "_links": {
        "self": {
          "href": "/block/operation/H2GGTYERy88Feh11Vrd5CrjGiWYZ41nXWaRdrTgjRYeC"
        },
        "block": {
          "href": "/block/24324"
        },
        "manifest": {
          "href": "/block/24324/manifest"
        },
        "operation:{hash}": {
          "templated": true,
          "href": "/block/operation/{hash:(?i)[0-9a-z][0-9a-z]+}"
        },
        "block:{height}": {
          "templated": true,
          "href": "/block/{height:[0-9]+}"
        }
      }
    }