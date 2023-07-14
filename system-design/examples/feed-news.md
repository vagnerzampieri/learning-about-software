## Example: Feed News

[SYSTEM DESIGN: ALÉM DA ENTREVISTA](https://www.youtube.com/watch?v=-8tdjn30SSw)

### Requerimentos

- Qual é o objetivo principal do sistema?
  - compartilhar notícias, escrever textos, adicionar imagens com texto, adicionar vídeos com texto, fazer comentários, curtir, seguir pessoas e feed.

- Qual os objetivos funcionais do sistema?
  - adicionar como descrição coisas como imagem, vídeo, notícias e texto.
  - pode ter no máximo 4 imagens.
  - qualquer link que for adicionado será contado como texto.
  - possibilidade de curtir e comentar.
  - possibilidade de seguir pessoas, ser seguido, excluir e bloquear.
  - ver feed de notícias.

- Qual os objetivos não funcionais do sistema?
  - consistente.
  - altamente disponível.
  - tolerante a falhas.
  - escalável.
  - seguro.

- Modelagem do banco de dados

- User
  - id
  - name
  - email
  - nickname
  - location
  - password

- Follow
  - id
  - follower_id (user_id)
  - following_id (user_id)

- Block
  - id
  - user_id
  - blocked_user_id

- Post
  - id
  - user_id
  - content
  - parent_id (post_id)
  - considerações: um post funciona como um comentário tbm, tendo outros comentários encadeados a ele, como uma lista encadeada. O post que não tiver um parent_id é um post raiz.

- Like
  - id
  - user_id
  - post_id

### Diagramas

![Feed News - v1](../images/feed-news-v1.png)
![Feed News - v2](../images/feed-news-v2.png)
