## Example: Landing Page

- Qual é o objetivo principal do sistema?
  - criar uma landing page para um cliente.
  
- Quais os objetivos funcionais do sistema
  - construir e editar uma landing page.
  - quando terminar a edição é necessário publicar a landing page.
  - a página deverá estar disponível para receber visitas.
  - é necessário pegar as informações de quantas pessoas visitaram a página em X dias e quantas clicaram para enviar as respostas.
  - não é para usar serviço de terceiros na captação das estatísticas.
- Quais os objetivos não funcionais do sistema?
  - A startup cresceu muito e dos 2.000 clientes que tinha, passou para 20.000. As páginas, ao longo do tempo foram ficando lentas, estatísticas de click e views passaram a ter atrasos muito grandes e precisamos de melhorias estruturais que façam o sistema comportar os seguintes requisitos:

  1. 1 cliente faz em média 2 edições (criação ou atualização) nas landing pages por dia.

  2. 30.000 publicações diárias (atualizações e novas).

  3. 100.000 landing pages publicadas.
   
  4. 10.000.000 acessos por hora às LP's no pior caso.

  5. 1.000.000 de clicks por hora nas LP's no pior caso.


### Modelagem do banco de dados

- Company
  - id
  - name
  - email
  - created_at
  - updated_at
  - deleted_at

- User
  - id
  - company_id
  - name
  - email
  - password
  - created_at
  - updated_at

- Landing Page
  - id
  - company_id
  - name
  - token (necessary for redis)
  - logo
  - image
  - fields (json)
  - created_at
  - updated_at
  - published_at
  - deleted_at

- Lead
  - id
  - landing_page_id
  - data (json, com as informações do lead, os campos são dinâmicos vindo de LandingPage#fields)
  - created_at
  - updated_at

- Landing Page View
  - id
  - landing_page_id
  - clicks
  - views
  - created_at (to know the day)
  - updated_at
  - considerações: essa tabela ficará em um serviço separado, esse serviço pegará os dados do Redis e salvará no banco de dados.
   
### Endpoints

- POST /landing_pages
  - company_id
  - name
  - logo
  - image
  - fields
  - published_at
  - considerações: é possível passar os campos para a landing page, mas não é obrigatório, caso não seja passado, a landing page será criada com os campos padrões. O token será gerado automaticamente, ele será uma concatenação de id e url.

- PATCH /landing_pages/:id
  - name
  - logo
  - image
  - fields
  - published_at

- GET /landing_pages/:id

- POST /landing_pages/:id/views
  - token
  - clicks
  - views
  - considerações: esse endpoint será usado para enviar as estatísticas de ao entrar na view e de click com as informações do Lead.

- POST /company
  - name
  - email

- POST /signup
  - body:
    - company_id
    - name
    - email
    - password

- POST /login
  - body:
    - email/nickname
    - password 

### Diagrama


### Informações adicionais

- A modelagem com Redis será o mínimo de dado possível, a ideia é fazer um contador em cima de um token, esse token vai representar a url de um cliente, é necessário que seja único e bem pequeno. De tempos em tempos esses dados vão ser extraídos para um DB que possa ser consultado com mais facilidade por alguma ferramenta de estatística.

- Ex.: { token: 123456, views: 200, clicks: 10 } ... a idea é que o token seja um número bem pequeno, para que seja possível fazer uma consulta rápida no Redis. Cada byte conta para o Redis, então, quanto menor o registro, melhor.