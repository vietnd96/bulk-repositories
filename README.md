## Introduction

This is a project with lots of micro repositories that would be managed and worked on.<br>
This provides some operations to interact with bulk repositories source code, such as: clone, pull and tag

## Documentation

* [Test Automation Framework Design](https://drive.google.com/file/d/1rBKc4p7IKA5iQXBX6F2gbWUtoq6sY1D9/view?usp=sharing)
* [Test Automation Tech Stack Decision](https://drive.google.com/file/d/125eQoai7GzwMWq6vDXe5K2Hum-WmNyzj/view?usp=sharing)
* [Test Reports attachment](https://drive.google.com/drive/folders/1ry2Hzd_Fb2uhLah_0djUtewlAcR2GkpD?usp=sharing)
* [Test Cases](https://docs.google.com/document/d/18lLFhcvEJlakTtT2YbWX3cFtFoaq_pshBVvwzz5sYEU/edit?usp=sharing)

## Defects

* [List defects which are found while executing test](https://github.com/vietnd96/test-automation-project/issues)

## List dependency repositories

1. [test-parent-pom](https://github.com/vietnd96/test-parent-pom)
2. [test-automation-fwk](https://github.com/vietnd96/test-automation-fwk)
3. [test-java2robot-adapter](https://github.com/vietnd96/test-java2robot-adapter)
4. [test-robot-framework](https://github.com/vietnd96/test-robot-framework)
5. [test-webdriver-downloader](https://github.com/vietnd96/test-webdriver-downloader)

## System requires

1. Git (Tested version 2.30.0). Ensure that code can be cloned from GitHub via SSH.
2. Apache Maven (Tested version 3.8.6). Ensure that there is no connection blocker to reach Maven Central Repository for
   downloading dependencies.
3. Java JDK, JRE (Tested in [17.0.2 (build 17.0.2+8)](https://jdk.java.net/archive/))
4. Chrome (Tested version 108.0.5359.125)

## Steps to execute test cases

#### 1. Clone this repository "test-automation-project"

```shell
git clone git@github.com:vietnd96/test-automation-project.git
```

#### 2. Clone dependency repositories by executing Maven command in repo "test-automation-project"

```shell
cd test-automation-project
```

```shell
mvn initialize -Dhelper=clone
```

Notes:

* In case you would like to pull the latest code from the remote.

```shell
mvn initialize -Dhelper=pull
```

* In case you would like to tag and push changes to remote.

```shell
mvn initialize -Dhelper=tag -Dgoal=tag -DpushChanges=true -Dname=RELEASE_TAG
```

#### 3. Ensure that all dependency repositories are cloned successfully

```text
test-automation-project$ ls -1
  pom.xml
  test-parent-pom
  test-automation-fwk
  test-java2robot-adapter
  test-robot-framework
  test-webdriver-downloader
```

#### 4. Build the repository "test-automation-project"

```shell
mvn clean install
```

#### 5. Ensure that selenium-server jar and drivers are downloaded successfully

Noted: Below result is tested on Ubuntu. Based on OS, the packages would be downloaded.

```text
test-automation-project$ ls -1 test-webdriver-downloader/Drivers
    chromedriver-linux-64bit
    chromedriver-linux-64bit.version
    edgedriver-linux-64bit
    edgedriver-linux-64bit.version
    geckodriver-linux-64bit
    geckodriver-linux-64bit.version
    operadriver-linux-64bit
    operadriver-linux-64bit.version
    selenium-server
    selenium-server.version
```

#### 6. Start Selenium Server (Hub & Node). Keep both these 2 terminals running

```shell
cd test-webdriver-downloader/Drivers
```

```shell
java -jar selenium-server hub
```

```shell
java -jar selenium-server node --port 5555
```

#### 7. Open another terminal to execute test cases

```shell
cd test-robot-framework
```

```shell
mvn -f pom.xml initialize robotframework:run -Dincludes=Statistics
```

Note: In case Selenium Hub is running in another server, kindly provide the hub URL via property "selenium.hub.url" from
command line<br>
For example:

```shell
mvn -f pom.xml initialize robotframework:run -Dincludes=Statistics -Dselenium.hub.url=https://controller-hub.ndviet.com:4444
```

#### 8. Checkout the test report.html and screenshots after execution completed

```text
test-automation-project/test-robot-framework$ ls -1 target/reports/
```

#### Video of demonstration steps to execute test cases

[![Video of demonstration](https://img.youtube.com/vi/bNN0VEqlRMc/maxresdefault.jpg)](https://youtu.be/bNN0VEqlRMc)
