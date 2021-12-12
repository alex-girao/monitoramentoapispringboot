# monitoramentoapispringboot
Projeto para monitoramento de Api's SpringBoot utilizando a biblioteca [Spring Boot Admin](https://github.com/codecentric/spring-boot-admin "Spring Boot Admin")
![Dashboard](/images/1-sba.png?raw=true "Dashboard")

## Como utilizar
### Executando o projeto de monitoramento
#### 1- Basta baixar o projeto, instalar as dependências maven e executar.
```code
mvn -f monitoramentoapispringboot/ clean install -DskipTests
```
#### 2- Acesso
O projeto de monitoramento está configurado para ser acesso na porta **8090**
```bash
http://localhost:8090
```
OBS: se preferir rodar em outra porta, basta alterar o arquivo de configurações **application.properties**

### Registrando o(s) projetos Cliente(s)
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
OBS: Está implementação atende a **versão 2.4.x**, caso a sua versão seja mais antiga, sugiro verificar o [User Guide](https://github.com/codecentric/spring-boot-admin) da biblioteca.

#### 2- Alterar seu arquivo de configurações(application.properties ou application.yml) apontando para o projeto de monitoramento e liberando acessos.
```code
spring.boot.admin.client.url=http://localhost:8080  
management.endpoints.web.exposure.include=*
```
OBS: Caso tenha alterado a porta do projeto de monitoramento, a porta apontada na key **spring.boot.admin.client.url** deve ser alterada também.

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

#### 4- Execute o projeto cliente
Após executar o projeto acesse o dashboard do projeto de monitoramento.
