# Rules Engine for Edge Firewall

Você pode transferir parte da lógica das regras de negócio de sua aplicação para o Edge Node da Azion e expandir essas funcionalidades com o produto Application Acceleration. Dessa forma, você constrói uma arquitetura que entrega performance para seus usuários consumindo menos recursos e processamento em sua origem.

O Rules Engine foi elaborado para permitir a codificação de uma lógica de execução condicional de comportamentos e ações diretamente no Edge Node da Azion, mais próximo de seus usuários e, portanto, com melhor performance e taxa de transferência para sua aplicação.

> 1. *[Como funciona?](#como-funciona)*
> 2. *[Regras](#regras)*

---

## 1. Como funciona? {#como-funciona}

Cada requisição de seus usuários para sua aplicação é processada em duas fases sequenciais:

1.  *Request Phase*
2.  *Reponse Phase*

Em cada fase de processamento, você pode definir um conjunto de regras para manipular a requisição de acordo com as necessidades de sua aplicação ou negócio. As regras são compostas por critérios, que representam as condições para execução da regra, e por comportamentos, que representam as ações que precisam ser executadas.

O processamento das fases é sequencial e você pode utilizar como critérios um poderoso conjunto de variáveis e operadores de comparação. Caso as condições sejam atendidas, os comportamentos de cada regra são executados até que todas as regras sejam processadas ou se encontre uma regra com um comportamento finalizador no caminho (_Deny_, _Redirect To_, _Deliver_).

---

## 2. Regras {#regras}

As regras são compostas por ***Criteria***, que determina o conjunto de condições que precisam ser atendidas para a execução dos ***Behaviors***.

**Critérios**

As regras são compostas por ***Criteria***, que determina o conjunto de condições que precisam ser atendidas para a execução dos ***Behaviors***.

**Variáveis**

| Criteria | Descrição | Requisitos |
|----------|-----------|------------|
| Header Accept | Cabeçalho que informa quais tipos de conteúdo, expressos como *MIME types*, o cliente é capaz de entender.| Web Application Firewall |
| Header Accept-Encoding | Cabeçalho que informa sobre o algoritmo de codificação, geralmente um algoritmo de compressão.| Web Application Firewall |
| Header Accept-Language | Cabeçalho que Informa ao sobre a linguagem esperada. | Web Application Firewall |
| Header Cookie | Cabeçalho que contém os Cookies HTTP armazenados que foram previamente enviados pelo servidor com o cabeçalho *Set-Cookie*. | Web Application Firewall |
| Header Origin | Cabeçalho que informa de onde uma request se origina. Não inclui nenhuma informação de caminho, apenas o nome do servidor. | Web Application Firewall |
| Header Referer | Cabeçalho que informa o endereço da página web anterior a partir da qual um link para a página solicitada no momento foi seguido. | Web Application Firewall |
| Header User Agent | Cabeçalho com uma sequência característica que permite que servidores identifiquem o aplicativo, sistema operacional, fornecedor e/ou versão do device. | Web Application Firewall |
| Hostname | Em ordem de precedência: o *hostname* da linha de requisição, ou o valor do campo de cabeçalho *Host* da requisição, ou o nome do servidor atendendo a requisição. | - |
| Network | O endereço IP do cliente que está realizando a requisição HTTP. ASN e *Country* também são obtidos a partir do endereço IP do cliente. | Network Layer Protection |
| Request Args | Todos os argumentos enviados pelo usuário na linha de requisição (*query string*). | Web Application Firewall |
| Request Method| O método HTTP da requisição. Por exemplo: GET, POST, PUT etc. | - |
| Request URI | A URI da requisição. | Web Application Firewall |
| *Scheme* | O scheme da requisição: http ou https. | - |


**Operadores de Comparação**

A condição para execução de um regra deve ser a comparação de uma variável com um argumento. Os operadores de comparação são:

| Operador | Descrição | Argumento | 
|----------|-----------|-----------|
| is equal | O valor da variável é igual ao argumento, comparado caracter a caracter. | string |
| is not equal | O valor da variável não é exatamente igual ao argumento. | string |
| starts with | O valor da variável inicia pelo argumento. | string |
| does not start with | O valor da variável não inicia pelo argumento. | string |
| matches | O valor da variável coincide com a expressão regular informada como argumento. | regular expression |
| does not match | O valor da variável não coincide com a expressão regular informada como argumento. | regular expression |
| exists | A variável tem valor definido. Por exemplo _${arg_search}_ existe se foi enviado um argumento _search_ na query string da requisição. | - |
| does not exist |A variável não tem valor definido. Por exemplo _${arg_search}_ não existe se não foi enviado um argumento _search_ na query string da requisição. | - |

**Operadores Lógicos**

Múltiplas condições podem ser definidas por meio dos operadores lógicos **and** e **or**. O operador and tem precedência implícita sobre o operador or.

Se necessária precedência explícita, você pode adicionar múltiplos grupos de critérios sob a lógica and.

**Comportamentos**

Em Behavior você adiciona os comportamentos que deseja executar, caso as condições da regra sejam satisfeitas.

| Behavior | Descrição | Requisitos |
|----------|-----------|------------|     
| Deny | 403 Forbidden| Network Layer Protection <br> Web Application Firewall |      
| Drop | Close Without Response| Network Layer Protection <br> Web Application Firewall|
| Set Rate Limit | Para que seja configurado um Rate Limit, aparecerão os  campos adicionais Average Rate Limit (req/s) e Maximum burst size, além da opção de seleção de restrição por endereço IP ou Global| Network Layer Protection <br> Web Application Firewall|
| Set WAF Rule Set | Atribui a Rule Set de WAF que deve ser utilizada na requisição. As políticas de WAF devem ser previamente configuradas no menu Edge Services > WAF.| Web Application Firewall |
| Run Function | Ativa a compressão de dados Gzip, caso suportada pelo browser do usuário.| Edge Functions |

---

Não encontrou o que procurava? [Abra um ticket.](https://tickets.azion.com/)