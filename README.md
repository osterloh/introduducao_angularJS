<h1 align="center">
    <img alt="AngularJS" src="https://angularjs.org/img/angularjs-for-header-only.svg" width="50%"/>
    <br>
    Introdução ao Framework AngularJS
</h1>

## Descrição

Este projeto está sendo desenvolvido em [AngularJS](https://angularjs.org/) para fins de capacitação pessoal

## Etapas

- Importação do AngularJS:

```bash
<script src="angular.js"></script>
```

- Declaração do nome da aplicação na diretiva <strong>ng-app</strong> declarada na tag HTML, definindo as fronteiras da aplicação:

```bash
<html ng-app="helloWorld">
```

- Declaração do módulo <strong>helloWorld</strong> com o parâmetro da injeção de dependências <strong>[]</strong>, utilizado para importação de novos módulos:

```bash
angular.module("helloWorld", []);
```

- Criação de um controller localizando o módulo pelo nome e criação de uma função, <strong>function</strong>, que será o local de declaração do controller como o <strong>\$scope</strong> declarado para ser a comunicação com a VIEW:

```bash
angular.module("helloWorld").controller("helloWorldCtrl", function ($scope) {
  $scope.message = "Hello World!";
});
```

- Declaração do <strong>ng-controller</strong> na view com interpolação da expressão através das <strong>{{}}</strong> para apresentar algo que foi declarado no <strong>\$scope</strong>:

```bash
<div ng-controller="helloWorldCtrl">
  {{message}}
</div>
```

- Diretivas: são extenções da linguagem HTML, que permite a implementação de novos comportamentos de forma declarativa.

- ngBind: substitui um elemento por expressão, parecido com a interpolação.

```bash
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.app = "Lista Telefonica";
    });
</script>

<div class="jumbotron">
  <h4 ng-bind="app"></h4>
</div>
```

- ngRepeat: permite a iteração entre arrays ou coleções e objetos. Em sua declaração possui uma variavel temporária, a palavra chave IN e o array declarado no \$scope com os dados.

```bash
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.contatos = [
        { nome: "Johnatan", telefone: "984727610" },
        { nome: "Mayara", telefone: "988166177" },
        { nome: "Anthony", telefone: "999765343" },
      ];
    });
</script>

<table>
  <tr>
    <th>Nome</th>
    <th>Telefone</th>
  </tr>
  <tr ng-repeat="contato in contatos">
    <td>{{contato.nome}}</td>
    <td>{{contato.telefone}}</td>
  </tr>
</table>
```

- Outra forma de imprimir os dados de um array utlizando o ngRepeat, é utilizando a declaração chave valor:

```bash
<tr ng-repeat="contato in contatos">
  <td ng-repeat="(key, value) in contato">{{value}}</td>
</tr>
```

- ngModel: realiza o inverso do ngBind, que pega algo do $scope e exibe, o ngModel pega algo da view e define no $scope. Os elementos que são aplicados o ngModel podem ser em: input, select e textArea.

```bash
<input type="text" ng-model="nome" />
<input type="text" ng-model="telefone" />
```

- ngClick: realiza a atribuição com base no comportamento disparado por algum evento, neste caso ao ser clicado no elemento o qual foi atribuido o ngClick.

```bash
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.app = "Lista Telefonica";
      $scope.contatos = [
        { nome: "Johnatan", telefone: "984727610" },
        { nome: "Mayara", telefone: "988166177" },
        { nome: "Anthony", telefone: "999765343" },
      ];
      $scope.adcionarContato = function () {
        $scope.contatos.push({nome: $scope.nome, telefone: $scope.telefone}); //deve ser evitado ao maximo ler o controller dentro do $scope
      };
    });
</script>
<button ng-click="adcionarContato()">Adicionar contato</button>
```

```bash
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.app = "Lista Telefonica";
      $scope.contatos = [
        { nome: "Johnatan", telefone: "984727610" },
        { nome: "Mayara", telefone: "988166177" },
        { nome: "Anthony", telefone: "999765343" },
      ];
      $scope.adcionarContato = function (nome, telefone) {
        $scope.contatos.push({ nome: nome, telefone: telefone }); //passando por parâmetro, declarando no ngClick
      };
    });
</script>
<button ng-click="adcionarContato(nome, telefone)">Adicionar contato</button>
```

```bash
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.app = "Lista Telefonica";
      $scope.contatos = [
        { nome: "Johnatan", telefone: "984727610" },
        { nome: "Mayara", telefone: "988166177" },
        { nome: "Anthony", telefone: "999765343" },
      ];
      $scope.adcionarContato = function (contato) {
        $scope.contatos.push(angular.copy(contato)); //melhor forma eh a utilizacao de abstracao
        delete $scope.contato;
      };
    });
</script>
<button ng-click="adcionarContato(contato)">Adicionar contato</button>
```

- ngDisabled: Desabilita um elemento dinamicamente.

```bash
<button ng-click="adcionarContato(contato)" ng-disabled="!contato.nome || !contato.telefone">
  Adicionar contato
</button>
```

-ngOptions: Serve para renderizar as opções do um select.

```bash
<script src="lib/angular/angular.js"></script>
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.app = "Lista Telefonica";
      $scope.contatos = [
        { nome: "Johnatan", telefone: "984727610" },
        { nome: "Mayara", telefone: "988166177" },
        { nome: "Anthony", telefone: "999765343" },
      ];
      $scope.operadoras = [
        { nome: "Oi", codigo: 14 },
        { nome: "Vivo", codigo: 15 },
        { nome: "Tim", codigo: 41 },
      ];
      $scope.adcionarContato = function (contato) {
        $scope.contatos.push(angular.copy(contato));
        delete $scope.contato;
      };
    });
</script>

<select
  ng-model="contato.operadora"
  ng-options="operadora.codigo as operadora.nome for operadora in operadoras"
>
  <option value="">Selecione uma operadora</option>
</select>

ou

<select
  ng-model="contato.operadora"
  ng-options="operadora.nome for operadora in operadoras"
>
  <option value="">Selecione uma operadora</option>
</select>

ou

<select
  ng-model="contato.operadora"
  ng-options="operadora.nome group by operadora.categoria for operadora in operadoras"
>
  <option value="">Selecione uma operadora</option>
</select>
```

- ngClass e ngStyle: Aplicar classes CSS e estilos dinamicamente

```bash
<style>
  .selecionado {
    background-color: green;
  }

  .negrito {
    font-weight: bold;
  }
</style>

<script src="lib/angular/angular.js"></script>
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.classe1 = "selecionado";
      $scope.classe2 = "negrito";
    });
</script>

<tr ng-class="[classe1, classe2]">
...
</tr>
```

```bash
<style>
  .selecionado {
    background-color: green;
  }

  .negrito {
    font-weight: bold;
  }
</style>

<script src="lib/angular/angular.js"></script>
<script>
  angular.module("listaTelefonica", []);
  angular
    .module("listaTelefonica")
    .controller("listaTelefonicaCtrl", function ($scope) {
      $scope.app = "Lista Telefonica";
    });
</script>

<tr ng-class="{selecionado: contato.selecionado, negrito: contato.selecionado}">
  <td><input type="checkbox" ng-model="contato.selecionado" /></td>
  ...
</tr>

ou

<tr ng-class="{'selecionado negrito': contato.selecionado}">
  <td><input type="checkbox" ng-model="contato.selecionado" /></td>
  ...
</tr>
```

- filter(): cria uma lista com os objetos que passam no teste implementado pela função fornecida, neste caso, retorna os contatos selecionados no checkbox, após clicar no botão Apagar Contatos.

```bash
  <script>
    angular.module("listaTelefonica", []);
    angular
      .module("listaTelefonica")
      .controller("listaTelefonicaCtrl", function ($scope) {
        $scope.app = "Lista Telefonica";
        $scope.contatos = [
          { nome: "Johnatan", telefone: "984727610", cor: "blue" },
          { nome: "Mayara", telefone: "988166177", cor: "yellow" },
          { nome: "Anthony", telefone: "999765343", cor: "red" },
        ];
        $scope.operadoras = [
          { nome: "Oi", codigo: 14, categoria: "Celular" },
          { nome: "Vivo", codigo: 15, categoria: "Celular" },
          { nome: "Tim", codigo: 41, categoria: "Celular" },
          { nome: "GVT", codigo: 25, categoria: "Fixo" },
          { nome: "Embratel", codigo: 21, categoria: "Fixo" },
        ];
        $scope.adcionarContato = function (contato) {
          $scope.contatos.push(angular.copy(contato)); //melhor forma eh a utilizacao de abstracao
          delete $scope.contato;
        };
        $scope.apagarContatos = function (contatos) {
          $scope.contatos = contatos.filter(function (contato) {
            if (!contato.selecionado) return contato;
          });
        };
      });
  </script>

  <button ng-disabled="!isContatoSelecionado(contatos)">Apagar contatos</button>
```

- some(): parecido com o filter().

```bash
  <script>
    angular.module("listaTelefonica", []);
    angular
      .module("listaTelefonica")
      .controller("listaTelefonicaCtrl", function ($scope) {
        $scope.app = "Lista Telefonica";
        $scope.contatos = [
          { nome: "Johnatan", telefone: "984727610", cor: "blue" },
          { nome: "Mayara", telefone: "988166177", cor: "yellow" },
          { nome: "Anthony", telefone: "999765343", cor: "red" },
        ];
        $scope.operadoras = [
          { nome: "Oi", codigo: 14, categoria: "Celular" },
          { nome: "Vivo", codigo: 15, categoria: "Celular" },
          { nome: "Tim", codigo: 41, categoria: "Celular" },
          { nome: "GVT", codigo: 25, categoria: "Fixo" },
          { nome: "Embratel", codigo: 21, categoria: "Fixo" },
        ];
        $scope.adcionarContato = function (contato) {
          $scope.contatos.push(angular.copy(contato)); //melhor forma eh a utilizacao de abstracao
          delete $scope.contato;
        };
        $scope.apagarContatos = function (contatos) {
          $scope.contatos = contatos.filter(function (contato) {
            if (!contato.selecionado) return contato;
          });
        };
        $scope.isContatoSelecionado = function (contatos) {
          return contatos.some(function (contato) {
            return contato.selecionado;
          });
        };
      });
  </script>

  <button ng-disabled="!isContatoSelecionado(contatos)">Apagar contatos</button>
```

## Tecnologias

- [AngularJS](https://code.angularjs.org/1.8.0/angular-1.8.0.zip)

---

Desenvolvido por [Johnatan Luiz Osterloh](https://www.linkedin.com/in/johnatanosterloh/)
