# :star2: Bem-vindo à Payments Analytics! :star2:


## :bulb: Sobre
A missão do nosso repositório é centralizar todas as queries de análise de resultados que utilizamos no BigQuery e RedShift. Nosso objetivo é criar um catálogo abrangente de informações e queries prontas, especificamente voltadas a payments.

![image](https://github.com/payments-analytics/.github/assets/154369193/1bac58eb-51c7-41e3-9d67-041031b6fdd0)

## :rocket: Nossos Projetos

- **[pay-gestao-negocio-analytics-queries](https://github.com/payments-analytics/pay-gestao-negocio-analytics-queries)**:
  - :bar_chart: Queries rotineiras para consultas no BigQuery, Metabase e Redshift.
- **[pay-gestao-negocio-looker-queries](https://github.com/payments-analytics/pay-gestao-negocio-looker-queries)**
  - :chart_with_upwards_trend: Queries para dashboards do Looker Studio.
- **[pay-gestao-negocio-scheduled-queries](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries)**
  - 🗓 Queries agendadas do Dataset `payments_analytics` no BigQuery.
- **[pay-gestao-scripts](https://github.com/payments-analytics/pay-gestao-scripts)**
  - :scroll: Scripts para o dia a dia do time.

## :compass: Guia de Análise  
Este guia é focado em ilustrar como realizar consultas fundamentais e identificar as tabelas chave no dataset de pagamentos para uma análise dos produtos. Vamos explorar as principais tabelas e como utilizá-las em consultas estratégicas para obter insights.

### Dataset Payments Analytics 
Scripts SQL que são executados diariamente para criar e atualizar as tabelas mais importantes do conjunto de dados payments_analytics

#### Índice
  - [Base Ativa](#base-ativa)
  - [Boleto](#boleto)
  - [DCC](#dcc)
  - [GMV](#gmv)
  - [Link](#link)
  - [Parcelamento](#parcelamento)
  - [Pix Pos](#pix-pos)
  - [Receita](#receita)
  - [Smart Pos](#smart-pos)
  - [Tap on Phone](#tap-on-phone)
  - [TPV](#tpv)
  - [Whatsapp Pay](#whatsapp-pay)
  - [Budget 2024](#budget-2024)

#### Base Ativa

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| pagarme_active_base_monthly_results         | 20:00                  | [Query](./consultas_agendadas/base_ativa/pagarme_active_base_monthly_results.sql) | Base ativa pagarme    | • Base Ativa  |
| payments_active_base_monthly_results        | 21:00                  | [Query](./consultas_agendadas/base_ativa/payments_active_base_monthly_results.sql) | Atividade do Cliente todas as marcas (inativa) |  • Base Ativa  <br> • Churn <br> • Novos Ativos <br> • Reativados|
| payments_active_base_monthly_results_v2     | 21:00                  | [Query](./consultas_agendadas/base_ativa/payments_active_base_monthly_results_v2.sql) | Atividade do Cliente todas as marcas  | • Base Ativa  <br> • Churn <br> • Novos Ativos <br> • Reativados |

#### Boleto

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| boleto_monthly_results         | 21:00                  | [Query](./consultas_agendadas/boleto/boleto_monthly_results.sql) | Principais KPIs Boleto Stone| • transactions  <br> • issued boleto <br> • charged boleto <br> • gross revenue <br> • net revenue <br> • active clients e accounts <br> • issued active account <br> • settled active account <br> • revenue active account <br> • new active accounts e gmv <br> • churn accounts e gmv <br> • migrated accounts e gmv <br> • reactivated accounts e gmv |
| boleto_monthly_results         | 21:00                  | [Query](./consultas_agendadas/boleto/boleto_monthly_results.sql) |Principais KPIs Boleto Stone por Tier| • transactions  <br> • issued boleto <br> • charged boleto <br> • gross revenue <br> • net revenue <br> • active clients e accounts <br> • issued active account <br> • settled active account <br> • revenue active account <br> • new active accounts e gmv <br> • churn accounts e gmv <br> • migrated accounts e gmv <br> • reactivated accounts e gmv |

#### DCC

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| dcc_stone_monthly_results         | 21:16                  | [Query](./consultas_agendadas/dcc/dcc_stone_monthly_results.sql) | Resultado DCC Stone| • Contagem distinta de Clientes <br> • Receita estimada |

#### GMV

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| payments_gmv_monthly_results         | 21:00                  | [Query](./consultas_agendadas/gmv/payments_gmv_monthly_results.sql) | Resultado do GMV referente aos principais produtos| • Boleto Stone <br> • Boleto PSP SMB e KA <br> • Boleto GTW SMB e KA <br> • TPV Pagarme SMB e KA <br> • Pix Pagarme SMB e KA  <br> • Gtw exStone Pagarme SMB	e Pagarme KA  <br> • TPV PP, Ton, Stone, Link Stone, Link Ton, Tap Ton e Total <br> • Pix Pagarme SMB e KA <br> • Pix POS Ton e Stone <br> • GMV Total <br> • Van_Stone|


#### Link

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| dim_payment_link_client         | 20:30                  | [Query](./consultas_agendadas/link/dim_payment_link_client.sql) | Informações dos clientes link| - |
| payment_link_stone_monthly_results         | 21:10                  | [Query](./consultas_agendadas/link/payment_link_stone_monthly_results.sql) | Resultado Link Stone | • clientes ativos <br> • warranty rate clients • active_clients <br> • novos clientes  <br> • churn <br> • reativados  <br> • Dias até ativação <br> • tpv <br> • churned tpv <br> • tpv reativado <br> • receita netmdr <br> • receita netmdr liquida  <br> • prepayment active clients <br> • receita bruta rav <br> • receita liquida rav <br> • receita liquida transacional <br> • tpv medio por cliente  <br> • receita net cof medio por cliente |
| payment_link_stone_tiered_monthly_results         | 21:10                  | [Query](./consultas_agendadas/link/payment_link_stone_tiered_monthly_results.sql) |Resultado Link Stone por tier| • clientes ativos <br> • warranty rate clients • Base Ativa  <br> • Churn <br> • Novos Ativos <br> • Reativados <br> • Dias até ativação <br> • tpv <br> • churned tpv <br> • tpv reativado <br> • receita netmdr <br> • receita netmdr liquida  <br> • prepayment active clients <br> • receita bruta rav <br> • receita liquida rav <br> • receita liquida transacional <br> • tpv medio por cliente  <br> • receita net cof medio por cliente |
| payment_link_ton_monthly_results         | 21:15                  | [Query](./consultas_agendadas/link/payment_link_ton_monthly_results.sql) | Resultado Link Ton| • Base Ativa  <br> • Churn <br> • Novos Ativos <br> • Reativados <br> • TPV Reativados  <br> • Clientes Migrados <br> • TPV Clientes Migrados <br> • TPV <br> • Transactions <br> • TPV antecipado <br> • dx <br> • Receita MDR <br> • Receita MDR Liquida <br> • Receita RAV Liquida <br> • Receita RAV  <br> • Receita Transacional <br> • Receita Líquida Transacional <br> • COF <br> • Receita Net COF
| payment_link_ton_tiered_monthly_results         | 21:18                  | [Query](./consultas_agendadas/link/payment_link_ton_tiered_monthly_results.sql) | Resultado Link Ton por tier |• Base Ativa  <br> • Churn <br> • Novos Ativos <br> • Reativados <br> • TPV Reativados  <br> • Clientes Migrados <br> • TPV Clientes Migrados <br> • TPV <br> • Transactions <br> • TPV antecipado <br> • dx <br> • Receita MDR <br> • Receita MDR Liquida <br> • Receita RAV Liquida <br> • Receita RAV  <br> • Receita Transacional <br> • Receita Líquida Transacional <br> • COF <br> • Receita Net COF

#### Parcelamento

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| parcelamento_stone         | 21:00                  | [Query](./consultas_agendadas/parcelamento/parcelamento_stone.sql) | Resultado do Tpv gerado por quantidade de parcelas (Stone)| • installment name <br> • tpv|

#### Pix Pos

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| pix_pos_stone_monthly_results_v2         | 21:03                  | [Query](./consultas_agendadas/pix_pos/pix_pos_stone_monthly_results_v2.sql) | Resultado PIX POS Stone | • gmv <br> • transactions <br> • fee free gmv <br> • fee free transactions <br> • charged gmv <br> • charged transactions <br> • gross revenue <br> • net revenue <br> • active clients <br> • fee free active account <br> • new active accounts <br> • new active gmv <br> • churn accounts <br> • churned gmv <br> • migrated accounts <br> •  migrated gmv <br> • reactivated accounts <br> • reactivated gmv|
| pix_pos_stone_tiered_monthly_results         | 21:30                  | [Query](./consultas_agendadas/pix_pos/pix_pos_stone_tiered_monthly_results.sql) |  Resultado PIX POS Stone por tier  )| • gmv <br> • transactions <br> • fee free gmv <br> • fee free transactions <br> • charged gmv <br> • charged transactions <br> • gross revenue <br> • net revenue <br> • active clients <br> • fee free active account <br> • new active accounts <br> • new active gmv <br> • churn accounts <br> • churned gmv <br> • migrated accounts <br> •  migrated gmv <br> • reactivated accounts <br> • reactivated gmv|
| pix_pos_ton_monthly_results_v2         | 21:03                  | [Query](./consultas_agendadas/pix_pos/pix_pos_ton_monthly_results_v2.sql) | Resultado PIX POS Ton | • gmv <br> • transactions <br> • fee free gmv <br> • fee free transactions <br> • charged gmv <br> • charged transactions <br> • gross revenue <br> • net revenue <br> • active clients <br> • fee free active account <br> • new active accounts <br> • new active gmv <br> • churn accounts <br> • churned gmv <br> • migrated accounts <br> •  migrated gmv <br> • reactivated accounts <br> • reactivated gmv|
| pix_pos_ton_tiered_monthly_results         | 21:12                  | [Query](./consultas_agendadas/pix_pos/pix_pos_ton_tiered_monthly_results.sql) |  Resultado PIX POS Ton por tier|• gmv <br> • transactions <br> • fee free gmv <br> • fee free transactions <br> • charged gmv <br> • charged transactions <br> • gross revenue <br> • net revenue <br> • active clients <br> • fee free active account <br> • new active accounts <br> • new active gmv <br> • churn accounts <br> • churned gmv <br> • migrated accounts <br> •  migrated gmv <br> • reactivated accounts <br> • reactivated gmv|

#### Receita

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Explicação da Query   |
|---------------------------------------------|------------------------|-----------------------|-----------------------|
| pagarme_revenue_daily_results         | 21:00                  | [Query](./consultas_agendadas/receita/pagarme_revenue_daily_results.sql) | Principais receitas (Pagarme) - dia |
| pagarme_revenue_results         | 21:00                  | [Query](./consultas_agendadas/receita/pagarme_revenue_results.sql) | Principais receitas (Pagarme) - mês |
| payments_net_cof_revenue         | 02:00                  | [Query](./consultas_agendadas/receita/payments_net_cof_revenue.sql) | Receita net cof (Payments) - mês |
| payments_net_cof_revenue_daily_results         | 21:00                  | [Query](./consultas_agendadas/receita/payments_net_cof_revenue_daily_results.sql) | Receita net cof (Payments) - dia|
| payments_net_cof_revenue_monthly_results         | 00:10                  | [Query](./consultas_agendadas/receita/payments_net_cof_revenue_monthly_results.sql) | Principais receitas (Payments) - mês|
| temp_payments_revenue_monthly_results_edit_pagarme         | 21:00                  | [Query](./consultas_agendadas/receita/temp_payments_revenue_monthly_results_edit_pagarme.sql) | Temp - Principais receitas (Pagarme)|

#### Smart Pos

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Explicação da Query   |
|---------------------------------------------|------------------------|-----------------------|-----------------------|
| smart_pos_ton_monthly_results         | 21:00                  | [Query](./consultas_agendadas/smart_pos/smart_pos_ton_monthly_results.sql) | Resultado dos principais KPIS|

#### Tap on Phone

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Explicação da Query   |
|---------------------------------------------|------------------------|-----------------------|-----------------------|
| tap_on_phone_ton_monthly_results        | 21:00                  | [Query](./consultas_agendadas/tap_phone/tap_on_phone_ton_monthly_results.sql) | Resultado dos principais KPIS|
| tap_on_phone_ton_tiered_monthly_results         | 21:15                  | [Query](./consultas_agendadas/tap_phone/tap_on_phone_ton_tiered_monthly_results.sql) | Resultado dos principais KPIS por tier|

#### Tpv

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Explicação da Query   |
|---------------------------------------------|------------------------|-----------------------|-----------------------|
| payments_mtd_pmtd_pytd         | 22:00                  | [Query](./consultas_agendadas/tpv/payments_mtd_pmtd_pytd.sql) | Resultado do TPV - dia|

#### Whatsapp Pay

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Explicação da Query   |
|---------------------------------------------|------------------------|-----------------------|-----------------------|
| whatsapp_pay_stone_monthly_results         | 22:00                  | [Query](./consultas_agendadas/whatsapp_pay/whatsapp_pay_stone_monthly_results.sql) | Resultado dos principais KPIS|

#### Liquidação Diaria

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Explicação da Query   |
|---------------------------------------------|------------------------|-----------------------|-----------------------|
| dim_client_liquidacao_diaria         | 20:00                  | [Query](./consultas_agendadas/liquidacao_diaria/dim_client_liquidacao.sql) | Informações por documento|
| temp_d1_d0_stone_tiered_monthly_results         | 20:00                  | [Query](./consultas_agendadas/liquidacao_diaria/temp_d1_d0_stone_tiered_monthly_results.sql) | Resultado dos principais KPIS|
|**Tabela**|**Produto**|**Indicadores**|**Query Tabela**|
|----------|-----------|---------------|----------------|
|`payments_analytics.pagarme_active_base_monthly_results`| Pagarme | • Base Ativa | [Fonte](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/base-ativa/pagarme_active_base_monthly_results.sql) |
|`payments_analytics.payments_active_base_monthly_results_v2`| • Stone <br> • Pagarme <br> • Ton | • Base Ativa  <br> • Churn <br> • Novos Ativos <br> • Reativados| [Fonte](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/base-ativa/payments_active_base_monthly_results_v2.sql) |
|`payments_analytics.boleto_monthly_results` | • Boleto Stone | • transactions  <br> • issued boleto <br> • charged boleto <br> • gross revenue <br> • net revenue <br> • active clients e accounts <br> • issued active account <br> • settled active account <br> • revenue active account <br> • new active accounts e gmv <br> • churn accounts e gmv <br> • migrated accounts e gmv <br> • reactivated accounts e gmv | [Fonte](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/boleto/boleto_monthly_results.sql)
|`payments_analytics.boleto_tiered_monthly_results`| • Boleto Stone por Tier |  • transactions  <br> • issued boleto <br> • charged boleto <br> • gross revenue <br> • net revenue <br> • active clients e accounts <br> • issued active account <br> • settled active account <br> • revenue active account <br> • new active accounts e gmv <br> • churn accounts e gmv <br> • migrated accounts e gmv <br> • reactivated - accounts e gmv | [Fonte](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/boleto/boleto_tiered_monthly_results.sql) |
|`payments_analytics.boleto_tiered_monthly_results`| • Boleto Stone por Tier |  • transactions  <br> • issued boleto <br> • charged boleto <br> • gross revenue <br> • net revenue <br> • active clients e accounts <br> • issued active account <br> • settled active account <br> • revenue active account <br> • new active accounts e gmv <br> • churn accounts e gmv <br> • migrated accounts e gmv <br> • reactivated  accounts e gmv | [Fonte](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/boleto/boleto_tiered_monthly_results.sql) |
|`payments_analytics.dcc_stone_monthly_results`| • DCC Stone | • Contagem distinta de Clientes <br> • Receita estimada |  [Fonte](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/dcc/dcc_stone_monthly_results.sql) |
|`payments_analytics.payments_gmv_monthly_results`| • Boleto Stone <br> • Boleto PSP SMB e KA <br> • Boleto GTW SMB e KA

#### 1.RAV

#### :bulb: 1.1 Casos de uso
- Analisar a receita líquida RAV de Link Stone nos últimos 6 meses por Segmento ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/link/payment_link_stone_tiered_monthly_results.sql)):
``` sql
SELECT
  reference_month
  , CASE
      WHEN tier_tpv IN ('A. 0-7k','B. 7-15k') THEN 'Micro'
      when tier_tpv IN ('C. 15-30k','D. 30-50k','E. 50-100k','F. 100k+') THEN 'SMB'
      ELSE null
   END AS Segmento
  , SUM(receita_liquida_rav) AS receita_liquida
FROM dataplatform-prd.payments_analytics.payment_link_ton_tiered_monthly_results
WHERE 1=1
  reference_month >= DATE_SUB(CURRENT_DATE(), INTERVAL 6 MONTH)
GROUP BY 1,2
```

- Analisar a receita RAV mensal do produto TAP TON e determinar a participação em relação a receita net cof ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/tap_phone/tap_on_phone_ton_monthly_results.sql)):
``` sql
SELECT
  reference_month
  , SUM(receita_liquida_rav) AS receita_liquida,
  , SUM(receita_net_cof) AS receita_net_cof,
  , SUM(receita_liquida_rav) / NULLIF(SUM(receita_net_cof), 0) AS percentual_sobre_net_cof
FROM
  dataplatform-prd.payments_analytics.tap_on_phone_ton_monthly_results
GROUP BY
  reference_month

```

#### 2.Boleto

#### :bulb: 2.1 Casos de uso
- Analisar a eficiência na conversão de boletos emitidos em boletos liquidados por mês ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/boleto/boleto_monthly_results.sql)):
``` sql
SELECT
  reference_month
  , SUM (transactions)/ SUM(issued_boleto) AS taxa_conversao
FROM dataplatform-prd.payments_analytics.boleto_tiered_monthly_results
GROUP BY 1
```
- Analisar a variação de boletos emitidos em 2022 vs 2023 (mês a mês) ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/boleto/boleto_monthly_results.sql)):
``` sql
SELECT
    EXTRACT(MONTH FROM reference_month) AS month
    , SUM(CASE WHEN EXTRACT(YEAR FROM reference_month) = 2022 THEN issued_boleto ELSE 0 END) AS issued_boleto_2022
    , SUM(CASE WHEN EXTRACT(YEAR FROM reference_month) = 2023 THEN issued_boleto ELSE 0 END) AS issued_boleto_2023
FROM dataplatform-prd.payments_analytics.boleto_tiered_monthly_results
WHERE 1=1
  AND EXTRACT(YEAR FROM reference_month) IN (2022, 2023)
GROUP BY 1
ORDER BY 1
```
- Analisar o net tpv de boletos PSP e Gateway ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/gmv/payments_gmv_monthly_results.sql)):
``` sql
SELECT
    mes
    , SUM(Boleto_PSP_SMB) + SUM(Boleto_PSP_KA) AS boleto_psp
    , SUM(Boleto_Gtw_SMB) + SUM(Boleto_Gtw_KA) AS boleto_gtw
FROM dataplatform-prd.payments_analytics.payments_gmv_monthly_results
GROUP BY 1
ORDER BY 1;
```
#### 3.Pix

#### :bulb: 3.1 Casos de uso
- Analisar o valor de receita pix de Stone e Ton ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/receita/payments_net_cof_revenue.sql)):
``` sql
SELECT
    reference_month
    , SUM(stone_pix_pos_revenue) AS receita_pix_stone
    , SUM(ton_pix_pos_revenue) AS receita_pix_ton
FROM dataplatform-prd.payments_analytics.payments_net_cof_revenue
GROUP BY 1
```
- Analisar os valores das transações e o volume de transações ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/pix_pos/pix_pos_stone_monthly_results.sql)):
``` sql
SELECT
    reference_month
    , SUM(pix_in_dynamic_pos_trx) AS qtd_transacoes_pix
    , SUM(pix_in_dynamic_pos_tpv) AS valor_transacoes_pix
FROM dataplatform-prd.payments_analytics.pix_pos_stone_monthly_results
GROUP BY 1
```

#### 4.Link

#### :bulb: 4.1 Casos de uso
- Analisar os valores de TPV Link Ton e Stone ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/gmv/payments_gmv_monthly_results.sql)):
``` sql
SELECT
    mes
    , SUM(TPV_Link_Ton) AS TPV_Link_Ton
    , SUM(TPV_Link_Stone) AS TPV_Link_Stone
FROM dataplatform-prd.payments_analytics.payments_gmv_monthly_results
GROUP BY 1
```

#### 5.Tap on Phone

#### :bulb: 5.1 Casos de uso
- Analisar a base ativa de Tap on Phone ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/tap_phone/tap_on_phone_ton_tiered_monthly_results.sql)):
``` sql
SELECT
    reference_month
    , SUM(active_clients) AS base_ativa_tap
FROM dataplatform-prd.payments_analytics.tap_on_phone_ton_monthly_results
GROUP BY 1
```
#### 6.DCC 

#### :bulb: 6.1 Casos de uso

- Analisar receita DCC ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/dcc/dcc_stone_monthly_results.sql))::
``` sql
SELECT
    reference_month
    , SUM(estimated_revenue) AS estimated_revenue
FROM dataplatform-prd.payments_analytics.dcc_stone_monthly_results
GROUP BY 1
```

#### 7.Adesão

#### :bulb: 7.1 Casos de uso
- Analisar receita de adesão partner program ([*Fonte*](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries/blob/main/consultas_agendadas/receita/payments_net_cof_revenue_monthly_results.sql)):
``` sql
SELECT
  reference_month
  , SUM(partner_program_adesao_net_revenue) AS receita_adesao_partner_program
FROM dataplatform-prd.payments_analytics.payments_net_cof_revenue_monthly_results
GROUP BY 1
```


### Payments Analytics - Budget 2024
- Base Ativa:
[`dataplatform-prd.payments_analytics.test_budget_base_ativa_payments`](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/budget-2024/budget_base_ativa_payments.sql)

| **Coluna** | **Tipo**      | **Descrição**   |
|--------------------|------------------------------------|----------------------------------------------|
|• reference_month|`DATE` | 	Mês de referência do budget|
|• company |`STRING` | Marca associada:<br> • *STONE* <br> • *PAGARME* <br> • *TON* |
|• canal |`STRING` | Canal associado:<br> • *TODOS* <br> • *SUBADQUIRENTES* <br> • *MARKETPLACES* <br> • *PARTNER PROGRAM* <br> •	*KEY ACCOUNTS* <br> • *PAGARME SMB* |
|• segmento |`STRING` | Segmento associado:<br> • *SMALL* <br> • *MICRO* <br> • *MEDIUM* <br> • *KA* <br> •	*DIGITAL_SMB* |
|• budget_ba_30d |`FLOAT` | Budget de clientes ativos |
|• budget_churn_30d |`FLOAT` | Budget de clientes churn |
|• budget_returning_30d |`FLOAT` | Budget de clientes reativados |
|• budget_new_actives_30d|`FLOAT` | Budget de novos ativos |

- Receita:
[`dataplatform-prd.payments_analytics.test_budget_receita_payments`](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/budget-2024/budget_receita_payments.sql)

| **Coluna** | **Tipo**      | **Descrição**   |
|--------------------|------------------------------------|----------------------------------------------|
|• reference_month|`DATE` | 	Mês de referência do budget|
|• company |`STRING` | Marca associada:<br> • *STONE* <br> • *PAGARME* <br> • *TON* |
|• canal |`STRING` | Canal associado:<br> • *TODOS* <br> • *SUBADQUIRENTES* <br> • *MARKETPLACES* <br> • *PARTNER PROGRAM* <br> •	*KEY ACCOUNTS* <br> • *PAGARME SMB* |
|• segmento |`STRING` | Segmento associado:<br> • *SMALL* <br> • *MICRO* <br> • *MEDIUM* <br> • *KA* <br> •	*DIGITAL_SMB* |
|• receita_mdr_liquida |`FLOAT` | Budget receita líquida MDR |
|• receita_rav_liquida |`FLOAT` | Budget receita líquida RAV |
|• receita_liquida_adesao |`FLOAT` | Budget receita líquida de adesão|
|• receita_liquida_aluguel|`FLOAT` | Budget receita líquida de aluguel |
|• receita_liquida_pix|`FLOAT` | Budget receita líquida de pix |
|• receita_liquida_boleto|`FLOAT` | Budget receita líquida de boleto |
|• receita_liquida_voucher|`FLOAT` | Budget receita líquida de voucher |
|• receita_liquida_gateway|`FLOAT` | Budget receita líquida de gateway |
|• receita_liquida_antifraude|`FLOAT` | Budget receita líquida de antifraude |
|• receita_liquida_outras_receitas|`FLOAT` | Budget receita líquida outras receitas |

- TPV:
[`dataplatform-prd.payments_analytics.test_budget_tpv_payments`](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-scheduled-queries/budget-2024/budget_tpv_payments.sql)

| **Coluna** | **Tipo**      | **Descrição**   |
|--------------------|------------------------------------|----------------------------------------------|
|• reference_month|`DATE` | 	Mês de referência do budget|
|• budget_tpv_cartao_stone_smb |`FLOAT` |Budget de tpv cartão **stone smb**|
|• budget_tpv_cartao_stone_micro |`FLOAT` |Budget de tpv cartão **stone micro**|
|• tpv_stone |`FLOAT` |Soma do tpv cartão **stone micro e smb**|
|• budget_tpv_cartao_ton_smb |`FLOAT` |Budget de tpv cartão **ton smb**|
|• budget_tpv_cartao_ton_micro |`FLOAT` |Budget de tpv cartão **ton micro**|
|• tpv_ton |`FLOAT` |Soma do tpv cartão **ton micro e smb**|
|• budget_tpv_cartao_pagarme_smb|`FLOAT` |Budget de tpv cartão **pagarme smb**|
|• budget_tpv_cartao_pagarme_lacc |`FLOAT` |Budget de tpv cartão **pagarme lacc**|
|• budget_tpv_cartao_pagarme_ka |`FLOAT` |Budget de tpv cartão **pagarme ka**|
|• budget_tpv_cartao_pagarme_pp |`FLOAT` |Budget de tpv cartão **pagarme pp**|
|• tpv_pagarme |`FLOAT` |Soma do tpv cartão **pagarme smb, lacc, ka e pp**|

#### :bulb: [Consolidação Budget 2024](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/budget/budget_2024.sql)

### Índice Payments Analytics - Produtos x Indicadores 

- Link Stone:
  
|**KPI**|**Descrição**|**Dimensões**|
|-------|-------------|-------------|


- Boleto:
  
|**KPI**|**Descrição**|**Dimensões**|
|-------|-------------|-------------|
|[active_accounts](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Contagem das account_id cujos boletos emitidos na conta Stone foram liquidados e a soma desses boletos liquidados por mês foi maior que 0| • Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[active_clients](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Contagem dos documentos cujos boletos emitidos na conta Stone foram liquidados e a soma desses boletos liquidados por mês foi maior que 0| • Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[new_active_accounts](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Contagem das account_id com gmv>0 pela primeira vez|• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[churn_accounts](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Contagem das account_id com status churn |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[migrated_accounts](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Contagem das account_id migrados |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[reactivated_accounts](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Contagem das account_id reativados |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[gmv](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Soma dos valores dos boletos emitidos na conta Stone que foram liquidadoss |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[new_active_gmv](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|GMV dos novos ativos |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[churned_gmv](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|GMV dos churn |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[reactivated_gmv](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|GMV dos reativados |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[migrated_gmv](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|GMV dos migrados |• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[transactions](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Contagem de boletos emitidos na conta Stone que foram liquidados|• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[gross_revenue](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Receita gerada pela cobrança de tarifa sobre boletos emitidos na conta Stone e liquidados|• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|
|[net_revenue](https://github.com/stone-payments/payments-analytics/blob/main/pay-gestao-negocio-analytics-queries/boleto/boleto_monthly_uf_document.sql)|Gross value aplicado imposto|• Mês: `reference_month` <br><br> • UF: `UF` <br><br> • Documento: `owner_document`|




## :mailbox_with_mail: Contato

Para falar conosco, nossas portas (virtuais) estão sempre abertas:

- :e-mail: E-mail [Duda](mailto:maria.mota@stone.com.br) | [Picotti](mailto:matheus.picotti@stone.com.br)
- :speech_balloon: Slack  [Duda](https://stonepgto.slack.com/team/U063SSKP4J3) | [Picotti](https://stonepgto.slack.com/team/U0684GLJL12)
