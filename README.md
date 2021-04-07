# Opensource Guide

## Site 구축(Gatsby)

## Github 구축

## Opensource CI
---
### Build - Travis
---
1.travis 페이지 가입(github계정) 후 repository 활성화  
1.travis.yml 작성
```yml
language: java
jdk:
  - openjdk8

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
 maven 프로젝트는 'mvn test -B' 커멘드를 기본으로 설정하기 때문에 별도의 script를 적지 않아도 테스트와 빌드를 진행한다.
1.github에 readme.md 태그 달기  

+ 참고 사이트  https://velog.io/@recordsbeat/travis-ci-maven-%EC%97%B0%EB%8F%99

### Test
### Code Coverage - CodeCov
1.codecov 사이트 가입 후 repository 활성화  
1.travis.yml script추가  
```yml
script: "mvn cobertura:cobertura"
after_success:
  - bash <(curl -s https://codecov.io/bash)
  - codecov
env:
   - CODECOV_TOME=583d22f4-1c33-4b5f-91ad-a370a0290fab
```
1.pom.xml plugin 추가  
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
### Code Quality - SonarCloud
1.SonarCloud와 Github연결  
+ SonarCloud 회원가입(https://sonarcloud.io/)  
+ 

3.ddd
### Static Test
### Release
