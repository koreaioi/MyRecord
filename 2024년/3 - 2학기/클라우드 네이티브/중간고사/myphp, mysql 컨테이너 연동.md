# myphp, mysql 컨테이너 연동

## 네트워크 흐름

![image](https://github.com/user-attachments/assets/c7380ee7-7db8-49ff-9c4b-e34cdd0cc9e6)

## 통신 절차

1. 브라우저(윈도우 크롬)에서 우분투 서버의 IP 주소 192.168.135.130:80 으로 접속한다.
2. Docker 가상 NAT 라우터의 포트포워딩 설정으로 172.18.0.3:80(myphp컨테이너)으로 접속한다.
3. myphp 서버의 첫 페이지가 로드된다.
4. 첫 페이지가 로드된 후, fetchtasks()함수의 $.ajax가 비동기적으로 tasks-list.php에 GET요청을 보낸다.
5. tasks-list.php에서 MySQL 데이터 베이스에 접속하여 task 데이터를 조회하여 반환한다.
6. myphp 컨테이너와 MySQL 컨테이너는 같은 네트워크에 있으므로 2 계층에서 통신한다.
7. MysQL 서버의 데이터가 myphp컨테이너로 반환된다.
8. myphp 컨테이너가 mysql 데이터를 기반으로 json을 반환한다.
9. 브라우저에서 js의 fetchtasks()함수에서 json을 response받고 파싱하여 현재 브라우저 화면을 업데이트한다.