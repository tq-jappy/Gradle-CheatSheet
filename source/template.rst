build.gradle のテンプレート
=========================

.. sourcecode:: groovy

  // plugins
  apply plugin: "java"
  apply plugin: "maven"
  apply plugin: "application"

  // properties
  sourceCompatibility = '1.7'
  def defaultEncoding = 'UTF-8'
  [
    compileJava,
    compileTestJava,
    javadoc
  ]*.options*.encoding = defaultEncoding

  // repositories
  repositories {
    mavenCentral()
    mavenLocal()
    maven {
      url "http://maven.seasar.org/maven2"
      url "http://repository.jboss.org/nexus/content/groups/public-jboss/"
    }
  }

  // configurations
  configurations {
    doc // extra configuration
  }

  // dependencies
  dependencies {
    // 'groupId:module:version'
    compile 'g:m:v'
    // runtime
    // providedCompile
    testCompile 'junit:junit:4.11'
    // testRuntime
    doc 'g:m:v@zip' // @ext
  }

  // tasks
