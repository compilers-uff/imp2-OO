# Orientação à objetos em Imp2

Trabalho do curso de compiladores de 2020.2.

## Objetivo 

Dar suporte básico à programação orientada à objetos em Imp2.

## Exemplos de construções OO em Imp2

1. Exemplo de declaração de classe:
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

1. Exemplo de instanciação:
```
var x = new C(2) ;
```

1. Exemplo de herança:
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
var x := new C(2) ;
y := x.mB(z) ;
```
