# ssh

## 생성
```bash
$ ssh-keygen -t rsa -C 'me@example.com'

Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):id_rsa_work
```

## 등록
```bash
# 추가
$ ssh-add ~/.ssh/id_rsa_me
$ ssh-add ~/.ssh/id_rsa_work

# 저장
$ ssh-add -l
```

## config
- config 파일 생성
```bash
$ touch ~/.ssh/config
```

- config 파일 내용
```
# me account
Host github.com-me
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_me

# work account
Host github.com-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_work
```

## 클립보드로 복사
```bash
$ pbcopy < ~/.ssh/id_rsa.pub
# or
$ cat ~/.ssh/id_rsa.pub | pbcopy
```
