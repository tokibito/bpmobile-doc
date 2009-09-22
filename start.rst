====
概要
====

django-bpmobileは\ `Djangoフレームワーク <http://www.djangoproject.com/>`_\ 向けのモバイルサイト開発支援モジュールです。日本の携帯電話キャリアのうち、\ `NTT DoCoMo <http://www.nttdocomo.co.jp/>`_\ 、\ `au <http://www.au.kddi.com/>`_\ 、\ `Softbank <http://mb.softbank.jp/mb/>`_\ のデバイスに対応しています。Djangoの標準機能ではサポートされない以下の機能を提供します。

* キャリア機種判別
* キャリアに応じた文字コード変換
* 絵文字
* 日本語メール送信
* iモードIDを利用したセッション

ダウンロード
============

現在djanbo-bpmobileは、\ `bitbucket.org <http://bitbucket.org/>`_\ 上で開発、公開されています。

開発バージョンは以下より入手できます。

`<http://bitbucket.org/tokibito/django-bpmobile/>`_ 

\ `Mercurial <http://mercurial.selenic.com/>`_\ を利用しているなら、以下のコマンドでもダウンロードできます:

.. code-block:: bash

  hg clone http://bitbucket.org/tokibito/django-bpmobile/

easy_installやpipでもインストールすることができます。

.. code-block:: bash

  easy_install django-bpmobile

または、

.. code-block:: bash

  pip install django-bpmobile

インストールの詳細については、インストールドキュメントを参照して下さい。
