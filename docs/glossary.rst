용어
-------------

tutorial.yml
..........................

* mitum currency는 설정으로 yaml 형식의 설정파일을 지원
* 작성시 주의할 항목
* network-id : multi 노드로 실행할 경우 모두 같은 값을 갖도록 해야한다.
* digest : digest를 외부에서 접근하게 할 경우, network의 bind는 https://0.0.0.0:<port>로
               network의 url은 https://<ip주소>:<port>로 설정하여야 한다.


Account
..........................

* account는 key와 balance로 구성
* Key는 account 소유자의 publickey
* balance는 account가 가진 보유량(amount)

Account Key
..........................

* key는 *threshold*, *weight*, *publickey* 로 구성
* key는 여러개의 *publickey* 를 등록 가능
* 각 *publickey* 는 *weight* 를 가짐
* 예를 들어서,
    - *publickey*, ``p0`` 은 ``50`` *weight*
    - *publickey*, ``p1`` 은 ``50`` *weight*
    - ``p0``, ``p1`` 이 *threshold*, ``100`` 으로 key와 account가 구성되어 있다면,
    - 이 account에서 전송하거나 key를 업데이트하기 위해서는,
    - ``p0`` 과 ``p1`` 의 key signing이 필요
    - ``p0`` 의 *weight* 와 ``p1`` 의 *weight* 를 합쳐서 *threshold*, ``100`` 이상이 되어야햠.

Account Balance, Amount
..........................

* *amount* 는 *big integer*
* *json* 등에서는 *string* 으로 표현

Operation
..........................

* Operation은 mitum의 데이터를 변경하는 단위
* 이 문서에서 설명하는 *create-account*, *transfer*, *key-updater* 가 Operation.
* Operation은 올바른 privatekey로 signing

Seal
..........................

* Seal은 mitum network로 전송되는 operation의 모음
* Seal은 올바른 privatekey로 signing
* 이 privatekey가 생성된 account의 privatekey일 필요는 없음
* 하나의 Seal 메세지에 여러 operation을 담아서 전송
* 최대 100개의 Operation을 담을 수 있음.

Network id
..........................

* 하나의 mitum network를 다른 mitum network와 구분지을 수 있는 unique value
* 같은 mitum network의 모든 노드와 client는 *netwokd id* 가 같아야함.

Node
..........................

* mitum network의 다른 노드와 연결된 process
* 다른 노드들과 동일한 *network id*, network interfaces를 가짐
* consensus에 참여하지 않고 syncing만 하는 것도 가능