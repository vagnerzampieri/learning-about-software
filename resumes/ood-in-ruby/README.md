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




