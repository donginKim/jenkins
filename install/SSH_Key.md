# SSH 키 등록하기

> 주어진 인스턴스에 키페어가 등록되지 않은 경우, pem키가 없는 경우 사용하고 있는 방법 중 하나



## #SSH 키 만들기

ssh-keygen을 사용하여 만드는 방식으로 아래와 같이 입력.

```shell
ssh-keygen -t rsa
```

여기서 -t rsa 는 rsa라는 암호화 방식으로 키를 생성한다는 의미.

```shell
Enter file in which to save the key (/home/centos/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
```

첫번째는 SSH 키 저장 위치를 지정해주며, 공백으로 둘 경우 홈 디렉토리의 .ssh 폴더안에 저장되며, 두번째 passphrase 같은 경우 private 키에 비밀번호를 여부를 입력하며, 권장 값은 10 ~ 30자 이내이며, 자동 로그인을 위해서는 생략.

```shell
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub  
chmod 644 ~/.ssh/authorized_keys
chmod 644 ~/.ssh/known_hosts
```

권한 설정은 위와 같이 설정함.



## #외부서버 SSH 키 등록

SSH 키 생성 후 authorized_keys 파일에 *.pub 파일 내용 등록을 해야 SSH로 로그인 없이 통신 할 수 있음.

```shell
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

authorized_keys 설정 후 id_rsa, id_rsa.pub, authorized_keys파일을 해당 서버에 scp로 복제 후 ssh 테스트 진행.

