# Orientação à objetos em Imp2

Trabalho do curso de compiladores de 2020.2.

## Objetivo 

Dar suporte básico à programação orientada à objetos em Imp2.

## Exemplos de construções OO em Imp2

1. Exemplo de declaração de classe. Neste exemplo a classe `C` é declarada com o atributo `x` e dois métodos: um construtor (obrigatório) que deve ter o mesmo nome da classe e o método m que recebe um parâmetro.
```
class C {
  var x = 0 ;
  def C(a) {
    self.x := a ;
  }
  def m(a) {
    self.x := a ;
  }
}
```
1. Exemplo de instanciação. A expressão `new` recebe uma outra expressão por parâmetro que deve ser composta por um identificador que dá nome a uma classe e uma lista de parâmetros atuais, que serão passados ao construtor da classe dada.
```
var x = new C(2) ;
```
1. Exemplo de herança. Ao declararmos uma classe podemos dizer que ela herda atributos e métodos de (uma única) outra classe, como na declaração da classe `C` abaixo, que herda (todos) os atributos e métodos da classe `O`.
```
class O {
  var k = 0 ;
  const pi = 3.1416 ;
  def mB(x) {
    self.k := self.pi + x;
    return self.k ;
  }
}
class C(O){
  # ...
}  

# ...
var y = 0 ;
var x = new C(2) ;
y := x.mB(z) ;
```
1. Exemplo de sobrecarga de operadores (operator overloading, ou _ad hoc_ polimorfism). Um nome de método pode ser sobrecarregado, isto é, declarado em diferentes classes. No entanto, se as classes que declaram o operador polimórfico estiverem na mesms hierarquia, 
o operador deve possuir um número diferente de parâmetros em cada declaração.  
```
class O {
  # ...
  def m(x) {
    # ...
  }
}
class C(O) {
  def m(x, y) {
   # ...
  }
}

var o = new C(2) ;
o.m(0) ; # Chamada ao método m da classe O.
o.m(0,1) ; # Chamada ao método m da classe C.
```

## Pi denotações

- Declaração `class`.
  Uma declaração de classe deve associar ao identificador da classe uma _closure_, no ambiente,
  denotando o corpo da classe. 
  - Declaração de herança.
    Quando uma classe herdar de outra, esta informação deve ficar registrada no ambiente também, associada a classe herdeira. 
   
- Uma declaração deve ser entendida como um binding do identificador da classe à um par com a primeira projeção 
    sendo a _closure_ que denota o corpo da classe e a segunda projeção contém o identificador da classe base. 
- Comando `return`
- Expressão `new`
- Expressão `self`
- Comando para chamada de método
