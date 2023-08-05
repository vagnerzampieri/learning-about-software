# Domain Driven Design

### Domínio

- É o contexto em que o software está inserido.
- Em vez de começar a escrever o software pensando na sua arquitetura, o correto é pensar nas regras de negócio e no domínio do problema que o software está resolvendo.
  - Exemplo: Uma classe Employee sem contexto é uma classe anêmica, sem sentido. Quando você pensa no domínio, você pensa que um Employee pode ter aumento via promoção, dissídio, acordo coletivo, etc. E aí você começa a pensar em como modelar isso. Sempre pensando nos domínios, nas regras de negócio.
- A ideia é usar a Linguagem de Domínio como uma Linguagem Onipresente, e trazer ela para o código.
- Com essa abordagem mudamos o nosso jeito de pensar em software, não é mais sobre criar um CRUD, mas sim sobre resolver um problema de negócio. Não é mais sobre escrever um monte de código pensando em todos os dados de um novo Employee, mas sim sobre pensar em como um Employee é contratado, como ele é promovido, como ele é demitido, etc.
- Você ao se preocupar com o domínio, você está se preocupando com o negócio, e não com a tecnologia. Você está se preocupando com o problema, e não com a solução. Você não quer apenas preencher o banco de dados, quer dar um sentido a toda informação cadastrada.
- No DDD a primeira coisa que temos que fazer é conversar com o Especialista do Domínio, que é a pessoa que entende do negócio, que sabe como as coisas funcionam. É com ele que vamos aprender sobre o domínio, e é com ele que vamos validar as nossas ideias.
- Um exemplo interessante sobre domínio, no domínio Hospital, para o médico temos um paciente, mas para o financeiro temos um cliente. Nesse caso aonde o paciente está internado é um subdomínio e o financeiro é outro.
- Tendo essa abordagem é mais fácil de criar serviços independentes, pois cada serviço vai ter o seu domínio, e não vai ter que se preocupar com o domínio dos outros serviços.
- As atividades que fazem a empresa ganhar dinheiro são o que chamamos de Core Domain, e as atividades que não fazem a empresa ganhar dinheiro são o que chamamos de Subdomain. Normalmente solução Core deve ser feita internamente, e solução Subdomain pode ser comprada de terceiros. O negócio tem um Core Domain e não a sua aplicação.
- No caso de implementação, por exemplo, você vai aposentar um funcionário, usando SOLID, você não vai modificar uma regra de aposentadoria, que pode mudar a partir do tempo, por causa de alguma lei específica, você vai implementar várias leis diferentes e suas regras, mas não vai mexer no ato de aposentar.
- Você pode ter duas entidades de Médico no sistema, no financeiro é necessário para o pagamento por exemplo, e na enfermagem esse médico pode não ter mais acesso ao sistema, pois ele foi demitido. Nesse caso temos dois subdomínios, o financeiro e o de enfermagem, e cada um tem a sua entidade de Médico. Com esse tipo de abordagem você diminui o custo de manutenção do sistema, pois não precisa ficar fazendo gambiarra para atender a todos os requisitos. Mas aumenta o custo de desenvolvimento, pois você vai ter que implementar a mesma entidade em vários lugares e fazer sync de dados entre os subdomínios, quando necessário.
- O domínio tem relação com você mudar os dados, mas se você precisa consultar os dados, você faz a consulta no banco de dados.

#### References

- [Domain Driven Design do Jeito Certo](https://www.youtube.com/watch?v=cz6EU7Z_BhE)
- [DDD do Jeito Certo](https://ddd-do-jeito-certo.online/)
