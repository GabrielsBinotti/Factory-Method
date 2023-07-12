# Factory-Method
Tem como objetivo encapsular a criação e os objetos de um sistema. Temos uma interface que define um "contrato" para os objetos a serem criados e tambem temos uma interface que define como as classes deverão ser construidas.

Na interface temos apenas a definição de métodos abstratos, sem qualquer definição de código dentro. Quando uma classe implementa uma interface, ela obrigatoriamente deve escrever os métodos abstratos, porém cada classe pode definir o comportamento para esse método, contanto que obedeça à assinatura definida na interface.

## Elementos que compõem o Factory Method ##
**Product** (produto abstrato): define uma interface de objetos que será criado pelo nosso método-fábrica que estará no Concrete Creator.

**Concrete Product** (produto concreto): é o produto final que será criado pelas fábricas.

**Creator** (criador abstrato): interface que define o contrato.

**Concrete Creator** (criador concreto): classe que implementa a interface creator, ela é a fabrica de objetos.

Exemplo de uso:
