.. _Send message to node:

Node에 메세지 전송하기
============================


Operation
---------------

* Mitum blockchain network에서 operation은 데이터를 변경하는 command의 단위입니다.
* Mitum currency를 기준으로 create-account, transfer, key-updater, currency-register, currency-policy-updater의 operation이 있습니다.
* 각각의 operation은 해당 내용에 따르는 실행주체의 private key로 만든 signature가 필요합니다.
* Operation안에 있는 fact는 실행할 내용을 담고 있으며 fact의 body를 요약한 hash값도 포함되어 있습니다.

Seal
------------

* Seal은 network로 전송하는 Operation의 모음입니다. 즉 Seal에 Opearation을 담아서 전송합니다.
* Seal을 전송하기 위해서는 private key로 만든 signature가 필요합니다.
* Signature를 생성하기 위해서는 Mitum의 keypair 패키지에서 생성된 private key를 사용해야 합니다.
* Signature에 사용되는 private key는 blockchain의 account와는 상관이 없습니다. 즉 account가 사용하는 private key일 필요는 없습니다.
* Seal은 최대 100개의 operation을 담을 수 있습니다.

전송하기
---------

* Client는 operation을 생성한 후 signature를 만들어 operation에 붙입니다.
* Seal에 포함될 수 있는 최대 갯수 안에서 필요한 만큼 operation을 작성하여 Seal에 담습니다.
* Seal에 signature를 붙입니다.
* Mitum 노드에 전송합니다.

Block에 저장
----------------

* Blockchain 네트워크에 전달된 operation은 정상적인 경우 account의 state를 변경하고 최종적으로는 block에 저장됩니다.
* Operation이 block에 저장여부는 digest API를 통해서 확인할 수 있습니다.
* API를 통해 확인하는 방법은 여기 `api`_ 를 참고하여 주십시오.