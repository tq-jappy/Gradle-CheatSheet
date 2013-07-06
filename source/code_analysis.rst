静的解析
=========================

build.xml

.. sourcecode:: groovy

  apply plugin: "checkstyle"
  apply plugin: "findbugs"
  buildscript {
    apply from: 'https://github.com/valkolovos/gradle_cobertura/raw/master/repo/'
                + 'gradle_cobertura/gradle_cobertura/1.2.1/coberturainit.gradle'
  }

  test.jvmArgs '-XX:-UseSplitVerifier'
  [checkstyleMain, checkstyleTest, findbugsMain, findbugsTest]*.ignoreFailures = true
  [checkstyleTest, findbugsTest]*.excludes = ['**/*']
  // checkStyleMain {
  //   configFile = file('config/checkstyle/checkstyle.xml')
  // }

タスク

- check
- coberturaMain

レポート

- :file:`build/reports/checkstyle/main.xml`
- :file:`build/reports/findbugs/main.xml`
- :file:`build/reports/cobertura/coverage.xml`
