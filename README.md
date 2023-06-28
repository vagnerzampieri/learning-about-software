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

<details>
  <summary>higher availability and consistency</summary>

  Alta disponibilidade e consistência são dois conceitos fundamentais em sistemas distribuídos e serviços online. Ambos visam garantir a confiabilidade e a qualidade dos sistemas em diferentes aspectos. Vamos entender melhor cada um deles:

  1. Alta disponibilidade: A alta disponibilidade refere-se à capacidade de um sistema ou serviço estar continuamente disponível e acessível aos usuários, com um tempo de inatividade mínimo. Isso implica que o sistema esteja funcionando corretamente e que os usuários possam acessá-lo sempre que precisarem. Para alcançar alta disponibilidade, são implementadas medidas como redundância de hardware e software, replicação de dados, balanceamento de carga, sistemas de recuperação de falhas e tolerância a falhas. Essas estratégias garantem que, mesmo se ocorrerem falhas em componentes individuais, o sistema continue operacional e os serviços permaneçam disponíveis para os usuários.

  2. Consistência: A consistência refere-se à propriedade de um sistema de garantir que todos os seus nós ou componentes tenham uma visão coerente e atualizada dos dados. Em sistemas distribuídos, onde várias cópias dos dados são mantidas em diferentes nós, garantir a consistência dos dados é um desafio. A consistência pode ser alcançada através de técnicas de sincronização e controle de concorrência, onde as operações de escrita e leitura são coordenadas para evitar leituras desatualizadas ou inconsistências nos dados. Diferentes modelos de consistência, como consistência forte ou consistência eventual, são adotados com base nos requisitos específicos do sistema e das aplicações.

  É importante destacar que há um trade-off entre alta disponibilidade e consistência. Em muitos casos, manter alta disponibilidade pode resultar em algum grau de inconsistência temporária nos dados, enquanto garantir uma consistência estrita pode levar a períodos de inatividade para sincronização e atualização dos dados. A escolha entre alta disponibilidade e consistência depende dos requisitos e das necessidades do sistema ou serviço em questão. Alguns sistemas podem priorizar a alta disponibilidade em cenários onde a disponibilidade contínua é crítica, enquanto outros podem priorizar a consistência em cenários onde a precisão dos dados é fundamental.
</details>

<details>
  <summary>caching</summary>

  Caching (ou cache) é uma técnica amplamente utilizada em sistemas de computação para melhorar o desempenho e a eficiência ao armazenar dados temporariamente em um local mais rápido e de acesso mais rápido do que a fonte original. O cache é uma memória auxiliar que armazena cópias de dados frequentemente acessados para fornecer acesso rápido a esses dados, reduzindo a necessidade de acessar a fonte original, que pode ser mais lenta.

  Quando um sistema faz uma solicitação por determinados dados, a primeira instância é verificar se esses dados estão disponíveis no cache. Se os dados estiverem no cache, eles são acessados diretamente, evitando a necessidade de recuperá-los da fonte original. Isso resulta em tempos de acesso mais rápidos e uma melhoria geral no desempenho.

  O cache é usado em vários níveis e em diferentes componentes de sistemas de computação. Alguns exemplos comuns incluem:

  1. Cache de hardware: Processadores modernos possuem caches embutidos em diferentes níveis (L1, L2, L3) para armazenar cópias de dados e instruções frequentemente utilizados. Esses caches são projetados para minimizar a latência de acesso à memória principal e acelerar a execução de instruções.

  2. Cache de software: Aplicativos e sistemas operacionais também podem utilizar caches em nível de software para armazenar dados frequentemente acessados. Isso pode incluir o cache de páginas da web em navegadores, cache de banco de dados, cache de arquivos em sistemas de arquivos, entre outros.

  3. Cache de rede: Em redes de computadores, os caches são usados para armazenar cópias de páginas da web, objetos de mídia, arquivos e outros dados frequentemente acessados. Isso é especialmente útil em servidores proxy, servidores de conteúdo em CDN (Content Delivery Network) e outros dispositivos de rede, que podem fornecer respostas mais rápidas aos clientes ao acessar dados armazenados em cache localmente.

  4. Cache de aplicativo: Aplicativos podem implementar caches para armazenar resultados de cálculos computacionalmente intensivos, resultados de consultas de banco de dados ou qualquer dado que possa ser reutilizado posteriormente. Esses caches ajudam a evitar o processamento repetido e a acelerar a resposta do aplicativo.

  Ao implementar caches, é necessário considerar estratégias de gerenciamento, como a substituição de dados no cache (políticas de substituição) e a atualização dos dados em cache para refletir mudanças na fonte original (invalidação ou expiração). O tamanho do cache também precisa ser considerado para equilibrar o espaço de armazenamento disponível e o benefício do cache.

  O caching é uma técnica poderosa para melhorar o desempenho, reduzir a carga em sistemas e otimizar a experiência do usuário, tornando o acesso a dados frequentes mais rápido e eficiente.
</details>

<details>
  <summary>proxies</summary>

  Proxies (ou servidores proxy) são intermediários entre os clientes e os servidores de destino em uma rede. Eles atuam como uma camada intermediária que recebe as solicitações dos clientes e encaminha essas solicitações aos servidores de destino, agindo em nome dos clientes. Os proxies podem desempenhar várias funções e oferecer diferentes benefícios. Vamos explorar algumas delas:

  1. Anonimato e privacidade: Um proxy pode ocultar o endereço IP do cliente, substituindo-o pelo seu próprio endereço IP. Isso proporciona anonimato e privacidade ao navegar na Internet, pois os servidores de destino não têm conhecimento direto do endereço IP do cliente original.

  2. Cache e aceleração de conteúdo: Os proxies podem armazenar em cache as respostas de servidores de destino para solicitações comuns. Quando um cliente faz uma solicitação semelhante, o proxy pode fornecer a resposta armazenada em cache em vez de encaminhar a solicitação ao servidor de destino novamente. Isso reduz o tempo de resposta e economiza largura de banda.

  3. Filtragem de conteúdo: Proxies podem ser usados para filtrar e bloquear certos tipos de conteúdo indesejado, como sites maliciosos, spam, anúncios ou conteúdo inapropriado. Isso é útil em ambientes corporativos ou em redes públicas para proteger os usuários contra ameaças e garantir o cumprimento de políticas de uso aceitável.

  4. Balanceamento de carga: Proxies também podem ser usados para distribuir o tráfego de entrada entre vários servidores de destino, distribuindo a carga de trabalho de forma mais equilibrada. Isso melhora o desempenho e a disponibilidade, evitando sobrecarga de servidores individuais.

  5. Controle de acesso: Os proxies podem ser configurados para controlar o acesso a recursos específicos, permitindo ou negando solicitações com base em regras de segurança ou políticas de acesso. Isso ajuda a reforçar a segurança da rede e proteger os recursos contra acessos não autorizados.

  Existem diferentes tipos de proxies, como proxies HTTP, proxies SOCKS, proxies reversos e proxies transparentes, cada um com suas características específicas e casos de uso. Os proxies podem ser implementados em hardware dedicado ou como software em sistemas ou dispositivos específicos.

  É importante mencionar que o uso de proxies também pode apresentar desvantagens, como a possível introdução de um ponto único de falha, impacto na latência das comunicações devido à introdução de um nó intermediário e a necessidade de configurar corretamente as políticas e regras de proxy para evitar problemas de acesso ou desempenho.

  Em resumo, os proxies desempenham um papel importante na rede, fornecendo funcionalidades adicionais, como anonimato, cache, filtragem, balanceamento de carga e controle de acesso. Eles são ferramentas versáteis que podem melhorar a segurança, desempenho e eficiência da comunicação entre clientes e servidores em uma rede.
</details>

<details>
  <summary>load balancing</summary>

  Load balancing é o processo de distribuir eficientemente o tráfego de rede de entrada em um grupo de servidores de back-end, também conhecido como um pool ou farm de servidores¹. Isso é feito para garantir que nenhum servidor fique sobrecarregado, o que poderia prejudicar o desempenho. Se um único servidor falhar, o balanceador de carga redireciona o tráfego para os servidores restantes que estão online. Quando um novo servidor é adicionado ao grupo de servidores, o balanceador de carga automaticamente começa a enviar solicitações para ele.

  Existem diferentes algoritmos de balanceamento de carga que fornecem diferentes benefícios; a escolha do método de balanceamento de carga depende das suas necessidades. Alguns exemplos incluem Round Robin, Least Connections, Least Time, Hash e IP Hash.

  O balanceamento de carga é importante porque ajuda a reduzir o tempo de inatividade, aumentar a escalabilidade e a redundância, fornecer flexibilidade e melhorar a eficiência. É comumente usado em sites com alto tráfego, servidores DNS, bancos de dados e sites FTP. Isso garante que as solicitações do usuário sejam processadas rapidamente e com precisão².
</details>

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
- idempotency
<details>
  <summary>elasticity and scalability</summary>

  Elasticidade e escalabilidade são dois conceitos relacionados à capacidade de expansão e adaptação de sistemas e recursos computacionais. Ambos são importantes para lidar com demandas variáveis e crescentes, mas possuem diferenças sutis. Vamos entender melhor cada um deles:

  1. Elasticidade: A elasticidade refere-se à capacidade de um sistema se adaptar dinamicamente às mudanças de carga ou demanda. Isso envolve aumentar ou diminuir automaticamente os recursos, como capacidade de processamento, armazenamento e largura de banda, de acordo com as necessidades em tempo real. A elasticidade permite que um sistema dimensione seus recursos de forma dinâmica para lidar com picos de demanda, garantindo um desempenho adequado e evitando sobrecarga ou desperdício de recursos em períodos de baixa demanda. Por exemplo, em serviços de nuvem, a elasticidade permite que os recursos computacionais sejam dimensionados automaticamente com base na carga de trabalho atual.

  2. Escalabilidade: A escalabilidade refere-se à capacidade de um sistema aumentar sua capacidade para atender a uma demanda crescente. Ela envolve adicionar recursos adicionais, como servidores, nós de processamento, bancos de dados ou infraestrutura de rede, para acomodar um número maior de usuários, maior volume de dados ou cargas de trabalho mais intensivas. A escalabilidade pode ser alcançada de forma vertical (escalabilidade vertical) ou horizontal (escalabilidade horizontal). A escalabilidade vertical envolve aumentar a capacidade dos recursos existentes, como adicionar mais memória ou processadores a um servidor. Já a escalabilidade horizontal envolve adicionar mais instâncias de recursos, como adicionar mais servidores ao sistema. A escalabilidade é geralmente planejada e implementada antes que o aumento da demanda ocorra, garantindo que o sistema possa crescer conforme necessário.

  Em resumo, a elasticidade está relacionada à capacidade de um sistema se ajustar de forma dinâmica às mudanças na demanda em tempo real, enquanto a escalabilidade está relacionada à capacidade de um sistema crescer de forma planejada e adicionar recursos adicionais para acomodar um aumento na demanda ao longo do tempo. Ambos os conceitos são cruciais para sistemas e serviços modernos, permitindo que sejam flexíveis, responsivos e capazes de lidar com cargas de trabalho variáveis.
</details>

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