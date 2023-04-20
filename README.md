## Cors
Como liberar o cors em uma aplicação spring-boot


1) Criar uma classe que implementa o WebMvcConfigurer e adicionar o seguinte código:

```
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings (CorsRegistry registry){
        registry.addMapping("/**")
                .allowedOrigins("http://localhost:8080")
                .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS", "HEAD");
    }
    
}
```

2) Para registrá-lo, você deve adicionar.cors() à sua classe de configuração
```
@Override
    protected void configure(HttpSecurity http) throws Exception {

            http.authorizeRequests()
                .antMatchers(HttpMethod.POST, "/login").permitAll()
                .anyRequest().authenticated()
                .and().csrf().disable()
                .cors()
                .and()
                .addFilter(new JWTAuthenticationFilter(authenticationManager()))
                .addFilter(new JWTValidateFIlter(authenticationManager()))
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);
    }
 ```
