アーティファクト
=========================

.. sourcecode:: groovy

   artifacts {
     archives jar
   }

   install
     repositories {
       mavenInstaller {
         pom.groupId = 'com.github.tq-jappy'
         pom.version = '1.0.0-SNAPSHOT'
         pom.artifactId = 'example'
       }
     }
   }
