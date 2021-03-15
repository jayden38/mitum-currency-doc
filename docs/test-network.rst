Multi-node 실행
========================

yml 설정 준비
-----------------

4대의 노드르 운영하는 경우
각각의 노드를 위한 별도의 yml 설정파일 준비한다.
같은 네트워크 안에서 실행된다고 할 경우, 노드들은 설정파일의 다음 항목에 대하여 같은 값을 가져야 한다.

* genesis-operations
* network-id

노드의 구성에 따라서 consensus에 참여하는 노드의 기본설정이 필요하다.

.. code-block:: yaml

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


yml 설정 sample
-----------------

.. code-block:: yml

    address: n0-010a:0.0.1
    genesis-operations:
        - account-keys:
            keys:
                - privatekey: L5GTSKkRs9NPsXwYgACZdodNUJqCAWjz2BccuR4cAgxJumEZWjok-0112:0.0.1
                publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1
                weight: 100
            threshold: 100
        currencies:
            - balance: "99999999999999999999"
            currency: MCC
        type: genesis-currencies
    network:
        bind: quic://0.0.0.0:54330
        url: quic://127.0.0.1:54330
    network-id: mitum contest; Sat 26 Dec 2020 05:29:13 AM KST
    policy:
        threshold: 100
    privatekey: Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA-0112:0.0.1
    publickey: skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1
    storage:
        blockfs:
            path: ./n0_data/blockfs
        uri: mongodb://127.0.0.1:27017/n0_mc
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

.. code-block:: yml

    address: n1-010a:0.0.1
    genesis-operations:
        - account-keys:
            keys:
                - privatekey: L5GTSKkRs9NPsXwYgACZdodNUJqCAWjz2BccuR4cAgxJumEZWjok-0112:0.0.1
                publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1
                weight: 100
            threshold: 100
        currencies:
            - balance: "99999999999999999999"
            currency: MCC
        type: genesis-currencies
    network:
        bind: quic://0.0.0.0:54331
        url: quic://127.0.0.1:54331
    network-id: mitum contest; Sat 26 Dec 2020 05:29:13 AM KST
    policy:
        threshold: 100
    privatekey: L4R2AZVmxWUiF2FrNEFi6rHwCTdDLQ1JuQHji69SbMcmWUdNMUSF-0112:0.0.1
    publickey: ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM-0113:0.0.1
    storage:
        blockfs:
            path: ./n1_data/blockfs
        uri: mongodb://127.0.0.1:27018/n1_mc
    nodes:
        - address: n0-010a:0.0.1
        publickey: skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1
        url: quic://127.0.0.1:54330
        - address: n2-010a:0.0.1
        publickey: wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd-0113:0.0.1
        url: quic://127.0.0.1:54332
        - address: n3-010a:0.0.1
        publickey: vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb-0113:0.0.1
        url: quic://127.0.0.1:54333

.. code-block:: yml

    address: n2-010a:0.0.1
    genesis-operations:
        - account-keys:
            keys:
                - privatekey: L5GTSKkRs9NPsXwYgACZdodNUJqCAWjz2BccuR4cAgxJumEZWjok-0112:0.0.1
                    publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1
                    weight: 100
            threshold: 100
            currencies:
            - balance: "99999999999999999999"
                currency: MCC
            type: genesis-currencies
    network:
        bind: quic://0.0.0.0:54332
        url: quic://127.0.0.1:54332
    network-id: mitum contest; Sat 26 Dec 2020 05:29:13 AM KST
    policy:
        threshold: 100
    privatekey: L3Szj4t3w33YLsGFGeaB3v1vwae82yp5KWPcT7v1Y4WyQkAH7eCR-0112:0.0.1
    publickey: wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd-0113:0.0.1
    storage:
        blockfs:
            path: ./n2_data/blockfs
        uri: mongodb://127.0.0.1:27019/n2_mc
    nodes:
        - address: n0-010a:0.0.1
            publickey: skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1
            url: quic://127.0.0.1:54330
        - address: n1-010a:0.0.1
            publickey: ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM-0113:0.0.1
            url: quic://127.0.0.1:54331
        - address: n3-010a:0.0.1
            publickey: vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb-0113:0.0.1
            url: quic://127.0.0.1:54333

.. code-block:: yml

    address: n3-010a:0.0.1
    genesis-operations:
        - account-keys:
            keys:
                - privatekey: L5GTSKkRs9NPsXwYgACZdodNUJqCAWjz2BccuR4cAgxJumEZWjok-0112:0.0.1
                    publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1
                    weight: 100
            threshold: 100
            currencies:
            - balance: "99999999999999999999"
                currency: MCC
            type: genesis-currencies
    network:
        bind: quic://0.0.0.0:54333
        url: quic://127.0.0.1:54333
    network-id: mitum contest; Sat 26 Dec 2020 05:29:13 AM KST
    policy:
        threshold: 100
    privatekey: KwxfBSzwevSggJz2grf8FWrjvXzrctY3WismTy6GNdJpWXe5tF5L-0112:0.0.1
    publickey: vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb-0113:0.0.1
    storage:
        blockfs:
            path: ./n3_data/blockfs
        uri: mongodb://127.0.0.1:27020/n3_mc
    nodes:
        - address: n0-010a:0.0.1
            publickey: skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1
            url: quic://127.0.0.1:54330
        - address: n1-010a:0.0.1
            publickey: ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM-0113:0.0.1
            url: quic://127.0.0.1:54331
        - address: n2-010a:0.0.1
            publickey: wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd-0113:0.0.1
            url: quic://127.0.0.1:54332


실행 순서
--------------------------------------------------------------------------------

* Multi 노드를 실행할 경우, 최초 genesis block을 생성하는 첫번째 노드를 정해야 한다.
* 첫번째 노드는 node init 명령을 통해서 genesis block을 생성한다.
* genesis block을 생성하는 노드가 아닌 다른 노드들은 init 명령을 실행할 필요가 없다.
* 첫번째 노드는 init 후 run 명령을 통해서 노드를 실행한다.
* 다른 노드들도 run 명령을 통해서 각각 노드를 실행한다.
* 다른 노드들은 sync 과정을 통해서 첫번째 노드의 블록을 따라가게 되고 이후 consensus 과정을 통해서 노드들은 블록을 생성하게 된다.

.. code-block:: sh

    n0
    $ ./bin/mc node init --log-level info ./n0.yml
    $ ./bin/mc node run --log-level info ./n0.yml

.. code-block:: sh

    n1
    $ ./bin/mc node run --log-level info ./n1.yml

.. code-block:: sh

    n2
    $ ./bin/mc node run --log-level info ./n2.yml

.. code-block:: sh    

    n3
    $ ./bin/mc node run --log-level info ./n3.yml