# Docker Login Error

> ** Message: 19:10:47.099: Remote error from secret service: org.freedesktop.DBus.Error.UnknownMethod: ?? /org/freedesktop/secrets/collection/login? ??? 'org.freedesktop.Secret.Collection' ?????? ????
> Error saving credentials: error storing credentials - err: exit status 1, out: `경로 /org/freedesktop/secrets/collection/login의 객체에 'org.freedesktop.Secret.Collection' 인터페이스가 없습니다`

## 발생
$ $(aws ecr get-login --no-include-email --region ap-northeast-2)
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
** Message: 19:10:47.099: Remote error from secret service: org.freedesktop.DBus.Error.UnknownMethod: ?? /org/freedesktop/secrets/collection/login? ??? 'org.freedesktop.Secret.Collection' ?????? ????
Error saving credentials: error storing credentials - err: exit status 1, out: `경로 /org/freedesktop/secrets/collection/login의 객체에 'org.freedesktop.Secret.Collection' 인터페이스가 없습니다`
$ sudo apt install gnupg2 pass
[sudo] crom의 암호: 
패키지 목록을 읽는 중입니다... 완료
의존성 트리를 만드는 중입니다       
상태 정보를 읽는 중입니다... 완료
다음의 추가 패키지가 설치될 것입니다 :
  libqrencode3 qrencode tree xclip
제안하는 패키지:
  ruby
다음 새 패키지를 설치할 것입니다:
  gnupg2 libqrencode3 pass qrencode tree xclip
0개 업그레이드, 6개 새로 설치, 0개 제거 및 10개 업그레이드 안 함.
144 k바이트 아카이브를 받아야 합니다.
이 작업 후 487 k바이트의 디스크 공간을 더 사용하게 됩니다.
계속 하시겠습니까? [Y/n] y
$ $(aws ecr get-login --no-include-email --region ap-northeast-2)
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /home/trms/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded

## 참조
- https://github.com/docker/docker-credential-helpers/issues/60
