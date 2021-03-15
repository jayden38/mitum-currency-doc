
Operation Guide
=================

.. toctree::
   :maxdepth: 1

   operations-guide-docs/keypair
   operations-guide-docs/seal-send
   operations-guide-docs/create-account
   operations-guide-docs/transfer
   operations-guide-docs/key-updater
   operations-guide-docs/currency-register
   operations-guide-docs/currency-policy-updater
   operations-guide-docs/check-account

.. note::
    * mitum은 block과 voting 메세지를 주고받는 등의 기본적인 network interface(API)만을 제공
    * account의 transaction history나 현황 등은 mitum에서 따로 API로 제공하지 않음
    * 이러한 부가적인 API는 분리된 API service를 통해서 제공(**예정**)
    * 이 문서에서 account 생성, 전송, key 업데이트의 결과를 확인하기 위해서는 mongodb를 직접 조회해야.
