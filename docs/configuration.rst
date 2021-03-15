Configuration
=============

* 노드 setting을 위한 configuration을 yml 형식으로 설정합니다.

address
-------------

* local node의 address(url 주소에 대한 별칭)

.. code-block:: yml

    address: n0-010a:0.0.1

genesis-operations
------------------------

* genesis-operation은 네트워크 초기화할 때 실행되는 genesis operation에 대한 설정입니다.
* genesis-operation은 최초 생성되는 블록에 대한 내용을 갖고 있습니다.
* currency model에서는 main currency와 genesis account에 대한 정보를 설정하여 줍니다.
* genesis account의 keypair(key, weight, threshold 값)를 등록하고 
* 생성될 currency의 초기물량(balance)과 Currency ID, 수수료 정책을 지정하여 줍니다.

.. code-block:: yml

    genesis-operations:
        - account-keys:
            keys:
                - publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1
                  weight: 100
            threshold: 100
          currencies:
              - balance: "99999999999999999999"
                currency: MCC
                new-account-min-balance: "33"
          type: genesis-currencies


network
---------

* 네트워크에서 사용되는 노드의 domain 또는 ip주소를 지정합니다.
* 노드 또는 클라이언트로부터 메세지를 받는 주소이며 quic 통신 프로토콜을 사용합니다.

.. code-block:: yml

    network:
        bind: quic://0.0.0.0:54330
        url: quic://127.0.0.1:54330
        cert-key: mitum.key
        cert: mitum.crt

* Mitum 노드는 기본적으로 CA signed certificate(public certificate)를 사용하는 것이 기본입니다.
* Network config에서 certificate 관련된 설정을 하지 않으면 노드는 self-signed certifate를 사용합니다.
* Mitum 노드가 self-signed certifate를 사용하는 경우, network-connection-tls-insecure: true 를 추가로 설정해주어야 합니다.

.. code-block:: yml

    policy:
        network-connection-tls-insecure: true

* network-connection-tls의 기본값은 false입니다.
* 다른 mitum 노드들이 self-signed certificate를 사용하고 있다면, 이 설정을 true로 해야 정상적으로 메세지를 주고 받을 수 있습니다.

network-id
------------

* Network id는 네트워크를 구분하는 식별자와 같은 역할을 합니다. 
* 같은 네트워크 위에 있는 노드들은 모두 동일한 network-id 값을 가집니다.

.. code-block:: yml

    network-id: mitum contest; Sat 26 Dec 2020 05:29:13 AM KST

keypair
---------

* 노드의 private key, public key를 입력합니다.
* keypair를 생성하는 방법은 여기를 참고하십시오.

.. code-block:: yml

    privatekey: Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA-0112:0.0.1
    publickey: skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1

storage
----------

* blockchain 데이터 storage의 file system 경로와 mongodb database address를 지정합니다.

.. code-block:: yml

    storage:
        blockdata:
            path: ./n0_data/blockfs
        database:
            uri: mongodb://127.0.0.1:27017/n0_mc

suffrage > nodes
--------

* consensus에 참여하는 suffrage node에 대한 address를 설정합니다.
* local node의 address가 n0-010a:0.0.1 라고 한다면, 
* local node를 포함하여 n1, n2, n3 노드를 모두 suffrage에 포함하는 경우 다음과 같이 설정할 수 있습니다.

.. code-block:: yml

    suffrage:
        nodes:
            - n0-010a:0.0.1
            - n1-010a:0.0.1
            - n2-010a:0.0.1
            - n3-010a:0.0.1

* local node인 n0노드를 suffrage > nodes에 포함시키지 않으면 
* local node는 None-Suffrage node가 되어 Syncing node로서의 역할만을 합니다.
* Syncing node는 consensus에 참여하지 않고 생성된 block data를 sync하기만 합니다.
* None-suffrage node는 operation을 담고 있는 seal만을 처리합니다.
* None-suffrage node는 노드간 voting과 관련된 ballot과 proposal은 처리하지 않습니다.
* Node-suffrage node가 operation seal을 저장하면 suffrage node들에게 broadcast합니다.
* None-suffrage node, 즉 local node가 suffrage node에 설정되지 않은 경우,
* 다른 suffrage node들을 설정하지 않은 경우, operation seal도 처리활 수 없습니다.

.. code-block:: yml

    suffrage:
        nodes:
            - n1-010a:0.0.1
            - n2-010a:0.0.1
            - n3-010a:0.0.1

sync-interval
-----------------

* None-suffrage node는 block data를 주기적으로 sync합니다.
* Default interval은 10 second입니다.
* sync-interval 설정을 통해서 interval 값을 바꿀 수 있습니다.

.. code-block:: yml

    sync-interval: 3s

nodes
-------

* blockchain 네트워크에서 known 노드들의 address(주소에 대한 별칭), public key, url(ip 주소)를 입력합니다.
* 작성하지 않은 경우 standalone 노드로 동작합니다.

.. code-block:: yml

    nodes:
        - address: n1-010a:0.0.1
          publickey: ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM-0113:0.0.1
          url: quic://127.0.0.1:54331
        - address: n2-010a:0.0.1
          publickey: wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd-0113:0.0.1
          url: quic://127.0.0.1:54332
        - address: n3-010a:0.0.1
          publickey: vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb-0113:0.0.1
          url: quic://127.0.0.1:54333

digest
--------

API로 제공할 데이터를 저장하기 위한 mongodb 주소와 API 접근 ip주소를 지정합니다.

.. code-block:: yml

    digest:
        storage: mongodb://127.0.0.1:27017/mc_digest
        network:
            bind: https://localhost:54322
            url: https://localhost:54322
            cert-key: mitum.key
            cert: mitum.crt

config example
----------------

.. code-block:: yml

    address: n0-010a:0.0.1
    genesis-operations:
        - account-keys:
            keys:
                - publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1
                weight: 100
            threshold: 100
        currencies:
            - balance: "99999999999999999999"
            currency: MCC
            new-account-min-balance: "33"
        type: genesis-currencies
    network:
        bind: quic://0.0.0.0:54330
        url: quic://127.0.0.1:54330
        cert-key: mitum.key
        cert: mitum.crt
    network-id: mitum
    policy:
        threshold: 100
        network-connection-tls-insecure: true
    privatekey: Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA-0112:0.0.1
    publickey: skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1
    storage:
        blockdata:
            path: ./data/blockfs
        database:
            uri: mongodb://127.0.0.1:27017/n0_mc
    digest:
        storage: mongodb://127.0.0.1:27017/mc_digest
        network:
            bind: http://0.0.0.0:54320
            url: http://127.0.0.1:54320
            cert-key: mitum.key
            cert: mitum.crt