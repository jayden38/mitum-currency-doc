.. _node configure:

Configuration
=============

* The configuration for node setting is written in YAML.

address
-------------

* local node의 address(alias for url address)

.. code-block:: yml

    address: n0-010a:0.0.1

genesis-operations
------------------------

* genesis-operation is a setting for the genesis operation that is executed when the network is initialized.
* genesis-operation contains the contents of the block that is initially created.
* In the currency model, information on the main currency and genesis account must be set.
* It registers the information (key, weight, threshold value) about the keys of the genesis account, and specifies the initial balance, currency ID, and fee policy of the currency to be created.

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

* Specify the domain address or IP address of the node used in the network.
* Address to receive messages from node or client, using quic communication protocol.

.. code-block:: yml

    network:
        bind: quic://0.0.0.0:54330
        url: quic://127.0.0.1:54330
        cert-key: mitum.key
        cert: mitum.crt

* Mitum nodes use CA signed certificate (public certificate) by default.
* If certificate related settings are not made in Network config, the node uses self-signed certifate.
* If the Mitum node uses self-signed certifate, network-connection-tls-insecure: true must be additionally set.

.. code-block:: yml

    policy:
        network-connection-tls-insecure: true

* The default value of network-connection-tls is false.
* If other Mitum nodes are using self-signed certificates, this setting must be set to true to send and receive messages.

network-id
------------

* Network id acts like an identifier that identifies a network.
* All nodes on the same network have the same network-id value.

.. code-block:: yml

    network-id: mitum contest; Sat 26 Dec 2020 05:29:13 AM KST

keypair
---------

* Enter the node's private key and public key.
* See :ref:`create keypair` to learn how to create a key pair.

.. code-block:: yml

    privatekey: Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA-0112:0.0.1
    publickey: skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1

storage
----------

* Specify the file system path and mongodb database address of blockchain data storage.

.. code-block:: yml

    storage:
        blockdata:
            path: ./n0_data/blockfs
        database:
            uri: mongodb://127.0.0.1:27017/n0_mc

suffrage > nodes
-----------------

* Set addresses for suffrage nodes participating in consensus.
* If the alias name of the local node is n0-010a:0.0.1 and the local node and all n1, n2, and n3 nodes are included in the suffrage nodes, it can be set as follows.

.. code-block:: yml

    suffrage:
        nodes:
            - n0-010a:0.0.1
            - n1-010a:0.0.1
            - n2-010a:0.0.1
            - n3-010a:0.0.1

* If the n0 node, which is a local node, is not included in the suffrage nodes, the local node becomes a None-Suffrage node and serves only as a syncing node.
* The Syncing node does not participate in consensus and only syncs the generated block data.
* The None-suffrage node handles only the seal containing the operation.
* The None-suffrage node does not process ballots and proposals related to voting between nodes.
* When the node-suffrage node stores the operation seal, it broadcasts the seal to the suffrage nodes.
* If the None-suffrage node does not add other nodes to the suffrage node, or does not configure other suffrage nodes, operation seal cannot be processed.

.. code-block:: yml

    suffrage:
        nodes:
            - n1-010a:0.0.1
            - n2-010a:0.0.1
            - n3-010a:0.0.1

sync-interval
-----------------

* None-suffrage node periodically syncs block data.
* The default interval is 10 seconds.
* You can change the interval value through the sync-interval setting.

.. code-block:: yml

    sync-interval: 3s

nodes
-------

* Write the address (alias for the address), public key, and url (ip address) of known nodes in the blockchain network.
* If not written, it operates as a standalone node.

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

Specify the mongodb address that stores the data to be provided by the API and the IP address of the API access.

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