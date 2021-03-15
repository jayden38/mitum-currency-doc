Transfer coin
==================

* transfer는 생성된 account들 사이에 coin을 송금하기 위해 사용됩니다.

.. code-block:: sh

    $ mitum-currency seal transfer --network-id=NETWORK-ID-FLAG <privatekey> <sender> <receiver> <currency> <big>

* ``ac0`` 에서 ``ac1`` 으로 currency ``MCC``를 amount, ``3`` 전송하는 예제입니다.

.. code-block:: sh

    $ AC0_PRV=e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1
    $ AC0_ADDR=HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1
    $ AC1_ADDR=HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1
    $ CURRENCY_ID=MCC
    $ NETWORK_ID="mc; Tue 08 Dec 2020 07:22:18 AM KST"
    $ ./bin/mc seal transfer --network-id=$NETWORK_ID $AC0_PRV $AC0_ADDR $AC1_ADDR $CURRENCY_ID 3 | jq
    {
      "_hint": "0151:0.0.1",
      "hash": "ACSP5cdJRTz4YFg72sAxsTzgECwNsJ9J2J3DtY7a2uYe",
      "body_hash": "G9C8x27G777hsTMXd1BcoMBqWyhnh7QX3H7jwxfmNFt3",
      "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
      "signature": "5BpRZ6YGtewJnaRw7mpK3DKJraAHTLrVY7Yuy1qy7Vs9bpLT2kbkZuKjG6Hr7TCHKahJunbqBKQGRenAGDktfYixQsYdY",
      "signed_at": "2020-09-16T13:31:12.203767242+09:00",
      "operations": [
        {
          "fact": {
            "_hint": "a001:0.0.1",
            "hash": "AVQivpcsT1gApMQZLTV1p89cVK3hZkJEzr26qxdxsbnW",
            "token": "MjAyMC0wOS0xNlQxMzozMToxMi4yMDM1NjExNDcrMDk6MDA=",
            "sender": "HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1",
            "items": [
              {
                "receiver": "HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1",
                "amount": "3"
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "0150:0.0.1",
              "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
              "signature": "5BpRZ96xDRW3QzpigYNPthKDJgEu2488bseE79G2YoKMsgV7jFm3SzWXciBgZdAAmFzcJ7R3EJvRkm4FTfekRCjuXeTFe",
              "signed_at": "2020-09-16T13:31:12.20375494+09:00"
            }
          ],
          "memo": "",
          "_hint": "a002:0.0.1",
          "hash": "JAgPABZ6vX8icHDQTJEyNXe5KzY3c6jF4UmCRTVQo24y"
        }
      ]
    }

    $ ./bin/mc seal transfer --network-id=$NETWORK_ID $AC0_PRV $AC0_ADDR $AC1_ADDR $CURRENCY_ID 3 | jq \
      ./bin/mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=-

* operation의 처리 성공 여부는 api를 통하여 확인할 수 있습니다.
* 자세한 내용은 :ref:`Operation Reason` 을 참고하여 주십시오.