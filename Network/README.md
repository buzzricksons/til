
# 트래픽
## 네트워크 전송량 단위
bps(Bit Per Second) 단위를 사용함.
초당 얼마를 전송할 수 있는지 나타내는 단위.1,000단위씩 오름.
- KBps = Kilo bps = 1,000 bps
- MBps = Mega bps = 1,000,000 bps
- GBps = Giga bps = 1,000,000,000 bps

## 스토리지 용량 단위
Byte 단위를 사용함.
1Byte는 8bit로써 8개의 bit 묶음.
- KByte = Kilo Byte = 1,000 Byte
- MByte = Mega Byte = 1,000,000 Byte
- GByte = Giga Byte = 1,000,000,000 Byte

## 용량 환산
1Byte는 8bit. 네트워크 전송량에서 나누기 8을 하면 스토리지 용량으로 환산이 가능함.

네트워크 트래픽이 1Mbps일경우 초당 전송 용량.

### 1Mbps
= 1 x 1,000 x 1,000 bit / 초
= 1,000,000 bit / 초

bit를 Byte로 전환↓
1Mbps / 8
= 1,000,000 bps / 8 / 초
= 125,000 Byte / 초
= 125KByte / 초
즉 초당 125KByte가 전송됨.

### 1GBps
= 1 x 1000 x 1000 x 1000 bit / 초
= 1,000,000,000 bit / 초

bit를 Byte로 전환↓
1Gbps / 8
= 1,000,000,000 bps / 8
= 125,000,000 Byte / 초
= 125MByte / 초
즉 초당 125MByte가 전송됨

### 하루 전송량
하루전송량을 계산하려면 60(초단위 환산) x 60(분단위 환산) x 24를 하면 하루 전송량이 나옴.

초당 10Mbps 전송량으로 하루 전송량을 계산시↓
10Mbps = 1.25Mbyte.

1.25MB x 하루(60 x 60 x 24)
= 1.25MB x 86,400초
= 108,000 MB
= 108 GB가 하루 전송량.

한달 전송량이면 108 GB x 30 = 3.24TB

