# Opensource Guide

This guide is for who want to restrucure own's system to open source.
There are some simple steps.

## Table of Contents

 - [Getting Started](#getting-started)
 - [CI/CD Pipeline](#ci/cd-pipeline)
 - [Documentation](#documentation)
 - [Site](#site)
 - [Etc](#etc)

## Getting Started
## CI/CD Pipeline]

### Planing

### Develop

### CI/CD

#### Travis
- Travis CI, Github계정으로 회원가입
- 연동시킬 Repository 활성화
- Project root경로에 .travis.yml 작성  

```yml   

language: java
jdk:
  - openjdk11  # using jdk11 at least for sonarcloud

branches:
  only:
    - master

# Travis CI 서버의 Home
cache:
  directories:
    - $HOME/.m2

# CI 실행 완료시 메일로 알람
notifications:
  email:
    recipients:
      - your@Email.com
      
```
- Github Readme.md에 Travis badge 추가  
+ 참고 사이트  https://velog.io/@recordsbeat/travis-ci-maven-%EC%97%B0%EB%8F%99

### Build

#### Code Coverage - CodeCov
- codecov 사이트 가입 후 repository 활성화  
- travis.yml script추가  

```yml
script: "mvn cobertura:cobertura"
after_success:
  - bash <(curl -s https://codecov.io/bash)
  - codecov
env:
   - CODECOV_TOME=583d22f4-1c33-4b5f-91ad-a370a0290fab
```
- pom.xml plugin 추가 
 
```xml
<plugin>
	<groupId>org.codehaus.mojo</groupId>
	<artifactId>cobertura-maven-plugin</artifactId>
	<version>2.7</version>
	<configuration>
		<formats>
			<format>html</format>
			<format>xml</format>
		</formats>
		<check />
	</configuration>
</plugin>
```
#### Code Quality - SonarCloud
- SonarCloud와 Github연결  
- SonarCloud 회원가입(https://sonarcloud.io/)  
- Allow to access for github repository
- get secure key

```shell
gem install travis
travis login --github-token ghp_uS****************wtN0iiSxg
travis encrypt SOMEVAR="fe7fe6**********e014803dfa8f" -r giyeonYu/OSS
```
ghp_uS****************wtN0iiSxg => github token
fe7fe6**********e014803dfa8f => travis token
+ edit .travis.yml

```yml
addons:
  sonarcloud:
    organization: "giyeonyu"
    token:
      secure: "**************************" # encrypted value of your token

script:
  # the following command line builds the project, runs the tests with coverage and then execute the SonarCloud analysis
  - mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install sonar:sonar -Dsonar.login=c1a58ac2e42e06851dd4e9c8de969a76a1d53a1f
```
sonarcloud needs over jdk11 at least.

### Verify

### Release

### Feedback

## Documentation

## Site - Gatsby Static Site Generator
+ Gatsby Starter Template사이트에 방문하여 원하는 Template 설치 
  https://www.gatsbyjs.com/starters/  
```shell
# Insatllation with 'git clone'
git clone git@github.com:<user>/<repository> my-site
cd my-site
# Installation dependency
yarn insatll       
# To develop
yarn develop
# To build
yarn build
# To start
gatsby develop
```
+ Git Repository에 Push
+ Git Page 연동
  - 해당 repository의 Settings
  - Pages에서 해당 branch, root 로 설정하여 저장
  ![image](https://user-images.githubusercontent.com/20086137/114368273-36c37900-9bb8-11eb-9d9b-e090513ce31c.png)

## Etc
### Telegram Notify
1.Add ./github/workflow/main.xml for github action
```yml
name: telegram message
on: [push]
jobs:

  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: send custom message
      uses: appleboy/telegram-action@master
      with:
        to: ${{ secrets.TELEGRAM_TO }}
        token: ${{ secrets.TELEGRAM_TOKEN }}
        message: |
          The ${{ github.event_name }} event triggered final step.
          echo This event is a pull request that had an assignee removed.
```
2.Add repository secrets
+ Settings ->  Secrets
- TELEGRAM_TO, TELEGRAM_TOKEN 생성
- guide to get TELEGRAM_TO, TELEGRAM_TOKEN (https://core.telegram.org/bots/api)



