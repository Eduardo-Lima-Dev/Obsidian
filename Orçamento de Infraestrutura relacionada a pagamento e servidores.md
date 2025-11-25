## Focos desse documento:

1. Custos com a API de pagamento do Asaas
2. Custos com a Infraestrutura elástica na AWS para suportar entre ~200 e ~400 usuários por dia
3. Custos de publicação nas lojas de aplicativos

---

## API de Pagamento Asaas

### Pontos importantes:

- A documentação da Asaas afirma que a utilização das APIs do Asaas é totalmente gratuita, sem qualquer custo extra ou anuidade. Você paga apenas pelos serviços que utilizar. O que pode combinar com a infraestrutura elástica da AWS e fazer com que os gastos sejam limitados no início, mas fáceis de manter e adaptar a longo prazo.
- As taxas da Asaas normalmente se referem às transações (boleto, PIX, cartão) ou notificações. Dessa forma, cada serviço utilizado possui taxas e limitações que devem ser levados em consideração.
- Também há custos para notificações (WhatsApp, SMS, e-mail), o que normalmente é feito para envio de comprovantes ou verificações relacionadas ao serviço de pagamento, sendo importante observar como o fluxo vai ocorrer para poder levantar um orçamento em conjunto entre esses serviços.

### Estimativa hipotética

Supondo duas premissas para esse cálculo aproximado:

- A aplicação processa entre 200 e 400 transações por dia via boleto/PIX ou cartão.
- A aplicação envia notificações por e-mail ou SMS para cada transação.

Foram utilizados esses valores e preços disponíveis no site da empresa para utilização de seus serviços, dados de outubro de 2025:

- **Pix / boleto** — R$1,99 por transação recebida
- **Cartão de débito** — R$0,35 + 1,89% por transação recebida
- **Cartão de crédito** — R$0,49 + taxa de crédito baseada nas parcelas e no total

#### Tabela de preço das taxas de crédito

|Modalidade|Taxa|
|---|---|
|À vista|2,99%|
|2 à 6 parcelas|3,49%|
|7 à 12 parcelas|3,99%|
|13 à 21 parcelas|4,29%|

Podemos calcular três situações de base, considerando o número de transações mínimo, médio e máximo para estimar o custo diário:

|Tipo de Pagamento|200 Transações (Mínimo)|300 Transações (Médio)|400 Transações (Máximo)|
|---|---|---|---|
|Boleto / PIX|R$398,00|R$597,00|R$796,00|
|Cartão Débito|R$1.204,00|R$1.806,00|R$2.408,00|
|Crédito à vista|R$1.892,00|R$2.838,00|R$3.784,00|
|Crédito 2–6x|R$2.192,00|R$3.288,00|R$4.384,00|

### Notificações

Considerando uma notificação por transação, temos duas possibilidades:

|Notificação|200 transações|300 transações|400 transações|
|---|---|---|---|
|Email / SMS (R$0,99)|200 × 0,99 = R$198,00|300 × 0,99 = R$297,00|400 × 0,99 = R$396,00|
|WhatsApp (R$0,55)|200 × 0,55 = R$110,00|300 × 0,55 = R$165,00|400 × 0,55 = R$220,00|

### Resumo Geral

Unindo os custos de notificação com o custo por transação, podemos separar em duas tabelas, uma considerando uso de notificações por email/sms e outra considerando notificações por whatsapp.

#### Custos com Email/SMS

|Tipo de Pagamento|200 transações + Email/SMS|300 transações + Email/SMS|400 transações + Email/SMS|
|---|---|---|---|
|Boleto / PIX|398,00 + 198,00 = R$596,00|597,00 + 297,00 = R$894,00|796,00 + 396,00 = R$1.192,00|
|Cartão Débito|1.204,00 + 198,00 = R$1.402,00|1.806,00 + 297,00 = R$2.103,00|2.408,00 + 396,00 = R$2.804,00|
|Crédito à vista|1.892,00 + 198,00 = R$2.090,00|2.838,00 + 297,00 = R$3.135,00|3.784,00 + 396,00 = R$4.180,00|
|Crédito 2–6x|2.192,00 + 198,00 = R$2.390,00|3.288,00 + 297,00 = R$3.585,00|4.384,00 + 396,00 = R$4.780,00|

#### Custos com WhatsApp

|Tipo de Pagamento|200 transações + Whatsapp|300 transações + Whatsapp|400 transações + Whatsapp|
|---|---|---|---|
|Boleto / PIX|398,00 + 110,00 = R$508,00|597,00 + 165,00 = R$762,00|796,00 + 220,00 = R$1.016,00|
|Cartão Débito|1.204,00 + 110,00 = R$1.314,00|1.806,00 + 165,00 = R$1.971,00|2.408,00 + 220,00 = R$2.628,00|
|Crédito à vista|1.892,00 + 110,00 = R$2.002,00|2.838,00 + 165,00 = R$3.003,00|3.784,00 + 220,00 = R$4.004,00|
|Crédito 2–6x|2.192,00 + 110,00 = R$2.302,00|3.288,00 + 165,00 = R$3.453,00|4.384,00 + 220,00 = R$4.604,00|

### Observações finais

- A integração da API em si não tem custo de assinatura, segundo informa a Asaas.
- Se o volume for menor ou se muitos forem via PIX (sem percentual) ou boletos simples, o custo será bem menor, o que permite trabalhar com pouco custo no início e ainda oferece expansão de forma automática com o crescimento do negócio.
- Importante destacar o período de 3 meses iniciais nos quais as taxas são mais baixas e entram em valores promocionais para todos os serviços, facilitando a integração para inícios de projeto.

---

## Infraestrutura AWS

Para estimar, precisamos definir alguns parâmetros: tipo de aplicação, picos de uso, armazenamento, backups, tráfego de internet, zona/região (Brasil ou outras).

### Assumindo os seguintes parâmetros:

- **Tipo de aplicação:** API backend para app mobile, com endpoints REST/GraphQL, autenticação e notificações push.
- **Tráfego:** moderado, crescendo com o tempo (início com até 400 usuários/dia, picos até 600).
- **Região:** São Paulo (sa-east-1).
- **Banco:** relacional (RDS) com 100–200 GB de armazenamento.
- **Armazenamento adicional:** S3 para imagens, documentos ou dados temporários.
- **Infra:** elástica, com Auto Scaling de 1 a 3 instâncias conforme carga.
- **Monitoramento e logs** via CloudWatch.
- **Backups automáticos** diários.
- **Tráfego externo (egress):** até 150 GB/mês (considerando app mobile com imagens leves e JSONs frequentes).

### Custos principais a considerar

|Serviço|Descrição|Estimativa mensal (USD)|Estimativa em R$ (≈ R$6,00/USD)|
|---|---|---|---|
|Compute (ECS/Fargate ou EC2 Auto Scaling)|1–3 instâncias equivalentes a t3.medium (2 vCPU, 4 GB RAM), com auto scaling.|50–80|300–480|
|Banco de Dados (RDS – PostgreSQL/MySQL)|Instância db.t3.medium, 100–200 GB SSD, backups automáticos.|60–90|360–540|
|Armazenamento (S3, EBS)|Armazenamento de imagens/arquivos de usuários, logs e snapshots.|15–25|90–150|
|Transferência de Dados (Egress Internet)|100–150 GB/mês de saída de dados.|12–18|70–110|
|CloudWatch (monitoramento/logs)|Logs, alarmes, métricas e alertas.|10–20|60–120|
|Elastic Load Balancer (ELB)|Distribuição de tráfego entre instâncias.|15–25|90–150|
|Outros (NAT Gateway, IPs elásticos, backups extras, etc.)|Custos acessórios para conectividade e redundância.|10–20|60–120|

**Subtotal estimado:** → USD 160 a 250/mês, cerca de R$950 a R$1.500 por mês.

Com picos de uso (auto scaling ativando mais instâncias temporariamente), o custo pode subir até ~USD 300 (R$1.800).

### Elasticidade e comportamento sob carga

- O Auto Scaling permitirá subir até 3 instâncias EC2/Fargate em momentos de pico (>600 usuários simultâneos).
- Em horários de baixa (ex: madrugada), o sistema reduz para 1 instância ativa, diminuindo o custo base.
- O banco de dados pode ser configurado com Read Replica futura, caso o número de requisições aumente.
- Se o tráfego crescer muito, vale considerar cache com ElastiCache (Redis) — o que adicionaria cerca de R$200 a R$300 por mês, mas melhora o desempenho.

### Cenários Estimados

|Cenário|Descrição|Estimativa Total (R$/mês)|
|---|---|---|
|Infra mínima/modesta|1 instância base, carga leve, backups e logs simples.|R$950 a R$1.200|
|Com margem de crescimento|Auto Scaling ativo, tráfego 400–600 usuários/dia, logs detalhados.|R$1.200 a R$1.800|
|Alta disponibilidade / crescimento acelerado|Múltiplas zonas, redundância de banco, cache Redis, backup estendido.|R$2.000 a R$2.500+|

---

## Publicação de Apps nas Lojas

### Publicação de Apps na Play Store

- Para publicar aplicativos na Google Play Store, é necessário pagar uma taxa única de registro de US$ 25 ao criar a conta de desenvolvedor no Google Play Console.
- Assinaturas têm uma taxa de serviço fixa de 15%, independentemente do volume de receita anual.

### Publicação de Apps na Apple Store

- Para publicar aplicativos na Apple App Store, é necessário pagar uma taxa anual de US$ 99 para se inscrever no Apple Developer Program.
- Comissão sobre vendas e compras no app: A Apple cobra uma taxa padrão de 30% sobre o preço de venda de apps pagos e compras internas de bens e serviços digitais via sistema de In-App Purchase (IAP).

|Item|Valor estimado inicial|
|---|---|
|Registro Google Play|US$ 25 (único)|
|Registro Apple Store|US$ 99 (anual)|

---

## Resumo Estimativo Final

|Item|Valor estimado|
|---|---|
|Infra AWS (API elástica, RDS, storage, logs)|R$950 a R$1.800 por mês|
|Com alta disponibilidade e picos sustentados|R$2.000 a R$2.500 por mês|
|Registro Google Play|US$ 25 (pagamento único)|
|Registro Apple Store|US$ 99 por ano|
|**Total inicial recomendado (mensal)**|**~R$1.200 a R$1.500 por mês**|