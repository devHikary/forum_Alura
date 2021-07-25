# Curso:  Spring Boot API REST: Construa uma API

Instrutor: Rodrigo Ferreira

- `@ResponseBody` → Indicar ao Spring que o retorno do método deve ser devolvido como resposta.
- Por padrão, o Spring considera que o retorno do método é o nome da página que ele deve carregar, mas ao utilizar a anotação `@ResponseBody`, indicamos que o retorno do método deve ser serializado e devolvido no corpo da resposta.
- O módulo **DevTools** inclui ferramentas utilitárias no projeto, dentre elas a **Automatic Restart**, que reinicia o servidor automaticamente ao detectar alterações no código fonte da aplicação.

    ```
    <dependency>
    			<groupId>org.springframework.boot</groupId>
    			<artifactId>spring-boot-devtools</artifactId>
    			<scope>runtime</scope>
    		</dependency>
    ```

- JPA

    ```
    <dependency>
    			<groupId>org.springframework.boot</groupId>
    			<artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    ```

- H2

    ```
    <dependency> 
        <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
    </dependency>
    ```

- application.properties

    ```tsx
    #datasource
    spring.datasource.driverClassName=org.h2.Driver
    spring.datasource.url=jdbc:h2:mem:alura-forum
    spring.datasource.username=sa
    spring.datasource.password=

    # jpa 
    sprinf.jpa.database-plataform=org.hibernate.dialect.H2Dialect
    spring.jpa.hibernate.ddl-auto=update

    # h2
    spring.h2.console.enable=true
    spring.h2.console.path=/h2-console
    ```

- Instalar o plugin SQL Editor.  Help --> Eclipse Marketplace
- Uma aplicação que utiliza o Spring Data JPA, o acesso ao banco de dados é feito com a criação de uma interface, seguindo o padrão Repository.

    ```java
    public interface TopicoRepository 
        extends JpaRepository<Topico, Long>{}
    ```

- Se não utilizar a convenção do Spring data, temos que indicar qual é a Query que você quer executar

    ```
    @Query("SELECT t FROM Topico t WHERE t.curso.nome = :nomeCurso")
            List<Topico> carregarPorNomeDoCurso(@Param("nomeCurso")(String nomeCurso);
    ```

- A anotação `@RequestBody` → Indicar ao Spring que os parâmetros enviados no corpo da requisição devem ser atribuídos ao parâmetro do método
- Na requisição foi adicionado um cabeçalho, chamado `Content-Type` → Indicar o formato das informações enviadas no corpo da requisição
- Utilizando a especificação **Bean Validation.** Foi necessário anotar o parâmetro **form**, no método cadastrar, com a anotação `@Valid` → Indicar ao Spring para executar as validações do **Bean Validation** no parâmetro do método
- O objetivo de se utilizar a anotação `@ResponseStatus` na classe que representa o `RestControllerAdvice` → alterar o status code devolvido como resposta
- Na funcionalidade para atualizar um tópico, sendo que no método do controller foi necessário adicionar a anotação `@Transactional` → Efetuar o commit automático da transação, caso não ocorra uma exception e executar o método dentro de um contexto transacional