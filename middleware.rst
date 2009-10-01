.. _middleware:

============
ミドルウェア
============

django-bpmobileでは、モバイル開発をサポートするためにいくつかのミドルウェアを提供しています。

BPMobileMiddleware
==================

キャリア判別を行い、request.agentにuamobileのagent情報を与えます。また、GET/POSTパラメータの絵文字をDoCoMoコードに変換します。

BPMobileConvertResponseMiddleware
=================================

キャリアごとに推奨する文字コードでresponseをエンコードします。
文字コードは以下の通りです。

========= ========= ========
DoCoMo    au(EZWeb) SoftBank
========= ========= ========
cp932     cp932     utf8
========= ========= ========

BPMobileSessionMiddleware
=========================

モバイル向けのセッション機能を提供します。au(EZWeb)、SoftBankはCookieを利用します。DoCoMoの場合には、iモードIDとセッションキーを対応させてセッションを利用できるようにします。iモードIDとセッションキーの対はDjangoのキャッシュフレームワークによって保持されます。\ :ref:`session`\ についてのドキュメントを参照してください。
