.. _context_processor:

======================
コンテキストプロセッサ
======================

.. _context_processor-agent:

agent
=====

uamobileのAgentオブジェクトです。

.. code-block:: html+django

  {% if agent.is_docomo %}
  DoCoMo端末です。
  {% endif %}
  モデル名は {{ agent.model }} です。

このコンテキストプロセッサを利用するには、 ``settings.py`` の ``TEMPLATE_CONTEXT_PROCESSORS`` に ``bpmobile.context_processors.agent`` を追加します。
