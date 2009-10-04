.. _session:

==========
セッション
==========

DoCoMo端末は一部機種を除いてCookieに対応していないため、Djangoのセッションミドルウェアでセッションを利用することができません。django-bpmobileではDoCoMo端末の場合にiモードIDを利用するセッションミドルウェアを提供しています。

セッションミドルウェアを設定する
================================

django-bpmobileのセッションミドルウェアを利用するには、 ``settings.py`` の ``MIDDLEWARE_CLASSES`` に必要なミドルウェアクラスを追加します。

.. code-block:: python

  MIDDLEWARE_CLASSES = (
      'django.middleware.common.CommonMiddleware',
      'django.contrib.sessions.middleware.SessionMiddleware',
      'django.contrib.auth.middleware.AuthenticationMiddleware',
      'bpmobile.middleware.BPMobileMiddleware', # added
      'bpmobile.middleware.BPMobileConvertResponseMiddleware', # added
      'bpmobile.middleware.BPMobileSessionMiddleware', # added
  )

設定は以上です。これでセッションを利用できます。DoCoMo端末ではGETパラメータに ``guid=on`` が含まれていないとiモードIDを取得できないため、このパラメータが含まれないリクエストに対しては、 ``guid=on`` を付与したURLに自動的にリダイレクトレスポンスを返します。

セッションを利用する場合の注意点
================================

iモードIDはHTTPSでは利用できないため、このセッションミドルウェアはHTTP専用です。

独自にセッションミドルウェアを書いて対応する必要があります。

良いコードがあるなら是非パッチを下さい:-)
