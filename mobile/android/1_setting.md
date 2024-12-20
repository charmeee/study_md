# 프로젝트 생성
![](assets/setting-20241219232030173.png)

- packagename : 앱의 식별값
	- 보통 도메인 역순 + ㅐ끝에 프로젝트명
- build configuration language
	- build.gradle 파일을 선택하는 부분
	- Groovy DSL과 Kotlin DSL이 있음
		- groovy : build.gradle
		- kotlin : build.gradle.kts
	- DSL가 뭔지 & 문법차이
		- https://blog.imqa.io/kotlin-dsl/
	- 장단점
		- https://kdhyo98.tistory.com/87

- `compileSdkVersion` :  일반적으로 최신 SDK 버전으로 설정하는 것이 권장됩니다.
- `targetSdkVersion` : 앱이 테스트된 최신 안드로이드 버전
- `minSdkVersion` : 앱이 지원하는 가장 낮은 안드로이드 버전

# 기타 설정
### android sdk 
![](assets/1_setting-20241221011941321.png)
- 안드로이드 개발하기 위한 툴킷
- setting > languages&framework > android sdk
- 개발 sdk는 최근 껄 하는게 좋다고한다.
	- 최신기기를 타겟팅하면서 하위호환성을 유지할 수 있다.
	- 호환성을 테스트하고자 의도적으로 낮출때도 있다.
- Android Tiramisu Privacy Sandbox Preview
	- 프라이버시기능을 특히 광고 관련쪽에서 강화한 한 버전이다

### sdk tool
![](assets/1_setting-20241221013449422.png)