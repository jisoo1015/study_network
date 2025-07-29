## 🧪 문제 1: 특정 IP 차단 상태 확인 후 차단 설정
✅ 실행 예시
$ sudo ./problem1.sh )
[INFO] 현재 rich rule 목록에 192.168.0.100 차단 룰이 존재하지 않습니다.
[INFO] 차단 룰을 추가합니다...
success

또는
$ sudo ./problem1.sh 192.168.0.100
[INFO] 192.168.0.100은 이미 차단되어 있습니다.
[SKIP] 추가 작업을 수행하지 않습니다.
```shell
#!/bin/bash

IP="192.168.0.41"

#현재 rich rule 목록 중에 해당 IP가 포함되어 있는지 확인
EXIST=$(sudo firewall-cmd --list-rich-rules | grep "$IP")
#만약 검색 결과가 없으면 (즉, 아직 차단 안 되어 있으면)
if [ -z $EXIST ]; then
        echo "[INFO] 현재 rich rule 목록에 $IP 차단 룰이 존재하지 않습니다."
        echo "[INFO] 차단 룰을 추가합니다..."
        sudo firewall-cmd --permanent --add-rich-rule="rule family='ipv4' source address='$IP' reject"
        sudo firewall-cmd --reload  # 설정을 적용하려면 reload 해야 함
else
        echo "[INFO] $1은 이미 차단되어 있습니다."
        echo "[SKIP] 추가 작업을 수행하지 않습니다."
fi
```
```shell
[kimjisoo@192.168.0.38 ~]$ sudo bash problem1.sh
problem1.sh: line 8: [: too many arguments
[INFO] 은 이미 차단되어 있습니다.
[SKIP] 추가 작업을 수행하지 않습니다.
```

## 🔒 문제 2: 포트 8080이 열려 있다면 닫기
✅ 실행 예시
$ sudo ./problem2.sh 8080/tcp
[INFO] 포트 8080/tcp 이 열려 있습니다. 제거합니다...
success

또는
$ sudo ./problem2.sh 8080/tcp
[INFO] 포트 8080/tcp 이 열려 있지 않습니다. 아무 작업도 수행하지 않습니다.



