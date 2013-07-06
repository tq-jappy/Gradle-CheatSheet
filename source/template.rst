build.gradle のテンプレート
=========================

.. sourcecode:: groovy

  // plugins
  apply plugin: "java"
  apply plugin: "maven"
  apply plugin: "groovy"
  apply plugin: "application"

  // default tasks
  defaultTasks 'clean', 'build'

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
    compile 'org.codehaus.groovy:groovy-all:2.0.5'
    // runtime
    testCompile 'junit:junit:4.11'
    // testRuntime

    // extra configuration
    doc 'g:m:v@zip' // @ext

    // providedCompile(War plugin)
    // providedRuntime(War plugin)
  }

  // tasks
