Installation
=============


Mitum Currency 실행파일 build하기
----------------------------------

Go 언어를 설치한 후, Mitum Currency 소스코드를 `download <https://github.com/spikeekips/mitum-currency>`_ 하십시오.

.. code-block:: sh

    $ mkdir -p mc/bin
    $ git clone https://github.com/spikeekips/mitum-currency.git src


build을 통해 실행파일을 생성하십시오.

.. code-block:: sh
    
    $ cd src
    $ go build -ldflags="-X 'main.Version=v0.0.1-tutorial'" -o ../bin/mc ./main.go
    $ cd ../
    $ bin/mc version
    v0.0.0