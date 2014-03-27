静的解析(Checkstyle/Findbugs/JaCoCo)
===========================================================

build.gradle

.. sourcecode:: groovy

  apply plugin: "checkstyle"
  apply plugin: "findbugs"
  apply plugin: "jacoco"

  test.jvmArgs '-XX:-UseSplitVerifier'
  [checkstyleMain, checkstyleTest, findbugsMain, findbugsTest]*.ignoreFailures = true
  [checkstyleTest, findbugsTest]*.excludes = ['**/*']
  // checkStyleMain {
  //   configFile = file('config/checkstyle/checkstyle.xml')
  // }
  // jacocoTestReport {
  //   xml.enabled true
  //   csv.enable true
  // }

タスク

- check
- jacocoTestReport

レポート

- :file:`build/reports/checkstyle/main.xml`
- :file:`build/reports/findbugs/main.xml`
- :file:`build/reports/jacoco/test/html/*.html`,
  :file:`build/reports/jacoco/test/jacocoTestReport.xml`,
  :file:`build/reports/jacoco/test/jacocoTestReport.csv`
