# Turbo

## Turbo Driver

É um JavaScript que intercepta os cliques nos links e formulários e faz uma requisição AJAX para o servidor. O servidor responde com um HTML que é inserido no DOM atualizando o conteúdo do `body` da página inteiro.

## Turbo Frame

É um elemento HTML que permite atualizar uma parte específica da página. O Turbo Frame é um container que pode ser atualizado com o conteúdo de uma requisição AJAX.

## Turbo Stream

É um formato de resposta do servidor que contém instruções para atualizar o DOM. O Turbo Stream é um JSON que contém instruções para adicionar, substituir ou remover pequenos elementos do DOM simultaneamente.

### Cheatsheet

- Não aplique o Turbo de cara, faça toda a construção do código recarregando a página e depois aplique o Turbo, com isso você vai ver mais facilmente se algo está errado no processo.

### Referências

- [Turbo Handbook](https://turbo.hotwired.dev/handbook/introduction)
- [Turbo Hotrails](https://www.hotrails.dev/turbo-rails)
