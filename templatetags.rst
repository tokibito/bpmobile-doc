================
テンプレートタグ
================

django-bpmobileのテンプレートタグセットを利用するには、テンプレート内に以下の内容を記述します。

.. code-block:: html+django

  {% load mobile %}

emoji
=====

DoCoMoの絵文字コードを挿入します。

.. code-block:: html+django

  {% emoji "識別名" %}

識別名については、絵文字についてを参照してください。

emojicontents
=============

emojicontents～endemojicontents間の絵文字コードをDoCoMoのコードに変換します。

.. code-block:: html+django

  {% emojicontents %} ... {% endemojicontents %}

mobileurl
=========

Django標準のurlタグと同等ですが、DoCoMoのAgentに対してguid=onパラメータを自動的に付与します。_paramsにはGETパラメータを指定することができます。_anchorにアンカーを指定することができます。_noguidを入れるとguid=onを付与しません。

.. code-block:: html+django

  {% mobileurl some_view arg1,arg2,name1=value1,_params=param1=val1&param2=val2,_anchor=foo,_noguid %}

mobile_input_format
===================

1行テキストフィールドに対して、英数、かな、数字などの入力フォーマットを指定します。

.. code-block:: html+django

  {% mobile_input_format some_form.field format %}

1つ目の引数には、フォームインスタンスのフィールドを指定します。2つ目の引数に入力フォーマットを指定します。このタグは、指定したフィールドに対してウィジェットを独自のものに差し替えてレンダリングを行います。指定できる入力フォーマットは以下の通りです。

============ ====================
フォーマット 意味
============ ====================
hiragana     ひらがな
hankana      半角カナ
alphabet     アルファベット(英数)
numeric      数字
============ ====================

キャリアごとに制限が違うので、必ずこの入力になるとは限りません。入力値の検証は必ず行ってください。

mobile_encoding
===============

キャリアごとで使用される文字コード名を出力します。

.. code-block:: html+django

  {% mobile_encoding %}

出力される文字列は以下の通りです。

========= ========= ========
DoCoMo    au(EZWeb) SoftBank
========= ========= ========
Shift_JIS Shift_JIS UTF-8
========= ========= ========

gif_or_png
==========

キャリアごとに推奨されるラスターイメージフォーマットの拡張子文字列を出力します。

.. code-block:: html+django

  {% gif_or_png %}

出力される文字列は以下の通りです。

====== ========= ========
DoCoMo au(EZWeb) SoftBank
====== ========= ========
gif    png       png
====== ========= ========

現在はGIFに統一することでもおおむね問題ないそうですが(詳細は未確認)、歴史的な事情もありこのタグを残しています。
