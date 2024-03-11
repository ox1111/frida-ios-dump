# [ frida-ios-dump:;남의 연구 리뷰 ] 
: jailbreak된 폰에서 복호화된 ipa 가져오기
- 아들 교육용
- 저작가 쓴 내용에 번역이나 필요한 내용 적어둠
- Review other people's research
## Usage

[+] frida 설치
[frida](http://www.frida.re/) frida 설치
```
pip install frida-tools
```
```
pip3 install frida-tools
```

[+] 사용할 기본 라이브러리 설치

```sudo pip install -r requirements.txt --upgrade```

[+] brew 설치

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
[+] frida-ios-dump 다운로드 
```
git clone https://github.com/ox1111/frida-ios-dump.git
cd frida-ios-dump
```
[+] iproxy 설정
```
iproxy 2222(mac에서 연결할 port ) -> 22(iphone에서 열어놓은 port )
    mac 2222 port -> iphone 22

iproxy 2222 22
```

[+] frida-ps
```
frida-ps -Ua | grep Cydia
```

[+] frida-ps
```
실행했는데 holing한다면 수동으로 앱을 한번 실행하면 동작한다.

python3 dump.py com.saurik.Cydia

```

[+] ssh 연결
```
SSH/SCP의 경우 대상 디바이스의 ~/.ssh/authorized_keys 파일에 공개키가 추가되어 있는지 확인

ssh -p 2222 root@localhost
root/alpine

삭제하고 싶을 때 위치
rm -rf /Users/hacker/.ssh

```

[+] dump.py 실행했는데 gadget-ios.dylib 없다고 에러나면 
```
https://github.com/frida/frida/releases


frida 홈페이지가서 frida-gadget-16.2.1-ios-universal.dylib 받고 
해당 파일을 /Users/hacker/.cache/frida/gadget-ios.dylib로 rename해서 복사한다.
```
[+] frida-ps -Us 실행안되고 에러 떨어지면
```
xcode 12.4기준 xcode 실행해서 windows->devices and simulators 에 가서 폰 연결 확인
```

Drag to [MonkeyDev](https://github.com/AloneMonkey/MonkeyDev), Happy hacking!

## Support

Python 2.x and 3.x


### issues

If the following error occurs:

* causes device to reboot
* lost connection
* unexpected error while probing dyld of target process

please open the application before dumping.



# frida-ios-dump 스크립트 함수 설명

이 문서에서는 `frida-ios-dump` 스크립트에 사용된 주요 함수들의 기능을 설명합니다.

## 메모리 관련 함수

- `allocStr(str)`: 문자열 `str`을 할당하고 해당 문자열의 포인터를 반환합니다.
- `putStr(addr, str)`: 주어진 주소 `addr`에 문자열 `str`을 씁니다.
- `getByteArr(addr, l)`: 주어진 주소 `addr`에서 `l`바이트만큼 바이트 배열을 읽어옵니다.
- `getU8(addr)`, `putU8(addr, n)`: 주어진 주소 `addr`에서 unsigned 8비트 정수를 읽거나 씁니다.
- `getU16(addr)`, `putU16(addr, n)`: 주어진 주소 `addr`에서 unsigned 16비트 정수를 읽거나 씁니다.
- `getU32(addr)`, `putU32(addr, n)`: 주어진 주소 `addr`에서 unsigned 32비트 정수를 읽거나 씁니다.
- `getU64(addr)`, `putU64(addr, n)`: 주어진 주소 `addr`에서 unsigned 64비트 정수를 읽거나 씁니다.
- `getPt(addr)`, `putPt(addr, n)`: 주어진 주소 `addr`에서 포인터를 읽거나 씁니다.
- `malloc(size)`: 지정된 크기 `size`의 메모리를 할당합니다.

## 파일 및 라이브러리 관련 함수

- `getExportFunction(type, name, ret, args)`: 주어진 이름 `name`으로 내보내기 함수를 찾아 반환합니다.
- `getDocumentDir()`: 애플리케이션의 문서 디렉토리 경로를 반환합니다.
- `open(pathname, flags, mode)`: 파일 경로 `pathname`에 대해 `flags`와 `mode`를 사용하여 파일을 엽니다.
- `read(fd, buffer, size)`: 파일 디스크립터 `fd`에서 `size`바이트만큼 `buffer`로 읽어옵니다.
- `write(fd, buffer, size)`: 파일 디스크립터 `fd`에 `buffer`의 내용을 `size`바이트만큼 씁니다.
- `lseek(fd, offset, whence)`: 파일 디스크립터 `fd`의 파일 오프셋을 `offset`만큼 이동합니다.
- `close(fd)`: 파일 디스크립터 `fd`를 닫습니다.
- `remove(pathname)`: 파일 경로 `pathname`에 해당하는 파일을 삭제합니다.
- `access(pathname, mode)`: 파일 경로 `pathname`에 대한 접근 권한을 확인합니다.
- `dlopen(filename, flag)`: 동적 라이브러리 `filename`을 `flag`와 함께 로드합니다.

## 모듈 관련 함수

- `getAllAppModules()`: 애플리케이션의 모든 모듈을 가져와 `modules` 배열에 저장합니다.
- `dumpModule(name)`: 이름이 `name`인 모듈을 덤프하고 파일로 저장합니다.
- `loadAllDynamicLibrary(app_path)`: 애플리케이션의 경로 `app_path`에 있는 동적 라이브러리를 모두 로드합니다.

## 유틸리티 함수

- `pad(str, n)`: 문자열 `str`을 `n`자리로 패딩합니다.
- `swap32(value)`: 32비트 정수 `value`의 엔디언을 변환합니다.

## 메시지 처리 함수

- `handleMessage(message)`: 메시지를 처리하는 함수로,
  애플리케이션의 모든 모듈을 덤프하고 결과를 전송합니다.

위의 함수들은 `frida-ios-dump` 스크립트에서 
iOS 애플리케이션의 바이너리를 덤프하고 분석하는 데 사용됩니다. 
