# monitoramentoapispringboot
Projeto para monitoramento de Api's SpringBoot utilizando a biblioteca [Spring Boot Admin](https://github.com/codecentric/spring-boot-admin "Spring Boot Admin")
![Dashboard](/images/1-sba.png?raw=true "Dashboard")

## Como utilizar
Basta baixar o projeto, instalar as dependências maven e executar.
sadasdasd

### Registrando o(s) projetos Cliente(s)
OBS: Está implementação atende a versão Version 2.4.x, caso a sua versão seja mais antiga, sugiro verificar o [User Guide](https://github.com/codecentric/spring-boot-admin) da biblioteca.
É necessário que o projeto cliente se inscreva no monitoramento, para isso precisamos executar os seguintes passos.
#### 1- Adicionar as dependências
```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>2.4.3</version>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```
#### 2- Alterar seu arquivo de configurações(application.properties ou application.yml) apontando para o projeto de monitoramento e liberando acessos.
```code
spring.boot.admin.client.url=http://localhost:8080  
management.endpoints.web.exposure.include=*
```

#### 3- Alterar a sua classe de segurança WebSecurityConfigurerAdapter para liberar os Endpoints.
```code
@Configuration
public static class SecurityPermitAllConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests().anyRequest().permitAll()  
            .and().csrf().disable();
    }
}
```
