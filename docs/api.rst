Digest API
===================

* Digets API는 노드가 blockchain 데이터를 조회할 수 있도록 제공하는 서비스입니다.
* Digest API서비스는 wallet과 blockchain explorer와 같은 application에서 사용할 수 있습니다.
* API는 HTTP/2 network 프로토콜을 통해서 제공됩니다.
* Response 메세지는 `HAL <https://tools.ietf.org/html/draft-kelly-json-hal-08>`_ 방식을 따르며 json 형식으로 전달됩니다.
* API 데이터 storage는 mitum currency의 `configurtion`_ 에서 설정할 수 있습니다.
* Mitum의 main storage를 사용할 수도 있고 별도의 database도 가능합니다.
* HTTP/2 에 필요한 TLS certificates는 파일의 path를 따로 설정하지 않으면 서비스 host가 localhost인 경우 self signed certificates를 임의로 생성합니다.
* 만약 어떤 operation이 특정한 문제로 인하여 block에 포함되지 못한 경우, 그 원인을 response를 통해서 확인할 수 있습니다.