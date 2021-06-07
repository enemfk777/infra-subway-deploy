# 그럴듯한 서비스 만들기
## 2단계 - 서비스 배포하기
### 요구사항
- [x] 운영 환경 구성하기
- [ ] 개발 환경 구성하기

### 요구사항 설명
**운영 환경 구성하기**
- [x] 웹 애플리케이션 앞단에 Reverse Proxy 구성하기
    - [x] 외부망에 Nginx로 Reverse Proxy를 구성
        * ec2 instance name : enemfk777-ec2-public-reverse-proxy
        * bastion alias name : nginx ex) ssh ubuntu@nginx
        * enemfk777-security-group-nginx security group 적용
            * 인바운드 80포트 모든 IP에 오픈
            * 인바운드 443포트 모든 IP에 오픈
            * 인바운드 22포트 admin subnet 대역에 대해 오픈
        * RUNNINGMAP 어플리케이션이 구동되는 인스턴스의 enemfk777-security-group-public security gorup은 인바운드 범위 축소
            * 인바운드 8080포트 public subnet 01 (reverse proxy 인스턴스가 속한 subnet)의 대역
            * 인바운드 22포트 admin subnet 대역에 대해 오픈
    - [x] Reverse Proxy에 TLS 설정
      * https://public.enemfk777.kro.kr/
- [x] 운영 데이터베이스 구성하기
    * ec2 instance name : enemfk777-ec2-private-01
    * bastion alias name : private01 ex) ssh ubuntu@private01
    * docker 설치를 위해 인터넷 게이트웨이 라우팅 테이블에 private subnet을 잠시 추가해서 작업후 다시 제거

**개발 환경 구성하기**
- [x] 설정 파일 나누기
    * JUnit : h2, Local : docker(mysql), Prod : 운영 DB를 사용하도록 설정
- [x] 데이터베이스 테이블 스키마 버전 관리
- [x] SonarLint 설정하기
- [x] MultiRun 설정하기
