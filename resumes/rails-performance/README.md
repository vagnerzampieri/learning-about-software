# The Complete Guide to Rails Performance by Nate Berkopec

A primeira coisa que penso sobre performance é, analise o seu problema e tente extrair o máximo das ferramentas que você tem utilizado no sistema para resolvê-lo.

Nem todo problema vai ser resolvido com performance, todo tem um limite que é possível chegar, talvez seja interessante descobrir primeiro os limites do seu problema, outra coisa importante sobre performance é ter ideias de custos, existem soluções no qual o custo não compensaria para sua empresa. Saber economizar dinheiro é algo que precisa colocar na balança.

Imagina se você for reescrever cada aplicação que você já deu manutenção por que alguém disse que a linguagem X é mais performática que a linguagem Y, você vai acabar perdendo muito tempo e dinheiro.

Lembre sempre do `The Pareto Principle`, 80% dos problemas são resolvidos com 20% do esforço, então foque no que é mais importante. É por isso que otimização prematura é tão ruim, monitorar a performance, profile e benchmark são muito importantes.

`Não otimize prematuramente nada na minha aplicação até as minhas métricas me dizerem que eu preciso otimizar.`

É preciso ter cuidado ao fazer becnhmark, por que colocar para "competir" duas coisas completamentes diferentes não faz sentido, por exemplo, comparar `Rails` e `Sinatra` não é justo, já que o `Rails` é um framework e é extremamente completo, principalmente quando falamos de verificações de segurança, coisas que o `Sinatra` não tem. Por isso além de se fazer `Benchmark` é necessário fazer `Profiling`.

O `Profiling` serve para descobrir por que um software ou subsistema funciona dessa maneira. Com isso, conseguimos ter a visão total do software e descobrir o que está acontecendo e onde.

Por isso que só fazer o `Benchmark` não é suficiente, você pode estar olhando para uma parte do código muito pequena, e precisa olhar esse código de forma mais global dentro de uma funcionalidade.

**Nate** explica um caso que aconteceu com ele, relacionado ao `minitest`, ele viu o código abaixo:

```ruby
def self.runnable_methods
  methods = methods_matching(/^test_/)

  case self.test_order
  when :random, :parallel then
    max = methods.size
    methods.sort.sort_by { rand max }
  when :alpha, :sorted then
    methods.sort
  else
    raise "Unknown test_order: # {self.test_order.inspect}"
  end
end
```

Ele achava que a parte relacionada ao ` methods.sort.sort_by { rand max }` não fazia muito sentido, que seria mais rápido usando `methods.shuffle`, mas ele estava errado, o `shuffle` é mais lento que o `sort_by`, e ele só descobriu isso por que ele fez o `Profiling` do código.

De forma isolada o código era mais rápido, mas ao colocar juntos com outras funcionalidade. e dessa forma fazendo um teste mais justo, se mostrou mais rápido.

Para ele testar de fato, uso o `time` do linux e não uma gem de como o `benchmark/ips`.

```bash
time for i in {1..10}; do bundle exec rake; done

...
real 15m59.384s
user 11m39.10
sys 1m15.767s
```

`Real` da o tempo total gasto na tarefa rodando, o `sys` é o tempo gasto no kernel e o `user` é o tempo gasto com o Ruby. Quando ele fez a modificação para tentar melhorar o código usando o `shuffle` o tempo foi `11m56s`, muito acima do anterior.

Isso quer dizer que mesmo o código tendo ficado mais rápido no cenário isolado, outras coisas podem ter influenciado no tempo a favor do código que por teoria seria mais lento. Mas o mais importante é que a diferença que estava causando não importa, por que era insignificante o impacto que teria no sistema.

Isso só mostra que `microbenchmarks e comparações relativas` podem trazer mal comprendimento sobre o que está acontecendo no sistema.

**Nota pessoal:**
> Igual quando você vai acompanhar um Dashboard do que está acontecendo no sistema, se você ficar olhando apenas para um momento curto da história do sistema, não vai conseguir olhar para tudo que vem acontecendo ao longo do tempo.

A otimização prematura é ignorar essas lições e otimizar “quando temos vontade”, ou otimizando constantemente o tempo todo. É uma perda de tempo garantida.

## The Business Case for Performance

Muitas vezes temos aplicações que tem toneladas de informações na tela sendo carregadas que deixam o sistema mais lento, ou que carregam dados sem serem usados, ou fazem métricas de tudo sem estarem usando, isso acaba gerando problemas de lentidão. E normalmente essas coisas são pedidas por outros departamentos.

> Os empresários, cara, eles só entendem de números. Se você pode justificar isso com números, eles farão o que você mandar
eles.

## The Case for Performance

Um grande problema que temos é não quantificar e explicar os custos do sacrifício da performance para o `business`. Muito da performance em um site começa a ficar ruim quando outras áreas pedem para adicionarmos algum script no site para que eles tenham mains informações do usuário, em vez de avaliarmos essa adição de forma mais crítica, acabamos aceitando e colocando no site, sem pensar no impacto que isso pode causar.

E na realidade deveríamos aceitar fazer o teste, mensurar e verificar o impacto que isso pode causar. Temos que ter uma estimativa de quanto nossas views podem demorar, ou o tamanho delas e o quanto colocar esse script pode ser prejudicial se ele extrapolar muito o tamanho da view. Temos sempre que pensar em números e trazer as respostas para a mesa baseado em números.

O time técnico e de produto sempre precisam se alinhar na questão dos objetivos de performance. Um site que tem estudos relacionados a performance é o [WPO Stats](https://wpostats.com/).

## Slowdowns are Outages

Para entender como um website performa links para dólares, vamos pensar como websites slowdowns são como um downtime.

Downtime é algo ruim e companias estão sempre evitar isso, mas ter um slowdown é a mesma coisa e ainda não aparece na maioria dos dashboards de monitoramento.

Por exemplo, se você tiver um serviço externo que demora alguns segundos para responder, como uma fonte externa, o cliente vai estar esperando a fonte carregar, para o cliente a sensação é a mesma que um site tiver caído.

## Longer Load Times are an Expense

Vários estudos relacionam o tempo de carregamento de um site com a taxa de conversão, quanto mais rápido o site carregar, mais conversões ele vai ter. Foi verificado que 100ms de melhoria pode aumentar entre 0.2-1% a taxa de conversão, dependendo do tamanho da empresa.

## Longer Load Times Turn Away Customers

Nem todas os tipos de empresas necessitam de conversão, empresas com `ad-focused business` precisam de pageviews, com a diminuição do tempo de carregamento, mais pageviews eles vão ter.

## Mobile and Global Users are Hardest-Hit

