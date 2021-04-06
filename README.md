# Orientação à objetos em Imp2

Trabalho do curso de compiladores de 2020.2.

## Objetivo 

Dar suporte básico à programação orientada à objetos em Imp2.

## Exemplos das construções OO em Imp2

1. Exemplo de declaração de classe. Neste exemplo a classe `C` é declarada com 
   o atributo `x` e dois métodos: um construtor (obrigatório) que deve ter o mesmo 
   nome da classe e o método `m` que recebe um parâmetro.  
   ```python
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
1. Exemplo de instanciação. A expressão `new` recebe uma outra expressão por parâmetro 
   que deve ser composta por um identificador que dá nome a uma classe e uma lista de 
   parâmetros atuais, que serão passados ao construtor da classe dada.
   ```python
   var x = new C(2) ;
   ```     
1. Exemplo de herança. Ao declararmos uma classe podemos dizer que ela herda atributos e 
   métodos de (uma única) outra classe, como na declaração da classe `C` abaixo, que herda 
   (todos) os atributos e métodos da classe `O`.
   ```python
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
1. Exemplo de sobrecarga de operadores (operator overloading, ou _ad hoc_ polimorfism). 
   Um nome de método pode ser sobrecarregado, isto é, declarado em diferentes classes. 
   No entanto, se as classes que declaram o operador polimórfico estiverem na mesms hierarquia, 
   o operador deve possuir um número diferente de parâmetros em cada declaração.  
   ```python
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

## &Pi; denotações, informalmente

- Declaração `class`.
  Uma declaração de classe deve associar ao identificador da classe uma _closure_, no ambiente,
  denotando o corpo da classe. 
  - Declaração de herança.
    Quando uma classe herdar de outra, esta informação deve ficar registrada no ambiente também, associada a classe herdeira. 
  - Uma declaração de classe deve então ser entendida como um binding do identificador da classe à um par com a primeira projeção 
    sendo a _closure_ que denota o corpo da classe e a segunda projeção contém o identificador da classe base. 
- Comando `return`. O comando `return` deve ser sempre o último comando de um bloco. 
  Recebe uma expressão como parâmetro. Sua execução deixa na pilha de valores o resultado da avaliação da expressão em seu argumento. 
  Note que esta é uma semântica simplificada do comando `return` pois não há desvio do fluxo de controle, como ocorre usualmente nas linguagens de programação.
- Expressão `new`. A expressão `new` só pode ser utilizada do lado direito de uma declaração. É parametrizada por um identificador ou 
  um identificador seguido de uma lista de expressões. Tem como semântica a criação de um binding entre o identificador do lado esquerdo 
  e uma **cópia** da _closure_ que denota a classe sendo instanciada, após a execução do construtor. 
- Expressão `self`. Os atributos de uma classe devem coexistir com variáveis no ambiente global e local. A expressão `self` serve 
  para resolver um eventual conflito de nomes. 
- Comando para chamada de método. Uma chamada de método deve ser entendida como uma chamada de função no contexto da closure que 
  define o objeto, estendendo o contexto apropriado. 

## Entregáveis

1. Implementação da gramática de Imp2 estendida com as construções descritas neste trabalho. (Arquivo `imp2.ebnf`.) 
1. Especificação das &Pi; denotações. (Slide 12 dos slides sobre o &Pi; framework. https://github.com/ChristianoBraga/PiFramework/blob/master/slides/cc/slides.pdf)
1. Implementação das &Pi; denotações. (Arquivo `impiler.py`.)
1. Implementação do comando `return`. (Arquivo `pi.py`.)

## Implementação

A menos do comando `return`, que deve estender &Pi; IR como uma nova construção `Ret` e o &Pi; autômato para comandos, 
todo o restante deve ser implementado como &Pi; denotações, isto é, um mapeamento entre a sintaxe da Imp2 e &Pi; IR.

1. Implementação das &Pi; denotações. (Arquivo `impiler.py`.)
