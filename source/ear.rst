Ear
=========================

.. sourcecode:: groovy

   dependencies {
     deploy project(':war')

     earlib 'log4j:log4j:1.2.15@jar'
   }

   war {
     appDirName 'src/main/app'
   }
