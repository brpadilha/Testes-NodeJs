# Testes NodeJs

## Por que testar?

Devemos testar para garantir que tudo vai funcionar na nossa aplicação, tanto em projetos pequenos ou grandes.

## Tipos de Testes

### Testes Unitários

Testam uma função mínima pura, onde não tem efeito colateral de acessar banco de dados e não tem integrações externas, ele é muito utilizado para teste de funções.

### Testes de integração

São os principais testes do back-end, onde testam as funcionalidades completas, como acessar as rotas e retorno do controller.

### Testes E2E

São testes de interface que simula o acesso do usuário na aplicação, dele preenchendo campos, clicando em botões e retorna o que se espera que ele receba, como clicar em um botão e ir para o Dashboard por exemplo.

## TDD

A prática de TDD é criar os testes antes de serem criados as funcionalidades, onde você cria primeiro o teste e depois vai fazendo a funcionalidade para que o teste dê certo. Assim facilita a visualização da regra de negócio da aplicação.

## Code Coverage

É uma funcionalidade para verificar se testou o suficiente na sua aplicação, ele separa por % do que foi testado na sua aplicação, é bastante importante que no final, tenha testado mais de 80% da aplicação.

# Jest

Vai ser a ferramenta utilizada no bootcamp para testes. É um framework do facebook muito utilizado, ele consegue concentrar várias libs de testes em uma coisa só. E nele você consegue testar o backend, frontend e mobile. Suas vantagens é de ter integrado o `Code Coverage e a Mult-thread`.

## Aula 05 - Teste de criação de usuário

Primeiro para a gente testar o nosso banco de dados de usuários, devemos realizar o sequelize de criação da migration de usuários.
Rode o código `yarn sequelize migration:create --name=create-users` e depois vá em migrations e no arquivo criado coloque o código:

```
'use strict';

module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.createTable('users', {
      id: {
        type: Sequelize.INTEGER,
        primaryKey: true,
        autoIncrement: true,
        allowNull: false,
      },
      name: { type: Sequelize.INTEGER, allowNull: false },
      email: { type: Sequelize.INTEGER, allowNull: false },
      password_hash: { type: Sequelize.INTEGER, allowNull: false },
      created_at: { type: Sequelize.DATE, allowNull: false },
      updated_at: { type: Sequelize.DATE, allowNull: false },
    });
  },

  down: queryInterface => {
    return queryInterface.dropTable('users');
  },
};
```

Para que a gente faça o migrate do banco de dados, fazer os testes e desfazer a migrate depois de realizar os testes, vamos no package.json e colocamos nos scripts.

```
"pretest": "NODE_ENV=test sequelize db:migrate",
    "test": "NODE_ENV = test jest",
    "posttest": "NODE_ENV=test sequelize db:migrate:undo:all"


```

Agora que configuramos, vamos no model e criamos o model de usuários:

```
import Sequelize, { Model } from 'sequelize';

class User extends Model {
  static init(sequelize) {
    super.init(
      {
        name: Sequelize.STRING,
        email: Sequelize.STRING,
        password_hash: Sequelize.STRING,
      },
      {
        sequelize,
      }
    );
    return this;
  }
}

export default User;
```

Agora a gente cria uma pasta /integration dentro de`__tests__` e lá criamos o nosso primeiro test `user.test.js`:

Instalamos a biblioteca `supertest`

```
import request from 'supertest';
import app from '../../src/app';

describe('User', () => {
  it('Should be able to register', async () => {
    const response = await request(app)
      .post('/users')
      .send({
        name: 'Diego Fernandes',
        email: 'diego@rocketseat.com.br',
        password_hash: '123456',
      });

    expect(response.body).toHaveProperty('id');
  });
});
```

Se rodarmos o teste, entretanto vai dar um erro, pois ainda não criamos a nossa rota.
Vamos em `routes.js`:

```
import { Router } from 'express';

const routes = new Router();

routes.get('/', (req, res) => res.json({ message: 'Welcome to Omni CLI' }));
routes.post('/users', (req, res) => {
  return res.json({ id: 1 });
});

export default routes;
```

Ai rodamos o teste e vemos q ele passou.

Aí podemos ir criar o nosso UserController:

```
import User from '../models/User';

class UserController {
  async store(req, res) {
    const user = await User.create(req.body);

    return res.json(user);
  }
}

export default new UserController();
```
 E importá-lo nas rotas.
