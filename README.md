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

- Declaração do nome da aplicação na diretiva <strong>ng-app</strong> declara na tag HTML:

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

## Tecnologias

- [AngularJS](https://code.angularjs.org/1.8.0/angular-1.8.0.zip)

---

Desenvolvido por [Johnatan Luiz Osterloh](https://www.linkedin.com/in/johnatanosterloh/)
