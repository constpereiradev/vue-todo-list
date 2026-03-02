# To do List

Este projeto contém uma lista de tarefas estática feita com Vue 3, seguindo as boas práticas do curso **Vue.js 3 Fundamentals with the Composition API** da Vue School.

## Configuração Recomendada da IDE

[VS Code](https://code.visualstudio.com/) + [Vue (Official)](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (desabilite o Vetur).

## Configuração Recomendada do Navegador

### Navegadores baseados em Chromium (Chrome, Edge, Brave, etc.)

- Vue.js Devtools  
- Ativar **Custom Object Formatter** no Chrome DevTools  

### Firefox

- Vue.js Devtools  
- Ativar **Custom Object Formatter** no Firefox DevTools  

## Personalizar Configuração

Veja a documentação:  
[Vite Configuration Reference](https://vite.dev/config/)

## Instalação do Projeto

```sh
npm install
```

### Compilar e Executar em Desenvolvimento (Hot-Reload)

```sh
npm run dev
```

### Compilar e Minificar para Produção

```sh
npm run build
```

### Executar Testes End-to-End com [Nightwatch](https://nightwatchjs.org/)

```sh
# Ao utilizar CI, o projeto deve ser buildado primeiro
npm run build

# Executa os testes end-to-end
npm run test:e2e
# Runs the tests only on Chrome
# Executa os testes apenas no Chrome
# Executa os testes de um arquivo específico
npm run test:e2e -- tests/e2e/example.js
# Executa os testes em modo debug
npm run test:e2e -- --debug
```
    
### Executar Testes de Componentes com [Nightwatch Component Testing](https://nightwatchjs.org/guide/component-testing/introduction.html)
  
```sh
npm run test:unit
npm run test:unit -- --headless # for headless testing
```

---

## Sobre a Autora

Amanda da Conceição Pereira  
Desenvolvedora Backend  

Email: amandapereiradevcontact@gmail.com  
LinkedIn: https://linkedin.com/in/amanda-pereira-dev  
GitHub: https://github.com/constpereiradev  

---

Projeto desenvolvido para fins de estudo com Vue 3 e Composition API.
