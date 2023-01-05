## Documentation

* [Test Automation Framework Design](https://drive.google.com/file/d/1rBKc4p7IKA5iQXBX6F2gbWUtoq6sY1D9/view?usp=sharing)
* [Test Automation Tech Stack Decision](https://drive.google.com/file/d/125eQoai7GzwMWq6vDXe5K2Hum-WmNyzj/view?usp=sharing)
* [Test Reports attachment](https://drive.google.com/drive/folders/1ry2Hzd_Fb2uhLah_0djUtewlAcR2GkpD?usp=sharing)
* [Test Cases](https://docs.google.com/document/d/18lLFhcvEJlakTtT2YbWX3cFtFoaq_pshBVvwzz5sYEU/edit?usp=sharing)

## Defects

* [List defects which are found while executing test](https://github.com/vietnd96/fs-test-automation/issues)

## List dependency repositories

1. [test-automation-fwk](https://github.com/vietnd96/test-automation-fwk)
2. [test-java2robot-adapter](https://github.com/vietnd96/test-java2robot-adapter)
3. [test-robot-framework](https://github.com/vietnd96/test-robot-framework)
4. [test-webdriver-downloader](https://github.com/vietnd96/test-webdriver-downloader)

## System requires

1. Git (Tested version 2.30.0). Ensure that code can be cloned from GitHub via SSH.
2. Apache Maven (Tested version 3.8.6). Ensure that there is no connection blocker to reach Maven Central Repository for
   downloading dependencies.
3. Java JDK, JRE (Tested openjdk 11.0.16 2022-07-19)
4. Chrome (Tested version 108.0.5359.125)

## Steps to execute test cases

#### 1. Clone this repository "fs-test-automation"

```shell
~$ git clone git@github.com:vietnd96/fs-test-automation.git
```

#### 2. Clone dependency repositories by executing Maven command in repo "fs-test-automation"

```shell
~$ cd fs-test-automation
fs-test-automation$ mvn -f checkout.xml initialize
```

Note: In the first time, this command is used to clone all dependency repositories. Later, it would be used to pull the
latest code from the remote.

#### 3. Ensure that all dependency repositories are cloned successfully

```shell
fs-test-automation$ ls -1
  checkout.xml
  pom.xml
  test-automation-fwk
  test-java2robot-adapter
  test-robot-framework
  test-webdriver-downloader
```

#### 4. Build the repository "fs-test-automation"

```shell
fs-test-automation$ mvn clean install
```

#### 5. Ensure that selenium-server jar and drivers are downloaded successfully

Noted: Below result is tested on Ubuntu. Based on OS, the packages would be downloaded.

```shell
fs-test-automation$ ls -1 test-webdriver-downloader/Drivers
    chromedriver-linux-64bit
    chromedriver-linux-64bit.version
    edgedriver-linux-64bit
    edgedriver-linux-64bit.version
    geckodriver-linux-64bit
    geckodriver-linux-64bit.version
    operadriver-linux-64bit
    operadriver-linux-64bit.version
    phantomjs-linux-64bit
    phantomjs-linux-64bit.version
    selenium-server
    selenium-server.version
```

#### 6. Start Selenium Server (Hub & Node). Keep both these 2 terminals running

```shell
fs-test-automation$ cd test-webdriver-downloader/Drivers
fs-test-automation/test-webdriver-downloader/Drivers$ java -jar selenium-server hub
```

```shell
fs-test-automation$ cd test-webdriver-downloader/Drivers
fs-test-automation/test-webdriver-downloader/Drivers$ java -jar selenium-server node --port 5555
```

#### 7. Open another terminal to execute test cases

```shell
fs-test-automation$ cd test-robot-framework
fs-test-automation/test-robot-framework$ mvn -f pom.xml initialize robotframework:run -Dincludes=Statistics
```

#### 8. Checkout the test report.html and screenshots after execution completed

```shell
fs-test-automation/test-robot-framework$ ls -1 target/reports/
    TEST-acceptance.xml
    log.html
    output.xml
    report.html
fs-test-automation/test-robot-framework$ ls -1 target/screenshots/
```

#### Video of demonstration steps to execute test cases

[![Video of demonstration](https://img.youtube.com/vi/bNN0VEqlRMc/maxresdefault.jpg)](https://youtu.be/bNN0VEqlRMc)
