OS : Ubuntu 24.04.4 LTS
Shell : Bash
Docker Version : 29.3.1
Git Version : 2.43.0

Check List
Terminal O
Permisson X
Docker O
Dockerfile X
Port X
Volume X
Git X
Github X

오류 해결 내용

4월 1일 
도커데스크탑을 deb패키지로 설치하려 했으나 

Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root? 

같은 메시지가 나오며 설치되지 않아 해결방법을 찾던중 우분투를 재시작 해보라는 글이 있어 따라 해보았습니다. 그랬더니 도커 데스크톱 버전 확인도 되고 앱서랍에 아이콘도 추가되어 정상설치가 된줄 알았지만 터미널과 
도커컨테이너에서 hello-world 이미지가 작동되지 않았습니다.
그래서 결국 도커 공식 리포지토리를 우분투에 추가하여 설치하는 방법으로 해결하였습니다.

위의 문제를 해결한 다음 제가 이용하는 우분투 버전과 동일한 이미지를 컨테이너에서 실행하려고 

docker run ubuntu 24.04.4 를 터미널에 입력했더니 

docker: Error response from daemon: failed to create task for container: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: exec: "24.04.4": executable file not found in $PATH

Run 'docker run --help' for more information

나오며 도커 라이브러리에서 풀링과 실행이 되지 않았습니다. 원인을 찾아보니 우분투 버전표기의 가장 마지막에 위치한 .4는 생략해야되는 특징이 있는 것을 알게 되었습니다.

4월 10일
이미 도커를 설치하고 헬로월드 이미지와 더불어 우분투 이미지가 실행될 컨테이너를 생성하여 실행에 성공했지만 
오늘 다시 container -ls로 생성된 컨테이너들 목록을 확인하려했더니

failed to connect to the docker API at unix:///home/almost/.docker/desktop/docker.sock; check if the path is correct and if the daemon is running: dial unix /home/almost/.docker/desktop/docker.sock: connect: no such file or directory

위와 같은 오류가 발생되어 도커 데스크탑을 재시작 하는 명령인 systemctl --user restart docker-desktop을 입력하여 이문제를 해결하였습니다.
