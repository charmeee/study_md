### 프로퍼티

- Math.PI  : 배정밀도 부동소수점 64비트 15자리까지.. 아마 가능할 듯?

### 메서드

- Math.abs : 절대값
- Math.round: 반올림
- Math.ceil: 올림
- Math.floor : 내림
- Math.sqrt :제곱근
- Math.random : 랜덤값
- Math.pow(x,n) : x^n -> 지수연산자생김 **
- Math.max,min() : 최대값,최소값, 값없을시 infinity apply(this 할때 햇던 그 메서드), 스프레드연산자를 통해 배열을넣을수 잇음



### 랜덤함수 알고리즘
[https://evan-moon.github.io/2019/07/14/what-is-random/](https://evan-moon.github.io/2019/07/14/what-is-random/)

[![Xorshift - Wikipedia|200](https://upload.wikimedia.org/wikipedia/commons/e/ee/Xorshift.png)
#### 중앙제곱법
![[스크린샷 2023-10-18 오후 8.12.58.png]]
- 폰노이만
- 예측 가능해서 잘안씀

#### 선형합동법
$$
Xn+1​=(aXn​+c)modm
$$

X: 수열
상수값 m, a, c << ANSI 표준씀

- 난수를 이어서 출력할경우 난수 열의 상관관계를 예측가능함 = 다음거 예측가능
- 메모리 적게사용
- 한번만 뽑거나 제한된상황에서 사용 


#### 메르센 트위스터
$$
메르센 수 Mn​=2n−1
$$

- 엑셀, MATLAB, PHP, Python, R, C++ 등에서 사용
- 초기값 624길이백터생성 하드웨어 노이즈 or 날짜 등
- twist 2번 shift register이용


#### XOR shift
- LFSR 이용 
- 메르센 난수 반복주기
- 보완한 XOR 시브프 128+알고리즘이 v8엔진에서 사용됨.
- https://en.wikipedia.org/wiki/Xorshift

