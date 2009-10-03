.. _tutorial:

==============
チュートリアル
==============

django-bpmobileを利用してみましょう。

bpmobileを有効にする
====================

まず、 ``django-admin.py startproject`` コマンドでプロジェクトを作成しておき、以下の手順でbpmobileを有効にします。

``settings.py`` の ``INSTALLED_APPS`` に ``bpmobile`` を追加します。

.. code-block:: python

  INSTALLED_APPS = (
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.sites',
      'bpmobile', # added
  )

``settings.py`` の ``MIDDLEWARE_CLASSES`` に必要なミドルウェアクラスを追加します。

.. code-block:: python

  MIDDLEWARE_CLASSES = (
      'django.middleware.common.CommonMiddleware',
      'django.contrib.sessions.middleware.SessionMiddleware',
      'django.contrib.auth.middleware.AuthenticationMiddleware',
      'bpmobile.middleware.BPMobileMiddleware', # added
      'bpmobile.middleware.BPMobileConvertResponseMiddleware', # added
  )

``settings.py`` の ``TEMPLATE_CONTEXT_PROCESSORS`` に必要なコンテキストプロセッサを追加します。

.. code-block:: python

  from django.conf import global_settings
  TEMPLATE_CONTEXT_PROCESSORS = global_settings.TEMPLATE_CONTEXT_PROCESSORS + (
      'bpmobile.context_processors.agent', # added
  )

``TEMPLATE_CONTEXT_PROCESSORS`` は、生成された ``settings.py`` では省略されているので上記のように書いています。

以上でbpmobileが有効になります。

ビューでキャリアの判定を行う
============================

``manage.py startapp`` コマンドで ``myapp`` という名前のアプリケーションを作成して、 ``INSTALLED_APPS`` に追加しておきます。

プロジェクトの ``urls.py`` で `myapp.views.my_view` を追加しておきます。

.. code-block:: python

  from django.conf.urls.defaults import *
  
  urlpatterns = patterns('',
      (r'^$', 'myapp.views.my_view'),
  )

``myapp/views.py`` にmy_viewを実装します。

.. code-block:: python

  # coding:utf-8
  from django.http import HttpResponse
  def my_view(request):
      if request.agent.is_docomo():
          return HttpResponse(u'DoCoMoです。')
      elif request.agent.is_ezweb():
          return HttpResponse(u'EZWebです。')
      elif request.agent.is_softbank():
          return HttpResponse(u'SoftBankです。')
      else:
          return HttpResponse(u'その他です。')

``manage.py runserver`` コマンドを実行して、ウェブブラウザで確認してみましょう。通常、PCからの場合には "その他です。" と表示されるはずです。他のAgentを試す場合には、\ `firemobilesimulator <http://firemobilesimulator.org/>`_\ などを利用すると便利です。

テンプレートでキャリアの判定を行う
==================================

テンプレートでも同様に :ref:`context_processor-agent` コンテキストを利用して、判定を行うことができます。

``urls.py`` で汎用ビューの ``direct_to_template`` を使うように変更します。

.. code-block:: python
  
  from django.conf.urls.defaults import *
  
  urlpatterns = patterns('',
      (r'^$', 'django.views.generic.simple.direct_to_template', {'template': 'index.html'}),
  )

``myapp/templates/index.html`` にテンプレートを作成します。

.. code-block:: html+django
  
  {% if agent.is_docomo %}
    DoCoMoです。
  {% else %}
    {% if agent.is_ezweb %}
      EZWebです。
    {% else %}
      {% if agent.is_softbank %}
        SoftBankです。
      {% else %}
        その他です。
      {% endif %}
    {% endif %}
  {% endif %}

以上です。このコードは前述のビューでキャリアの判別を行った例と同様の動作します。

フォームの入力フォーマットを指定する
====================================

フォームの入力時に英数やひらがななどの入力フォーマットの指定を行うことができます。

``urls.py`` で ``myapp.views.my_view`` を使うように変更しておきます。

``myapp/views.py`` でフォームを使うように変更します。

.. code-block:: python
  
  from django.views.generic.simple import direct_to_template
  from django import forms
  
  class MyForm(forms.Form):
      my_field = forms.CharField()
  
  def my_view(request):
      form = MyForm()
      return direct_to_template(request, 'index.html', {'form': form})

``myapp/templates/index.html`` で ``mobile`` テンプレートタグセットをロードし、 :ref:`templatetags-mobile_input_format` タグにフォームのフィールドと入力フォーマットを指定します。

.. code-block:: html+django
  
  {% load mobile %}
  <?xml version="1.0" encoding="{% mobile_encoding %}"?>
  <!DOCTYPE html PUBLIC "-//i-mode group (ja)//DTD XHTML i-XHTML(Locale/Ver.=ja/1.1) 1.0//EN" "i-xhtml_4ja_10.dtd">
  <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="ja">
    <head>
      <meta http-equiv="Content-Type" content="application/xhtml+xml; charset={% mobile_encoding %}" />
      <title></title>
    </head>
    <body>
      <form>
        {% mobile_input_format form.my_field alphabet %}
      </form>
    </body>
  </html>

mobile_input_formatはスタイルシートによる指定を行うため、XHTML+CSSを使えるようにしています。
