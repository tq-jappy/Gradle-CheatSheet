実行可能Jar
=========================

.. sourcecode:: groovy

   jar {
       copy {
           from configurations.compile
           into "build/distribution/lib"
       }
       def manifestClasspath = configurations.compile.collect{ 'lib/' + it.getName() }.join(' ')
       manifest {
           attributes "Main-Class" : "foo.bar.Main"
           attributes 'Class-Path': manifestClasspath
       }
       from (configurations.compile.resolve().collect { it.isDirectory() ? it : fileTree(it) }) {
           exclude 'META-INF/MANIFEST.MF'
           exclude 'META-INF/*.SF'
           exclude 'META-INF/*.DSA'
           exclude 'META-INF/*.RSA'
           exclude '**/*.jar'
       }
       destinationDir = file("build/distribution")
   }

実行可能FatJar
=========================

.. sourcecode:: groovy

   jar {
     from configurations.compile.collect { it.isDirectory() ? it : zipTree(it) }
     manifest.mainAttributes("Main-Class" : "foo.bar.Main")
   }
