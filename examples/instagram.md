## Example: Instagram

[System Design Mock Interview: Design Instagram](https://www.youtube.com/watch?v=VJpfO6KdyWE)

- Qual é o objetivo principal do sistema?
  - compartilhar fotos, vídeos, fazer comentários, curtir, seguir pessoas e feed.
- Quantos usuários o sistema precisa suportar?
  - 10 milhões de usuários.
- Qual a média de fotos e vídeos que um usuário posta por mês?
  - 10 fotos ou vídeos por mês.
- Qual a média de comentários que um usuário faz por mês?
  - 10 comentários por mês.
- Qual a média de tamanho de fotos?
  - 5 MB.
- Qual a média de tamanho de vídeos?
  - 50 MB.
- Qual a taxa de armazenamento que o sistema precisa suportar?
  - 10 milhões de usuários * 10 fotos por mês * 5 MB = 500 TB.
  - 10 milhões de usuários * 10 vídeos por mês * 50 MB = 50 PB.
  - 10 milhões de usuários * 10 comentários por mês * 1 KB = 100 GB.  
- Quais requisitos funcionais do sistema?
  - adicionar uma foto ou vídeo com uma descrição.
  - deletar uma foto ou vídeo.
  - curtir uma foto ou vídeo.
  - descurtir uma foto ou vídeo.
  - fazer comentário em uma foto ou vídeo.
  - deletar um comentário.
  - seguir uma pessoa.
  - parar de seguir uma pessoa.
- Quais requisitos não funcionais do sistema?
  - consistente.
  - altamente disponível.
  - tolerante a falhas.
  - escalável.
  - seguro.

### Modelagem do banco de dados

- User
  - id
  - name
  - email
  - nickname
  - location
  - password

- Post
  - id
  - user_id
  - description
  - image_path
  - video_path

- Comment
  - id
  - user_id
  - description

- Follow
  - id
  - follower_id (user_id)
  - following_id (user_id)

- Like
  - id
  - user_id
  - post_id
   
### Endpoints

- POST /posts
  - body:
    - description
    - image_path
    - video_path

- GET /feed
  - params:
    - user_id
  - consiferações: 
    - ordenar por data de criação.
    - mostrar apenas os posts dos usuários que o usuário segue.

- GET /posts/:id

- DELETE /posts/:id
  - user_id

- POST /posts/:id/comments
  - body:
    - description
    - user_id

- DELETE /posts/:post_id/comments/:comment_id
  - user_id

- POST /posts/:id/likes
  - user_id

- DELETE /posts/:post_id/likes/:like_id

- POST /follows
  - body:
    - follower_id
    - following_id

- DELETE /follows/:id
  - body:
    - follower_id
    - following_id

- POST /signup
  - body:
    - name
    - email
    - nickname
    - password

- POST /login
  - body:
    - email/nickname
    - password 


### Diagrama


### Conclusão