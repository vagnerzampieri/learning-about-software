## System Design

<details>
  <summary>client-server model</summary>
  
  O modelo cliente-servidor é uma abordagem arquitetônica utilizada em sistemas de rede e aplicativos de computador, onde há uma divisão clara de papéis e responsabilidades entre os componentes chamados "cliente" e "servidor". Esse modelo permite que dispositivos ou programas se comuniquem e trabalhem juntos de maneira eficiente.

  Nesse modelo, o cliente é um dispositivo ou programa que solicita e utiliza os serviços fornecidos por outro dispositivo ou programa chamado servidor. O cliente inicia a comunicação enviando uma solicitação ao servidor, e o servidor responde a essa solicitação fornecendo os serviços ou recursos solicitados. Essa interação é baseada em um protocolo de comunicação, como HTTP (Hypertext Transfer Protocol) para aplicativos da web ou SMTP (Simple Mail Transfer Protocol) para envio de e-mails.
</details>

<details>
  <summary>networks protocols</summary>

  Os protocolos de rede são conjuntos de regras e procedimentos que governam a comunicação entre dispositivos em uma rede. Eles definem como os dispositivos trocam dados, estabelecem conexões, detectam erros, gerenciam endereçamento e realizam outras funções essenciais para a comunicação eficiente na rede. Aqui estão alguns dos protocolos de rede mais comuns:

  1. TCP/IP (Transmission Control Protocol/Internet Protocol): É o conjunto de protocolos mais amplamente utilizado na Internet. O TCP é responsável pelo controle de transmissão confiável dos dados, enquanto o IP é responsável pelo endereçamento e roteamento dos pacotes na rede.

  2. HTTP (Hypertext Transfer Protocol): É um protocolo usado para transferir recursos, como páginas da web, na World Wide Web. Ele permite a comunicação entre clientes e servidores web.

  3. HTTPS (Hypertext Transfer Protocol Secure): É uma extensão do HTTP que adiciona uma camada de segurança usando criptografia. É amplamente usado para acessar sites seguros, como serviços bancários online e compras.

  4. FTP (File Transfer Protocol): É um protocolo usado para transferir arquivos entre um cliente e um servidor em uma rede. Ele permite fazer upload, download e gerenciar arquivos em servidores remotos.

  5. SMTP (Simple Mail Transfer Protocol): É usado para enviar e-mails entre servidores de e-mail. É responsável pela transferência confiável de mensagens de e-mail pela Internet.

  6. POP3 (Post Office Protocol version 3): É um protocolo usado pelos clientes de e-mail para recuperar mensagens de um servidor de e-mail remoto. Ele permite que os usuários façam o download de e-mails para seus dispositivos.

  7. IMAP (Internet Message Access Protocol): É outro protocolo de e-mail que permite que os clientes acessem e gerenciem mensagens de e-mail armazenadas em um servidor remoto. Ao contrário do POP3, o IMAP permite que os usuários visualizem e organizem as mensagens no servidor sem precisar fazer o download delas.

  Esses são apenas alguns exemplos de protocolos de rede. Existem muitos outros protocolos que desempenham funções específicas em diferentes camadas do modelo OSI (Open Systems Interconnection) ou do modelo TCP/IP. Cada protocolo tem seu propósito e características específicas, e sua seleção depende das necessidades e requisitos da rede ou aplicativo em questão.
</details>

<details>
  <summary>storage</summary>

  O armazenamento refere-se ao processo de retenção e organização de dados, informações e arquivos em dispositivos físicos ou sistemas de armazenamento digital. É essencial para preservar e acessar dados de maneira confiável e eficiente. Existem várias formas de armazenamento, incluindo:

  1. Armazenamento local: Envolve o uso de dispositivos de armazenamento físico conectados diretamente a um computador ou servidor. Exemplos comuns incluem discos rígidos (HDDs), unidades de estado sólido (SSDs), unidades de fita e unidades ópticas (como CDs e DVDs). O armazenamento local é rápido e oferece acesso direto aos dados, mas está limitado pela capacidade física do dispositivo.

  2. Armazenamento em rede: Refere-se ao uso de dispositivos de armazenamento conectados a uma rede, como servidores de arquivos ou sistemas de armazenamento em rede (NAS - Network Attached Storage). Isso permite que vários dispositivos acessem e compartilhem os dados armazenados centralmente. É útil para compartilhar arquivos e recursos em ambientes de rede, mas também pode exigir configuração e gerenciamento adicionais.

  3. Armazenamento em nuvem: É um modelo de armazenamento baseado na Internet, onde os dados são armazenados em servidores remotos e acessados por meio da Internet. Provedores de serviços em nuvem, como Amazon Web Services (AWS), Google Cloud Platform (GCP) e Microsoft Azure, oferecem espaço de armazenamento virtualmente ilimitado, permitindo armazenar e acessar dados de qualquer lugar com conexão à Internet. O armazenamento em nuvem é escalável, flexível e geralmente oferece recursos adicionais, como backup automático e compartilhamento de arquivos.

  5. Armazenamento em memória flash: É uma tecnologia de armazenamento digital não volátil que usa chips de memória flash para armazenar dados. É amplamente usado em dispositivos como unidades USB, cartões de memória, SSDs e dispositivos móveis. A memória flash é rápida, resistente a choques e consome menos energia em comparação com as unidades de disco rígido tradicionais.

  Além disso, existem outras formas de armazenamento, como armazenamento em banco de dados, armazenamento em cache e armazenamento em memória RAM, que são otimizados para diferentes tipos de dados e aplicações específicas.

  A escolha do tipo de armazenamento depende dos requisitos individuais, como capacidade, velocidade, confiabilidade, segurança e custo. Frequentemente, uma combinação de diferentes tecnologias de armazenamento é usada para atender às necessidades específicas de um sistema ou organização.
</details>

<details>
  <summary>latency and throughput</summary>

  Latência e taxa de transferência (throughput) são dois conceitos importantes relacionados ao desempenho e eficiência de sistemas de comunicação e armazenamento de dados. Ambos têm um impacto significativo na experiência do usuário e na capacidade de processamento dos sistemas. Vamos entender melhor cada um deles:

  1. Latência: A latência é o tempo decorrido entre o envio de uma solicitação de dados e o recebimento da resposta. É uma medida do atraso que ocorre durante a transmissão ou processamento de informações. A latência é influenciada por vários fatores, como a distância física entre os dispositivos, a velocidade do meio de comunicação utilizado (por exemplo, cabos de fibra ótica ou conexões sem fio), o tempo de processamento necessário nos dispositivos envolvidos e a eficiência dos protocolos de comunicação utilizados. Uma latência menor é desejável, pois implica em tempos de resposta mais rápidos e maior agilidade nos sistemas.

  2. Taxa de transferência (Throughput): A taxa de transferência é a quantidade de dados que pode ser transmitida em um determinado período de tempo. É uma medida da capacidade de processamento ou da largura de banda de um sistema. A taxa de transferência é influenciada por vários fatores, como a largura de banda da rede, a capacidade de processamento dos dispositivos envolvidos, o tipo de meio de comunicação utilizado e a eficiência dos protocolos de comunicação. Uma taxa de transferência mais alta é desejável, pois indica uma maior capacidade de processamento e transmissão de dados.

  É importante observar que a latência e a taxa de transferência são conceitos distintos, embora estejam relacionados. Uma alta taxa de transferência pode ajudar a reduzir o tempo total necessário para transmitir uma grande quantidade de dados, enquanto uma baixa latência pode melhorar a responsividade de uma aplicação ou sistema em tempo real. Ambos os aspectos são relevantes em diferentes contextos e precisam ser considerados ao projetar e avaliar sistemas de comunicação e armazenamento de dados, dependendo dos requisitos específicos e das necessidades do uso pretendido.

</details>

- higher availability and consistency
- caching
- proxies
- load balancing
- hashing
- SQL and NoSQL
- replication and sharding
- leader election
- P2P
- polling and streaming
- configuration
- rate limiting
- logging and monitoring
- publish/subscribe
- map reduce
- security and HTTPS
- API design
- elasticity and scalability
  - elasticity: sazionalidade de picos
  - scalability: quantia do DAU

### Perguntas para entender o problema

  Devemos fazer algumas perguntas para entender o problema e definir os requisitos do sistema, como:

  - Qual é o objetivo principal do sistema?
  - Quem serão os usuários do sistema e quais são suas necessidades?
  - Quais são os requisitos funcionais e não funcionais do sistema?
  - Qual é a escala do sistema? Quantos usuários ele precisa suportar?
  - Quais são as limitações ou restrições técnicas que você precisa levar em consideração?
  - Quais são os componentes principais do sistema e como eles interagem entre si?
  - Quais tecnologias, linguagens de programação, frameworks ou plataformas você planeja utilizar?
  - Como você garantirá a segurança do sistema e protegerá os dados dos usuários?
  - Como você planeja lidar com possíveis falhas ou problemas de escalabilidade?
  - Quais são os requisitos de desempenho do sistema? Ele precisa ser altamente disponível ou ter baixa latência?
  - Como você planeja monitorar e realizar manutenção do sistema após o lançamento?
  - Qual é o plano de implantação do sistema? Como você irá configurar, testar e lançar o sistema?
  - Como você irá lidar com a migração de dados, se necessário?
  - Você considerou a modularidade e a extensibilidade do sistema? Ele pode ser facilmente adaptado a mudanças futuras?
  - Como você irá documentar o sistema e compartilhar conhecimento sobre sua arquitetura e funcionamento?

### Example: Feed News
  
  [Link para o exemplo](examples/feed-news.md)

### Example: Parking Garage
  
  [Link para o exemplo](examples/parking-garage.md)

### Videos:

  - [20 System Design Concepts Explained in 10 Minutes](https://www.youtube.com/watch?v=i53Gi_K3o7I)
  - [ENTREVISTA SYSTEM DESIGN: O ROADMAP PARA VOCÊ SER CONTRATADO!](https://www.youtube.com/watch?v=-NF06EaAr0I&list=PLs-l5bSgIMhAIi4QIWvzwdyoTFXj9CDFv&index=4)
    - [miro](https://miro.com/app/board/uXjVPfOXbs8=/) 
  - [Design a Payment System - System Design Interview](https://www.youtube.com/watch?v=olfaBgJrUBI) 
  - [Design a Basic Search Engine (Google or Bing) | System Design Interview Prep](https://www.youtube.com/watch?v=0LTXCcVRQi0)

### References:

- [miro](https://miro.com/app/board/uXjVORFgFfA=/)
- [architectural katas](https://nealford.com/katas/list.html)
- [system design course](https://github.com/karanpratapsingh/system-design)
- [sytem desgin roadmap](https://roadmap.sh/system-design)