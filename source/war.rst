War
=========================

.. sourcecode:: groovy

   configurations {
     moreLibs
   }

   war {
     from 'src/main/webapp'
     classPath configurations.moreLibs
   }
