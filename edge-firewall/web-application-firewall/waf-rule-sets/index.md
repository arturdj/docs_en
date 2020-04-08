# WAF Rule Sets

O WAF Rule Set protege as suas aplicações contra ameaças como SQL Injections, Remote File Inclusion (RFI), Cross-Site Scripting (XSS) e muito mais. O WAF analisa as requisições HTTP e HTTPS, detecta e bloqueia atividades maliciosas antes que elas alcancem a sua infraestrutura, sem impactar na performance de suas aplicações.

> 1. *[Como funciona?](#como-funciona)*
> 2. *[Hands-on: Criando uma configuração WAF para sua aplicação](#hands-on)*
> 3. Monitorando a detecção de ameaças (*monitorando-a-deteccao-de-ameacas)

---

## 1. Como funciona {#como-funciona}

O Azion WAF é baseado na metodologia de scoring de requisições. Cada requisição *http/https* é comparada com um conjunto extremamente restritivo de regras de bloqueio e recebe uma pontuação para cada família de ameaças.

De acordo com a pontuação recebida pela requisição, a mesma poderá ser liberada ou bloqueada diretamente nos Edge Servers da Azion, antes que a ameaça atinja sua origem. Você define o nível desejado de sensibilidade para o bloqueio de cada família de ameaças.

Para evitar o bloqueio de requisições lícitas e o mal funcionamento de sua aplicação, você deve executar uma etapa de aprendizagem, na qual o ***WAF*** identifica os comportamentos legítimos de sua aplicação, inserindo-os em uma *whitelist*.

Você ainda pode monitorar o comportamento e a efetividade de suas configurações de **WAF**. Através de nossas ferramentas **Real-Time Events** e **Data Streaming**, a Azion disponibiliza dashboards e relatórios para consultas de logs de eventos on-line e em tempo real. Além disso, você pode importar os registros de logs da Azion e manipulá-los dentro de suas próprias ferramentas de análise.

~~~
Para utilizar o recurso de WAF Rule Sets  é necessário habilitar o módulo Web Application Firewall (WAF).
~~~

**Modo de Operação**

Para obter o máximo de desempenho e precisão do produto é necessária a etapa de aprendizagem. Você conta com dois modos de operação para lhe apoiar nessa etapa:

*   **Counting Mode:** é utilizado para especificar que o WAF não deve bloquear nenhuma requisição. O tráfego de suas aplicações será analisado e as ameaças encontradas serão apenas contabilizadas. Utilize esse modo de operação durante a primeira etapa de aprendizagem.
*   **Blocking Mode:** é utilizado para analisar e bloquear as ameaças detectadas, protegendo as suas aplicações dos usuários maliciosos. Você pode executar a etapa de aprendizagem sempre que julgar necessário, mesmo em Blocking Mode.

**Famílias de Ameaças**

As ameaças são categorizadas em famílias de acordo com o objetivo do ataque. Você pode ativar ou desativar a proteção para cada família de ameaças individualmente de acordo com as proteções requeridas pelo tipo de sua aplicação e funcionalidades que ela apresente.


| Threat Type | Description |
| ----------- | ----------- |
| SQL Injections | Previne tentativas de ataque através de injeção de código SQL na aplicação. |
| Remote File Inclusions (RFI) | Previne tentativas de incluir arquivos, usualmente através de scripts no servidor web. |
| Directory Traversal          | Previne a exploração de vulnerabilidade referente a sanitização insuficiente de campos de nomes de arquivo fornecidos pelos usuários, de modo que caracteres representando atalhos para o diretório pai sejam passados através da API de arquivos. |
| Cross-Site Scripting (XSS)   | Previne a injeção de scripts client-side em páginas vistas por seus visitantes. |
| File Upload                  | Previne a tentativa de envio de arquivos para o servidor web. |
| Evading Tricks               | Previne contra algunas truques de codificação utilizados para tentar escapar dos mecanismos de proteção. |
| Unwanted Access              | Previne as tentativas de acesso a páginas administrativas ou vulneráveis, bots e ferramentas de scanning de segurança. |
| Identified Attacks           | Previne vários tipos de ataques comuns e vulnerabilidades conhecidas que certamente deverão ser bloqueados. |

**Sensitivity (Sensibilidade)**

A sensibilidade define o rigor com o qual o WAF irá considerar uma requisição como uma ameaça:

- **Lowest**: é nível de sensibilidade mais baixo, a requisição será considerada uma ameaça se apresentar indícios muito fortes e receber uma pontuação alta. Essa sensibilidade tem um menor nível de proteção para suas aplicações, mas também evitará o bloqueio de requisições com menor chance de representar ameaças (falsos positivos)

- **Low**: é nível de sensibilidade mais baixo, a requisição será considerada uma ameaça se apresentar indícios muito fortes e receber uma pontuação alta. Essa sensibilidade tem um menor nível de proteção para suas aplicações, mas também evitará o bloqueio de requisições com menor chance de representar ameaças (falsos positivos).

- **Medium**: é o nível de sensibilidade recomendado pela Azion. A requisição será considerada como ameaça se apresentar indícios suficientes e receber uma pontuação intermediária.

- **High**: é o maior nível de proteção para sua aplicação. Ao menor indício de uma ameaça, a requisição poderá ser bloqueada, mesmo quando apresentar uma pontuação relativamente baixa. Esse nível de sensibilidade pode apresentar mais falsos positivos, se a etapa de aprendizagem não tiver cobertura suficiente sobre a variabilidade de cenários e usos de sua aplicação.

- Highest: é o maior nível de proteção para sua aplicação. Ao mínimo indício de uma ameaça, a requisição poderá ser bloqueada, mesmo quando apresentar uma pontuação muito baixa. Esse nível de sensibilidade pode apresentar muitos falsos positivos, se a etapa de aprendizagem não tiver cobertura suficiente sobre a variabilidade de cenários e usos de sua aplicação.

**Regras** {#regras}

O conjunto de regras que incrementam o score de uma requisição. Quanto maior o score, maior a probabilidade da requisição ser considerada um ataque pelo WAF.

A Azion trabalha com um conjunto extremamente restritivo de regras para assegurar a segurança de sua aplicação. Cada regra é composta pelos campos que seguem.

| Campo | Descrição |
| ----- | --------- |
| Rule Id | Id numérico único de cada regra do WAF.                      |
| Rule Description | Uma descrição textual do que a regra faz. |
| Match Pattern | Condição de comparação, string ou regex, que será buscada na requisição. |
| Path | Quando especificado, restringe a aplicação da _Match Zone_ somente ao _path_ definido. O _path_ delimita o escopo de atuação da regra. |
| Match Zones | Partes ou campos da requisição que serão comparados com o _Match Pattern_. Pode ser:<br> **Path:** o <em>match pattern</em> será comparado com o <em>path</em> da requisição. <br> **Query String:** o _match pattern_ será comparado com a _query string_, também chamada de GET _arguments_. <br> **Request Header:** o _match pattern_ será comparado com os cabeçalhos HTTP da requisição. <br> **Request Body:** o _match pattern_ será comparado com o _body_ de um POST, também chamado de POST _arguments_. <br> **File Name (Multipart Body):** o _match pattern_ será comparado com o nome de arquivos em _multipart POSTs_. <br> **Raw Body:** o _match pattern_ será comparado com o _body_ não interpretado de uma requisição, também chamado de _unparsed body_. |
| Attack Family | A(s) família(s) de ataques para as quais a regra incrementa a pontuação. |

**Whitelist**

É a listagem de comportamentos legítimos de sua aplicação, que não devem incrementar o _score_ das requisições. Pode ser gerada automaticamente durante a etapa de aprendizagem ou inserida manualmente por meio de regras customizadas.

Cada regra de bloqueio possui _match zones_, conforme explicado na seção [Regras](#regras). A _whitelist_ tem o objetivo de desativar determinadas _Match Zones_ de uma regra de bloqueio.

| Campo | Descrição |
| ----- | --------- |
| Rule Id | Id numérico único da regra de bloqueio para a qual a whitelist foi gerada.                   |
| Rule Description | Uma descrição textual do que faz a regra de bloqueio para a qual a whitelist foi gerada. |
| Path | Quando especificado, restringe a aplicação da whitelist somente ao path definido. O path delimita o escopo de atuação da whitelist. |
| Whitelist Match Zone | É a whitelist propriamente dita. Define a parte ou campo da requisição para a qual a regra de bloqueio deve ser desativada. <br><br> **Path:** a rule id não será aplicada ao path da requisição. <br><br> **Query String:** a rule id não será aplicada a query string, também chamada de GET arguments. Pode ser restrito tanto ao nome quanto ao valor dos argumentos. É possível delimitar o escopo da whitelist a um único GET argument utilizando Conditional Query String. <br><br> **Request Header:** a rule id não será aplicada aos cabeçalhos HTTP da requisição. Pode ser restrito tanto ao nome quanto ao valor dos cabeçalhos. É possível delimitar o escopo da whitelist a um único cabeçalho HTTP utilizando Conditional Request Header. <br><br> **Request Body:** a rule id não será aplicada ao body de um POST, também chamado de POST arguments. Pode ser restrito tanto ao nome quanto ao valor dos argumentos. É possível delimitar o escopo da whitelist a um único POST argument utilizando Conditional Request Body. <br><br> **File Name (Multipart Body):** a rule id não será aplicada ao nome de arquivo em um multipart POST. <br><br> **Raw Body:** a rule id não será aplicada ao body não interpretado de uma requisição, também chamado de unparsed body. |
| Status | O status de ativação da regra na whitelist. |

---

## 2. Hands-on: Criando uma configuração WAF Rule Set para sua aplicação {#hands-on}

_Rule set_ é o conjunto de regras do WAF que habilita a proteção contra os mais variados tipos de ataque. Nela estão definidas as proteções que você deseja ativar, o nível de sensibilidade da detecção e a _whitelist_.

Para criar uma _rule set_:

1.  Acesse o [Real-Time Manager](https://manager.azion.com/) e entre no menu ***Edge Services > WAF***, ou acesse o atalho “**Manage WAF**” na tela inicial.
2.  Adicione uma nova **_rule set_** clicando no botão **_Add_**.
3.  Na aba **Main Settings**, ative as proteções e o nível de sensibilidade desejados.
4.  Salve sua **_rule set_** com um nome sugestivo. Você vai precisar dele para realizar posteriormente a associação da _rule set_ através do **Rules Engine**.

No primeiro momento, recomendamos que você ative a regra em **_Counting Mode_**, para que possa acompanhar o número de ameaças detectadas e realizar a etapa de aprendizagem, antes de efetivamente bloquear as requisições. Dessa forma você poderá também regular a sensibilidade da detecção, de acordo com a sua aplicação.

Durante o Counting Mode é recomendado que você deixe todas as proteções ativadas para que possa monitorar as ameaças detectadas pelo WAF.

Se forem detectados falsos positivos, algumas regras poderão ser incluídas na _whitelist_ pelo Suporte da Azion, sem a necessidade de desativar a proteção completa para uma família de ameaças. Entre em contato se desejar avaliar a necessidade de incluir regras em _whitelist_, antes de desabilitar a sua proteção.

Por fim, a _rule set_ deve estar ativa para que o WAF analise as suas requisições. O checkbox Active serve para permitir que você habilite e desabilite o WAF rapidamente para todos os _paths_ que estiverem associados a rule set.

---

## 3. Monitorando a detecção de ameaças {#associe-a-rule-set-criada-com-as-aplicacoes-que-deseja-monitorar}

Deixe a rule set do WAF em modo Counting pelo tempo que julgar necessário para que a maior parte das funcionalidades de sua aplicação sejam cobertas. Você deve acompanhar os gráficos da aba WAF pelo Analytics ou os logs do WAF por meio dos produtos **Real-Time Events** e **Data Streaming**.

No Analytics, o primeiro gráfico da aba WAF (Threats vs Requests) apresenta três séries temporais:

*   **Regular Requests:** todas as requisições HTTP e HTTPS analisadas pelo WAF e consideradas seguras.
*   **Threats:** o volume de ameaças detectadas pelo WAF e contabilizadas, quando em modo *Counting*. Essas ameaças não estão sendo bloqueadas nesse momento.
*   **Threats Blocked:** ameaças efetivamente bloqueadas pelo WAF. Para começar a bloquear as ameaças encontradas, a rule set tem que estar em *Blocking Mode*.

Se você possuir também o serviço Data Streaming, é possível acompanhar informações mais detalhadas sobre IP, data e horário de acesso, status code, família de ataque detectada e modo de atuação configurado.

~~~
$time-iso8601 $azion-client-id $azion-virtualhost-id $azion-configuration-id $azion-solution $azion-solution-id $host $conn-request-time $req-method $resp-status $req-uri $waf-threat-family $waf-threat-action $client-geoip-country-name $client-geoip-region-name $client-addr $client-port $req-header(User-Agent) $req-header(Referer) 2017-01-04T17:00:19+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.129 GET 200 /request-uri?key=value $XSS $LEARNING-BLOCK Brazil Sao Paulo 1.2.3.4 61511 Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36 https://www.yoursite.com/referrer 2017-01-04T17:00:19+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.025 POST 200 /request-uri $SQL $LEARNING-BLOCK Brazil Santa Catarina 2.3.4.5 61513 Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36 https://www.yoursite.com/referrer 2017-01-04T17:00:40+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.026 GET 301 /request-uri?key=value $RFI $LEARNING-BLOCK Brazil Rio de Janeiro 5.6.7.8 26102 Mozilla/5.0 (Linux; Android 5.1.1; SM-G800H Build/LMY47X) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.91 Mobile Safari/537.36 https://www.yoursite.com/referrer 2017-01-04T17:00:41+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.391 POST 200 /request-uri $UWA $LEARNING-BLOCK Brazil Rio Grande do Sul 9.10.11.12 26102 Mozilla/5.0 (Linux; Android 5.1.1; SM-G800H Build/LMY47X) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.91 Mobile Safari/537.36 https://www.yoursite.com/referrer
~~~

Com base nessas informações, você pode ajustar a sensibilidade da _rule_ set do WAF, como mencionado anteriormente, até que não ocorram mais falsos positivos. Ou mesmo solicitar para Azion a geração de _whitelist_ para sua aplicação.

---

Não encontrou o que procurava? [Abra um ticket.](https://tickets.azion.com/)