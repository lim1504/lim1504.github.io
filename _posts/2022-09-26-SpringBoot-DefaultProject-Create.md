---
title:  "Spring boot Empty Poject Create" 
categories:
    - memo
toc: true
toc_sticky: true
date: 2022-09-26
last_modified_at: 2022-09-26
--- 

### PurPose

2가지의 큰 틀의 목적을 가지고 프로젝트를 생성했다.

1. 간단한 Default Project를 활용해, 습관처럼 사용했던 부분과 심도깊게 관심을 가졌던 영역에 대해서 테스트를 하는 것이 첫번째 목표이다.
2. 토비의 스프링, SpringInAction5, 여러 강의 영상을 듣고 직접 코딩해봄으로써 학습과 실천을 동시에 함으로 써 효율적인 학습을 하기 위해 생성했다.

### issue

- Spring Security 학습과 정리를 위해 Spring Security를 포함해서 생성했는데, Spring Security의 기본 로그인 화면이 제거되지 않는 사소한 이슈가 있었다.

### Try

- 내 기억을 더듬어 다음과 같은 방법을 사용했다. 구글에 떠돌아 다니는 보편적인 방법이기도 하다.
    
    ```java
    @Configuration
    @EnableWebSecurity
    public class Configration extends WebSecurityConfigurerAdapter{
    	
    	protected void configure(HttpSecurity http) throws Exception {
    		http.httpBasic().disable();
    	}
    }
    ```
    

---

- 위 방법으로 해결되지 않아 두번째로 모든 권한을 허용하는 방법을 사용했다.
    - 또한, 기존에 상속받는 WebSecurityConfigurerAdapter 클래스는 더 이상 상속받을 필요가 없어
        
        제거했다.
        
    
    ```java
    @Configuration
    @EnableWebSecurity
    public class Configration{
    	
    	protected void configure(HttpSecurity http) throws Exception {
    		http.authorizeHttpRequests().antMatchers("/").permitAll();
    	}
    }
    ```
    

→ 위 두 방법으로 Spring Security login Page가 사라지지 않아, 여러 검색을 시도했다.

### Solution

몇가지 추가적인 방법을 찾았다.

1. Spring Project Build시, Spring Security를 제외하고 실행시키는 방법

```java
@SpringBootApplication(exclude = {SecurityAutoConfiguration.class})
```

1. yml을 활용해 제외하는 방법

```java
spring:
  autoconfigure:
    exclude:
    - org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration
```

→ 두가지 방법을 활용하면 Spring Security Login Page를 건너뛸 수 있다.

이 조치는 임시적인 조치로 후에 다시 스프링 시큐리티를 정상 작동시키기 위해서는 위에 추가된 코드를 제거해야한다.