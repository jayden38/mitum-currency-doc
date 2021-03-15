Account 확인하기
================

Prerequisite
---------------------

* *curl*
    * cli로 api 조회하기 위해서 필요. https://curl.se

* *jq*
    * json 결과를 처리하기 위해서 필요. https://stedolan.github.io/jq/



Genesis account 확인
--------------------------------------------------------------------------------

* local blockfs 에서 확인,

.. code-block:: sh

    $ find blockfs -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance: " + .value.value.amount]'
    [
      "height: 0",
      "state_key: 7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:balance",
      "balance: 99999999999999999999"
    ]

* ``99999999999999999977 = 99999999999999999999 - (2 create account: 10 * 2) - (2 fee: 1 * 2)``

* digest에서 확인: account가 생성되었는지 확인

.. code-block:: sh

    $ curl --insecure -v https://localhost:54322/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1 | jq
    {
      "_hint": "a016:0.0.1",
      "hint": {
        "name": "mitum-currency-account-value",
        "hint": "a018:0.0.1"
      },
      "_embedded": {
        "_hint": "a018:0.0.1",
        "hash": "CkNB7yu1YbAU5c8LFRV6HbFiuj9azQ3LCwuTuxMREbkd",
        "address": "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1",
        "keys": {
          "_hint": "a004:0.0.1",
          "hash": "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv",
          "keys": [
            {
              "_hint": "a003:0.0.1",
              "weight": 100,
              "key": "04b96826d72457a38aa9a2298c3f435f655c28a7d8e94b4e3adf772ac11e3101cbecf9e755312f8a61bd565c182f0d9d67d24f1590ddd2fef1d0af126b5bdfa5a7-0115:0.0.1"
            }
          ],
          "threshold": 100
        },
        "balance": "99999999999999999977",
        "height": 5,
        "previous_height": 0
      },
      "_links": {
        "previous_block": {
          "href": "/block/0"
        },
        "self": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1"
        },
        "operations": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations"
        },
        "operations:{offset}": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}",
          "templated": true
        },
        "operations:{offset,reverse}": {
          "templated": true,
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}&reverse=1"
        },
        "block": {
          "href": "/block/5"
        }
      }
    }

``ac0`` 확인
--------------------------------------------------------------------------------

* local blockfs 에서 확인,

.. code-block:: sh

    $ find blockfs -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance: " + .value.value.amount]'
    [
      "height: 5",
      "state_key: HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:balance",
      "balance: 50"
    ]

* digest에서 확인

.. code-block:: sh

    $ curl --insecure -v https://localhost:54322/account/HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1 | jq
    {
      "_hint": "a016:0.0.1",
      "hint": {
        "name": "mitum-currency-account-value",
        "hint": "a018:0.0.1"
      },
      "_embedded": {
        "_hint": "a018:0.0.1",
        "hash": "EcGgCGGNFGbRN7twtMw4eBJpTEXQ7en148waBv9Q1VPb",
        "address": "HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1",
        "keys": {
          "_hint": "a004:0.0.1",
          "hash": "HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T",
          "keys": [
            {
              "_hint": "a003:0.0.1",
              "weight": 100,
              "key": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
            }
          ],
          "threshold": 100
        },
        "balance": "50",
        "height": 5,
        "previous_height": -2
      },
      "_links": {
        "operations": {
          "href": "/account/HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1/operations"
        },
        "operations:{offset}": {
          "templated": true,
          "href": "/account/HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1/operations?offset={offset}"
        },
        "operations:{offset,reverse}": {
          "templated": true,
          "href": "/account/HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1/operations?offset={offset}&reverse=1"
        },
        "block": {
          "href": "/block/5"
        },
        "self": {
          "href": "/account/HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1"
        }
      }
    }

``ac1`` 확인
--------------------------------------------------------------------------------

* local blockfs 에서 확인,

.. code-block:: sh

    $ find blockfs -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance: " + .value.value.amount]'
    [
      "height: 5",
      "state_key: HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:balance",
      "balance: 50"
    ]

.. code-block:: sh

    $ curl --insecure -v https://localhost:54322/account/HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1 | jq
    {
      "_hint": "a016:0.0.1",
      "hint": {
        "name": "mitum-currency-account-value",
        "hint": "a018:0.0.1"
      },
      "_embedded": {
        "_hint": "a018:0.0.1",
        "hash": "ERWC4HZuagN6jsBwcJbPoz491qh8ioUmLBz2iMmTEBT4",
        "address": "HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1",
        "keys": {
          "_hint": "a004:0.0.1",
          "hash": "HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC",
          "keys": [
            {
              "_hint": "a003:0.0.1",
              "weight": 100,
              "key": "04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
            }
          ],
          "threshold": 100
        },
        "balance": "50",
        "height": 5,
        "previous_height": -2
      },
      "_links": {
        "self": {
          "href": "/account/HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1"
        },
        "operations": {
          "href": "/account/HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1/operations"
        },
        "operations:{offset}": {
          "templated": true,
          "href": "/account/HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1/operations?offset={offset}"
        },
        "operations:{offset,reverse}": {
          "templated": true,
          "href": "/account/HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1/operations?offset={offset}&reverse=1"
        },
        "block": {
          "href": "/block/5"
        }
      }
    }

.. note::
    * *address* 로 mongodb에서 **state** 를 조회할 때, ``:`` 뒷부분은 제거하고 key로 사용.
    * ``7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1`` → ``7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000``
    