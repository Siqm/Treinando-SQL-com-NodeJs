*Dia 01*

# Instalação:
    Criado o repositório, acessado com o terminal e executado "npm init -y"
    Instalado tambem o sequelize, "npm install sequelize"
    Criado o .gitignore, conteúdo: "node_modules"
    Instalando express, pg e pg-hstore para utilizar postgre
    Instalado o nodemon
    Criei script "start" para iniciar a aplicação
    Criado a pasta src e ./src/routes.js e ./src/server.js
## Primeiro commit finalizado

# Configurando database:
    Criado database/index.js, para conectar ao banco de dados
    Criado config/database.js, para configurar o banco de dados
    Erro ao executar "npx sequelize db:create", 
        ERROR: Error reading "config\config.json". Error: Error: Cannot find module 'C:\Users\rafael.mello\Documents\GitHub\Treinando-Autenticacao-Com-Node.js\config\config.json'
    Resolução:
        Criação de ./.sequelizerc para informar o caminho do arquivo
    Erro ao executar "npx sequelize db:create",
        ERROR: getaddrinfo EAI_FAIL postgres://rhcvhoyy:LbkbHqgKa_MskKcbl-HeEywXn9uwMN0P@kesavan.db.elephantsql.com/rhcvhoyy
    Resolução:
        Instalei postgres na maquina, porta: 5432
### Finalizando o dia, commit realizado, problema não resolvido

*Dia 02*

# Resolvendo problema do dia anterior
    Problema: Erro ao executar "npx sequelize db:create",
    Resolução:
        Reinstalado o portgres e conectando à servido local ao invés de elephantsql
    Base de dados "sqlnode" criada com sucesso, através do comando "npx sequelize db:create"
# Configurando database Parte 02:
    Implementando as Migrações
    O caminho para as migrações será src/database/migrations, e para o sequelize ficar ciente disso,
    foi feita uma alteração no .sequelizerc, para avisar o caminho
    Criando a micração com o comando "npx sequelize migration:create --name=create-users", criando a tabela de usuários
### Terceiro Commit finalizado, database configurada

# Preparando a migration de usuario:
    Editando a migrations de users, editando campo id e adicionando name, email, created_at e updated_at
    Rodando as migrations com "npx sequelize db:migrate"
#### E se eu quiser adicionar uma nova coluna e meu banco já está em produção?
1. O único jeito é fazendo uma nova migration para resolver essa questão, então temos:
        "npx sequelize migration:create --name=_ _ _ _ _" (nome que faça sentido com o campo novo e a tabela que se faz referencia)

2. e dentro da classe criada, colocamos o código: 

        module.exports = {
            up: (queryInterface, Sequelize) => {
                return queryInterface.addColumn(
                    'users',    //nome da tabela
                    'age',      //nome da coluna a ser adicionada
                    {
                    type: Sequelize.INTEGER,
                    },
                );
            },
 
            down: (queryInterface, Sequelize) => {
                return queryInterface.addColmn(
                    'users',
                    'age',
                )
            }
        };

3. É importante não esquecer de executar o comando de migração!

### Quarto commit realiado, implementada a tabela de usuario com migrações!

# Começando a implementar os modelos!
1. É criada o diretorio "src/models" e o arquivo User.js dentro de "models"
User será nosso primeiro modelo e precisamos construir os objetos de configuração dentro dele
2. Feito isso, tambem precisamos ir em "src/database/index.js", importar e declarar o init dele
    Com esses passos, o modelo já está funcional
3. Para testar, vamos criar uma rota em "src/routes.js"
4. Também é importante criar um diretório "src/controllers" onde criamos o controlador de usuario "UserController.js"
5. Com a rota de post para usuarios configurada, rodamos a aplicação e torcemos para não ter erros! (esta tinha e eles foram corrigidos neste commit) 
    
##### Mas e para métodos get?
    Para isso vamos primeiro configuar a rota e depois a gente implementa o método no controller!
### Quinto commit realizado, implementado o modelo de usuario, seus métodos e rotas para acesa-lo
### Sexto commit realizado, correção no changelog e finalizando o dia 2!

*Dia 03*

# Adicionando uma classe com relacionamento
1. Criar a migration da classe "npx sequelize migration:create --name=addresses"
2. Copiei o conteudo da *./migrations/__-create-users* e alterei os campos e nome da tabela para **./migrations/__-addresses**
3. Criei o modelo de Adress em Models
4. Copiei o conteudo do modelo de user para modelo de address, alterando o conteúdo
5. Iniciei o Address em ./database/index.js
6. Criei o controller de Addresses
7. Definir uma rota
    Tudo pronto e bora rodar né?
    OPSSS na hora do post a gente percebe que algo ta errado!
8. Faltou definir a associação entre as tabelas, pra fazer isso, vamos no modelo de address e definir 
9. Também é importante dizer no database/index.js que a associação está sendo feita

*dia finalizado*

### Sétimo commit realizado, Classe com relacionamento unidirecional

*dia 04*
    Finalização do sétimo commit, era domigão né...

*Dia 05*
    Mais uma segunda-feira abençoada fml, pra cima deles!

# Implementando o relacionamento de users > Addresses e Devolvendo a lista de endereços de um usuário

### Oitavo Commit, Changelog duplicado

*NEM SEMPRE É NECESSÁRIO TER UMA RELAÇÃO COMO ESSA*

1. Definir a associação no modelo User.js
2. Criar o método responsável pelo calculo da solicitação no AdressController.js
3. Informar a associação em ./database/index.js

### Nono Commit realizado, relacionamento de usuario TEM MUITOS endereços implementado e método que devolve uma lista de endereços de terminado usuario

*Dia **nemSeiMais***

# Implementando relacionamento muitos para muitos

1. Criando tabela techs com o comando 'npx sequelize migration:create --name=create-techs'
2. Criando a tabela de relacionamento N-N "npx sequelize migration:create --name=user_techs"
3. Criar um controller para Techs
4. Criar um modelo para Tech e definir a associação
5. Criar rotas
6. Iniciar os modelos e suas associações na database
7. Deixar explícito a pluralização de Tech para o sequelize

### Commit 12 realizado, Implementado método post em um relacionamento muito para muitos

*Dia 08*

Implementado o método de get para as tecnologias de um usuário
