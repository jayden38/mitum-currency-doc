Prerequisite
============

Database
------------------
| Mitum currency는 main storage engine으로 mongodb를 사용하고 있습니다.
| Mitum currency 노드를 실행하기 위해서는 먼저 mongodb를 준비하여야 합니다.

* MongoDB
    - Installation
        - `Manual Installation Guide <https://docs.mongodb.com/manual/installation/>`_
        - `docker container <https://hub.docker.com/_/mongo>`_ 사용하기
        - ``$ docker run --name mc-test-mongo-27017 -it -p 27017:27017 -d mongo``
    - 사용설정
        * 사용설정에 대한 자세한 내용은 `configuration`_ 에서 확인하실 수 있습니다.


Golang
-------------
| Mitum currency는 `Go <https://golang.org>`_ 언어로 개발되었습니다.
| 실행가능한 바이너리를 생성하기 위하여 소스파일에서 build하여야 합니다.
| 여기서는 Go 언어를 install하는 자세한 방법은 제공하지 않습니다.
| 자세한 내용은 `Go 설치 방법 <https://golang.org/doc/install>`_ 을 참고하여 주십시오.