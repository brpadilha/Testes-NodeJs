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

## Aula 03 - Configurando jest

Primeiramente vamos instalar o framework jest do facebook, que tem todas as ferramentas precisas para realizar testes:

```
yarn add jest -D
```

Agora a gente roda o comando `yarn jest --init` para responder o questionário.

Depois de responder, basicamente tudo yes e node para a segunda opção.

Criamos uma pasta chamada `__tests__` na raiz do projeto e configuramos o jest .json ficando assim:

```// For a detailed explanation regarding each configuration property, visit:
// For a detailed explanation regarding each configuration property, visit:
// https://jestjs.io/docs/en/configuration.html

module.exports = {
  // All imported modules in your tests should be mocked automatically
  // automock: false,

  // Stop running tests after `n` failures
  bail: 1, // quando rodar o comando de testes, e encontrar uma falha, ele para de executar o teste.

  // Respect "browser" field in package.json when resolving modules
  // browser: false,

  // The directory where Jest should store its cached dependency information
  // cacheDirectory: "/tmp/jest_0",

  // Automatically clear mock calls and instances between every test
  clearMocks: true,

  // Indicates whether the coverage information should be collected while executing the test
  collectCoverage: true,

  // An array of glob patterns indicating a set of files for which coverage information should be collected
  collectCoverageFrom: ['src/app/**/*.js'], // irá testar todos os arquivos .js dentro da pasta app.

  // The directory where Jest should output its coverage files
  coverageDirectory: 'coverage',

  // An array of regexp pattern strings used to skip coverage collection
  // coveragePathIgnorePatterns: [
  //   "/node_modules/"
  // ],

  // A list of reporter names that Jest uses when writing coverage reports
  coverageReporters: ['text', 'lcov'],

  // An object that configures minimum threshold enforcement for coverage results
  // coverageThreshold: null,

  // A path to a custom dependency extractor
  // dependencyExtractor: null,

  // Make calling deprecated APIs throw helpful error messages
  // errorOnDeprecated: false,

  // Force coverage collection from ignored files using an array of glob patterns
  // forceCoverageMatch: [],

  // A path to a module which exports an async function that is triggered once before all test suites
  // globalSetup: null,

  // A path to a module which exports an async function that is triggered once after all test suites
  // globalTeardown: null,

  // A set of global variables that need to be available in all test environments
  // globals: {},

  // The maximum amount of workers used to run your tests. Can be specified as % or a number. E.g. maxWorkers: 10% will use 10% of your CPU amount + 1 as the maximum worker number. maxWorkers: 2 will use a maximum of 2 workers.
  // maxWorkers: "50%",

  // An array of directory names to be searched recursively up from the requiring module's location
  // moduleDirectories: [
  //   "node_modules"
  // ],

  // An array of file extensions your modules use
  // moduleFileExtensions: [
  //   "js",
  //   "json",
  //   "jsx",
  //   "ts",
  //   "tsx",
  //   "node"
  // ],

  // A map from regular expressions to module names that allow to stub out resources with a single module
  // moduleNameMapper: {},

  // An array of regexp pattern strings, matched against all module paths before considered 'visible' to the module loader
  // modulePathIgnorePatterns: [],

  // Activates notifications for test results
  // notify: false,

  // An enum that specifies notification mode. Requires { notify: true }
  // notifyMode: "failure-change",

  // A preset that is used as a base for Jest's configuration
  // preset: null,

  // Run tests from one or more projects
  // projects: null,

  // Use this configuration option to add custom reporters to Jest
  // reporters: undefined,

  // Automatically reset mock state between every test
  // resetMocks: false,

  // Reset the module registry before running each individual test
  // resetModules: false,

  // A path to a custom resolver
  // resolver: null,

  // Automatically restore mock state between every test
  // restoreMocks: false,

  // The root directory that Jest should scan for tests and modules within
  // rootDir: null,

  // A list of paths to directories that Jest should use to search for files in
  // roots: [
  //   "<rootDir>"
  // ],

  // Allows you to use a custom runner instead of Jest's default test runner
  // runner: "jest-runner",

  // The paths to modules that run some code to configure or set up the testing environment before each test
  // setupFiles: [],

  // A list of paths to modules that run some code to configure or set up the testing framework before each test
  // setupFilesAfterEnv: [],

  // A list of paths to snapshot serializer modules Jest should use for snapshot testing
  // snapshotSerializers: [],

  // The test environment that will be used for testing
  testEnvironment: 'node',

  // Options that will be passed to the testEnvironment
  // testEnvironmentOptions: {},

  // Adds a location field to test results
  // testLocationInResults: false,

  // The glob patterns Jest uses to detect test files
  testMatch: ['**/__tests__/**/*.test.js'],

  // An array of regexp pattern strings that are matched against all test paths, matched tests are skipped
  // testPathIgnorePatterns: [
  //   "/node_modules/"
  // ],

  // The regexp pattern or array of patterns that Jest uses to detect test files
  // testRegex: [],

  // This option allows the use of a custom results processor
  // testResultsProcessor: null,

  // This option allows use of a custom test runner
  // testRunner: "jasmine2",

  // This option sets the URL for the jsdom environment. It is reflected in properties such as location.href
  // testURL: "http://localhost",

  // Setting this value to "fake" allows the use of fake timers for functions such as "setTimeout"
  // timers: "real",

  // A map from regular expressions to paths to transformers
  transform: {
    '.(js|jsx|ts|tsx)': '@sucrase/jest-plugin',
  },

  // An array of regexp pattern strings that are matched against all source file paths, matched files will skip transformation
  // transformIgnorePatterns: [
  //   "/node_modules/"
  // ],

  // An array of regexp pattern strings that are matched against all modules before the module loader will automatically return a mock for them
  // unmockedModulePathPatterns: undefined,

  // Indicates whether each individual test should be reported during the run
  // verbose: null,

  // An array of regexp patterns that are matched against all source file paths before re-running tests in watch mode
  // watchPathIgnorePatterns: [],

  // Whether to use watchman for file crawling
  // watchman: true,
};

```

Agora vamos instalar uma biblioteca do sucrase jest para podermos usar o import export.

```yarn add --dev @sucrase/jest-plugin

```

E dentro do jest.config, procuramos o `transform` e colocamos a configuração do jest q está na documentação [aqui][https://www.npmjs.com/package/@sucrase/jest-plugin]

```
"jest": {
    "transform": {
      ".(js|jsx|ts|tsx)": "@sucrase/jest-plugin"
    },
    ...
  }
```

Agora dentro do `nodemon.json` vamos passar uma configuração ignore, para que não reinicie o servidor em desenvolvimento quando está sendo testado:

```
{
  "execMap": {
    "js": "sucrase-node"
  },
  "ignore": ["__tests__"]
}
```

Agora vamos criar o nosso primeiro teste para testar a nossa configuração.

---

Vamos instalar uma biblioteca de intelicense:

`yarn add -D @types/jest`

Primeiro a gente cria um arquivo chamado `example.test.js` dentro da pasta `__tests__` e podemos até rodar `yarn test` e vemos que irá rodar, mas não vai testar nada.

Então vamos começar a escrever nosso teste.

```
function soma(a, b) {
  return a + b;
}

test('if I call soma function with 4 and 5 it should return 9.', () => {
  const result = soma(4, 5);

  expect(result).toBe(9);
});
```
