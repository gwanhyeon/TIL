# nginx 사용하여 포트리다이렉트

Nginx
기본 nginx 설정 파일을 보면 Forward(순방향) Proxy입니다. Forward Proxy는 경로로 들어오는 경우, root에 지정된 경로에 따라 일치하는 파일로 이동하여 웹에서 내용을 보여줍니다.
하지만, Nginx 서버에서 Reverse Proxy 기능을 제공합니다. Forward Proxy와 다르게 외부에서 내부 서버가 제공하는 서비스에 접근할 때, proxy 서버를 먼저 거쳐 내부 서버로 들어오는 방식입니다. 외부 클라이언트는 실제 내부 서버의 존재를 모릅니다.
모든 접속은 Reverse Proxy 서버에게 들어오며, Reverse Proxy 서버는 요청에 맵핑되는 서버의 정보에게 요청을 넘겨줍니다. 이처럼 내부 서버의 정보를 외부로부터 숨길 수 있기 때문에 보안이 높아집니다.
또, proxy 서버가 내부 서버의 정보를 알고 있으므로 로드 밸런싱을 통해 부하 여부에 따라 요청을 분배할 수 있습니다. proxy 서버를 사용하여 캐싱 기능과 트랙핑 분산 기능을 결합시켜 전반적인 서버 성능의 향상 또한 기대할 수 있습니다.

Nginx 관련 커맨드
nginx -t                    # nginx 설정 파일의 문법이 올바른지 확인

sudo service nginx status     # nginx 상태 확인

sudo service nginx start    # nginx 실행
sudo service nginx restart    # 중지 후 재실행
sudo servcie nginx reload    # 수정된 파일 적용하여 연결을 끊지 않고 재실행
sudo service nginx stop        # nginx 중지

# 기본적으로 Nginx는 서버가 부팅될 때 자동으로 시작됩니다.
sudo service disable nginx    # 자동 시작 비활성화
sudo service enable nginx    # 자동 시작 활성화
Nginx 설치
sudo apt-get update
sudo apt install nginx -y
nginx -v
sudo service nginx status
Nginx가 active 상태라고 뜹니다. 만약 active 상태가 아니라면 sudo service nginx start를 입력해 서버를 실행할 수 있습니다.
퍼블릭 IP 주소를 주소창에 입력해보면 Nginx 기본 페이지가 출력됩니다!
개발자 도구(F12)를 눌러 Network를 살펴보면 HTTP인 80번 포트로 연결된 것을 볼 수 있습니다😀! 이제 Nginx를 이용해, HTTP 80번 포트로 접속했을 때 Tomcat 8080번 포트로 리다이렉트할 수 있게 해보겠습니다. 이 과정을 거쳐 Spring Boot 프로젝트가 화면에 보여집니다!

Nginx 'server block(서버 블록)' 설정
Nginx 웹 서버를 사용할 때, (Apache의 가상 호스트와 유사한) 서버 블록을 사용해 구성 세부 정보를 캡슐화하고 단일 서버에서 둘 이상의 도메인을 호스팅할 수 있습니다. Nginx는 기본적으로 활성화된 하나의 서버 블록(/var/www/html)이 있으며, 단일 사이트에서는 잘 작동하지만 여러 사이트를 호스팅할 경우 작동하지 않을 수 있습니다. 여러 사이트를 호스팅할 경우에는 /var/www/{domain}/html와 같은 방식으로 디렉토리 구조를 수정해 적용할 수 있습니다.

Nginx 파일 및 디렉토리
콘텐츠
/var/www/html : 기본적으로 기본 Nginx 페이지가 있습니다. Nginx 구성 파일을 변경 수 있습니다.

서버 구성
/etc/nginx/nginx.conf : 기본 Nginx 구성 파일입니다. Nginx 전역 구성을 변경하도록 수정할 수 있습니다.
/etc/nginx/sites-available/ : 사이트별로 서버 블록을 저장할 수 있는 디렉토리입니다. Nginx는 sites-enabled 디렉토리에 연결되지 않은 경우 이 디렉토리의 구성 파일을 사용하지 않습니다. 일반적으로 sites-available 디렉토리에서 서버 블록이 구성된 후에 다른 디렉토리에 연결되어 사용할 수 있게 됩니다.
/etc/nginx/sites-enabled : 활성화된 사이트별 서버 블록이 저장되는 디렉토리입니다. 일반적으로 sites-available 디렉토리에 있는 구성파일에 연결해 생성됩니다.

서버 로그
/var/log/nginx/access.log : 별도로 구성되지 않는 한 웹 서버에 대한 모든 요청이 기록됩니다.
/var/log/nginx/error.log : 모든 Nignx 오류가 기록됩니다.

ngingx.conf
우선 sudo cat /etc/nginx/nginx.conf을 실행해 기본 Nginx 구성 파일을 살펴보겠습니다.
Nginx가 /etc/nginx/conf.d/*.conf 파일들과 /etc/nginx/sites-enabled 디렉토리의 모든 파일들을 include 해온다는 것을 알 수 있습니다. 만약 이 두 줄이 없으면 http {...} 안에 붙여넣으면 됩니다.

http {
    ...
    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
    ...
}
연동하기
proxy 설정
sudo mkdir /var/log/nginx/proxy/    # log, error 파일이 들어갈 디렉토리 생성
sudo vi /etc/nginx/proxy_params
포트번호가 80인 http에서 요청이 오면, Spring Boot 프로젝트에서 8080번 포트를 바라볼 수 있도록 proxy 설정을 해주겠습니다. proxy_params에 아래의 코드를 붙여넣어줍니다.

# 넘겨 받을 때 프록시 헤더 정보 지정
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header Host $http_host;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-NginX-Proxy true;

client_max_body_size 256M;
client_body_buffer_size 1m;

proxy_buffering on;
proxy_buffers 256 16k;
proxy_buffer_size 128k;
proxy_busy_buffers_size 256k;

proxy_temp_file_write_size 256k;
proxy_max_temp_file_size 1024m;

proxy_connect_timeout 300;
proxy_send_timeout 300;
proxy_read_timeout 300;
proxy_intercept_errors on;
서버 블록 생성
현재 가지고 있는 도메인과 jar 파일을 이용하기 위해서 기본 구성 파일을 수정해 서버 블록을 생성해주겠습니다.

명령어 sudo vi /etc/nginx/sites-available/{domain} 입력 후, 아래 코드를 복사해 붙여넣어줍니다.

{domain} : '.com', '.co.kr' 등이 포함되어 있어야 합니다.
server { # server 블록
    listen 80;

    server_name {domain} www.{domain};
    
    access_log /var/log/nginx/proxy/access.log;
    error_log /var/log/nginx/proxy/error.log;

    location / { # location 블록
        include /etc/nginx/proxy_params;
        proxy_pass http://{퍼블릭IP주소}:8080;    # reverse proxy의 기능
    }
}
location 블록의 proxy_pass를 통해 8080번 포트를 통해 접속해야 볼 수 있는 화면(Spring Boot 프로젝트 화면)을 80번(HTTP) 포트에 접속했을 때 확인할 수 있도록 설정, 즉 Reverse proxy의 기능을 하게 할 수 있습니다.

server 블록
Nginx는 이제 listen 지시문에 의해 포트 번호 80으로 들어오는 요청들에 대해 server_name 값과 정확하게 일치하는 서버 블록을 찾으려고 시도합니다.

참고 : server_name을 추가할 때, 해시 버킷 메모리 문제가 발생할 수 있습니다. 이를 방지하기 위해 /etc/nginx/nginx.conf파일에서 옵션을 조정해주겠습니다.

sudo vi /etc/nginx/nginx.conf

http { ...
    server_names hash_bucke_size 64;    # 주석 처리를 제거합니다.
    ...
}
location 블록
아래는 location 블록의 일반적인 형식입니다.

    location {optinal_modifier} {location_match} {
        ...
    }
{location_match}의 내용을 통해 Nginx가 확인해야 하는 요청 URI를 정의합니다. 예를 들어, 응답할 {domain}/site가 있다면, location /site {...}으로 정의할 수 있습니다. 더 자세한 내용을 이 튜토리얼에서 참고할 수 있습니다.

새로 생성한 파일 활성화
이제, sites-available 디렉토리로부터 site-enabled 디렉토리에 대한 링크를 생성해 파일을 활성화해보겠습니다.

sudo ln -s /etc/nginx/sites-available/{domain} /etc/nginx/sites-enabled/
기본 구성 파일 삭제
sites-available 디렉토리와 sites-enabled 디렉토리에서 명령어 ls -al을 실행해보면 원래 nginx 서버를 연결하던 default 파일이 새로 생성한 파일과 함께 보입니다.

ls -al /etc/nginx/sites-available/
ls -al /etc/nginx/sites-enabled/
이대로 연결시킬 경우 에러가 발생하기 때문에 default 파일을 삭제해주겠습니다.

sudo rm  /etc/nginx/sites-available/default
sudo rm  /etc/nginx/sites-enabled/default
Nginx 재시작
Nginx에 대해 구문 오류가 없는지 테스트하고, Spring Boot 프로젝트와 함께 재시작해보겠습니다

sudo nginx -t
sudo service nginx reload
java -jar {jar 파일명}.jar
도메인 주소로 들어가면 정상 작동되는걸 볼 수 있습니다! 👍

Tip: 백그라운드에서도 실행하기!
nohup + & 명령어로 우분투 터미널의 세션 연결이 종료됐을 때도 jar 파일을 멈추지 않고 실행할 수 있습니다.

nohup java -jar {jar 파일명}.jar &
종료
1) ps -ef 명령어를 실행해 현재 실행중인 프로세스 중 java 명령어를 찾습니다.
2) kill -9 {ProcessID(PID)}를 실행해줍니다.

