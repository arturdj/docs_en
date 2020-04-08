# Web Application Firewall

Web Application Firewall protege as suas aplicações contra ameaças como SQL Injections, Remote File Inclusion (RFI), Cross-Site Scripting (XSS) e muito mais. O *WAF* analisa as requisições HTTP e HTTPS, detecta e bloqueia atividades maliciosas antes que elas alcancem a sua infraestrutura, sem impactar na performance de suas aplicações.

> 1. *[Como funciona?](#como-funciona)*
> 2. *[Hands-on: Criando uma configuração Web Application Firewall usando Criteria e Behavior](#hands-on-criteria-behavior)*
> 2. *[Hands-on: Criando uma configuração WAF para sua aplicação](#hands-on)*
> 3. *[Documentação de Suporte](#documentacao-de-suporte)*

---

## 1. Como funciona? {#como-funciona}

Construa seu Web Application Firewall programável e proteja a camada de aplicação, de forma personalizada, combinando múltiplos critérios e comportamentos para proteger suas aplicações de ameaças *OWASP* Top 10. 

Ao ser ativado no Edge Firewall Rule Set, o módulo Web Application Firewall permite o uso de:

**Rules Engine Criterias**: Headers Accept, Header Accept-Encoding, Header Accept-Language, Header Cookie, Header Origin, Header Referer, Header User Agent, Hostname, Request Args, Request Method, Request URI e Scheme.

**Behavior Set WAF Rule Set** - O Azion WAF Rule Set é baseado na metodologia de scoring de requisições. Cada requisição *http/https* é comparada com um conjunto extremamente restritivo de regras de bloqueio e recebe uma pontuação para cada família de ameaças.

**Rules Engine Behaviors:** Deny, Drop, Set Rate Limit e Set WAF Rule Set.

---
## 2. Hands-on: Criando uma configuração Web Application Firewall usando Criteria e Behavior {#hands-on-criteria-behavior}

Criar uma configuração com regras de negócio de **Web Application Firewall** através das **Rules Engine. Ex. Rate Limit de 2 requests por segundo com burst de 10** para user-agent Googlebot.

1. Selecione a aba **Rules Engine**;
2. Clique em **New Rule** para adicionar uma nova regra.
3. Preencha os campos que aparecerão, conforme abaixo:

**Rule Name(Nome da sua regra)**

Atribua um nome sugestivo para sua Rule Engine. ex: Rate Limiting Googlebot

**Criteria**

Parametrize sua Rule Engine com os critérios que vão definir a forma de atuação da sua regra. 

- **IF**: Operador condicional. Selecione o atributo, selecione a condição e adicione o valor a ser testado.
    
    Ex: *IF Request User-Agent* **Matches** *Googlebot* . Este condição testará toda requisição em que o cabeçalho user-agent contenha "*Googlebot*"

    Ex: *Header User Agent* **Matches** *Googlebot* **And Network** Matches **Azion Tor Exit Nodes** - Nesse caso a regra só irá se aplicar a requisições originadas na Rede Tor.

**Behavior**:

- Then: Escolha Set Rate Limit

    Ex: *Then* *Set Rate Limit*, *Average Rate* *Limit* *(req/s) 2*, *Client IP Address*, *Maximum burst size 10*. Neste exemplo, para a ação **Set Rate Limit**, aparecerão os  campos adicionais **Average Rate Limit (req/s) e Maximum burst size**, além da opção de seleção de restrição por endereço IP ou Global, ou seja, se a requisição satisfazer os critérios da Rule, então será definido um rate limit de 2 requisições por segundo, por endereço IP, com um limite de burst de 10 requisições.

4. Seleicione o campo ***Active*** para ativar a rule set.
5. Clique em ***Save*** para salvar o Edge Firewall Rule Set

---

## 3. Hands-on: Criando uma configuração Web Application Firewall usando WAF Rule Set para sua aplicação {#hands-on}

_Rule set_ é o conjunto de regras do WAF que habilita a proteção contra os mais variados tipos de ataque. Nela estão definidas as proteções que você deseja ativar, o nível de sensibilidade da detecção e a _whitelist_.

Criar uma configuração WAF dentro de seu Edge Firewall é muito simples, consiste nos seguintes passos:

1. Acesse o [Real-Time Manager](https://manager.azion.com/), acesse o menu Edge Services > WAF. Você visualizará a interface principal onde poderá criar e administrar suas Web Application Firewall;
2. Para incluir uma nova configuração de WAG, clique no botão Add;
3. Preencha os campos que aparecerão, conforme abaixo:
    
    **Name (Nome do seu WAF)**
    
    Atribua um nome sugestivo para seu WAF.
Para criar uma _rule set_:

    **Mode (Modo de operação do WAF)**

   - **Counting**: Analisa todas as requisições e identifica aquelas com comportamento malicioso, porém não bloqueia, apenas contabiliza. Recomendamos utilizar esta opção apenas na etapa de aprendizagem(calibração) do seu WAF.
   - **Blocking**: Analisa todas as requisições e bloqueia aquelas com comportamento malicioso.

    **Threat Type (Famílias de ameaças)**

    Uma lista com as famílias ou tipos de ameaças tratadas pelo ***WAF*** é apresentada. Selecione o nível de sensibilidade do WAF que você deseja para cada uma em **Sensitivity**. Ative todos os tipos que julgar necessário, selecionando **Status**.

    **Active**

    Marque esta opção para ativar seu WAF.

4. Clique em SAVE para salvar suas configurações.

Para que seu WAF entre efetivamente em ação é necessário associá-lo a um Behavior, dentro de uma Rule Engine de seu Edge Firewall:

1.  Acesse o [Real-Time Manager](https://manager.azion.com/) e entre no menu Edge, e selecione Edge Firewall.
2.  Adicione uma nova _rule set_ clicando no botão _Add Rule Set_.
3.  Na aba Main Settings, habilite Web Application Firewall em Edge Firewall Modules e selecione um ou mais domains para receber a proteção do WAF.
4.  Salve sua _rule set_ com um nome sugestivo. Você vai precisar dele para realizar posteriormente a configuração do Rule Set na aba Rules Engine.
5.  Na aba ***Rules Engine***, na seção ***Behavior***, no campo ***Then***,  selecione "Set WAF Rule Set" e associe o **WAF Rule Set** desejado. Certifique-se que a opção ***Active*** está selecionada.
6. Utilize o Analytics ou logs do WAF por meio dos produtos Real-Time Events e Data Streaming para acompanhar as ameaças detectadas.

~~~
Lembre-se: O WAF só bloqueia as ameaças se estiver configurado em Blocking Mode.
~~~
---

## 4. Documentação de Suporte {#documentação de suporte}

- [WAF Rule Sets](https://www.azion.com/pt-br/docs/produtos/edge-firewall/web-application-firewall/waf-rule-sets)

---

Não encontrou o que procurava? [Abra um ticket.](https://tickets.azion.com/)