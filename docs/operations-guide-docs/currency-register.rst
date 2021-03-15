Currency 등록
===================

Currency-register
---------------------------

* mitum-currency seal currency-register --network-id=NETWORK-ID-FLAG --feeer=STRING --policy-new-account-min-balance=BIG <node privatekey> <currency-id> <genesis-amount> <genesis-account>
* 새로운 currency를 등록하는 경우 설정이 필요한 항목
* genesis account : 새로운 currency 등록과 함께 발행된 토큰이 등록될 account
* genesis amount : 새롭게 발행될 토큰의 양
* --policy-new-account-min-balance=<amount>를 설정하여야 함.
* feeer : feeer는 세가지 정책 {nil, fixed, ratio} 중 선택할 수 있다.
* nil은 fee 지불이 없는 경우, fixed는 고정된 양을 지불하게 하는 경우, ratio는 operation amount에 비례하여 지불하게 하는 경우이다.
* fee 정책이 fixed인 경우 그에 따른 --feeer-fixed-receiver=<fee receiver account address>와 --feeer-fixed-amount=<fee amount>를 설정해주어야 함.
* fee 정책이 ratio인 경우 그에 따른 --feeer-ratio-receiver=<fee receiver account address>와 --feeer-ratio-ratio=<fee ratio, multifly by operation amount>, --feeer-ratio-min=<minimum fee>, --feeer-ratio-max=<maximum fee>를 설정해주어야 함.
* 새로운 currency를 등록하는 경우 consensus에 참여하는 suffrage 노드들의 signature가 consensus threshold(67%)를 넘어야만 실행이 됨.


Currency-register 예제
---------------------------

* genesis-account : ac1
* genesis-amount : 9999999999999
* currency-id : MCC2
* feeer : fixed
* feeer-fixed-receiver : ac1
* feeer-fixed-amount : 3
* seal sender : ac1
* suffrage node : n0, n1, n2, n3

.. code-block:: sh

    $ NETWORK_ID="mc; Thu 10 Sep 2020 03:23:31 PM UTC"
    $ AC1_ADDR="HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1"
    $ AC1_PRV="792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be-0114:0.0.1"
    $ N0_PRV=<n0 private key>
    $ N1_PRV=<n1 private key>
    $ N2_PRV=<n2 private key>
    $ N3_PRV=<n3 private key>
    $ ./bin/mc seal currency-register --network-id=$NETWORK_ID --feeer="fixed" --feeer-fixed-receiver=$AC1_ADDR \ 
      --feeer-fixed-amount=3 --policy-new-account-min-balance=10 $N0_PRV MCC2 9999999999999 $AC1_ADDR \
      | ./bin/mc seal sign-fact $N1_PRV --network-id=$NETWORK_ID --seal=- \
      | ./bin/mc seal sign-fact $N2_PRV --network-id=$NETWORK_ID --seal=- \
      | ./bin/mc seal sign-fact $N3_PRV --network-id=$NETWORK_ID --seal=- \
      | ./bin/mc seal send --network-id=$NETWORK_ID $AC1_PRV --seal=-