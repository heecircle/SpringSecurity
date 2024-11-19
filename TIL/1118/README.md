
## 11/18

기본적으로 모든 요청에 대해서 별도의 설정이나 코드를 작성하지 않아도 기본적인 웹 보안 기능이 현재 시스템에 연동되어 작동함.
어떠한 인증방식인가?
- form login
- http basic

실행할 때에 처음 시큐리티 초기화가 진행되면 -> 초기 password가 떠짐. (OAuth 해놓으면 안보인다..)

1. SecurityProperties 내부에서 초기 User에 대한 정보를 id : user, pw : random uuid로 설정함
2. SecurityFilterChainConfiguration에서 최하위 우선순위 -5 를 설정했던 User를 받아와
   SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
   http.authorizeHttpRequests((requests) -> requests.anyRequest().authenticated());
   http.formLogin(withDefaults());
   http.httpBasic(withDefaults());
   return http.build(); 다음과 같은 인증을 진행함
3. http secutiry class가 하는 일
- httpsecurity 설정을 진행할 때, 각 요소들에 대한 설정을 진행한다. ex) csrf의 설정과 같은 것들
- csrf 설정의 경우, csrf configurer에 의해 설정이 진행되는데, 이 configurer의 경우 security configurer를 implements하여 만들어진다.


