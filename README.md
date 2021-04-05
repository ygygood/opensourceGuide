# Opensource Guide

## Site 구축(Gatsby)

## Github 구축

## Opensource IC
### Build
Travis연동
https://velog.io/@recordsbeat/travis-ci-maven-%EC%97%B0%EB%8F%99
1.travis 페이지 가입(github계정) 후 repository 활성화
2..travis.yml 작성
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
3.github에 readme.md 태그 달기
### Test
### Code Coverage
1.codecov 사이트 가입 후 repository 활성화
2..travis.yml script추가
3.pom.xml plugin 추가
### Static Test
### Release
