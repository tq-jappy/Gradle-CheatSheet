Wrapper
=========================

before 1.6
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   task wrapper(type: Wrapper) {
     gradleVersion = '1.6'
   }

:command:`gradlew` で実行。

1.7 or later
~~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: groovy

   wrapper {
     gradleVersion '1.6'
   }

:command:`gradle wrapper` で実行できるようになる（らしい）。。