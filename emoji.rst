.. _emoji:

======
絵文字
======

bpmobileでは、限定的ですが絵文字の取り扱いをサポートしています。

絵文字をテンプレート内に記述する
================================

単純に表示するだけであれば、DoCoMoの絵文字コードをそのまま埋め込むことで表示することができます。EZWeb、SoftBankではこの場合、各キャリアのサーバで変換されるようです。

しかし、絵文字を表示するためのフォントや入力するソフトウェアが必要な点を考え、django-bpmobileではemojiを代替のタグで記述可能にしています。

:ref:`templatetags-emoji` を利用することで絵文字を表示することができます。

.. code-block:: html+django

  {% emoji "識別名" %}

.. _emoji-identify_name:

絵文字の識別名
==============

:ref:`templatetags-emoji` タグ用の識別名は現在\ `Table for Working Draft Proposal for Encoding Emoji Symbols <http://www.unicode.org/~scherer/emoji4unicode/20081210/full.html>`_\ のName&Annotationsを使用しています。

.. code-block:: html+django

  {% emoji "BLACK SUN WITH RAYS" %}

テンプレートコンテキストの絵文字を表示する
==========================================

コンテキストの絵文字を表示する場合は :ref:`templatetags-emojicontents` タグをを利用します。
