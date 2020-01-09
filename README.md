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
