Keypair
===============

* keypair 생성을 통해서 private key와 public key가 만들어집니다.
* 생성된 keypair는 account 생성, 노드의 keypair 등록, operation과 seal의 signature를 만드는데 사용됩니다.

Keypair 생성
--------------------

* 새로운 keypair는 다음과 같이 생성할 수 있습니다.

.. code-block:: sh

      $ ./bin/mc key new --type=<key type>

* Mitum에서는 bitcoin, ethereum, stellar 형식의 keypair를 사용할 수 있습니다.
* key type에 btc, ether, stellar를 선택할 수 있습니다. (default: btc)

.. code-block:: sh

      $ ./bin/mc key new --type btc
            hint: hint{type="btc-privatekey" code="0112" version="0.0.1"}
      privatekey: KyJFEE8GpjBUDJbtEz5NW2QndUs4o994zJn1mstYR6Uc5U37BWv6-0112:0.0.1
       publickey: zwaGS678yT5HieAao45sbM3f6x4VAK19NZENQSNdMAGa-0113:0.0.1

Multi Sig Account
------------------------

* Account는 Mitum currency에서 currency와 balance를 갖고 있는 data structure입니다.
* Account는 address라는 고유값을 갖고 있어 이를 통해 식별할 수 있습니다.
* 사용자의 Account에 대한 authentication을 위해서 public key를 등록합니다.
* Mitum currency의 account는 multi signature가 가능하기 때문에 여러 개의 public key를 등록할 수 있습니다.

.. csv-table::
   :widths: 30, 150

   "address", "5terLZQX4fTPpjmBsjPjvwBLMY78qRWhKZ6j1kEiDNeV-a000:0.0.1"
   "threshold", "100"
   "keys", "{key: rd89Gx..., weight: 50}, {key: skRdC6..., weight: 50}"
   "balance", "{currency: MCC, amount: 10000}, {currency: MCC2, amount: 20000}"

* Account에는 threshold값을 설정합니다. 1 < thresohold <= 100.
* key들의 weight 합은 100이 되어야 합니다.
.. csv-table:: "key가 한 개만 있는 경우"
    :widths: 30, 300

    "keys", "{key: rd89Gx..., weight: 100}                                                           "

.. csv-table:: "key가 여러개 있는 경우"
    :widths: 30, 300

    "keys", "{key: rd89Gx..., weight: 40}, {key: skRdC6..., weight: 30}, {key: mymMwq..., weight: 30}"

* 같은 *publickey* 의 조합에서도 *weight* 나 *threshold* 가 다르면 *address* 는 다른 값을 갖게 됩니다.

Address 확인
---------------

* public key에서 address를 확인하는 방법은 다음과 같습니다.

.. code-block:: sh

      $ ./bin/mc key address <threshold> <publickey>,<weight>

.. code-block:: sh
     
      $ ACC_PUB=042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1
      $ THRESHOLD=100
      $ WEIGHT=100
      $ ./bin/mc key address $THRESHOLD $ACC_PUB,$WEIGHT
        HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1