# Practical Object-Oriented Design in Ruby by Sandi Metz

## Chapter 2 - Designing Classes with a Single Responsibility

A fundação da orientação a objeto é a **menssagem**, mas a mais visivel estrutura organizacional é a **classe**. A organização do código serve para que seja possível modificar a classe sem muitos problemas.

O código precisa seguir as seguintes qualidades (TRUE):

  - **Transparent:** As consequências de mudar o código devem ser óbvias e a intenção do código deve ser clara.
  - **Reasonable:** O custo de implementar uma mudança deve ser proporcional ao benefício que ela traz.
  - **Usable:** O código deve ser utilizável em novas situações.
  - **Exemplary:** O código deve encorajar aqueles que o modificam a perpetuar essas qualidades.

Uma classe deve ter uma única responsabilidade, ou seja, ela deve ter apenas um motivo para mudar. Se uma classe tiver mais de uma responsabilidade, ela terá mais de um motivo para mudar. Isso significa que ela terá mais de um motivo para ser alterada.

### Example Application: Bicycles and Gears

```ruby
class Gear
  attr_reader :chainring, :cog

  def initialize(chainring, cog)
      @chainring = chainring
      @cog       = cog
    end

    def ratio
      chainring / cog.to_f
    end
  end
end

puts Gear.new(52, 11).ratio # => 4.7272727272727275
puts Gear.new(30, 27).ratio # => 1.1111111111111112
```

Gear é uma classe que calcula a proporção entre a coroa e o pinhão. Ela tem apenas um motivo para mudar: se a forma de calcular a proporção mudar. Gear é a subclasse de Object, que é a classe base de todas as classes Ruby. Object é uma classe que tem muitas responsabilidades, mas Gear não herda essas responsabilidades.

Caso eu quiser levar em conta o tamanho da roda para o cálculo da proporção, eu posso adicionar um método na classe Gear:

```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog       = cog
    @rim       = rim
    @tire      = tire
  end

  def ration
    chainring / cog.to_f
  end

  def gear_inches
    # tire goes around rim twice for diameter
    ratio * (rim + (tire * 2))
  end
end

puts Gear.new(52, 11, 26, 1.5).gear_inches # => 137.0909090909091
puts Gear.new(52, 11, 24, 1.25).gear_inches # => 125.27272727272728
puts Gear.new(52, 11).ratio # => ArgumentError: wrong number of arguments (given 2, expected 4)
```
O bug acima acontece porque o método initialize espera 4 argumentos, mas eu só passei 2. Isso acontece porque eu adicionei mais uma responsabilidade para a classe Gear, que é a de calcular o tamanho da roda.

### Why Single Responsibility Matters

A classe Gear tem duas responsabilidades: calcular a proporção e calcular o tamanho da roda. Se eu quiser mudar a forma de calcular a proporção, eu vou ter que mudar a classe Gear. Se eu quiser mudar a forma de calcular o tamanho da roda, eu vou ter que mudar a classe Gear. Isso significa que a classe Gear tem dois motivos para mudar.

Uma classe com mais de uma responsabilidade é difícil de reutilizar. Se as responsabilidades são muito acopladas você não consegue reutilizar uma sem a outra. Com isso você teria que duplicar o código para reutilizar apenas uma das responsabilidades. Duplicar código pode aumentar as chances de gerar bugs.

### Determining if a Class has a Single Responsibility

Como saber se uma classe tem uma única responsabilidade? Para isso você pode fazer as seguintes perguntas:

  - O que a classe faz?
  - O que a classe sabe?
  - Com quem a classe conversa?
  - É possível mudar a classe sem afetar outras partes do sistema?

Para exemplificar, no caso anterior podemos fazer as seguintes perguntas:

  - Por favor Gear, qual é sua proporção?
  - Por favor Gear, quais são as polegadas do seu equipamento?
  - Por favor Gear, qual é o tamanho da roda? - Não faz sentido perguntar isso para Gear, porque Gear ele não deveria saber o tamanho da roda.

Uma classe deve ser fácil de descrever. Se você consegue descrever uma classe em uma sentença, quer dizer que ela tem uma responsabilidade única.

**Nota Pessoal:**
> Uma outra forma de você forçar uma classe a ter uma única responsabilidade é você criar uma classe que tenha apenas um método. No Caso, em vez de eu chamar a classe de Gear, eu poderia chamar de GearInches.

### Determining When to Make Design Decisions

É comum estar em uma situação onde você não sabe o que é certa a fazer com uma classe. Não tem certeza se a classe está com a responsabilidade certa, ou se ela está com várias responsabilidades e o projeto é pequeno, muitas vezes você não sabe do futuro e é difícil tomar uma decisão hoje. Infelizmente em casos que muitas coisas podem acontecer, o melhor é você não perder muito tempo escolhendo, já que você pode tomar uma decisão errada pelas incertezas.

Não se sinta coagido em tomar uma decisão prematura, muitas vezes resistir é o melhor caminho. Mas lembre que decisões tomadas podem ter implecações futuras, já que o código que foi colocado anteriormente pode servir de base para outras decisões. Já que outras pessoas podem não saber que você preferiu não tomar uma abordagem com um designer melhor.

**Nota Pessoal:**
> Uma forma de você minimizar o impacto da sua decisão é deixar de forma explícita o motivo de seguir com aquela abordagem, deixando comentário com data no código. Não vejo como uma prática ruim, comunicação é importante.

### Writing Code That Embraces Change

É possível deixar o código de um jeito que seja fácil mudar **Gear**, mesmo você não sabendo como serão as mudanças futuras.

#### Depend on Behavior, Not Data

Comportamento é capturado nos métodos e invocados pelas mensagens. A frase "Don't Repeat Yourself" (DRY) é baseado nessa ideia. Data pode ser qualquer coisa desde uma simples String até um complexo Hash. Data você pode acessar de duas maneiras, diretamente da variável de instância ou de um método de acesso.

- **Hide instance variables:** Sempre envolva variáveis ​​de instância em métodos de acesso em vez de usar diretamente a variável de instância. Isso permite que você altere a implementação sem alterar a interface pública. Além de você conseguir facilmente identificar quando uma variável está com erro de digitação, já que variáveis de instância sempre vão retornar **nil** caso não existam.

Quando se usa o `attr_reader` está criando um método que encapsula a variável.

```ruby
# default implementation via attr_reader
def cog
  @cog
end
```

This `cog` method é agora o único lugar que entende o que `@cog` significa. Se você quiser mudar a implementação, você pode mudar o método `cog` sem afetar o resto do sistema.

```ruby
# a simple reimplementation of cog
def cog
  @cog * unanticipated_adjustment_factor
end
```

```ruby
# a more complex one
def cog
  @cog * (foo? ? bar_adjustment : baz_adjustment)
end
```

O primeiro exemplo é uma mudança simples, o segundo é uma mudança mais complexa. Mas em ambos os casos, o resto do sistema não precisa saber que a implementação mudou.


#### Hide Data Structures

Se você tem uma coleção de dados, como um Array ou Hash, você pode encapsular a coleção em um objeto. Isso permite que você mude a implementação sem afetar o resto do sistema.

```ruby
class ObscruingReferences
  attr_reader :data

  def initialize(data)
    @data = data
  end

  def diameters
    # 0 is rim, 1 is tire
    data.collect {|cell|
      cell[0] + (cell[1] * 2)}
  end
end
```

```ruby
# rim and tire sizes (now in milimeters!) in a 2d array
@data = [[622, 20], [622, 23], [559, 30], [559, 40]]
```

Caso você mude a estrutura, teria que mudar a implementação do método `diameters`. Mas se você encapsular a coleção em um objeto, você pode mudar a implementação sem afetar o resto do sistema. Este exemplo já é ruim, imagine as consequências se o `data` retornasse um array de hashes que fossem referidos em vários lugares, uma mudança de estrutura poderia cascatiar em vários lugares.

```ruby
class RevealingReferences
  attr_reader :wheels

  def initialize(data)
    @wheels = wheelify(data)
  end

  def diameters
    wheels.collect {|wheel|
      wheel.rim + (wheel.tire * 2)}
  end

  # now everyone can send rim/tire to wheel
  Wheel = Struct.new(:rim, :tire)
  def wheelify(data)
    data.collect { |cell| Wheel.new(cell[0], cell[1]) }
  end
end
```

Essa abordagem é melhor e faz com que `diameters` não se preocupe com a estrutura de `data`, já que esse dado é encapsulado em um objeto. Caso a estrutura mude, você só precisa mudar o método `wheelify`.

**Nota Pessoal:**
> Nesse caso eu passaria o `wheelify` no parâmetro do construtor, para essa classe nem saber o que precisava transformar o dado e botaria um comentário no topo da classe recomendando sempre usar o `wheelify` para transformar o dado.

#### Enforce Single Responsibility Everywhere

Métodos são como classes, eles devem ter uma única responsabilidade. No caso anterior `diameters` faz mais de uma ação, ele percorre o array e calcula o diâmetro. Neste caso você não vai se preocupar com performance, o objetivo é deixar o código mais fácil de mudar.

```ruby
# first - iterate over the array
def diameters
  wheels.collect {|wheel| diameter(wheel)}
end

# second - calculate diameter of ONE wheel
def diameter(wheel)
  wheel.rim + (wheel.tire * 2)
end
```

Neste caso a refatoração não se tornou overdesign, já que o mesmo cálculo já foi usado em outro lugar.

```ruby
def gear_inches
  # tire goes around rim twice for diameter
  ratio * (rim + (tire * 2))
end
```

Claramente o método `gear_inches` está fazendo mais de uma coisa, ele calcula o diâmetro e multiplica pelo `ratio`. Neste caso você pode usar o método `diameter` para deixar o código mais simples.

```ruby
def gear_inches
  ratio * diameter
end

def diameter
  rim + (tire * 2)
end
```

Além de separar as reposabilidades o método ficou mais fácil de ler. Esse problema fez responder que `gear_inches` é uma responsabilidade de `Gear`, mas `diameter` não é. O impacto dessa refatoração é pequeno, mas a acumulação desse efeito no código é gigante. Métodos com responsabilidade única tem os seguintes benefícios:

- **Expose previously hidden qualities:** Refatorar uma classe para ter métodos com responsabilidade única faz com que você entenda melhor a classe e o que ela faz.
- **Avoid the need for comments:** Métodos com responsabilidade única são mais fáceis de ler e entender, não precisando de comentários. Uma documentação bem escrita é melhor que um comentário.
- **Encourage reuse:** Métodos com responsabilidade única são mais fáceis de reutilizar. Dessa forma acaba encorajando a reutilização de código.
- **Are easy to move to another class:** Métodos com responsabilidade única são mais fáceis de mover para outra classe. Dessa forma você pode mover métodos para onde eles pertencem.

**Nota pessoal:**
> Concordo muito com o fato de tentarmos isolar as resposabilidades o máximo possível e tentar deixar o código mais claro, fica muito mais fácil de remover e reutilizar, pra mim por exemplo, toda fórmula deveria ser construída em uma classe de Ruby puro e só ser chamada, se não existe aquele cálculo, vai lá e cria. Uma coisa que não concordo é a interpretação do uso de comentários, em um ambiente real nem todo mundo leu um livro de OOD por exemplo, ou está codando com um prazo apertado, às vezes não tem experiência o suficiente, podem ter diversos motivos para necessitar o uso de comentários, e já vi diversas vezez alguém convencendo todos os outros programadores que é uma prática ruim. Acaba que todos continuam a não fazer documentação, o código permanece ruim e sem a possibilidade de você entender facilmente, comentários são bem vindos sim para sinalizar a intenção por trás daquele código, mas claro, não é pra sair comentando tudo, mas também não é pra sair removendo todos os comentários.

#### Isolate Extra Responsibilities in Classes

Quando você tem um método com mais de uma responsabilidade, você pode isolar as responsabilidades em classes diferentes. Isso é um pouco mais complexo que isolar em métodos, mas o resultado é um código mais fácil de entender e de mudar.

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog       = cog
    @wheel     = Wheel.new(rim, tire)
  end

  def ratio
    chainring / cog.to_f
  end

  def gear_inches
    ratio * wheel.diameter
  end

  Wheel = Struct.new(:rim, :tire) do
    def diameter
      rim + (tire * 2)
    end
  end
end
```

O uso de `Wheel` dentro de `Gear` não é muito comum, pode parecer que necessita extrair essa classe, mas como ela só funciona no contexto de `Gear` no momento, não tem por que fazer essa movimentação. Se você tiver muitas responsabilidades em uma classe, separe-as em classes diferentes. Concentre-se nas responsabilidades da classe principal, não deixe que as responsabilidades secundárias atrapalhem, lembre que outra pessoa vai olhar seu código e pode acrescentar algo se você não deixar claro o que está acontecendo.

**Nota pessoal:**
> No mundo real essa técnica é pouca usada e já vi até ser desencorajada, as pessoas sempre vão reclamar, uma coisa que se pode fazer para diminuir o atrito é explicar o fato de ela não necessitar ser extraída no momento, mas seria interessante já criar o teste de forma separada, uma coisa não depende da outra.

> Não tenha medo de postergar uma decisão, mas também não pode ter medo de modificar uma classe, por isso que é importante deixar suas intenções claras em comentários.

#### Finally, the Real Wheel

Agora é necessário aplicar uma nova funcionalidade em `Wheel`, é necessário fazer o cálculo para saber a circunferência. Com isso faz todo o sentido separar `Wheel` de `Gear`.

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, wheel=nil)
    @chainring = chainring
    @cog = cog
    @wheel = wheel
  end

  def ratio
    chainring / cog.to_f
  end

  def gear_inches
    ratio * wheel.diameter
  end
end

class Wheel
  attr_reader :rim, :tire

  def initialize(rim, tire)
    @rim = rim
    @tire = tire
  end

  def diameter
    rim + (tire * 2)
  end

  def circumference
    diameter * Math::PI
  end
end

@wheel = Wheel.new(26, 1.5)
puts @wheel.circumference # 91.106186954104

puts Gear.new(52, 11, @wheel).gear_inches # 137.090909090909

puts Gear.new(52, 11).ratio # 4.72727272727273
```

As duas classes tem responsabilidades únicas, o código não é perfeito, mas conseguiu chegar a um nível de muito bom.

## Chapter 3 - Managing Dependencies

### Understanding Dependencies

`Um objeto depende de outro se quando um objeto muda, o outro objeto é forçado a mudar também.`

Se você examinar o código antigo de `Gear` e `Wheel`, você vai perceber o uso de várias dependências que não eram necessárias para `Gear` funcionar. Essas dependências tinham efeitos sobre o estilo do código. Estou falando do código abaixo:

```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog       = cog
    @rim       = rim
    @tire      = tire
  end

  def ratio
    chainring / cog.to_f
  end

  def gear_inches
    ratio * Wheel.new(rim, tire).diameter
  end
end

class Wheel
  attr_reader :rim, :tire

  def initialize(rim, tire)
    @rim = rim
    @tire = tire
  end

  def diameter
    rim + (tire * 2)
  end
end

Gear.new(52, 11, 26, 1.5).gear_inches # 137.090909090909
```

#### Recognizing Dependencies

Um objeto depende de outro se ele sabe:
- O nome de outra classe. `Gear` espera uma classe com nome de `Wheel` exista.
- O nome da mensagem que ele pretende enviar para alguém que ele conhece. `Gear` sabe que `Wheel` tem um método chamado `diameter`.
- Os argumentos da mensagem são requeridos. `Gear` sabe que `Wheel.new` requer `rim` e `tire`.
- A ordem dos argumentos. `Gear` sabe a ordem dos argumentos de `Wheel.new`.

Cada uma das dependencias criam uma chance de `Gear` mudar. Se `Wheel` mudar o nome do método `diameter` para `wheel_circumference`, `Gear` vai ter que mudar também. Se `Wheel` mudar a ordem dos argumentos, `Gear` vai ter que mudar também.

Essas dependências desnecessárias deixam o código mais difícil de reusar e qualquer pequena mudança gerar uma cascata de modificações em todo o código.

#### Coupling Between Objects (CBO)

`CBO` é uma medida de quanto uma classe conhece sobre outra classe. Quanto mais uma classe conhece sobre outra, mais elas estão acopladas. `Gear` e `Wheel` estão acopladas, pois `Gear` conhece o nome de `Wheel` e o nome do método `diameter`.

![Acoplamento imagem do livro](images/acoplamento.png)

A ilustração acima demontra o acoplamento entre as classes. Quando um código é escrito pela primeira vez, tudo fica bem, são as interações constantes sem o devido cuidado que fazem o código ficar ruim. As classes que antes eram independentes, começam a ficar acopladas. E o acoplamento gera dificuldade de reutilizar a classe, então em vez de usar uma classe para resolver o problema, você está tendo que levar junto outras classes que não deveriam ser necessárias.

### Writing Loosely Coupled Code

Para diminuir o acoplamento entre as classes, é necessário diminuir a dependência entre elas. Para isso é necessário diminuir o conhecimento que uma classe tem sobre a outra. Reduzir dependências significa reconhecer e remover o que você não precisa.

#### Inject Dependencies

Para diminuir o acoplamento entre `Gear` e `Wheel`, é necessário remover a dependência de `Gear` sobre `Wheel`. Para isso é necessário injetar `Wheel` em `Gear`. Isso ocorre por que `Wheel` pode vir a mudar de nome e `Gear` não precisa lidar com isso, mesmo sendo uma mudança simples de fazer, por isso muitas vezes acabamos não fazendo, mas não é apenas esse o problema `Wheel` não interage com `Gear`, então não faz sentido `Gear` conhecer `Wheel`.

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, wheel)
    @chainring = chainring
    @cog       = cog
    @wheel     = wheel
  end

  def ratio
    chainring / cog.to_f
  end

  def gear_inches
    ratio * wheel.diameter
  end
end

# Gear expects a 'Duck' that knows 'diameter'
Gear.new(52, 11, Wheel.new(26, 1.5)).gear_inches # 137.090909090909
```

Uma grande vantagem dessa pequena modificação é que agora `Gear`, pode colaborar com qualquer método que responda a `diameter`. Essa técnica se chama `Dependency Injection` e é uma das técnicas mais poderosas para escrever código flexível e reutilizável.

#### Isolate Dependencies

Muitas vezes não é possível injetar uma dependência, uma coisa que pote fazer é isolar a dependência. Isolar a criação da dependência é uma alternativa para diminuir o acoplamento entre as classes.

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog       = cog
    @wheel     = Wheel.new(rim, tire)
  end

  def ratio
    chainring / cog.to_f
  end

  def gear_inches
    ratio * wheel.diameter
  end
end
```

```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog       = cog
    @rim       = rim
    @tire      = tire
  end

  def ratio
    chainring / cog.to_f
  end

  def gear_inches
    ratio * wheel.diameter
  end

  def wheel
    @wheel ||= Wheel.new(rim, tire)
  end
end
```

Em ambos os casos `Gear` sabe muito sobre `Wheel`, recebe `rim` e `tire` na sua inicialização, que para a classe `Gear` é inútil, mas foi feito alguma melhoria.

O jeito que voê administra as dependências com nomes de classes externas, tem um profundo efeito na sua aplicação. Se você tem o hábito de injetar dependências, suas classes naturalmente vão perder acoplamento. Se você ignora isso, suas classes vão ficar acopladas e inflexíveis. Um código precisa ser consiso, explícito, isolado e fácil adaptação.

**Nota pessoal:**
> A minha experiência diz que tudo é questão de consistência, então se você desiste de fazer algo por que é difícil fazer no começo, você está desistindo do fato que aquilo vai facilitar no futuro, por que você está treinando para ficar fácil. No começo para mim era muito difícil testar, mas a prática levou a perfeição, não foi fácil, mas hoje é muito fácil e ajuda muito no meu dia a dia.

#### Isolate Vulnerable External Messages

Quando sua classe tem um método complexo demais, é necessário tmabém isolar as mensagens externas. Isolar mensagens externas é uma forma de diminuir o acoplamento entre as classes.

```ruby
def gear_inches
  ratio * wheel.diameter
end
```

```ruby
def gear_inches
  ratio * diameter
end

def diameter
  wheel.diameter
end
```

Essa técnica não é necessária de usar quando o uso dela é isolado e em algum lugar simples, você deve analisar o contexto e ver se vale a pena.

#### Remove Argument-Order Dependencies

Uma preocupação são os argumentos de uma classe, precisar passar os argumentos em uma certa ordem pode gerar dificuldade para mudança depois, já que terá que mudar em todos os lugares que usa aquela classe. Para resolver isso podemos usar no Ruby < 2.1 o Keyword Arguments, que permite passar os argumentos sem ordem, mas no Ruby >= 2.1 já temos o Keyword Arguments nativo.

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring:, cog:, wheel:)
    @chainring = chainring
    @cog       = cog
    @wheel     = wheel
  end

  # ...
end

chainring = 52

Gear.new(
  chainring:,
  cog: 11,
  wheel: Wheel.new(26, 1.5)).gear_inches # 137.090909090909
```

**Nota pessoal:**
> Não uso se tiver apenas um argumento, mais de um normalmente uso. Se o Ruby não estiver na versão correta, pode se usar Hash como argumento, mas não é a mesma coisa. Fica mais fácil de entender o que está acontecendo, e não precisa passar em uma ordem específica.

Caso queira usar com Hash:

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(args)
    @chainring = args[:chainring]
    @cog       = args[:cog]
    @wheel     = args[:wheel]
  end

  # ...
end

Gear.new(
  chainring: 52,
  cog: 11,
  wheel: Wheel.new(26, 1.5)).gear_inches # 137.090909090909
```

Outra vantagem dessa utilização é que a dependência de nomear os argumentos gera um tipo de documentação, em que fica fácil de entender o que está acontecendo, sem precisar abrir a classe.

#### Eplicitly Define Defaults

Quando você precisa definir um valor paadrão para o argumento:

```ruby

class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring:, cog: 10, wheel:)
    @chainring = chainring
    @cog       = cog
    @wheel     = wheel
  end

  # ...
end

class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(args)
    @chainring = args[:chainring] || 40
    @cog       = args[:cog]       || 18
    @wheel     = args[:wheel]
  end

  # ...
end
```

No caso do Hash, ele não vai funcionar se você passar `nil` como argumento, então você pode usar o `fetch`:

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(args)
    @chainring = args.fetch(:chainring, 40)
    @cog       = args.fetch(:cog, 18)
    @wheel     = args[:wheel]
  end

  # ...
end
```

Usando o Hash, você pode ignorar os métodos enviados, como:

```ruby
# specifying defaults by merging a defaults hash
def initialize(args)
  args = defaults.merge(args)
  @chainring = args[:chainring]
  @cog       = args[:cog]
  @wheel     = args[:wheel]
end

def defaults
  {:chainring => 40, :cog => 18}
end
```

#### Isolate Multiparameter Initialization

Algumas vezes não conseguimos controlar o código que estamos usando, às vezes ele pode fazer parte de uma interface externa. Imagina essa interface sendo chamada em várias partes do seu código e algo mudando, você tendo que mudar em todo código, a dor de cabeça seria gigantesca. Nesses casos é necessário isolar a inicialização multiparametro.

```ruby
# When Gear is part of an external interface
module SomeFramework
  class Gear
    attr_reader :chainring, :cog, :wheel
    def initialize(chainring, cog, wheel)
      @chainring = chainring
      @cog       = cog
      @wheel     = wheel
    end
    # ...
  end
end

# wrap the interface to protect yourself from changes
module GearWrapper
  def self.gear(args)
    SomeFramework::Gear.new(args[:chainring],
                            args[:cog],
                            args[:wheel])
  end
end

# Now you can create a new Gear using an arguments hash.
GearWrapper.gear(
  :chainring => 52,
  :cog       => 11,
  :wheel     => Wheel.new(26, 1.5)).gear_inches # 137.090909090909
```

Tem duas coisas que são necessárias serem olhadas nesse código. A primeira é que não usamos uma `class` e sim um `module`, então você não vai precisar ficar instânciando essa classe em todo lugar. A outra coisa interessante é o uso de `Factories`, que é uma forma de encapsular a criação de um objeto. O uso de `Factories` é uma forma de diminuir o acoplamento entre as classes.

### Managing Dependency Direction

A escolha da direção da dependência pode causar um grande impacto no seu código. Se você não tomar cuidado, você pode acabar com um código que é difícil de mudar.

## Chapter 4 - Creating Flexible Interfaces

Interface é uma parte visível de uma classe e usada para expor as funcionalidades. Pense em uma cozinha de restaurante, a interface é o cardápio, que é a única coisa que o cliente precisa saber. O cliente não precisa saber como a comida é feita, ele só precisa saber o que ele pode pedir. A classe cozinha tem uma responsabilidade única, que é entregar os pratos que estão no cardápio, mas implementa muitos métodos dentro da cozinha, por que ela tem toda uma dinâmica para saber como os pratos são feitos.

**Nota pessoal:**
> Essa analogia do menu é excelente para falar em interface e para pensar no geral o que é Single Responsability. Ter responsabilidade única é diferente de ter apenas um método, é ter uma responsabilidade única, que pode ser implementada em vários métodos.

### Public Interfaces

Os métodos que compoem uma interface pública, tem as seguintes características:

- Revelam a responsabilidade principal da classe.
- São esperados para serem invocados por outros objetos/classes.
- Não são vulneráveis a mudanças.
- São seguros para serem reutilizados em outro contexto.
- São documentados e testados.

Encontrar as Interfaces Públicas é um desafio que vai ficando mais fácil com o tempo. Uma forma de encontrar é olhar os testes, eles vão te mostrar o que é esperado que a classe faça. Outra forma é olhar o código e ver o que é usado em outros lugares.

### Private Interfaces

Todos os outros métodos da classes são os privados:

- Lidam com detalhes de implementação.
- Não são esperados para serem invocados por outros objetos/classes.
- Podem mudar por qualquer motivo.
- Não são seguros para quem depende deles.
- Não são referidos nos testes.

### An Example Application: Bicycle Touring Company

FastFeet, Inc., é uma empresa de turismo com bicicleta, o negócio funciona no papel e caneta. Os passeios podem ser de Mountain Bike ou de ciclismo de estrada, as rotas são pensadas refletindo a dificuldade técnica com seus participantes. Os participantes podem usar suas próprias bicicletas ou contratar da FastFeet, a FastFeet oferece o passeio com guia e carro de apoio com mecânico. As bicicletas alugadas podem ter vários tamanhos e modelos.

**Nota pessoal:**
> Eu conversaria primeiro com as pessoas que fazem o software para tentar entender como agir em cima do Domínio, para poder consolidar a Linguagem Ubíqua, que é a linguagem que todos entendem. A partir disso, partiria para estruturar tudo.

### Create Explicit Interfaces

O seu objetivo é criar uma interface que funcione agora, que seja fácil de reusar e se adapte em um inexperado uso no futuro. Outras pessoas irão invocar seus métodos, é sua obrigação comunicar quais são dependentes.

Toda vez que criar uma classe, declare sua interfaces. Os métodos que estão `public` devem ter:

- Seja explícito
- Seja mais sobre `o que` do que `como`
- Tenha nomes que, até onde você possa prever, não mudarão
- Sempre que possível use keywords arguments

### Public, Protected, and Private Keywords

`Public` é o padrão, então não precisa declarar. `Protected` é usado para métodos que são usados apenas dentro da classe e suas subclasses. `Private` é usado para métodos que são usados apenas dentro da classe.

Tenha cuidado com os métodos privados, não deixe eles virarem uma dependência perigosa.

## The Law of Demeter

LoD é um grupo de regras que resulta em perder acoplamento nos objetos. Fraco acoplamento é quase sempre uma virtude, mas é apenas um componente do design
e deve ser equilibrado com necessidades concorrentes.

### Defining Demeter

Demeter restringe o grupo de objetos no qual um método deveria enviar mensagens. Proíbe
rotear uma mensagem para um terceiro objeto através de um segundo objeto de um tipo diferente. Demeter é parafrazeado como "só fale com seus amigos imediatos", ou "use apenas um ponto". Exemplo:

```ruby
customer.bicycle.wheel.tire
customer.bicycle.wheel.rotate
hash.keys.sort.join(', ') # is ok because has the same object
```

Cada linha é uma mensagem encadeada por um número de pontos. Esse encadeamento é conhecido por `train wrecks`, cada nome de método representa um carro de trem e os pontos são as conexões. Esse trem é a indicação que você está violando Demeter.

Uma forma de esconder um `train wrecks` é o uso do `delegate`, que é uma mensagem sendo passada por outro objeto, via a `wrapper method`. Um `wrapper method` encapsula, um conhecimento que de outra forma seria incorporado na cadeia de mensagens. Delegar para esconder forte acoplamento não é o mesmo que desacoplar código.

O problema de ter `chain methods` é que uma classe além que só queria se preocupar com o `rotate` por exemplo, está passando por diferentes métodos até chegar ao que ela realmente precisa.

**Summary:**
> Aplicações orientadas a objetos são definidas pelas mensagens que passam entre objetos.Essa passagem de mensagens ocorre em interfaces “públicas”. Public interfaces bem definidas, que consistem em métodos estáveis ​​que expõem as responsabilidades de suas classes e fornecer o máximo benefício a um custo mínimo. Focar nas mensagens revela objetos que, de outra forma, poderiam passar despercebidos. Quando as mensagens são confiáveis ​​​​e perguntam o que o remetente deseja em vez de dizer ao destinatário como se comportar, os objetos evoluem naturalmente em interfaces públicas que são flexíveis e reutilizáveis de maneiras novas e inesperadas.

## Chapter 5 - Reducing Costs with Duck Typing

Duck types são interfaces pública que não são vinculadas a uma classe específica, mas sim a um comportamento. Elas tem uma enorme flexibilidade para sua aplicação, removendo o custo de dependências na classe.

Polimorfismo é a habilidade de de diferentes objetos responderem a mesma classe.
