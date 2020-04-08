# Edge **Firewall**

O Azion Edge Firewall oferece uma gama de funcionalidades para proteger sua aplicação, desde filtros de endereços IP até complexas regras para tratamento de requisições no nível de aplicação. Ele permite a criação de regras de controle de acesso ao seu conteúdo que são processadas diretamente nos Azion Edge Nodes, mais perto dos usuários, evitando que requisições indesejadas cheguem a sua origem ou que tenham acesso às suas aplicações.

O Edge Firewall permite construir uma *firewall* programável para proteger as camadas de rede e aplicação, de forma personalizada. Com essa solução sua empresa pode: 

- Criar *whitelists*, *blacklists* e *greylists* com base na rede ou localização do usuário; 
- Proteger suas aplicações da rede *Tor*; 
- Limitar a taxa de acessos à aplicação para evitar ataques de *brute force*; 
- Mitigar ataques de negação de serviço (*DDoS*); 
- Proteger aplicações de ameaças *OWASP* Top 10 com o módulo de WAF;
- Adicionar seu código fonte de proteção, para ser executado no Edge Firewall;
- Portar bibliotecas de terceiros para processar no Edge Firewall, por exemplo, soluções líderes de mercado contra *credential stuffing*, *account takeover attempts*, *price* and *contact scraping*, etc.

> 1. *Como Funciona?*
> 2. *Edge Firewall Modules*
> 3. *Hands On*
> 4. *Permissões*
> 5. *Documentação de Suporte*

---

## 1. Como Funciona?

Através dos módulos disponíveis, crie *whitelists*, *blacklists* ou *graylists* por país de acesso do usuário (*geo* *blocking*), ASN ou endereços IP, para evitar que seu conteúdo ou aplicações *web* sejam acessados de determinados locais. Se preferir, defina que somente os IPs da Azion acessem seus servidores de origem, concentrando o acesso externos em nossos Edges.

Implemente regras inteligentes para prevenir diversos tipos de ataques. Através do **Rules Engine**, é possível parametrizar comportamentos específicos para responder a comportamentos maliciosos e proteger suas aplicações.


---

## 2. Edge Firewall Modules

O Azion Edge Firewall possui os seguintes módulos para que você possa construir *web applications* de alta performance, escalabilidade e segurança, com muito mais simplicidade e livre de tarefas operacionais. Consulte as documentações de cada produto:|

### [DDoS](https://www.azion.com/pt-br/docs/produtos/ddos-protection/) 

O módulo de DDoS Protection protege seu conteúdo e aplicações contra ataques do tipo *Distributed Denial of Service* (*DDoS*).
Por meio de uma moderna abordagem de detecção e mitigação de ataques das camadas de rede, transporte e aplicação, reduzimos o downtime sem impactar na performance de seu serviço.

---
### [Edge Functions](https://www.azion.com/pt-br/docs/produtos/edge-functions)

Edge Functions são componentes da plataforma Edge Computing da Azion, que permitem a implementação de funções serverless em suas aplicações, desonerando sua infraestrutura, executando funções mais próximo do usuário, garantindo a agilidade e a escalabilidade necessárias para atender seus objetivos de negócio.

Você poderá se beneficiar de uma arquitetura baseada em micro serviços, criando facilmente funções que executam próximas aos usuários. 

Aproveite as soluções de segurança de *third-party* para proteger seus dados sensíveis e aplicações contra ataques na borda da rede.

---
### [Network Layer Protection](https://www.azion.com/pt-br/docs/produtos/edge-firewall/network-layer-protection)

Este módulo possibilita a criação de filtros por endereços de IP ou por países (*geolocation*), através da configuração de Network Lists e da definição de regras de negócio que validarão critérios de bloqueio ou de liberação, conforme a sua necessidade, especificados nas Rules Engine de seu Edge Firewall.

Atuando nas camadas 3 e 4 do modelo *OSI*, o Network Layer Protection é uma ferramenta poderosa que consiste em uma opção segura e eficiente de proteger seu negócio contra ataques e acessos de usuários indesejados.

####  **Add-on Origin Shield**

Com este add-on do Azion Edge Firewall você poderá criar um perímetro de segurança para a sua infraestrutura de origem, seja ela um provedor de cloud, hosting ou mesmo o seu próprio datacenter. Com este serviço, sua origem poderá restringir o acesso apenas de endereços IP’s específicos da nossa rede e bloquear qualquer outro acesso a sua origem.

---
### [Web Application Firewall](https://www.azion.com/pt-br/docs/produtos/edge-firewall/web-application-firewall)
Web Application Firewall (WAF) protege as suas aplicações contra ameaças como SQL Injections, Remote File Inclusion (RFI), Cross-Site Scripting (XSS) e muito mais. O WAF analisa as requisições HTTP e HTTPS, detecta e bloqueia ameaças antes que elas alcancem a sua infraestrutura e sem impactar na performance de suas aplicações. 

---
## 3. Hands On - Passo a passo para configurar o Edge Firewall

Passo 1: Criando um novo Edge Firewall

1. Acesse o [Real-Time Manager](https://manager.azion.com/)  e entre no menu **Edge Services > Edge Firewall**. Você visualizará a interface principal onde poderá criar e administrar suas rule sets de **Edge Firewall**;
2. Para incluir uma nova rule set, clique no botão **Add Rule Set**;
3. Preencha os campos que aparecerão, conforme abaixo:
 
    Add Edge Firewall (Nome da sua rule set)

    Atribua um nome sugestivo para seu Edge Application.
    
    **Domain Settings**

    Dentro desta seção, selecione o(s) domínio(s) para os quais você deseja que sejam aplicadas essas configurações. No campo ***Domains***, uma lista com os seus domínios disponíveis será apresentada. Selecione os domínios na aba ***Available Domains*** e mova para aba ***Chosen Domains*** para vincular à rule set.

    **Edge Firewall Modules**

    Lista de módulos disponíveis para o Edge Firewall. Habilite os módulos que julgar necessário para poder ter acesso a funcionalidades específicas de cada um. Os módulos disponíveis são:

    - Network Layer Protection
    - Web Application Firewall
    - Edge Functions
4. Selecione o campo ***Active*** para ativar a rule set.
5. Clique em ***Save*** para salvar.

Passo 2: Criando regras de negócio através das ***Rules Engine***

1. Selecione a aba ***Rules Engine***;
2. Clique em ***New Rule*** para adicionar uma nova regra.
3. Preencha os campos que aparecerão, conforme abaixo:
    
    **Rule Name(Nome da sua regra)**

    Atribua um nome sugestivo para sua Rule Engine.

    **Criteria**
    
    Parametrize sua Rule Engine com os critérios que vão definir a forma de atuação da sua regra.

    - **IF**: Operador condicional. Selecione o atributo, selecione a condição e adicione o valor a ser testado.

        Ex: *IF Request URI starts with /product*. Este condição testará toda requisição em que a URI começar com */product*.

        Você pode aninhar mais de uma condição dentro de uma mesma Rule Engine, basta ir adicionando regras através dos operadores lógicos ***And*** e ***Or***.
    
    **Behavior**: Defina a ação a ser executada caso a requisição coincida com os critérios definidos. Selecione o atributo, e, se necessário, selecione a condição e adicione o valor de referência. Algumas Ações não necessitam de complemento, basta  selecioná-las para que seu comportamento seja definido, como, por exemplo, na ação **Deny (403 Forbidden)**, que irá retornar um erro 403.

    - **Then**: Escolha uma das ações disponíveis (Podem variar de acordo com os módulos do Edge Firewall habilitados). Dependendo da opção selecionada outros campos complementares de preenchimento serão exibidos.
        
        Ex: *Then Set Rate Limit, Average Rate Limit (req/s)* 2, *Client IP Address*, *Maximum burst size 10*. Neste exemplo, para a ação ***Set Rate Limit***, aparecerão os  campos adicionais ***Average Rate Limit (req/s)*** e ***Maximum burst size***, além da opção de seleção de restrição por endereço IP ou Global, ou seja, se a requisição satisfazer os critérios da *Rule*, então será definido um *rate limit* de 2 requisições por segundo, por endereço IP, com um limite de *burst* de 10 requisições.
4. Selecione o campo ***Active*** para ativar a rule set.
5. Clique em ***Save*** para salvar o Edge Firewall Rule Set

---
## 4. Permissions

Como um cliente que possui **Real-Time Manager**, e possui o módulo de Edge Firewall, é possível realizar as configurações de permissões para o usuários e times. Essa configuração permite mais flexibilidade no momento de definição das funções e papéis dos usuários e times.

O módulo de Edge Firewall conta com dois tipos de permissões de times para ser configurado:

- View / Edit Edge Firewall
- View / Edit Network List

Cada permissão tem a função de *View* ou *Edit*, isso significa que o usuário pode visualizar ou editar uma configuração no respectivo  módulo

Como configurar as permissões de Edge Firewall:
1. Com uma conta com privilégios de administrador, acesse o [Real-Time Manager](https://manager.azion.com/)  e entre no menu ***Your Account*** na seção superior direita do Topo.
2. Selecione o menu ***Teams***.
3. Edite ou Adicione um ***Team***.
4. Confirme as permissões de **View/Edit Edge Firewall** ou **View/Edit Network List**.
5. Clique em ***Save*** para salvar a configuração.

---

## 5. Documentação de Suporte

- [DDoS](https://www.azion.com/pt-br/docs/produtos/ddos-protection/)
- [Edge Functions](https://www.azion.com/pt-br/docs/produtos/edge-functions)
- [Network Layer Protection](https://www.azion.com/pt-br/docs/produtos/edge-firewall/network-layer-protection)
- [Web Application Firewall](https://www.azion.com/pt-br/docs/produtos/edge-firewall/web-application-firewall)
- [Edge Firewall Rules Engine](https://www.azion.com/pt-br/docs/produtos/edge-firewall/rules-engine/)
- [Network Lists](https://www.azion.com/pt-br/docs/produtos/edge-firewall/network-layer-protection/network-lists)
- [WAF Rule Sets](https://www.azion.com/pt-br/docs/produtos/edge-firewall/web-application-firewall/waf-rule-sets)
---

Não encontrou o que procurava? [Abra um ticket.](https://tickets.azion.com/)