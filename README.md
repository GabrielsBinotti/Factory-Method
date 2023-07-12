# Factory-Method
Tem como objetivo encapsular a criação e os objetos de um sistema. Temos uma interface que define um "contrato" para os objetos a serem criados e tambem temos uma interface que define como as classes deverão ser construidas.

Na interface temos apenas a definição de métodos abstratos, sem qualquer definição de código dentro. Quando uma classe implementa uma interface, ela obrigatoriamente deve escrever os métodos abstratos, porém cada classe pode definir o comportamento para esse método, contanto que obedeça à assinatura definida na interface.

## Elementos que compõem o Factory Method ##
**Product** (produto abstrato): define uma interface de objetos que será criado pelo nosso método-fábrica que estará no Concrete Creator.

**Concrete Product** (produto concreto): é o produto final que será criado pelas fábricas.

**Creator** (criador abstrato): interface que define o contrato.

**Concrete Creator** (criador concreto): classe que implementa a interface creator, ela é a fabrica de objetos.

### Exemplo de uso: ###

```
interface CarroProduct
{
  public function acelerar(): void;
  public function frear(): void;
  public function trocarMarcha(): void;
}
```

A interface **CarroProduct** serve como contrato, possuindo os metodos que devem ser escritos obrigatoriamente quando a interface for implementada. São os métodos em comum das classes. Agora iremos criar as classes de produtos concretos.
```
class Fox implements CarroProduct
{

  public function acelerar(): void
  {
    echo "Acelerando Fox\n";
  }

  public function frear(): void
  {
    echo "Freando Fox\n";
  }

  public function trocarMarcha(): void
  {
    echo "Trocando marcha do Fox\n";
  }

}

class Gol implements CarroProduct
{

  public function acelerar():	void
  {
    echo "Acelerando Gol\n";
  }

  public function frear(): void
  {
    echo "Freando	Gol\n";
  }

  public function trocarMarcha(): void
  {
    echo "Trocando marcha do Gol\n";
  }

}

```
Assim não teriamos problemas caso precisassemos futuramente substituir um modelo por outro. Note que cada metodo foi implementado à sua maneira e cada um exibe uma mensagem diferente.
```
use FactoryMethod\Product\CarroProduct;
interface CarroFactory
{
  public function	criarCarro(string	$modeloCarro):	CarroProduct;
}
```
A interface **CarroFactory** usa a CarroProduct pelo bloco de código **use FactoryMethod\Product\CarroProduct;**. Onde é definido apenas um único método que recebe uma string por parametro que representa o modelo a ser criado. Tambem é definido o tipo de retorno que será um CarroProduct, garantindo assim a compatibilidade de nossas fábricas.
```
use FactoryMethod\Product\{
  CarroProduct,	Fox,	Gol
};
class VolkswagenFactory implements CarroFactory
{
  public function criarCarro(string $modeloCarro): CarroProduct
  {
    if ($modeloCarro	==	'Fox')	{
      return new Fox();
    }	elseif ($modeloCarro == 'Gol')	{
      return new Gol();
    }	else {
      throw new \Exception("Modelo de carro \"{$modeloCarro}\" não existe no sistema.");
    }
  }
}
```
Agora foi criado toda a logica de criação de modelos de carro da volkswagen.

Modo de usar:
```
$volskFactory	= new \FactoryMethod\VolkswagenFactory();
$FoxModel	= $volskFactory->criarCarro('Fox');
$GolModel	= $volskFactory->criarCarro('Gol');

echo $teslaModeloS->acelerar();
echo $teslaModeloS->frear();
echo $teslaModeloS->trocarMarcha();

```
