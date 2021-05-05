.. _test nodes:

Set up a Test Nodes
========================

yml configuration
-----------------

In case of operating 4 nodes
Prepare a separate yml configuration file for each node.
If running in the same network, nodes should have the same value for the next item in the configuration file.

* genesis-operations
* network-id

Depending on the configuration of the node, it is necessary to configure the nodes participating in consensus.

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


yml configuration example
------------------------------

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


Order of execution
--------------------------------------------------------------------------------

* When executing a multi node, the first node that creates the first genesis block must be determined.
* The first node creates the genesis block through the node init command.
* Nodes other than the one that creates the genesis block do not need to execute the init command.
* The first node executes the node through the run command after init.
* Other nodes also execute each node through the run command.
* Other nodes follow the block of the first node through the sync process, and the nodes create blocks through the consensus process.

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