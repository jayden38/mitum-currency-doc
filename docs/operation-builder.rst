Operation Builder 사용하기
=============================

* Digest API에는 operation message 작성을 돕는 Operation Builder 가 있습니다.
* Operation Builder는 sdk를 사용하지 않고도 api를 통해서 operation message를 생성할 수 있게 합니다.
  
Get operation fact template
-------------------------------------------------

* Operation fact templete을 요청하여 Operation 타입별로 template를 받을 수 있습니다.
* template의 field 값을 변경하여 fact message를 작성할 수 있습니다.

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

* 응답받은 template의 내용중 _embedded 객체가 fact를 나타냅니다.
* fact json 객체의 내용을 편집하여 ``Build operation message`` 에서 사용합니다.
* create-accounts fact 편집 예제.

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

* hash값은 builder에 의해서 자동 완성됩니다. 편집하지 않아도 됩니다.
* token은 base64 인코딩된 값입니다.
* keys와 관련된 account의 key 등록 내용은 `Keypair <keypair>`_ 를 확인하여 주십시오.
* _hint 항목은 그대로 사용하십시오.

Build operation message
-------------------------------

* 작성한 fact message를 json 형식의 request body로 전달하여 완성된 fact message를 응답받습니다.

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

* 응답 데이타의 fact.hash 값을 확인합니다.
* fact.hash값을 데이터로 사용하여 fact_sign 객체의 값을 완성합니다.
* signer는 signature를 만드는데 사용된 keypair의 publickey입니다.
* signature는 signer에 의해서 생성됩니다.
* signed_at은 signature가 생성된 datetime입니다.

Sign operation message
----------------------------

* 응답받은 fact의 hash를 이용하여 signature을 만들고 fact_sign을 추가합니다.
* 작성한 fact message를 json 형식의 request body로 전달하면 완성된 Operation message를 응답받습니다.

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

* Operation 또는 Seal message를 request body로 요청하여, 네트워크에 전파할 수 있습니다.
* 이 경우 Seal의 signer는 digest 노드가 됩니다.
* request body가 operation이면 새로운 seal이 생성되고 digest 노드가 sign합니다.
* request body가 seal이면 seal은 digest 노드가 sign합니다.

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

Operation의 성공 확인
-------------------------

* operation의 처리 성공 여부는 api에서 fact hash값으로 operation을 조회하여 확인할 수 있습니다. 
* GET https://api_url/block/operation/{operation_fact_hash}
* 응답 메세지에서 ``_embedded.in_state`` 값이 ``true`` 인 경우 operation이 block에 저장되었습니다.
* ``_embedded.in_state`` 값이 ``false`` 인 경우에는 operation이 block에 저장되지 않았습니다.
* operation이 실패한 경우 그 이유는 다음과 같은 경우가 될 수 있습니다.
* 송금할 때 sender의 balance 부족한 경우, 잘못된 signature, creation-account인 경우, amount가 new-account-min-balance 보다 작은 경우 등등.
* 실패 이유는 응답메세지의 ``_embedded.reason.msg`` 에서 확인할 수 있습니다.


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