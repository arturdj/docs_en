# Web Application Firewall

Web Application Firewall protege as suas aplicações contra ameaças como SQL Injections, Remote File Inclusion (RFI), Cross-Site Scripting (XSS) e muito mais. O WAF analisa as requisições HTTP e HTTPS, detecta e bloqueia ameaças antes que elas alcancem a sua infraestrutura e sem impactar na performance de suas aplicações.

> 1. [Como funciona](#como-funciona)
> 2. [Crie uma rule set do WAF para monitorar o tráfego de suas aplicações](#crie-uma-rule-set-do-waf-para-monitorar-o-trafego-de-suas-aplicacoes)
> 3. [Associe a rule set criada com as aplicações que deseja monitorar](#associe-a-rule-set-criada-com-as-aplicacoes-que-deseja-monitorar)
> 4. [Utilize o Analytics ou o Rawlogs para acompanhar as ameaças detectadas](#utilize-o-analytics-ou-o-rawlogs-para-acompanhar-as-ameacas-detectadas)
> 5. [Aprove a whitelist desejada](#aprove-a-whitelist-desejada)
> 6. [Ative o bloqueio de ameaças na rule set](#ative-o-bloqueio-de-ameacas-na-rule-set)

---

## 1. Como funciona {#como-funciona}

O Azion WAF é baseado na metodologia de _scoring_ de requisições. Cada requisição http/https é comparada com um conjunto extremamente restritivo de regras de bloqueio e recebe uma pontuação para cada família de ameaças.

De acordo com a pontuação recebida pela requisição, a mesma poderá ser liberada ou bloqueada diretamente nos Edge Servers da Azion, antes que a ameaça atinja sua origem. Você define o nível desejado de sensibilidade para o bloqueio de cada família de ameaças.

Para evitar o bloqueio de requisições lícitas e o mal funcionamento de sua aplicação, você deve executar uma etapa de aprendizagem, na qual o WAF identifica os comportamentos legítimos de sua aplicação, inserindo-os em uma _whitelist_.

**Modo de Operação**

Para obter o máximo de desempenho e precisão do produto é necessária a etapa de aprendizagem. Você conta com dois modos de operação para lhe apoiar nessa etapa:

*   **Counting Mode:** é utilizado para especificar que o WAF não deve bloquear nenhuma requisição. O tráfego de suas aplicações será analisado e as ameaças encontradas serão apenas contabilizadas. Utilize esse modo de operação durante a primeira etapa de aprendizagem.
*   **Blocking Mode:** é utilizado para analisar e bloquear as ameaças detectadas, protegendo as suas aplicações dos usuários maliciosos. Você pode executar a etapa de aprendizagem sempre que julgar necessário, mesmo em Blocking Mode.

**Famílias de Ameaças**

As ameaças são categorizadas em famílias de acordo com o objetivo do ataque. Você pode ativar ou desativar a proteção para cada família de ameaças individualmente de acordo com as proteções requeridas pelo tipo de sua aplicação e funcionalidades que ela apresente.


| Threat Type | Description |
|-------------|-------------|
| SQL Injections | Previne tentativas de ataque através de injeção de código SQL na aplicação. |
| Remote File Inclusions (RFI) | Previne tentativas de incluir arquivos, usualmente através de scripts no servidor web. |
| Directory Traversal | Previne a exploração de vulnerabilidade referente a sanitização insuficiente de campos de nomes de arquivo fornecidos pelos usuários, de modo que caracteres representando atalhos para o diretório pai sejam passados através da API de arquivos. |
| Cross-Site Scripting (XSS) | Previne a injeção de scripts client-side em páginas vistas por seus visitantes. |
| File Upload | Previne a tentativa de envio de arquivos para o servidor web. |
| Evading Tricks | Previne contra algunas truques de codificação utilizados para tentar escapar dos mecanismos de proteção. |
| Unwanted Access | Previne as tentativas de acesso a páginas administrativas ou vulneráveis, bots e ferramentas de scanning de segurança. |
| Identified Attacks | Previne vários tipos de ataques comuns e vulnerabilidades conhecidas que certamente deverão ser bloqueados. |


**Whitelist**

É a listagem de comportamentos legítimos de sua aplicação, que não devem incrementar o _score_ das requisições. Pode ser gerada automaticamente durante a etapa de aprendizagem ou inserida manualmente por meio de regras customizadas.

Cada regra de bloqueio possui _match zones_, conforme explicado na seção [Regras](#regras). A _whitelist_ tem o objetivo de desativar determinadas _Match Zones_ de uma regra de bloqueio.

| Campo | Descrição |
|-------|-----------|
| Rule Id | Id numérico único de cada regra do WAF. |
| Rule Description | Uma descrição textual do que a regra faz. |
| Match Pattern | Condição de comparação, string ou regex, que será buscada na requisição. |
| Path | Quando especificado, restringe a aplicação da _Match Zone_ somente ao _path_ definido. O _path_ delimita o escopo de atuação da regra. |
| Match Pattern | Condição de comparação, string ou regex, que será buscada na requisição. |
| Path | Quando especificado, restringe a aplicação da _Match Zone_ somente ao _path_ definido. O _path_ delimita o escopo de atuação da regra. |
| Match Zones | Partes ou campos da requisição que serão comparados com o _Match Pattern_. Pode ser:<br> **Path:** o <em>match pattern</em> será comparado com o <em>path</em> da requisição. <br> **Query String:** o _match pattern_ será comparado com a _query string_, também chamada de GET _arguments_. <br> **Request Header:** o _match pattern_ será comparado com os cabeçalhos HTTP da requisição. <br> **Request Body:** o _match pattern_ será comparado com o _body_ de um POST, também chamado de POST _arguments_. <br> **File Name (Multipart Body):** o _match pattern_ será comparado com o nome de arquivos em _multipart POSTs_. <br> **Raw Body:** o _match pattern_ será comparado com o _body_ não interpretado de uma requisição, também chamado de _unparsed body_.|
| Attack Family | A(s) família(s) de ataques para as quais a regra incrementa a pontuação. |

---

## 2. Crie uma rule set do WAF para monitorar o tráfego de suas aplicações {#crie-uma-rule-set-do-waf-para-monitorar-o-trafego-de-suas-aplicacoes}

_Rule set_ é o conjunto de regras do WAF que habilita a proteção contra os mais variados tipos de ataque. Nela estão definidas as proteções que você deseja ativar, o nível de sensibilidade da detecção e a _whitelist_.

Para criar uma _rule set_:

1.  Acesse o [Real-Time Manager](https://manager.azion.com/) e entre no menu Cloud Security > WAF, ou acesse o atalho “Manage WAF” na tela inicial.
2.  Adicione uma nova _rule set_ clicando no botão _Add_.
3.  Na aba Main Settings, ative as proteções e o nível de sensibilidade desejados.
4.  Salve sua _rule set_ com um nome sugestivo. Você vai precisar dele para realizar posteriormente a associação da _rule set_ com o _path_ de sua aplicação.

No primeiro momento, recomendamos que você ative a regra em _Counting Mode_, para que possa acompanhar o número de ameaças detectadas e realizar a etapa de aprendizagem, antes de efetivamente bloquear as requisições. Dessa forma você poderá também regular a sensibilidade da detecção, de acordo com a sua aplicação.

Durante o Counting Mode é recomendado que você deixe todas as proteções ativadas para que possa monitorar as ameaças detectadas pelo WAF.

Se forem detectados falsos positivos, algumas regras poderão ser incluídas na _whitelist_ pelo Suporte da Azion, sem a necessidade de desativar a proteção completa para uma família de ameaças. Entre em contato se desejar avaliar a necessidade de incluir regras em _whitelist_, antes de desabilitar a sua proteção.

Por fim, a _rule set_ deve estar ativa para que o WAF analise as suas requisições. O checkbox Active serve para permitir que você habilite e desabilite o WAF rapidamente para todos os _paths_ que estiverem associados a rule set.

---

## 3. Associe a rule set criada com as aplicações que deseja monitorar {#associe-a-rule-set-criada-com-as-aplicacoes-que-deseja-monitorar}

Você deve associar a _rule set_ criada aos _paths_ de sua aplicação. Para tanto:

1.  Acesse o menu Content Delivery e edite a Configuration que você deseja proteger.
2.  Na aba Rules Engine, edite as regras referentes ao _path_ de sua aplicação.
3.  Para associar uma _rule set_ do WAF a um _path_ em Rules Engine, o behavior selecionado deve ser Application Acceleration.
4.  A associação da _rule set_ do WAF ao _path_ é feita na seção WAF Settings, mas lembre-se que essa seção só aparece se o _behavior_ for Application Acceleration.

A partir deste momento, as requisições realizadas para essa aplicação serão analisadas pelo WAF. Enquanto sua _rule set_ estiver em Counting Mode, os ataques estão sendo apenas detectados, mas não serão bloqueados.

---

## 4. Utilize o Analytics ou o Rawlogs para acompanhar as ameaças detectadas {#utilize-o-analytics-ou-o-rawlogs-para-acompanhar-as-ameacas-detectadas}

Recomenda-se que você deixe a _rule set_ do WAF em modo Counting pelo tempo que julgar necessário para que a maior parte das funcionalidades de sua aplicação sejam cobertas. Você deve acompanhar os gráficos da aba WAF pelo Analytics ou os logs do WAF por meio do produto Rawlogs.

No Analytics, o primeiro gráfico da aba WAF (Threats vs Requests) apresenta três séries temporais:

*   **Regular Requests:** todas as requisições HTTP e HTTPS analisadas pelo WAF e consideradas seguras.
*   **Threats:** o volume de ameaças detectadas pelo WAF e contabilizadas, quando em modo Counting. Essas ameaças não estão sendo bloqueadas nesse momento.
*   **Threats Blocked:** ameaças efetivamente bloqueadas pelo WAF. Para começar a bloquear as ameaças encontradas, a rule set tem que estar em Blocking Mode.

Se você possuir também o serviço Rawlogs, poderá solicitar a configuração dos logs para o Suporte da Azion. Através dos logs é possível acompanhar informações mais detalhadas sobre IP, data e horário de acesso, status code, família de ataque detectada e modo de atuação configurado.

~~~
$time-iso8601 $azion-client-id $azion-virtualhost-id $azion-configuration-id $azion-solution $azion-solution-id $host $conn-request-time $req-method $resp-status $req-uri $waf-threat-family $waf-threat-action $client-geoip-country-name $client-geoip-region-name $client-addr $client-port $req-header(User-Agent) $req-header(Referer) 2017-01-04T17:00:19+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.129 GET 200 /request-uri?key=value $XSS $LEARNING-BLOCK Brazil Sao Paulo 1.2.3.4 61511 Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36 https://www.yoursite.com/referrer 2017-01-04T17:00:19+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.025 POST 200 /request-uri $SQL $LEARNING-BLOCK Brazil Santa Catarina 2.3.4.5 61513 Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36 https://www.yoursite.com/referrer 2017-01-04T17:00:40+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.026 GET 301 /request-uri?key=value $RFI $LEARNING-BLOCK Brazil Rio de Janeiro 5.6.7.8 26102 Mozilla/5.0 (Linux; Android 5.1.1; SM-G800H Build/LMY47X) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.91 Mobile Safari/537.36 https://www.yoursite.com/referrer 2017-01-04T17:00:41+00:00 1234a 10203b 1020304050 ha 1441740010 www.yoursite.com 0.391 POST 200 /request-uri $UWA $LEARNING-BLOCK Brazil Rio Grande do Sul 9.10.11.12 26102 Mozilla/5.0 (Linux; Android 5.1.1; SM-G800H Build/LMY47X) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.91 Mobile Safari/537.36 https://www.yoursite.com/referrer
~~~

Com base nessas informações, você pode ajustar a sensibilidade da _rule_ set do WAF, como mencionado anteriormente, até que não ocorram mais falsos positivos. Ou mesmo solicitar para Azion a geração de _whitelist_ para sua aplicação.

---

## 5. Aprove a whitelist desejada {#aprove-a-whitelist-desejada}

Solicite ao Suporte da Azion a geração da proposta de whitelist, baseada na etapa de aprendizagem de sua aplicação.

A proposta de whitelist gerada pela Azion será inserida na plataforma e estará disponível para sua aprovação:

1.  Acesse o menu Cloud Security > WAF, ou acesse o atalho “Manage WAF” na tela inicial.
2.  Edite a _rule set_ para a qual deseja avaliar a _whitelist_.
3.  Na aba _Whitelist_, habilite todas as regras que desejar aprovar.
4.  Salve sua _rule set_.

---

## 6. Ative o bloqueio de ameaças na rule set {#ative-o-bloqueio-de-ameacas-na-rule-set}

Após monitorar o comportamento de sua aplicação e as ameaças detectadas após a etapa de aprendizagem e aprovação da _whitelist_, você deve alterar a _rule set_ para Blocking:

1.  Acesse o menu Cloud Security > WAF
2.  Edite a _rule set_ do WAF desejada.
3.  Altere o modo de Counting para Blocking.

A partir desse momento, sua aplicação estará protegida e as ameaças detectadas serão efetivamente bloqueadas.

O WAF só bloqueia as ameaças se estiver configurado em Blocking Mode.

---

Didn't find what you were looking for? [Open a support ticket.](https://tickets.azion.com/)

[Edit this page](https://github.com/aziontech/docs_en/edit/master/web-application-firewall/index.md) on GitHub.
