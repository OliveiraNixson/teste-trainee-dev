
# Relatório Técnico – Nixson Oliveira Pires

## 1. Visão Geral da Solução

Este projeto consiste em uma aplicação web de gerenciamento de tarefas (To-do List), originalmente fornecida com erros e funcionalidades incompletas. Realizei uma série de correções e melhorias para tentar fazer ela mais funcional, intuitiva e moderna. Entre as principais alterações estão: correção de bugs de renderização e comportamento, melhoria na UX, implementação de ordenação alfabética, exportação de tarefas em PDF, adição de múltiplas tarefas simultaneamente, filtragem de palavras ofensivas e integração com bibliotecas para melhorar a interação com o usuário.


## 2. Como Executar a Aplicação

### Pré-requisitos

* Node.js (v16 ou superior)
* Angular CLI instalado globalmente

### Passos

```bash
# Clonar o repositório
git clone https://github.com/seu-usuario/todo-app.git

# Acessar o diretório do projeto
cd todo-app

# Instalar as dependências
npm install

# Rodar a aplicação
npm start
```

---

## 3. Correção dos Erros Iniciais (npm start)

### Erros encontrados:


* Falta de start apontando para ng serve, sendo declarado no pack json
* Erro de importação de módulo (`Module not found`), havia um erro de digitação
* Template quebrado por falta de imports(TodoService)
* Falta de bibliotecas essenciais

### Soluções aplicadas:

* Corrigi a falta de start nos scripts
* Mudei o nome errado do componente sendo importado
* Importação correta do todoservice no arquivo
* Importação de bibliotecas faltantes


## 4. Relatório de Correção de Bugs

1. Eliminação de chamada duplicada ao this.todoService.addTodo(newTodo);
Identifiquei que o serviço  estava sendo chamado mais de uma vez desnecessariamente. Refatorei o código para garantir chamadas únicas e eficientes, evitando redundâncias.

2. Sempre que o contador era maior que um ele não entrava mais dentro do if.
Reescrevi a condição responsável por salvar tarefas para deixar apenas string não vazias criarem a função 

3. Removi parametro : [innerHTML]="labelClearAll" 
  Adicionei apenas o nome traduzido dentro da clausula button

4,5. Os textos estavam invertidos: Exibir Tarefas Concluídas' : 'Ocultar Tarefas Concluídas'
Apenas inverti a ordem que apareciam

6. Não havia nenhum tipo de confirmação para exclusão. 
Apenas adicionei uma pergunta Confirm 

7. Ao fazer o filtro dos elementos filter fazia isso de maneira invertida
apenas troquei completed === true para false

8. O botão não tinha evento de click
Adicionei ao botão esse evento e criei uma função para chamar o serviço updateTodo já provida

  
9. Reordenação de botões na interface
Apenas Criei uma div e adicionei editar e remover nela, além de fazer umas alterações no css para impedir que caso o titulo seja muito grande ele não amasse os botões


10. Remoção de CSS inline com prioridade indevida
Eliminei estilos aplicados diretamente via `style` no componente, os quais estavam sobrepondo o CSS declarado nos arquivos de estilo dedicados.


11. Alterei esse parametro no css verflow-y
Mudei para auto e permitir rolagem lateral


12 e 13. Validação de tarefas vazias ou com espaços
Corrigi isso durante  commit dois quando tratava o problema referente a duplicação na hora de salvar. Trim() remove o espaco da string e caso retorne false(não fez nada) não retorna nada.

## 5. Relatório de Implementação de Melhorias

| Funcionalidade                          | Descrição Técnica                                                         | Bibliotecas Usadas                                                                              |
| --------------------------------------- | ------------------------------------------------------------------------- | -----------------------------------------------------------------
| Ordenar tarefas de A-Z                  | Utilizei `.sort()` com `localeCompare()` apenas em tarefas não concluídas | Nenhuma                                                                                         |
| Exportar PDF                            | Usei `html2canvas` e `jsPDF` com captura de tela da lista                 | [`html2canvas`](https://html2canvas.hertzen.com/), [`jsPDF`](https://github.com/parallax/jsPDF) |
| Adição múltipla de tarefas              | Divisão de `this.newTaskTitle` por vírgula                                | Nenhuma                                                                                         |
| Filtro de palavrões                     | Usei a lib `bad-words` para impedir adição de linguagem ofensiva          | [`bad-words`](https://github.com/web-mech/badwords)                                             |
| Substituição de `alert()` e `confirm()` | Implementei `Swal.fire()` com botões personalizados                       | [`SweetAlert2`](https://sweetalert2.github.io/)                                                 |



## 6. Relatório de Débito Técnico

| Item                              | Dificuldade Enfrentada                           | Observação                                         |
| --------------------------------- | ------------------------------------------------ | -------------------------------------------------- |
| Exportação para PDF               | O `html2canvas` não captura bem todos os estilos | Necessario mais pesquisas para saber o motivo      |




## 7. Relatório de Melhorias Futuras

* Edição inline de tarefas (sem `prompt`)
* Filtro de busca por título
* Responsividade para dispositivos móveis
* Modo escuro
* Persistência via localStorage ou backend


## 8. Decisões e Considerações

* Optei por separar tarefas concluídas das pendentes na ordenação, pois é natural ver elas indo para o final da lista.
* O uso de SweetAlert2 melhorou muito a interface sem impactar na lógica da aplicação.
* Tentei utilizar soluções como `canvas` ou `jsPDf` para fazer a exportação .
* Algumas decisões de UI foram tomadas para facilitar a usabilidade.



