# Network Lists

Network Lists é o recurso da plataforma da Azion que permite a implementação e o gerenciamento de *whitelists*, *blacklists* ou mesmo *greylists* baseadas na rede ou localização do usuário. Com ele é possível prevenir diversos tipos de ataques a sua rede, até mesmo impedir que usuários com comportamentos maliciosos ten
ham acesso à suas aplicações.

Através de regras de restrições por IPs, ASN ou por *geolocation*. As Network Lists são utilizadas nas regras de negócio do **Rules Engine** do **Edge Firewall**, mitigando riscos de segurança e otimizando a performance de seus recursos.

~~~
Atenção: Para utilizar o recurso de Network Lists é necessário habilitar o módulo Network Layer Protection.
~~~

> 1. *[Como funciona?](#como-funciona)*
> 2. *[Hands-On](#hands-on)*
> 3. *[Documentação de Suporte](#documentacao-de-suporte)*

---

## 1. Como funciona? {#como-funciona}

O funcionamento de uma ***Network List*** é muito simples. Primeiro, é necessário criar uma lista dos itens que se deseja filtrar. Depois de criadas, as listas podem ser aplicadas na implementação de regras do Edge Firewall Rule Set, na aba ***Rules Engine***. Assim, toda vez que uma requisição satisfazer os ***Criterias*** da respectiva ***Rule***, o respectivo ***Behavior*** associada será utilizado. Por exemplo, sua equipe de segurança detectou, através dos logs da Azion, que o IP **XXX.XYZ.XXX.XY** está tentando realizar um ataque de ***SQL Injection*** na sua aplicação. Você então cria uma ***Network List*** e inclui o IP identificado. Depois, cria uma ***Rule Engine*** para filtrar o comportamento indesejado e associa a lista com os IPs que devem ser barrados. Na próxima requisição efetuada, ***Edge Firewall*** da Azion vai executar a regra definida e bloquear a requisição antes mesmo que ela possa chegar na sua infraestrutura. Você também poderá facilmente gerenciar Network Lists, incluindo ou removendo itens conforme sua necessidade via **API**.

Para proporcionar ainda mais agilidade aos seus processos, a Azion provê e mantém algumas Network Lists que qualquer cliente pode utilizar. Uma delas é a *Network List* ***Azion IP Tor Exit Nodes***, que contém os endereços IP de saídas da rede ***Tor*** e poderá ser utilizada em uma ou mais Rules de acordo com suas necessidades de negócio.

~~~
O conteúdo das Network Lists providas pela Azion não pode ser editado.
~~~

---

## 2. Hands On: Passo a Passo para criar uma Network List {#hand-on}

1. A partir do **Real-Time Manager**, acesse o menu **Libraries > Network Lists**.
2. Para incluir uma nova lista, clique no botão **Add**;
3. Preencha os campos que aparecerão, conforme abaixo:
    - Add Network List (Nome da sua lista): Atribui um nome sugestivo para sua ***Network List***. Esse nome aparecerá na lista de opções na seção ***Criterias***, dentro da configuração de ***Rules Engine***.
    - Type: Tipo da ***Network List***. Podem ser os seguintes tipos:
      - ASN (*Autonomous System Number*)
      - *Countries* (Países)
      - *IP/CIDR* (Endereços IP ou classes de endereços)
    - List: Adicione aqui os itens que irão compor a sua lista. Para os tipos *ASN* e *IP/CIDR*, um campo de livre digitação será apresentado. Inclua apenas um endereço por linha. Itens duplicados serão excluídos automaticamente. Para o tipo Countries, uma lista para seleção será apresentada. Selecione os itens na aba **Available Countries** e mova para aba **Chosen Countries** para incluí-los na lista.
4. Clique en ***Save*** para finalizar a configuração;
5. Tudo pronto. Sua **Network List** já está criada e já pode ser utilizada em **Rules** de **Rules Engine** que contenham o **Criteria: Network**;

---

## 4. Documentação de Suporte {#documentacao-de-suporte}

- [Network Lists API](https://www.azion.com/en/docs/products/api/v3/network-lists/)

---

Não encontrou o que procurava? [Abra um ticket.](https://tickets.azion.com/)