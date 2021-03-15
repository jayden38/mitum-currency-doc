Mitum technical spec
=======================

* Mitum(blockchain core framework)은 *PBFT* 기반의 *ISAAC+* consensus protocol을 사용하고 있습니다.
* network transport protocol은 `quic <https://en.wikipedia.org/wiki/QUIC>`_ (based on udp) 입니다.
* blockchain의 main storage engine은 *mongodb* 를 사용하고 있으며 block storage로는 local file system을 사용하고 있습니다.
* **parallel** operation processing
* main hash algorithm: `Keccak <https://keccak.team>`_ 256, `SHA-3 <https://pkg.go.dev/golang.org/x/crypto/sha3#New256>`_
* supports multiple hash algorithm: *keccak 256*, *keccak 512*, raw bytes.
* supports multiple keypair: *btc*, *ethereum*, *stellar*.
* supports multiple message serialization format: *json*, *bson*
* small amount of code.
* *json* logging