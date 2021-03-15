Account 생성하기
==================================

* create-account은 새로운 account를 생성하는 operation입니다.
* publickey를 새로운 account의 key로 등록합니다. key들의 weight 합은 ``100`` 이 되어야 합니다.

.. code-block:: sh

    $ mitum-currency seal create-account --network-id=NETWORK-ID-FLAG <privatekey> <sender> <currency> <big>

* ac0, ac1 2 개의 account를 생성하는 과정을 예제로 진행하겠습니다.
* account 당 한 개의 key를 등록하는 경우, 2 개의 public key가 필요합니다.
* keypair를 생성하는 방법은 `여기 <keypair>`_ 에서 확인하여 주십시오.
* Account ac0을 생성하는 operation은 다음과 같이 만들 수 있습니다.

.. code-block:: sh

    $ NETWORK_ID="mc; Tue 08 Dec 2020 07:22:18 AM KST"
    $ GENESIS_PRV=c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1
    $ GENESIS_ADDR=7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1
    $ AC0_PUB=042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1
    $ ./bin/mc seal create-account --network-id=$NETWORK_ID $GENESIS_PRV $GENESIS_ADDR XXX 50 --key=$AC0_PUB,100 | jq
    {
      "_hint": "0151:0.0.1",
      "hash": "6HfMCxykmvJtpYTEeJF9RvF7UbYaVp7UtjcXd8C1MMbt",
      "body_hash": "3MSx7GpdRZ5ibGsg1Ly3z7eXURTtu34Gkff88VxgFiWV",
      "signer": "04b96826d72457a38aa9a2298c3f435f655c28a7d8e94b4e3adf772ac11e3101cbecf9e755312f8a61bd565c182f0d9d67d24f1590ddd2fef1d0af126b5bdfa5a7-0115:0.0.1",
      "signature": "5BpRZ8BBgoXEFYuE7SyiRJBdg2oYjwsgJMEY5rJSHg1ARy2xPUAk3C1LKGAEbNfZbdcSLcyhZ7cEFdeDTjYJzsWCJ9JM1",
      "signed_at": "2020-09-16T06:15:53.513265367+09:00",
      "operations": [
        {
          "memo": "",
          "_hint": "a006:0.0.1",
          "hash": "BqEvnWarCuvx7cM3sh1cdfdHXiTi5nKZKriCBm9tiV8b",
          "fact": {
            "_hint": "a005:0.0.1",
            "hash": "DoYeMxsrFGQ8kke65DEXvfZsW1x4H8s9yCNPBgLYvQDy",
            "token": "MjAyMC0wOS0xNlQwNjoxNTo1My41MTI5OTk3MTIrMDk6MDA=",
            "sender": "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1",
            "items": [
              {
                "keys": {
                  "_hint": "a004:0.0.1",
                  "hash": "EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1",
                  "keys": [
                    {
                      "_hint": "a003:0.0.1",
                      "weight": 100,
                      "key": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amount": "10"
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "0150:0.0.1",
              "signer": "04b96826d72457a38aa9a2298c3f435f655c28a7d8e94b4e3adf772ac11e3101cbecf9e755312f8a61bd565c182f0d9d67d24f1590ddd2fef1d0af126b5bdfa5a7-0115:0.0.1",
              "signature": "5BpRZ5a1NS2yJ5qGnD1jno71zjrraSRPScLxo3T679e3TVbPiL1NBXqk8NrSKZprpccCsG9fC4MonRP2FpBLrfQNtbH6s",
              "signed_at": "2020-09-16T06:15:53.513249931+09:00"
            }
          ]
        }
      ]
    }

* Account ``ac1`` 을 생성하는 operation은 다음과 같이 만들 수 있습니다.

.. code-block:: sh

    $ NETWORK_ID="mc; Tue 08 Dec 2020 07:22:18 AM KST"
    $ GENESIS_PRV=c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1
    $ GENESIS_ADDR=7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1
    $ AC1_PUB=04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1
    $ ./bin/mc seal create-account --network-id=$NETWORK_ID $GENESIS_PRV $GENESIS_ADDR XXX 50 --key=$AC1_PUB,100 | jq
    {
      "_hint": "0151:0.0.1",
      "hash": "mgvCR9cfGJ6Qdsj2AVciq9tVKTmL6VBda3dDvuWsSmF",
      "body_hash": "G9mr5kEJw9Ft16mFuWtJhsKEDF35Rj5h126CCWaf2KUP",
      "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
      "signature": "5BpRZ4HnVxL5CUxNkZipDQ98APefbBrjFbbYSYSjVtw5RCuVQFJz5YrC3ZNopcjsk8LHhsYvXERHmAExaNSL92iCytuv6",
      "signed_at": "2020-09-16T13:23:33.693851357+09:00",
      "operations": [
        {
          "_hint": "a006:0.0.1",
          "hash": "4AW1oFKb7VLPh8jW2G92UJYyXaXL2rRPeLADZt85P1M1",
          "fact": {
            "_hint": "a005:0.0.1",
            "hash": "3YZZ1kNxdt7Aof7cuwfiNGFNXB85nFypMcdsqux1ezHT",
            "token": "MjAyMC0wOS0xNlQxMzoyMzozMy42OTM2NDU4NjMrMDk6MDA=",
            "sender": "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1",
            "items": [
              {
                "keys": {
                  "_hint": "a004:0.0.1",
                  "hash": "Emvn6Zc5WVsSsNBbQEGiHn11fe6gsgKcbzWSckYG2xEb",
                  "keys": [
                    {
                      "_hint": "a003:0.0.1",
                      "weight": 100,
                      "key": "04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amount": "10"
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "0150:0.0.1",
              "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
              "signature": "5BpRZ59febcwKFPa9ooGpWGXBwGHZ9LM44ubQF9upkR3Zm1zYDmi4DsV3TsHTkoPZm9aDfC4vCg1C4M6GuXAVqShD9oN6",
              "signed_at": "2020-09-16T13:23:33.693840485+09:00"
            }
          ],
          "memo": ""
        }
      ]
    }

* 위 json 메세지들을 seal에 담아 노드에 전달합니다.

.. note::
    * mitum currency에서는 한 account가 signing한 operation을 두 개 이상 한 block에 처리하지 않음
    * 예를 들어, ``ac0`` 에서 ``ac1``, ``ac2`` 로 각각 ``5`` amount를 보내는 두 개의 operation을 동시에 처리할 수 없음
    * 이와 같은 경우에는 먼저 도착한 operation만 처리하고 나머지는 무시됨.


.. code-block:: sh

    $ NETWORK_ID="mc; Tue 08 Dec 2020 07:22:18 AM KST"
    $ GENESIS_PRV=c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1
    $ GENESIS_ADDR=7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1
    $ CURRENCY_ID=MCC
    $ AC0_PUB=042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1
    $ AC1_PUB=04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1
    $ ./bin/mc seal create-account --network-id=$NETWORK_ID \
      $GENESIS_PRV $GENESIS_ADDR $CURRENCY_ID 50 \
      --key=$AC0_PUB,100" |
    ./bin/mc seal create-account --network-id="mc; Thu 10 Sep 2020 03:23:31 PM UTC" \
      "c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1" \
      "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1" \
      XXX 50 \
      --key="04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1,100" --seal=- | \
    ./bin/mc seal send --network-id="mc; Thu 10 Sep 2020 03:23:31 PM UTC" \
        "c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1" \
        --seal=- --node=quic://127.0.0.1:54321
    $ echo $?
    0

* Operation의 block 저장여부는 digest API에 Operation의 ``fact.hash`` 조회를 통해 확인할 수 있습니다.

.. code-block:: sh

    $ FACT_HASH=3YZZ1kNxdt7Aof7cuwfiNGFNXB85nFypMcdsqux1ezHT
    $ DIGEST_API="https://localhost:54322"
    $ curl --insecure -v $DIGEST_API/operation/$FACT_HASH | jq
    {
      "_hint": "a016:0.0.1",
      "hint": {
        "hint": "a019:0.0.1",
        "name": "mitum-currency-operation-value"
      },
      "_embedded": {
        "_hint": "a019:0.0.1",
        "hash": "Dk5zt5E8aicToCmTi8CUDbWyWUjFJy6UcixDkAZPweyx",
        "operation": {
          "_hint": "a006:0.0.1",
          "hash": "Faa2yz5nB9EeRdxcBXXZPizqNXURfLLJFCYtpk4cY6Zw",
          "fact": {
            "_hint": "a005:0.0.1",
            "hash": "3YZZ1kNxdt7Aof7cuwfiNGFNXB85nFypMcdsqux1ezHT",
            "token": "MjAyMC0xMC0wNVQwMToyNjo0MC4wNDE3NzYxODgrMDk6MDA=",
            "sender": "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1",
            "items": [
              {
                "keys": {
                  "_hint": "a004:0.0.1",
                  "hash": "EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1",
                  "keys": [
                    {
                      "_hint": "a003:0.0.1",
                      "weight": 100,
                      "key": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amount": "10"
              },
              {
                "keys": {
                  "_hint": "a004:0.0.1",
                  "hash": "Emvn6Zc5WVsSsNBbQEGiHn11fe6gsgKcbzWSckYG2xEb",
                  "keys": [
                    {
                      "_hint": "a003:0.0.1",
                      "weight": 100,
                      "key": "04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amount": "10"
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "0150:0.0.1",
              "signer": "04b96826d72457a38aa9a2298c3f435f655c28a7d8e94b4e3adf772ac11e3101cbecf9e755312f8a61bd565c182f0d9d67d24f1590ddd2fef1d0af126b5bdfa5a7-0115:0.0.1",
              "signature": "5BpRZ6XAED35YRre4SgJeUmrfdnfgzm4NugZ9wzp1ir3GqbZX6dpnj3m5dsbzRoS2LbH4SvWYiWyq41yd2v87CP5Zgn7D",
              "signed_at": "2020-10-05T01:26:40.043241127+09:00"
            }
          ],
          "memo": ""
        },
        "height": 722,
        "confirmed_at": "2020-10-04T16:26:42.729Z",
        "in_state": true
      },
      "_links": {
        "operation:{hash}": {
          "templated": true,
          "href": "/operation/{hash:(?i)[0-9a-z][0-9a-z]+}"
        },
        "account:{address}": {
          "templated": true,
          "href": "/account/{address:(?i)[0-9a-z][0-9a-z\\-]+\\-[a-z0-9]{4}\\:[a-z0-9\\.]*}"
        },
        "block:{height}": {
          "templated": true,
          "href": "/block/{height:[0-9]+}"
        },
        "self": {
          "href": "/operation/Dk5zt5E8aicToCmTi8CUDbWyWUjFJy6UcixDkAZPweyx"
        },
        "block": {
          "href": "/block/722"
        }
      }
    }

* operation의 처리 성공 여부는 api를 통하여 확인할 수 있습니다.
* 자세한 내용은 :ref:`Operation Reason` 을 참고하여 주십시오.