## 오늘 찾아보 링크 목록

[s3 관련 application.yml 설정](https://antdev.tistory.com/93)

## 공부한 내용

### s3 application.yml

s3를 사용하기 위해서 application.yml 설정을 진행했다. accesskey와 secretkey만 있으면 되는 줄 알았는데
cloud.aws.stack.auto를 안해줘서 문제가 생겼다. ec2에서 프로그램을 실행하면 자동으로 Cloud Formation가 실행되는 데 이게 문제가 되어 실행이 안된다고 한다.
