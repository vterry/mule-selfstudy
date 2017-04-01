### Gerenciador de Tarefas (TO DO List) ###

Foi abordado neste exemplo o uso do MULE ESB para expor serviços REST utilizando HTTP Connector. Além disso foi abordade neste exemplo o tratamento de exceções utilizando Exception Strategy and Filters, bem como Conectores com Banco de Dados

### Exemplo ###

A aplicação expõe operações de manutenção de tarefas (CRUD):

* Recursos:
   ##### Tarefas = http://localhost:8081/{task}
   * Parametros:
        * id - ID da Tarefa
        * taskname - Nome da tarefa
        * description - Descrição da tarefa
        * target - Data prevista para conclusão da tarefa
        
    * Operações:
      * GET - http://localhost:8081/task?id=1 : Consulta uma tarefa pelo ID
      * POST- http://localhost:8081/task?taskname=TESTE&description=TESTE&target=21-MAR-2018 : Cadastra uma nova tarefa
      * PUT - http://localhost:8081/task?taskname=TESTE&description=TESTE&target=21-MAR-2019 : Atualiza um atributo da tarefa
      * DELETE - http://localhost:8081/task?id=1 : Deleta uma tarefa através de seu ID
      
### Configurando o Projeto ###

Antes de tudo é necessário instalar um banco de dados no seu computador, ou instaciar um em tempo de execução no próprio MULE, em meu caso utilizei o MySQL:

#### Script de criação do banco de dados (MySQL):

```sql
Create database tasks;

Use tasks;

Create Table to_dos (id int not null auto_increment,
task_name varchar(30) not null,
task_description varchar(100) not null,
expected_date varchar(12) not null,
primary key(id))
;
```

O próximo passo é configurar uma váriavel global dentro do projeto configurando o banco de dados - (https://docs.mulesoft.com/mule-user-guide/v/3.7/database-connector-examples)

A aplicação está configurada para iniciar na porta 8081, isso pode ser alterado no HTTP Listener que já esta configurado no projeto.
É importante adicionar ao classpath do seu projeto o Driver JDBC para configurar o Banco de Dados corretamente no seu projeto.

A titulo de conhecimento, o Tranformer configurado no projeto utilizar o JSON Schema abaixo como referência:

```json
{
  "id": "Task",
  "type": "object",
  "properties": {
    "ID": {
      "type": "integer"
    },
    "Task name": {
      "type": "string"
    },
    "Description": {
      "type": "string"
    },
    "Target date": {
      "type": "string"
    }
  },

  "required": ["ID", "Task name", "Description", "Target date"]
}
```
