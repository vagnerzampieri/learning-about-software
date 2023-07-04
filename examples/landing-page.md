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

- Landing Page
  - id
  - name
  - url
  - token (necessary for redis)
  - logo
  - image
  - fields (json)
  - created_at
  - updated_at
  - published_at
  - deleted_at

- 

   
### Endpoints


### Diagrama


### Informações adicionais

- A modelagem com Redis será o mínimo de dado possível, a ideia é fazer um contador em cima de um token, esse token vai representar a url de um cliente, é necessário que seja único e bem pequeno. De tempos em tempos esses dados vão ser extraídos para um DB que possa ser consultado com mais facilidade por alguma ferramenta de estatística.