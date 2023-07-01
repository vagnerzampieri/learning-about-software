## System Design

### Summary of System Design

  - How do define system requirements? 
    - System Requirements
    - Functional Requirements
    - High Availability
    - Fault Tolerance, resilience, reliability
    - Scalability
    - Performance
    - Durability
    - Consistency
    - Mentability, security, cost
  - How to achieve certain system qualities with the help of hardware?
    - Regions, availability zones, data centers, racks, servers
    - Physical servers, virtual machines, containers, serverless
  - Fundamentals of reliable, scalable, and fast communication
    - Syncronous vs Asyncronous communication
    - Asynchronous messaging patterns
    - Network protocols
    - Blocking vs non-blocking I/O
    - Data encoding formats
    - Message acknowledgement
  - How to improve system performance with caching?
    - Caching 
    - Caching strategies
    - Cache invalidation
    - Cache eviction policies
    - Cache consistency
    - Cache coherency
    - Cache partitioning
    - Cache aside vs read through vs write through
    - Deduplication cache
    - Metadata cache
  - The importance of queues in distributed systems
    - Message queues
    - Task queues
    - Priority queues
    - Delay queues
    - Bounded queues
    - Unbounded queues
    - Blocking queues
    - Producer-consumer pattern
    - Thread pools
  - Data store internals
    - Log
    - Index
    - Time series data
    - Simple key-value database
    - B-tree index
    - Embedded database
    - RocksDB
    - LSM-tree vs B-tree
    - Page cache
  - How to build efficient communication in distributed systems?
    - Push vs pull
    - Host discovery
    - Service discovery
    - Peer discovery
    - How to choose a network protocol?
    - Network protocols in real-life systems
    - Video over HTTP
    - CDN
    - Push and pull technologies
    - Large scale push architectures
  - How to deliver data reliably?
    - What else to know to build reliable, scalable, and fast systems?
    - What to do with failed requests?
    - When to retry?
    - How to retry?
    - Message delivery garanties
    - Consummer offsets
  - How to delivery data quickly?
    - Batching
    - Compression
  - How to deliver data at large scale?
    - How to scale message consumption?
    - Partitioning in real-life systems
    - Partioning strategies
    - Request routing
    - Rebalancing partitions
    - Consistent hashing
  - How to protect servers from clients?
    - System overload
    - Autoscaling
    - Autoscaling system design
    - Load shedding
    - Rate Limiting
  - How to protect clients from servers?
    - Syncronous vs Asyncronous clients
    - Circuit breaker
    - Fail-fast design principle
    - Bulkhead
    - Shuffle sharding

### System Design Basics

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

<details>
  <summary>hashing</summary>

  - Hashing é um processo utilizado para mapear dados de tamanho variável para um valor fixo, geralmente uma sequência de caracteres de tamanho fixo. O resultado desse processo é chamado de "hash" ou "valor de hash". O objetivo do hashing é gerar um resumo único e representativo dos dados de entrada, de forma eficiente e determinística.

  - Principais características e usos do hashing:

  1. Unicidade: Um bom algoritmo de hash deve minimizar a probabilidade de colisões, ou seja, de gerar o mesmo valor de hash para diferentes conjuntos de dados. Embora seja possível que dois conjuntos de dados diferentes gerem o mesmo valor de hash (colisão), algoritmos de hash comumente utilizados possuem uma baixa taxa de colisões.

  2. Integridade: O valor de hash é usado para verificar se os dados foram alterados ou corrompidos. Qualquer modificação nos dados de entrada resultará em um valor de hash completamente diferente. Isso torna o hashing útil para detectar alterações acidentais ou maliciosas nos dados.

  3. Eficiência: Algoritmos de hash são projetados para serem rápidos e eficientes, permitindo o processamento rápido dos dados e o cálculo do valor de hash. Mesmo para grandes volumes de dados, o tempo necessário para calcular o valor de hash é geralmente muito pequeno.

  4. Criptografia: Algoritmos de hash criptográficos, como SHA-256 (Secure Hash Algorithm 256 bits), são usados para garantir a segurança e a confidencialidade dos dados. Esses algoritmos são amplamente utilizados em aplicações como autenticação de senhas, assinatura digital e verificação de integridade de arquivos.

  5. Indexação e pesquisa: O hashing também é usado em estruturas de dados como tabelas de dispersão (hash tables), que permitem uma pesquisa eficiente de elementos com base em suas chaves. Os valores de hash são usados para mapear as chaves para posições de armazenamento, acelerando o processo de busca.

  - Alguns exemplos de algoritmos de hashing amplamente utilizados são MD5 (Message Digest Algorithm 5), SHA-1 (Secure Hash Algorithm 1), SHA-256, SHA-3 e HMAC (Hash-based Message Authentication Code). Cada um desses algoritmos tem suas próprias características e níveis de segurança, sendo selecionados de acordo com as necessidades específicas de cada aplicação.

  - É importante notar que, embora os algoritmos de hash sejam úteis em várias aplicações, eles não são reversíveis. Isso significa que, uma vez que os dados são convertidos em um valor de hash, não é possível recuperar os dados originais a partir do valor de hash. Portanto, os algoritmos de hash são usados principalmente para verificação, resumo e pesquisa eficiente, mas não para fins de criptografia ou armazenamento seguro de dados.
</details>

- SQL and NoSQL
- replication and sharding
<details>
  <summary>leader election</summary>

  - Leader election (eleição de líder) é um processo utilizado em sistemas distribuídos para selecionar um único nó (ou processo) entre vários para atuar como líder ou coordenador. O líder é responsável por tomar decisões e coordenar as atividades dos demais nós no sistema distribuído.

  - A eleição de líder é necessária em sistemas distribuídos para garantir a consistência e a coerência das operações. Quando o líder atual falha ou é desconectado do sistema, um novo líder precisa ser eleito para assumir suas responsabilidades. Esse processo de eleição ocorre de forma automática entre os nós remanescentes e é crucial para manter a continuidade do sistema.

  - Existem várias abordagens e algoritmos para realizar a eleição de líder. Alguns dos algoritmos populares incluem:

  1. Algoritmo do Bully: Neste algoritmo, cada nó tem um identificador único e o nó com o maior identificador assume o papel de líder. Quando um nó descobre que o líder atual está inativo, ele convoca uma eleição enviando mensagens para os outros nós com identificadores mais altos. Se nenhum nó responder, ele se declara líder. Caso contrário, o nó com o identificador mais alto assume a liderança.

  2. Algoritmo do Anel: Neste algoritmo, os nós são organizados em uma topologia em anel. Cada nó possui um identificador único e o processo de eleição ocorre no sentido horário ou anti-horário ao longo do anel. Quando um nó detecta a falha do líder atual, ele envia uma mensagem para o próximo nó no anel. A mensagem de eleição é passada pelos nós até chegar a um nó com o identificador mais alto, que se torna o novo líder.

  3. Algoritmo do Wave: Neste algoritmo, cada nó tem um identificador único e é atribuído um número sequencial chamado "onda" para cada eleição. Quando um nó inicia uma eleição, ele envia mensagens para todos os outros nós com um número de onda mais alto. Os nós que recebem a mensagem de eleição escolhem o identificador mais alto entre si e continuam propagando a mensagem para os outros nós. O nó com o identificador mais alto se torna o novo líder.

  - Esses são apenas alguns exemplos de algoritmos de eleição de líder. Cada algoritmo tem suas características e requisitos específicos, e a escolha depende do contexto e das necessidades do sistema distribuído em questão.

  - A eleição de líder é um mecanismo fundamental para garantir a continuidade das operações em sistemas distribuídos, permitindo que um novo líder seja selecionado automaticamente quando o líder atual não estiver mais disponível.

</details>

- P2P
- polling and streaming
- configuration

<details>
  <summary>rate limiting</summary>

  - Rate limiting (limitação de taxa) é uma técnica usada para controlar e limitar a taxa de solicitações ou acessos a um sistema, serviço ou API. É uma estratégia de gerenciamento de tráfego que impõe restrições na frequência com que uma determinada ação pode ser executada por um cliente ou usuário.

  - A implementação do rate limiting geralmente envolve definir limites em termos de número de solicitações por unidade de tempo (por exemplo, X solicitações por segundo ou Y solicitações por minuto). Quando um cliente ou usuário ultrapassa esse limite, o sistema responde com um código de status apropriado (como 429 Too Many Requests) e nega temporariamente ou restringe o acesso adicional por um período de tempo determinado.

  - Existem várias razões para implementar o rate limiting em um sistema:

  1. Proteção contra abuso: O rate limiting ajuda a prevenir abusos e ataques, limitando a frequência com que um cliente ou usuário pode acessar recursos ou realizar solicitações. Isso evita sobrecargas no sistema e protege contra ataques de negação de serviço (DoS) ou ataques de força bruta.

  2. Garantia de desempenho e estabilidade: Ao limitar o número de solicitações em um determinado período de tempo, o rate limiting ajuda a evitar a sobrecarga do sistema e a garantir que ele permaneça estável e responsivo. Isso é especialmente importante em sistemas com recursos limitados ou em momentos de pico de tráfego.

  3. Equilíbrio da carga: Ao impor limites na taxa de solicitações, o rate limiting permite distribuir a carga de forma equilibrada entre os usuários ou clientes. Isso evita que alguns usuários monopolizem os recursos e garante uma experiência justa para todos os usuários do sistema.

  4. Cumprimento de políticas de uso: O rate limiting pode ser usado para fazer cumprir políticas de uso, como limites de acesso por assinatura, planos de pagamento ou restrições de uso gratuito. Ele garante que os usuários estejam aderindo aos termos e condições estabelecidos e impede o uso excessivo ou não autorizado dos recursos.

  5. Controle de custos: Em sistemas baseados em nuvem ou que envolvem custos de infraestrutura, o rate limiting pode ser usado para controlar e limitar o consumo de recursos, ajudando a evitar faturas inesperadas ou excessivas.

  - A implementação do rate limiting pode variar dependendo do sistema ou serviço em questão. Pode envolver o uso de cabeçalhos HTTP, tokens de autenticação, contadores de solicitações ou outras técnicas de controle de acesso. A configuração adequada dos limites de taxa depende das necessidades e capacidades do sistema, equilibrando a segurança, desempenho e experiência do usuário.

</details>

- logging and monitoring
- publish/subscribe
- map reduce
- security and HTTPS
- API design

<details>
  <summary>API gateways</summary>

  - API gateways (portões de acesso de API) são componentes de infraestrutura que atuam como pontos de entrada para as APIs (Interfaces de Programação de Aplicativos). Eles desempenham um papel fundamental no gerenciamento, segurança e otimização do tráfego de uma API, atuando como intermediários entre os clientes e os serviços subjacentes.

  - Aqui estão algumas funcionalidades e benefícios dos API gateways:

  1. Gerenciamento de tráfego: Os API gateways atuam como um ponto centralizado de controle para o tráfego de uma API. Eles direcionam as solicitações dos clientes para os serviços correspondentes, garantindo que as solicitações sejam roteadas corretamente e distribuídas de forma equilibrada entre os serviços disponíveis.

  2. Segurança: Os API gateways fornecem camadas de segurança para proteger as APIs contra ameaças e ataques maliciosos. Eles podem autenticar e autorizar as solicitações dos clientes, aplicar políticas de segurança, como controle de acesso baseado em função (RBAC) e limitação de taxa, e criptografar o tráfego entre os clientes e os serviços.

  3. Transformação de dados: Os API gateways podem realizar transformações nos dados das solicitações e respostas da API. Isso inclui conversões de formatos, agregação de dados de diferentes fontes, enriquecimento de dados e validações. Essas transformações permitem que os clientes e os serviços se comuniquem de maneira eficiente e compatível.

  4. Cache: Os API gateways podem implementar camadas de cache para melhorar o desempenho e reduzir a carga nos serviços subjacentes. Eles podem armazenar em cache as respostas das solicitações para reutilização posterior, evitando que as mesmas solicitações sejam processadas repetidamente pelos serviços.

  5. Monitoramento e análise: Os API gateways podem coletar métricas e registros detalhados sobre o tráfego da API, fornecendo informações valiosas sobre o desempenho, utilização e comportamento dos clientes. Isso permite monitorar a saúde da API, detectar problemas, identificar gargalos de desempenho e tomar decisões informadas de otimização.

  6. Versionamento e controle: Os API gateways facilitam o gerenciamento de versões das APIs. Eles permitem que diferentes versões das APIs coexistam e sejam acessadas por clientes específicos. Isso ajuda a garantir a compatibilidade com versões anteriores e a introdução suave de alterações nas APIs.

  7. Integração de serviços: Os API gateways podem simplificar a integração de serviços diferentes, permitindo que sejam expostos por uma única interface unificada. Isso reduz a complexidade para os clientes, pois eles podem acessar diferentes serviços por meio de uma única API.

  - Em resumo, os API gateways são componentes essenciais para o gerenciamento, segurança e otimização de APIs. Eles fornecem recursos como gerenciamento de tráfego, segurança, transformação de dados, cache, monitoramento e análise, versionamento e controle, e integração de serviços. Essas funcionalidades ajudam a simplificar o desenvolvimento, melhorar a segurança, otimizar o desempenho e facilitar a integração de sistemas complex

  - https://www.redhat.com/en/topics/api/what-does-an-api-gateway-do
  
</details>
<details>
  <summary>serverless</summary>
  
  - Serverless computing (computação sem servidor) é um modelo de computação em nuvem em que os desenvolvedores podem escrever e executar código sem a necessidade de gerenciar a infraestrutura subjacente. Nesse modelo, o provedor de serviços em nuvem é responsável por provisionar, dimensionar e gerenciar automaticamente os recursos necessários para executar o código.

  - Em um ambiente serverless, os desenvolvedores se concentram na escrita do código da aplicação em vez de lidar com a configuração e manutenção dos servidores. Eles criam funções individuais (também chamadas de funções serverless ou funções como serviço) que são acionadas por eventos específicos, como uma solicitação HTTP, uma atualização em um banco de dados ou um arquivo sendo enviado para um armazenamento em nuvem.

  - Aqui estão algumas características e benefícios do modelo serverless:

  1. Escalabilidade automática: O provedor de serviços em nuvem dimensiona automaticamente a infraestrutura para atender à demanda. As funções serverless são escaladas horizontalmente, o que significa que várias instâncias da função podem ser executadas simultaneamente para lidar com cargas de trabalho mais pesadas.

  2. Pagamento por uso: O modelo serverless permite que os desenvolvedores paguem apenas pelos recursos consumidos durante a execução de suas funções. Os provedores de serviços em nuvem geralmente oferecem uma estrutura de preços baseada no tempo de execução e nos recursos consumidos, em vez de um modelo de pagamento por servidor ou capacidade fixa.

  3. Gerenciamento simplificado: Com o modelo serverless, os desenvolvedores podem se concentrar apenas na lógica do código e não precisam se preocupar com a administração de servidores, patches de segurança, escalabilidade manual, etc. O provedor de serviços em nuvem cuida de todas essas tarefas operacionais.

  4. Tempo de resposta rápido: As funções serverless são projetadas para serem executadas rapidamente em resposta a eventos. Isso permite um tempo de resposta mais rápido em comparação com o modelo tradicional de provisionamento de servidores.

  5. Maior produtividade: Com a infraestrutura gerenciada pelo provedor de serviços em nuvem, os desenvolvedores podem se concentrar mais na lógica do aplicativo e na entrega de valor aos usuários finais. Isso aumenta a produtividade e acelera o processo de desenvolvimento.

  - Em resumo, o modelo serverless permite que os desenvolvedores se concentrem na lógica do código, enquanto a infraestrutura é gerenciada automaticamente pelo provedor de serviços em nuvem. Isso oferece escalabilidade, pagamento por uso, gerenciamento simplificado e maior produtividade.
  
  - O modelo serverless pode ser utilizado em uma variedade de casos de uso, incluindo:

  1. Aplicações web: O serverless é adequado para o desenvolvimento de aplicações web que possuem demanda variável e podem enfrentar picos de tráfego. Ele permite que as aplicações sejam dimensionadas automaticamente para lidar com o aumento de usuários e solicitações, sem a necessidade de gerenciar manualmente a infraestrutura.

  2. Processamento de eventos em tempo real: O serverless é eficaz para lidar com eventos em tempo real, como processamento de streams de dados, análise de logs, processamento de eventos de IoT (Internet das Coisas) e notificações em tempo real. As funções serverless podem ser acionadas por esses eventos e executar as ações necessárias de forma rápida e escalável.

  3. APIs e serviços back-end: O modelo serverless é frequentemente usado para desenvolver APIs e serviços back-end, onde as funções serverless podem ser acionadas por solicitações HTTP. Isso permite criar facilmente serviços de API escaláveis, sem a necessidade de gerenciar servidores ou preocupar-se com a infraestrutura subjacente.

  4. Tarefas agendadas: O serverless também pode ser aplicado em tarefas agendadas, como processamento em lotes, geração de relatórios programados, atualização de caches e outras tarefas recorrentes. As funções serverless podem ser programadas para serem executadas em intervalos específicos ou em determinados momentos, automatizando essas tarefas sem a necessidade de manter servidores em execução o tempo todo.

  5. Processamento de imagens e vídeos: O serverless é útil para processamento de mídia, como redimensionamento de imagens, transcodificação de vídeos, reconhecimento de imagens e processamento de vídeo em tempo real. As funções serverless podem ser acionadas por eventos de upload de arquivos e realizar o processamento necessário sem a necessidade de infraestrutura dedicada.

  - Esses são apenas alguns exemplos de casos de uso em que o modelo serverless pode ser aplicado. Sua flexibilidade e escalabilidade tornam-no uma opção atraente para uma ampla gama de aplicações e serviços.
  
  - https://www.redhat.com/en/topics/cloud-native-apps/what-is-serverless
  
</details>

<details>
  <summary>idempotency</summary>

  - Idempotência é um conceito importante em computação e se refere à propriedade de uma operação ou função que, quando aplicada várias vezes, produz o mesmo resultado do que quando aplicada uma única vez. Em outras palavras, realizar a mesma operação múltiplas vezes não tem efeito adicional além do efeito da primeira execução.

  - Para uma operação ser idempotente, ela deve satisfazer duas condições:

  1. O resultado da operação deve ser o mesmo, independentemente do número de vezes que a operação é executada.
  
  2. A execução repetida da operação não deve ter efeitos colaterais indesejados além da primeira execução.
   
  - A idempotência é especialmente importante em sistemas distribuídos e em comunicações de rede, onde mensagens podem ser perdidas, duplicadas ou entregues fora de ordem. Ao projetar sistemas ou APIs, a idempotência é uma propriedade desejável para evitar resultados inesperados ou indesejados.

  - Alguns exemplos de operações idempotentes incluem:

  1. Ler um arquivo: A leitura de um arquivo é uma operação idempotente, pois a mesma leitura do arquivo produzirá sempre o mesmo conteúdo, independentemente de quantas vezes seja realizada.

  2. Excluir um recurso: A exclusão de um recurso, como um registro em um banco de dados, é uma operação idempotente. Se o recurso já foi excluído, a operação não terá efeito adicional.

  3. Atualizar um recurso com os mesmos valores: Se você atualiza um recurso com os mesmos valores várias vezes, o resultado será o mesmo. Por exemplo, se você atualiza um campo de um registro em um banco de dados com o mesmo valor repetidamente, o resultado será o mesmo e o registro não será alterado além da primeira atualização.

  A idempotência é uma propriedade importante a ser considerada no design de sistemas distribuídos, APIs e operações críticas, pois ajuda a garantir consistência, previsibilidade e segurança nas interações entre componentes ou sistemas.
</details>

<details>
  <summary>webRTC</summary>

  - WebRTC (Web Real-Time Communication) é uma tecnologia de comunicação em tempo real que permite a transmissão de áudio, vídeo e dados diretamente entre navegadores da web, sem a necessidade de plugins ou aplicativos adicionais. É uma API de código aberto que faz parte dos padrões web e é suportada por navegadores modernos, como Chrome, Firefox, Safari e Edge.

  - Aqui estão alguns conceitos e recursos-chave do WebRTC:

  1. Comunicação ponto a ponto: O WebRTC permite a comunicação direta entre dois navegadores da web, estabelecendo uma conexão ponto a ponto (peer-to-peer) sem a necessidade de servidores intermediários. Isso permite a transmissão de áudio, vídeo e dados em tempo real entre os participantes.

  2. Acesso a dispositivos: O WebRTC oferece acesso aos dispositivos de áudio e vídeo do usuário, como microfone e câmera, diretamente pelo navegador. Isso permite que os aplicativos web utilizem esses dispositivos para capturar e transmitir áudio e vídeo em tempo real.

  3. NAT traversal: O WebRTC incorpora técnicas de Network Address Translation (NAT) traversal para superar os desafios de estabelecer conexões ponto a ponto através de roteadores e firewalls. Ele utiliza protocolos como ICE (Interactive Connectivity Establishment) e STUN (Session Traversal Utilities for NAT) para descobrir e estabelecer a melhor rota de comunicação entre os participantes.

  4. Compartilhamento de tela: O WebRTC também suporta o compartilhamento de tela, permitindo que os usuários compartilhem suas telas com outros participantes em uma chamada ou sessão. Isso é útil em cenários de colaboração, apresentações e suporte remoto.

  5. Segurança: O WebRTC possui recursos de segurança integrados, incluindo criptografia de ponta a ponta para proteger a privacidade e a integridade dos dados transmitidos. Ele utiliza protocolos como DTLS (Datagram Transport Layer Security) para garantir a segurança da comunicação.

  6. APIs e eventos: O WebRTC é acessado por meio de uma API JavaScript, que fornece métodos e eventos para controlar e gerenciar a comunicação em tempo real. Isso inclui funções para estabelecer conexões, transmitir mídia, gerenciar dados e lidar com eventos relacionados à comunicação.

  - O WebRTC é usado em uma variedade de aplicativos e serviços, incluindo videoconferências, chamadas de voz, bate-papo em tempo real, jogos multiplayer e transmissões ao vivo. Ele oferece uma alternativa nativa para a comunicação em tempo real na web, eliminando a necessidade de plugins ou soluções proprietárias.

  - É importante mencionar que o WebRTC funciona melhor em redes com boa largura de banda e latência baixa, pois a qualidade da comunicação depende desses fatores. Além disso, em alguns casos, pode ser necessário utilizar servidores de sinalização para ajudar na inicialização e coordenação das conexões entre os navegadores.

  - O WebRTC pode ser usado em aplicativos móveis, incluindo aplicativos de mensagens como o WhatsApp. O WebRTC é suportado pelos principais sistemas operacionais móveis, como Android e iOS, por meio de seus respectivos navegadores embutidos.

  - No caso do WhatsApp, ele utiliza o WebRTC para fornecer chamadas de voz e vídeo em tempo real entre os usuários. Quando você realiza uma chamada no WhatsApp, a tecnologia subjacente que permite a comunicação em tempo real é o WebRTC. Isso permite que os usuários do WhatsApp façam chamadas de áudio e vídeo diretamente através do aplicativo, sem a necessidade de plugins adicionais.

  - Em aplicativos móveis, o uso do WebRTC é semelhante ao seu uso em navegadores da web. Através da API do WebRTC, os aplicativos móveis podem estabelecer conexões ponto a ponto, transmitir áudio e vídeo em tempo real, compartilhar telas e realizar outras funcionalidades de comunicação em tempo real.

  - Além do WhatsApp, existem muitos outros aplicativos de mensagens e chamadas de voz/vídeo que utilizam o WebRTC em seus aplicativos móveis para fornecer recursos de comunicação em tempo real. Isso inclui aplicativos como o Signal, Facebook Messenger, Google Meet, entre outros.

  - Portanto, o WebRTC é uma tecnologia versátil que pode ser usada tanto em aplicativos web como em aplicativos móveis, permitindo a comunicação em tempo real em diferentes plataformas.

  - https://ably.com/topic/webrtc-vs-websocket

</details>

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
  - [System Design Mock Interview: Design WhatsApp](https://www.youtube.com/watch?v=0iyLURrWIgQ)

### References:

- [miro](https://miro.com/app/board/uXjVORFgFfA=/)
- [architectural katas](https://nealford.com/katas/list.html)
- [system design course](https://github.com/karanpratapsingh/system-design)
- [sytem desgin roadmap](https://roadmap.sh/system-design)