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
frida-ps -Ua | grep Cyder
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
frida 홈페이지가서 frida-gadget-16.2.1-ios-universal.dylib 받고 
해당 파일을 /Users/hacker/.cache/frida/gadget-ios.dylib로 rename해서 복사한다.

[+] frida-ps -Us 실행안되고 에러 떨어지면
xcode 12.4기준 xcode 실행해서 windows->devices and simulators 에 가서 폰 연결 확인


Drag to [MonkeyDev](https://github.com/AloneMonkey/MonkeyDev), Happy hacking!

## Support

Python 2.x and 3.x


### issues

If the following error occurs:

* causes device to reboot
* lost connection
* unexpected error while probing dyld of target process

please open the application before dumping.


