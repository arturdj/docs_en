# Network Layer Protection

Você pode transferir parte da lógica das regras de negócio de sua aplicação para o Edge Node da Azion e expandir essas funcionalidades com o produto Application Acceleration. Dessa forma, você constrói uma arquitetura que entrega performance para seus usuários consumindo menos recursos e processamento em sua origem.

O Rules Engine foi elaborado para permitir a codificação de uma lógica de execução condicional de comportamentos e ações diretamente no Edge Node da Azion, mais próximo de seus usuários e, portanto, com melhor performance e taxa de transferência para sua aplicação.

> 1. *[Como funciona?](#como-funciona)*
> 2. *[Network Lists](#network-lists)*
> 3. *[Origin Shield](#origin-shield)*
> 4. *[Documentação de Suporte](#documentacao-de-suporte)*

---

## 1. Como funciona? {#como-funciona}

Este módulo possibilita a criação de filtros por endereços de IP ou por países (*geolocation*), através da configuração de ***Network Lists*** e da definição de regras de negócio que validarão critérios de bloqueio ou de liberação, conforme a sua necessidade, especificados nas ***Rules Engine*** de seu ***Edge Firewall***.

Atuando nas camadas 3 e 4 do modelo ***OSI***, o ***Network Layer Protection*** é uma ferramenta poderosa que consiste em uma opção segura e eficiente de proteger seu negócio contra ataques e acessos de usuários indesejados. 

---

## 2. Network Lists {#network-lists}

Através de **Network Lists** você pode criar, consultar ou atualizar Network Lists utilizadas no Rules Engine do Novo Edge Firewall. Cada Network List pode ser utilizada em um ou mais Rule Sets do Novo Edge Firewall.

---

## 3. Origin Shield {#origin-shield}

Com este add-on do Azion Edge Firewall você poderá criar um perímetro de segurança para a sua infraestrutura de origem, seja ela um provedor de *cloud*, *hosting* ou mesmo o seu próprio *datacenter*. Com este serviço, sua origem poderá restringir o acesso apenas de endereços IP’s específicos da nossa rede e bloquear qualquer outro acesso a sua origem.

Nossa lista de IP’s pode sofrer alterações frequentes, mas após atualizá-la só colocaremos os novos servidores em produção para quem utiliza o *add-on Origin Shield* 4 dias após a publicação da lista. Assim, sugerimos que você consulte de forma automatizada a nossa lista de IP’s e atualize os seus filtros de borda sempre que ela receber atualizações, para evitar indisponibilidade de serviço.

Para garantir a segurança contra ataques realizados diretamente na sua origem, sugerimos o uso do **Azion DDoS Protection** com o ***add-on Infrastructure Protection***, que irá garantir a proteção do seu ASN via BGP utilizando a rede distribuída da Azion.

---

## 4. Documentação de Suporte {#documentacao-de-suporte}

- [Network Lists](https://www.azion.com/pt-br/docs/produtos/edge-firewall/network-layer-protection/network-lists)
- [Edge Firewall Rules Engine](https://www.azion.com/pt-br/docs/produtos/edge-firewall/rules-engine/)

---

Não encontrou o que procurava? [Abra um ticket.](https://tickets.azion.com/)