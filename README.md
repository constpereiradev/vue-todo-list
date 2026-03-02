# To do List

Este projeto contém uma lista de tarefas estática feita com Vue 3, seguindo as boas práticas dos cursos:
- Vue.js 3 [Fundamentals with the Composition API** da Vue School](https://vueschool.io/courses/vue-js-fundamentals-with-the-composition-api);
- Vue.js 3 [Component Fundamentals with the Composition API** da Vue School](https://vueschool.io/courses/vue-component-fundamentals-with-the-composition-api);

Além da [documentação oficial do Vue 3](https://vuejs.org/guide/introduction.html).

## Conceitos aplicados

Durante o desenvolvimento deste projeto, trabalhei com:

### Reatividade
- Diferença entre `ref` e `reactive`
- Derivação de estado com `computed`
- Efeitos colaterais com `watch`

### Ciclo de Vida
- Uso do `onMounted` para recuperação de dados persistidos

### Gerenciamento de Estado
- Persistência de dados com `LocalStorage`
- Observação profunda (`deep watch`) para sincronização automática

### Manipulação de Dados
- Criação, remoção e marcação de itens
- Filtragem dinâmica via propriedades computadas
- Controle de exibição condicional (dark mode)

### Interação com o Usuário
- Eventos (`v-on`)
- Two-way binding (`v-model`)
- Validação de formulário

### Componentes
- Criação de componentes locais e globais
- Utilização de componentes
- Comunicação entre componentes com eventos customizados
- Props e emits

## Decisões Técnicas

- Utilização de `computed` para filtragem ao invés de mutação direta do estado dos itens.
- Uso de `watch` apenas para efeitos colaterais (persistência).
- Manutenção de uma única fonte de verdade para os dados (`items`).

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
