War
=========================

.. sourcecode:: groovy

   apply plugin: "war"

   configurations {
     moreLibs
   }

   war {
     from 'src/main/webapp'
     classPath configurations.moreLibs
   }
