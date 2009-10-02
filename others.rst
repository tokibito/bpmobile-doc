.. _others:

======
その他
======

iモードIDを利用する
===================

2009年9月現在、NTT DoCoMoが公開している\ `iモードHTMLシミュレータII <http://www.nttdocomo.co.jp/service/imode/make/content/browser/html/tool2/index.html>`_\ はiモードIDに対応していません。django-bpmobileでは、Djangoの ``runserver`` コマンドの代わりに、サーバサイドでiモードIDのシミュレーションをサポートする ``runserver_imode`` コマンドを提供しています。iアプリの開発で利用することもできます。

.. code-block:: bash

  $ python manage.py runserver_imode --guid=1234567

指定した文字コードで出力したい
==============================

django-bpmobileのデフォルト出力文字コード以外のコードで、レスポンスを返したい場合には ``encoded_response`` デコレータを使用します。

.. code-block:: python

  from django.http import HttpResponse
  from bpmobile.decorators import encoded_response

  @encoded_response(encoding='cp932', charset='Shift_JIS', content_type='text/html')
  def some_view(request):
      return HttpResponse(u'これはどのキャリアでもShift_JISになります。')
