Installation
=============


Building Mitum Currency executable file
-----------------------------------------

After installing the Golang, please download the `Mitum Currency source code <https://github.com/spikeekips/mitum-currency>`_ .

.. code-block:: sh

    $ mkdir -p mc/bin
    $ git clone https://github.com/spikeekips/mitum-currency.git src


Build the executable file.

.. code-block:: sh
    
    $ cd src
    $ go build -ldflags="-X 'main.Version=v0.0.1-tutorial'" -o ../bin/mc ./main.go
    $ cd ../
    $ bin/mc version
    v0.0.0