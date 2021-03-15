Run a node
===================

Overview
----------------
여기서 노드를 실행하기 위한 과정을 설명합니다.  

.. note::

  * Digest API가 mitum-currency에 포함되어 있어 기본적으로 API 서비스를 제공합니다.
  * Digest를 위한 설정은 `Configuration`_ 을 확인하여 주십시오.
  * Digest를 설정하지 않으면, API 서비스를 위한 데이터를 따로 처리하여야 합니다.

Node 설정하기
---------------------
* 노드를 실행하기전 `configuration`_ 을 위해 tutorial.yml을 준비하여 주십시오.

Standalone 노드 실행하기
----------------------------------

Node init
..............

* 먼저 genesis block과 genesis account을 먼저 생성하여야 합니다.
* genesis block 생성을 통해서 main currency가 발행되고 genesis account의 balance에 저장됩니다.
* tutorial.yml : config file

.. code-block:: sh

    $ ./bin/mc node init --log-level info ./tutorial.yml
    2021-03-29T09:16:55.759447Z INF dryrun? dryrun=false module=command-init
    2021-03-29T09:16:55.762494Z INF prepare to run module=command-init
    2021-03-29T09:16:55.762545Z INF prepared module=command-init
    2021-03-29T09:17:06.165294438Z INF database and block data was cleaned by force module=command-init
    2021-03-29T09:17:06.889790438Z INF genesis block created block={"hash":"EnwumZhg1eUxwjh8HARUceya9gqwzU8gK5Ecka9KjJbd","height":0} module=command-init
    2021-03-29T09:17:07.896340438Z INF stopped module=command-init
    ...
    $ echo $?
    0

.. note::

    * 이미 저장된 block 데이터가 발견될 경우, ``already blocks exist, clean first`` 라는 error가 발생합니다.
    * error를 무시하고 초기화하려면, ``--force`` option 추가하여 실행합니다.
    * ``$ ./bin/mc --log-level info init ./tutorial.yml --force``

Node run
..............

* 노드를 실행하면 blockchain의 저장상태와 consensus 참여 상태에 SYNC, JOIN, CONSENSUS 모드로 변경되며 block 생성을 시작합니다.

.. code-block:: sh

    $ ./bin/mc node run --log-level info ./tutorial.yml
    2021-03-29T09:17:38.942065Z INF dryrun? dryrun=false module=command-run
    2021-03-29T09:17:38.94577Z INF prepare to run module=command-run
    2021-03-29T09:17:38.945824Z INF prepared module=command-run
    2021-03-29T09:17:46.196241322Z INF new blocks found to digest last_block=-2 last_manifest=0 module=command-run
    2021-03-29T09:17:47.396357322Z INF digested new blocks module=command-run
    2021-03-29T09:17:47.398958322Z INF trying to start http2 server for digest API bind=https://0.0.0.0:54320 module=command-run publish=https://127.0.0.1:54320
    2021-03-29T09:17:49.533142322Z INF new block stored block={"hash":"GPUqoNjhQ9GSh6p7NPuYekeJBy4K2gWkXMBGd7WwLrDB","height":1,"round":0} elapsed=38.619459 module=basic-consensus-state proposal_hash=oDhisx9UqhYGV7sujFcHKfDfL6QCpUEyn3xNerbcQpm voteproof_id=9YVXwz971QMWQerdiRNVnUJvWbwP6dqWqaNQpnhRjPq1
    2021-03-29T09:17:49.554807322Z INF block digested block=1 module=digester
    2021-03-29T09:17:51.592903322Z INF new block stored block={"hash":"Ccc79abTEQYAEeGggSnUyYY1WkyW12iBAm6PeshdzJe4","height":2,"round":0} elapsed=22.395125 module=basic-consensus-state proposal_hash=CZwieMxiCL1robs9YmeAySbQ67iQV95g1LM2Ttdj1kvb voteproof_id=Bthy5R9EW56vdPcPTYMUiMJw9tq7FAYL3oST3F1dwKGJ
    2021-03-29T09:17:51.606397322Z INF block digested block=2 module=digester
    2021-03-29T09:17:53.655096322Z INF new block stored block={"hash":"3secyQ9KYNVag2E4hhVShofM3vBYxZiBGWNq9fXEsn2H","height":3,"round":0} elapsed=25.89425 module=basic-consensus-state proposal_hash=GndqA1bQeufDmgkm8HoJ4thGn5qAmMxXgwr6Xd9PAhCr voteproof_id=2aw8Upm4pkwq5Pu16hMpcHxycPBtV4qQs1365PWc2a9E
    2021-03-29T09:17:53.667322322Z INF block digested block=3 module=digester

* log level을 info로 설정하면 새로 생성되는 block의 정보를 쉽게 확인할 수 있습니다.

Genesis account 확인
...........................

* file system에 저장된 block 파일들을 통해서 genesis account 정보를 확인할 수 있습니다.

.. code-block:: sh

    $ find blockfs -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1") | [ "height: "+(.height|tostring), "state_key: " + .key, "address: " + .value.value.address, .operations, .value.value.keys.keys, .value.value.keys.threshold]'
    [
      "height: 0",
      "state_key: 7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:account",
      "address: 7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1",
      [
        "2sQk264zRzLHUhFKHTkBQcgjJrQhZeWzymqn2SfCE3es"
      ],
      [
        {
          "_hint": "a003:0.0.1",
          "weight": 100,
          "key": "04b96826d72457a38aa9a2298c3f435f655c28a7d8e94b4e3adf772ac11e3101cbecf9e755312f8a61bd565c182f0d9d67d24f1590ddd2fef1d0af126b5bdfa5a7-0115:0.0.1"
        }
      ],
      100
    ]
    $ find blockfs -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000-MCC:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance:" + .value.value.amount]'
    [
      "height: 0",
      "state_key: 7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000-MCC:balance",
      "balance:99999999999999999999"
    ]

* *height*, ``0`` 에서 genesis account의 *address*, ``7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1`` 가 block에 저장.
* Account 정보는 Digest API를 통해서도 확인가능합니다.

Digest API를 사용하여 확인하기
...................................

* Digest 설정 `Configuration <configuration>`_ 에 따른 api 주소는 https://localhost:54322 입니다.
* node info를 통해서 genesis account 확인

.. code-block:: sh

    $ curl --insecure -v https://localhost:54322 | jq '._embedded.genesis'
    {
        "account": {
            "_hint": "a014:0.0.1",
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
            }
        },
        "balance": "999"
    }

* account 정보를 통해서 Genesis Account 확인

.. code-block:: sh

    $ curl --insecure -v https://localhost:54322/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1 | jq
    {
      "_hint": "a016:0.0.1",
      "hint": {
        "hint": "a018:0.0.1",
        "name": "mitum-currency-account-value"
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
        "balance": "999",
        "height": 0,
        "previous_height": -2
      },
      "_links": {
        "operations": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations"
        },
        "operations:{offset}": {
          "templated": true,
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}"
        },
        "operations:{offset,reverse}": {
          "templated": true,
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}&reverse=1"
        },
        "block": {
          "href": "/block/0"
        },
        "self": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1"
        }
      }
    }