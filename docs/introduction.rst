Introduction
==============

What is Mitum currency?
---------------------------

* Mitum currency는 Mitum blockchain networks 위에서 운영되는 currency 모델입니다.
* Mitum 모델은 Mitum 메인체인을 확장하는 extension layer로 다양한 서비스를 제공할 수 있는 솔루션입니다.
* Currency 발행 및 운영과 관련된 유연한 정책 설정이 가능합니다.
* `Mitum currency <https://github.com/spikeekips/mitum-currency>`_ 는 `Mitum <https://github.com/spikeekips/mitum>`_ (blockchain core framework)를 기반으로 구현되었습니다.
* Mitum의 `technical spec`_ 을 확인하여 보십시오.

.. image:: ../images/mitum_blockchain_layer.png
  :align: center
  :width: 400
  :alt: Mitum blockchain layer

Mitum currency feature
--------------------------

* Mitum currency는 토큰과 관련된 다양한 분야의 비즈니스 요구사항을 충족시키기 위한 핵심 기능을 제공합니다.
* Account 생성시 multiple key를 등록할 수 있으며 Key update를 통해서 관련 키를 교체할 수 있습니다.
* Mitum currency는 새로운 currency를 발행할 수 있으며 관련 policy를 custom하게 setting할 수 있습니다.
* 필요에 따라서 currency 관련 policy를 언제든지 update할 수 있습니다.
* Mitum currency는 블록생성에 따른 보상이 없으며 따라서 inflation 역시 발생하지 않습니다. 
* Mitum currency 운영을 위한 노드 구성은 Mitum blockchain의 노드 운영 방식을 따르며 자세한 내용은 `TestNet 구성 <test-network>`_ 에서 확인할 수 있습니다.

Digest Service
-----------------------

* Digest 서비스는 mitum이 저장하는 새로운 block 데이터를 HTTP 기반의 API로 서비스하기 위해 별도로 저장하는 내부 서비스입니다.
* Digest 서비스와 관련된 자세한 내용은 `여기 <api>`_ 에서 확인하실 수 있습니다.