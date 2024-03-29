
1. CPU와 GPU의 역할 및 특징과 차이점, 역할, 작업 분산 등을 조사하고 CPU와 GPU가 어떻게 컴퓨팅 성능을 향상시키는지 설명하라.
   ![[assets/Pasted image 20240323173037.png]]
   Cpu는 중앙처리 장치로 각종 리소스들의 순서를 정하고 지휘하는 역할을 한다.다른 기기에 비해 코어성능이 강력하고 명령을 직렬 처리한다. 주요  제어장치, 누산기, ALU, 레지스터가 있다. 최근에는 코어수를 늘려 약간의 병렬처리도 지원하지만 비율이 gpu에 비해서는 현저히 낮다. 
   
   Gpu는 복잡한 계산을 병렬적으로 처리하는 곳에 사용한다. 비교적 낮은 차원(cpu에 비해)의 계산을 방대하게 처리할 수 있어 이미지분석, 그래픽, 인공지능 학습에서도 많이 쓰인다
   현재에는 두가지 동시에 많이 쓰이며 Cpu에서 기본적인 프로그램제어를 하고 복잡한 계산을 작은차원의 계산으로 나눠서 gpu에게 병렬처리하도록 맡기는 방식으로 작동한다.

2. 디스크의 회전수, 데이터 접근속도, 단위면적당 자기밀도가 각각 하드디스크의 성능에 어떻게 영향을 미치는지 조사하라.
   회전수는 데이터의 접근속도를 높여준다. 단위면적당 자기밀도는 같은 디스크 크기에 많은 용량을 저장할 수 있다. 이는 작은 물리적 이동으로 많은데이터를 처리할 수 이어 데이터 접근 속도에도 영향을 끼치기도한다. 데이터 접근속도는 하드 디스크의 역할, 데이터를 읽고 쓰는 속도기에 하드디스크의 성능이라고 볼 수 있다.

  

3. 메인 메모리와 캐시 메모리의 역할과 구성에 대하여 설명하고, 최근  PC에 사용되고 있는 메인 메모리와 캐시 메모리의 스펙에 대하여 조사하라.  또한 게임용 PC와 같이 고성능을 요구하는 PC와 일반용 저가용 PC에서 사용하는 스펙에 대하여 조사하고 차이점에 대하여 설명하라.
   메인 메모리 : 메인메모리(주기억장치)는 현재 처리중인 데이터와 명령을 담고 있는 메모리로 휘발성 메모리다. 하드디스크나 ssd에 비해서 빠르다. CPU 외부에 있는 메모리중에서는 가장 빠르며 CPU가 직접 접근 할 수 있는 장치다. 프로그램을 실행하기위해서는 반드시 메인메모리에 올라와야한다. 이 메인메모리가 많을 수록 많은 프로그램을 한번에 실행시킬 수 있다. 부족시에는 가상메모리라는 기법을 사용하여 실제 메모리보다 더 많은 정보를 저장할 수있다. Dram을 이용한다.
   캐시 메모리 : 캐쉬메모리는 메인 메모리와 cpu사이에 속도를 더 빨리 하기 위한 메모리다. 지역성의 특징을 가지고 사용될 데이터들을 미리 더 cpu에 가깝고 빠른 캐쉬 메모리에 저장시키므로써 속도 향상을 도모한다.
   메인메모리는 일반 상용컴퓨터에서 8G~64G까지 많이 이용하지만 캐시메모리의 경우 주로 4M~16M까지 사용한다고한다.
   게임용에서는 cpu i7or i5(높은세대), ram 16-32g, gpu rtx2060이면 충분히 게임용으로 사용 가능하다. 일반저사양 컴의경우 cpu는 i3-i5 , ram 4-8G ,gpu는 굳이 필요하지 않는 경우가 많다. 각각의 성능이 높은것도 중요하지만 성능의 균형을 맞추는것도 중요하다. 게임용의 경우, 복잡한계산작업을 빠르고 많이 해야하고 여러가지 정보를 많이 사용하기에 cpu , ram, gpu가 다 좋아야한다. 일반저사양 컴의 경우 요즘 cpu만으로도 기본적인 처리를 다 할 수 있을 만큼의 시대가 되었기 때문에 gpu까지는 굳이 필요없는 경우가 많다.