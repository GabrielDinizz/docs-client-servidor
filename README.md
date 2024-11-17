# Documentação para Projeto Client-Servidor no Node.js

## 1. Configuração do Projeto

### 1.1. Criar Diretório do Projeto

1. Crie um diretório para o projeto principal.

### 1.2. Configurar Terminais

1. Abra dois terminais e divida a tela para que você possa trabalhar simultaneamente com o cliente e o servidor.
2. No terminal para o cliente:
   - Execute o comando para criar o projeto cliente:
     ```bash
     npm create vite@latest {client}
     ```
   - Selecione "React" e "JavaScript" ou o framework e a linguagem de sua preferência.

3. No terminal para o servidor:
   - Crie um diretório para o servidor:
     ```bash
     mkdir server
     cd server
     ```

### 1.3. Resultado: 

<div style="text-align: center;">
   ![image](https://github.com/user-attachments/assets/b5dc3725-a30d-4624-8149-789fa5bf8dc9)
   <img src="https://github.com/user-attachments/assets/03e13e8b-b6f1-416a-abd9-ec4e38dae308" alt="Exemplo de Estrutura de Projeto" width="300"/>
</div>


## 2. Configuração do Servidor

### 2.1. Inicializar o Projeto no Servidor

1. Dentro do diretório do servidor, inicialize um novo projeto Node.js:
   ```bash
   npm init -y

------------------------

### 2.2. Instalação de Dependências

Esse comando criará um arquivo `package.json`, contendo as dependências e algumas informações do projeto. Com isso, você pode instalar as dependências necessárias.

- **Instalar Dependência do Cliente**
  - Para instalar o `react-router-dom` no cliente, execute:
    ```bash
    npm install react-router-dom
    ```

### 2.3. Instalação de Dependências (Server)

- **Instalar Dependência do Banco de Dados**
  - Para instalar o `mysql2`, execute:
    ```bash
    npm install mysql2
    ```

- **Instalar Dependência Sequelize**
  - Para trabalhar com scripts SQL sem precisar escrever as strings de conexão e comandos SQL manualmente, instale o `sequelize`:
    ```bash
    npm install sequelize
    ```

- **Instalar Dependência CORS**
  - Para gerenciamento de rotas do servidor, instale o `cors`:
    ```bash
    npm install cors
    ```

- **Instalar Dependência bcryptjs**
  - Para encriptação de senhas, instale o `bcryptjs`:
    ```bash
    npm install bcryptjs
    ```

- **Instalar Dependência Express**
  - Para o funcionamento das outras dependências e execução dos comandos Node.js, instale o `express`:
    ```bash
    npm install express
    ```

- **Instalar Dependência Axios**
  - Para fazer requisições HTTP de forma fácil e eficiente, instale o `axios`:
    ```bash
    npm install axios
    ```

> [!IMPORTANT]
> Quando estamos trabalhando em um projeto de terceiros, como projetos do GitHub, é essencial verificar o `package.json` para instalar as dependências necessárias e garantir que o projeto funcione corretamente. Vale ressaltar que o `package.json` também é criado no diretório do cliente quando você inicializa o cliente com `npm create vite@latest {client}`, logo também deve ser verificado.

------------------------

### 3. Criação de Arquivos

Agora você pode criar diversos arquivos, podendo ter diferentes funcionalidades:

![image](https://github.com/user-attachments/assets/b5dc3725-a30d-4624-8149-789fa5bf8dc9)

- **Arquivo `index.js`**
  - Este será o arquivo responsável por executar o projeto, pois está definido como o `main` no `package.json`:
    <img src="https://github.com/user-attachments/assets/b117fbac-bdaa-4125-a7a1-8bfac6761d20" width="800">
    <img src="https://github.com/user-attachments/assets/95ea908f-0403-4dcc-88b3-b214efebb4b2" width="800">

- **Criar Pasta `BD` ou `CONFIG`**
  - Esta pasta deve conter o arquivo `bd.js`, que terá a string de conexão com o banco de dados.

- **Criar Pasta `MODEL`**
  - Esta pasta terá toda a configuração das tabelas do banco de dados. Por exemplo, para a tabela `User`, você terá um arquivo `user.js` contendo as configurações correspondentes: <br>
    ![image](https://github.com/user-attachments/assets/5e0e5f17-3f7a-45d3-926c-cb8db802471a)

- **Criar Arquivo `sync.js`**
  - Este arquivo será responsável pela sincronização das tabelas, criando a referência das tabelas e inicializando-as no banco de dados. Ele será o primeiro arquivo executado no projeto.

- **Criar a Pasta `Routes`**
  - Adicione um arquivo, como `Auth.js`, para gerenciar as rotas de autenticação e outras funcionalidades relacionadas.

#### 3.1 Estrutura Final Server
![image](https://github.com/user-attachments/assets/591ddfb3-9b0f-46e0-9019-879dc5fae04a)


------------------------

### 4. Criando o Banco de Dados

1. Abra o WampServer e o MySQL ou o sistema de banco de dados de sua preferência.
2. No WampServer, inicie o MySQL.
3. No MySQL, crie o banco de dados necessário:

![image](https://github.com/user-attachments/assets/92207d36-f09b-4149-ba59-e40e58859329)

4. Se for Sqlite, baixe as dependencias necessárias e installar a extensão do sqlite
![image](https://github.com/user-attachments/assets/ad6ceee0-c62c-44ab-b08c-91da2e27195c)
![image](https://github.com/user-attachments/assets/1be75291-2e21-46f4-b626-03254f1f8aca)

### 4.1. Criar String de Conexão

1. **Obter Informações do Banco de Dados**
   - Primeiro, é necessário saber as informações do banco de dados, como `localhost`, `root`, senha e nome do banco.
   - ![image](https://github.com/user-attachments/assets/5d167a93-f065-466b-a0f9-80d7967f771b)

2. **Configurar a String de Conexão**
   - No arquivo de configuração do banco de dados (pode ser `config`, `bd`, ou o nome que você escolher), insira a string de conexão utilizando Sequelize, um gerenciador de banco de dados para MySQL. Sequelize fornece uma interface de código semelhante ao phpMyAdmin:
     ![image](https://github.com/user-attachments/assets/14172847-2a49-4f9d-88b4-a4d385093357)
     ![image](https://github.com/user-attachments/assets/beefd093-3136-4555-bae1-984593399f03)


3. **Importação e Exportação no Arquivo `.js`**
   - Como o arquivo é `.js`, você deve importar o Sequelize usando `require`, e não `import`, como é feito nos arquivos React `.jsx`.
   - Utilize a palavra reservada `module.exports` para exportar a configuração do Sequelize:
     ```javascript
     const Sequelize = require('sequelize');

     const sequelize = new Sequelize('nome_do_banco', 'usuario', 'senha', {
       host: 'localhost',
       dialect: 'mysql',
     });

     module.exports = sequelize;
     ```

### 4.2. Models

- Na pasta `models` e no arquivo (`User`) referente à tabela, você deve definir toda a descrição da tabela:
```javascript
const { DataTypes } = require('sequelize');
const sequelize = require('../config/config');

const User = sequelize.define('User', {
  username: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  email: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  password: {
    type: DataTypes.STRING,
    allowNull: false,
  },
});
```

![Exemplo de Model](https://github.com/user-attachments/assets/d3e8efbf-c8d7-4ab2-8c49-723d1fea4e08)

- [https://sequelize.org/](#link-desejado)Na variável `Sequelize`, importada da pasta `config` (ou `bd`), estamos trazendo a string de conexão com o banco de dados.

- A variável `DataTypes` é utilizada para definir o tipo de dado dos atributos. Por exemplo, para o campo `Username`, o tipo pode ser `String`:
  ![image](https://github.com/user-attachments/assets/1bd29f74-6d81-4dcb-a341-cefa681f1de9)

- Após definir os tipos de dados, crie os campos da tabela e a própria tabela no arquivo de modelagem.

### 4.3. Sincronizar a Tabela

- Para criar as tabelas no banco de dados, você deve realizar a sincronização no arquivo de sincronização:
  ![image](https://github.com/user-attachments/assets/6cb8f6fc-9a3f-478c-b396-6ba214173508)

- Após escrever o código no arquivo de sincronização, execute a sincronização com o comando:
  ```bash
  node sync.js

- Execute O arquivo principal do servidor:
  ```bash
  node .\index.js

### 4.4. Estrutura Final
![image](https://github.com/user-attachments/assets/c61801d5-a1ed-4e86-a795-1c792f47c135)

-----------------------

### 5. Após Projeto Pronto

1. Ainda nos terminais, ou se você estiver saindo e entrando novamente em dois terminais (um para o cliente e outro para o servidor), execute o comando npm install tanto no cliente quanto no servidor para instalar as dependências:
2. 
   ![image](https://github.com/user-attachments/assets/31b7e639-0930-478a-9b0d-cb06a9bb6e62)

3. **Instalar Dependências do Cliente**
   - **Instalar Axios**: Utilizado para acessar as rotas do servidor (semelhante ao Fetch):
     ```bash
     npm install axios
     ```
     ![image](https://github.com/user-attachments/assets/7994e220-6dc9-4c1d-9665-cd7e67cd946e)

   - **Instalar `react-router-dom`**: Para gerenciamento das rotas do cliente.

4. **Instalar Dependências do Servidor**
   - Instalar as seguintes dependências: `cors`, `mysql2`, `sequelize`, `bcryptjs`, `express`:
     ![image](https://github.com/user-attachments/assets/bdc23a09-b7e8-41b9-b153-d952b5a6b384)







