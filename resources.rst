Sumber-sumber Pengembang
========================


.. note::

	Bagian ini masih dalam pengerjaan.


Core
----

* `Membangun Halaman Admin baru <https://github.com/NodeBB/NodeBB/wiki/How-to-build-a-new-Admin-Page>`_ (Jadul)


Plugins
-------

* `Menulis plugins dengan Grunt <https://github.com/NodeBB-Community/nodebb-grunt>`_
* `Menulis plugin NodeBB pertama kamu <http://burnaftercompiling.com/nodebb/writing-your-first-nodebb-plugin/>`_


Themes
------

Widgets
-------

Debugging 
-------
(Linux and OSX)

* Instal node-inspector lewat npm: ``npm i node-inspector -g``

* Memulai NodeBB dalam mode pengembangan: (dari direktori root NodeBB): ``./nodebb dev``

  * Ini akan menjalankan NodeBB hanay dengan satu fork sehingga tidak ada error ``EADDRINUSE``

* Dari terminal baru, jalankan ``node-inspector &`` (dijalankan lewat proses di belakang, jadi jika ada yang tidak beres, bisa menggunakan ``ps aux | grep node-inspector`` untuk melihat pid-nya dan menghentikannya/kill)

Ini akan menghasilkan seperti ini:

.. code::

    Visit http://127.0.0.1:8080/debug?ws=127.0.0.1:8080&port=5858 to start debugging.

* Tekan enter untuk kembali ke baris perintah

* ketik ``ps aux | grep app.js`` untuk melihat:

.. code::

    brian           79177   0.0  0.0  2432772    660 s006  R+   10:03PM   0:00.00 grep app.js
    brian           79089   0.0  1.1  3763608 183804 s005  S+    9:41PM   0:04.91 /usr/local/Cellar/node/0.12.5/bin/node app.js

* Pada contoh ini pid NodeBB adalah 79089, jadi tinggal ketik ``kill -s USR1 79089`` dan akan muncul ini di terminal dimana kamu menjalankan dengan ./nodebb dev:

.. code::

    Starting debugger agent.
    Debugger listening on port 5858

* Coba buka browser dengan alamat yang diberikan node-inspector ^ (tunggu beberapa detik dulu)

* Tentukan satu breakpoint (dimana kamu bisa eksekusi) dan seharusnya NodeBB sudah bisa kembali aktif!

* Sekarang coba tekan ctrl-C untuk menghentikan proses NodeBB. Dan jika sudah siap, jalankan lagi:

* Mulai lagi dengan ./nodebb dev 
* Gunakan ``ps aux | grep app.js`` untuk melihat pid-nya lagi
* Karena node-inspector masih berjalan di latar belakang, maka kita perlu menjalankan ``kill -s USR1 <pid>`` dengan pid baru dimana instansi nodebb yang sedang berjalan, lalu refresh browser dimana sebelumnya debugger aktif

Mengatasi Masalah
^^^^^^^^^^^^^^^^^^

**Saya masih dapat EADDRINUSE error**

* Upgrade ke node 0.12.5 (0.12.x seharusnya cukup)

* Jika pernah menginstal node-inspector dan NodeBB sebelum meng-upgrade ke node 0.12.x, maka perlu melakukan rebuild paket node:

  * Dalam direktori root NodeBB, jalankan ``npm rebuild``
  * Dalam direktori root node-inspector, jalankan juga ``npm rebuild``
    * Jika node-inspector diinstal lewat npm (``npm install -g node-inspector``), masuk ke ``/usr/local/lib/node_modules/node_inspector`` dan jalankan ``npm rebuild``
