# Sistema de Gestão de Chalés (Trabalho Final PC2)

Projeto em Java para gerenciar chalés, clientes, hospedagens, serviços, itens e telefones.

## Descrição

Aplicação com arquitetura MVC e persistência usando DAOs. O projeto apresenta as camadas `model`, `persistence`, `controller` e `view`, além de utilitários e classes de teste/dataseed.

## Estrutura do projeto

- `src/` — código-fonte Java dividido em pacotes:
	- `controller/` — controladores da aplicação.
	- `model/` — classes de domínio (`Chale`, `Cliente`, `Hospedagem`, `Item`, `Servico`, `Telefone`).
	- `persistence/` — DAOs e `DatabaseConnection`.
	- `view/` — classes de interface (ponto de entrada: `MainApp`).
- `bin/` — classes compiladas (Eclipse).

Principais arquivos:

- [src/persistence/DatabaseConnection.java](src/persistence/DatabaseConnection.java#L1-L40)
- [src/persistence/TestConnection.java](src/persistence/TestConnection.java#L1-L40)
- [src/persistence/TestDataInserter.java](src/persistence/TestDataInserter.java#L1-L200)
- [src/view/MainApp.java](src/view/MainApp.java#L1-L200)

## Requisitos

- Java 11 ou superior (JDK).
- PostgreSQL (o projeto usa `jdbc:postgresql://localhost:5432/AppPC2` por padrão).
- Driver JDBC do PostgreSQL (`org.postgresql:postgresql`).
- IDE recomendada: Eclipse (o projeto já possui metadados `.project` / `.classpath`).

## Configuração do banco de dados

Por padrão, a conexão é:

- URL: `jdbc:postgresql://localhost:5432/AppPC2`
- Usuário: `postgres`
- Senha: `bancodedados`

Essas configurações ficam em `src/persistence/DatabaseConnection.java`. Você pode alterar essas informações para conectar em outro servidor/usuário.

Exemplo para criar o banco e definir a senha do usuário `postgres` (executar como usuário do sistema `postgres`):

```sh
sudo -u postgres psql -c "CREATE DATABASE AppPC2;"
sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD 'bancodedados';"
```

Observação: o repositório não inclui scripts DDL das tabelas. Crie as tabelas necessárias (`Cliente`, `Chale`, `Servico`, `Hospedagem`, `Telefone`, etc.) conforme as colunas usadas nas DAOs, ou adicione seus próprios scripts antes de executar o inseridor de dados.

## Compilar e executar

Opção A — Eclipse (recomendado):

1. `File -> Import -> Existing Projects into Workspace` e selecione a pasta `trabalhofinal`.
2. Adicione o driver JDBC do PostgreSQL no classpath do projeto (Project Properties -> Java Build Path -> Libraries).
3. Execute `view.MainApp` como aplicação Java.

Opção B — Linha de comando (Linux):

1. Baixe o driver JDBC do PostgreSQL e coloque o JAR em `lib/postgresql.jar`.
2. Compile:

```sh
mkdir -p bin
find src -name "*.java" > sources.txt
javac -d bin -cp "lib/postgresql.jar" @sources.txt
```

3. Execute o aplicativo (exemplo `MainApp`):

```sh
java -cp "bin:lib/postgresql.jar" view.MainApp
```

Executar utilitários/testes:

```sh
java -cp "bin:lib/postgresql.jar" persistence.TestConnection
java -cp "bin:lib/postgresql.jar" persistence.TestDataInserter
```

## Inserir dados de exemplo

- `TestConnection` — verifica conexão com o banco.
- `TestDataInserter` — insere registros de exemplo (clientes, chalés, serviços, hospedagens e telefones). Execute-o somente depois que o esquema/tabelas estiverem criados.