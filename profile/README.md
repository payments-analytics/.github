# :star2: Bem-vindo à Payments Analytics! :star2:


## :bulb: Sobre
A missão do nosso repositório é centralizar todas as queries de análise de resultados que utilizamos no BigQuery e RedShift. Nosso objetivo é criar um catálogo abrangente de informações e queries prontas, especificamente voltadas a payments.

![image](https://github.com/payments-analytics/.github/assets/154369193/1bac58eb-51c7-41e3-9d67-041031b6fdd0)

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

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| pagarme_revenue_daily_results         | 21:00                  | [Query](./consultas_agendadas/receita/pagarme_revenue_daily_results.sql) | Receitas pagarme por dia | • tpv <br> • tpv antecipado <br> • receita liquida <br> • receita trx liquida <br> • receita rav liquida <br> • receita mdr liquida <br> • receita aluguel liquida <br> • receita adesao <br> • cof <br> • outras receitas liq <br> • receita antifraud <br> • receita boleto <br> • receita boleto refund <br> • receita fraud coverage <br> • receita gateway <br> • receita onboarding <br> • receita pix <br> • receita pos <br> • receita set up <br> • receita transfer |
| pagarme_revenue_results         | 21:00                  | [Query](./consultas_agendadas/receita/pagarme_revenue_results.sql) | Principais receitas pagarme por mês | • tpv <br> • tpv antecipado <br> • receita liquida <br> • receita trx liquida <br> • receita rav liquida <br> • receita mdr liquida <br> • receita aluguel liquida <br> • receita adesao <br> • cof <br> • outras receitas liq <br> • receita antifraud <br> • receita boleto <br> • receita boleto refund <br> • receita fraud coverage <br> • receita gateway <br> • receita onboarding <br> • receita pix <br> • receita pos <br> • receita set up <br> • receita transfer
| payments_net_cof_revenue         | 02:00                  | [Query](./consultas_agendadas/receita/payments_net_cof_revenue.sql) | Receita net cof pagarme por mês  |• payments net cof revenue <br> • stone net cof revenue <br> • stone net cof revenue ex adesao <br> • stone adesao net revenue <br> • stone pix pos revenue <br> • stone boleto banking revenue <br> • partner program net cof revenue <br> • partner program net cof revenue ex adesao <br> • partner program adesao net revenue <br> • ton net cof revenue <br> • ton net cof revenue ex adesao tapton floating <br> • ton adesao net revenue <br> • ton pix pos revenue <br> • ton tap on phone revenue <br> • pagarme smb net cof revenue <br> • pagarme grandes contas net cof revenue
| payments_net_cof_revenue_daily_results         | 21:00                  | [Query](./consultas_agendadas/receita/payments_net_cof_revenue_daily_results.sql) | Receita net cof payments por dia| • date ref <br> • payments net cof revenue with adjustment <br> • stone net cof revenue <br> • ton net cof revenue <br> • pagarme net cof revenue with adjustment |
| payments_net_cof_revenue_monthly_results         | 00:10                  | [Query](./consultas_agendadas/receita/payments_net_cof_revenue_monthly_results.sql) | Principais receitas payments por mês| • payments net cof revenue with adjustment <br> • payments net cof revenue <br> • stone net cof revenue <br> • stone net cof revenue ex adesao <br> • stone mdr net revenue <br> • stone rav net revenue <br> • stone cof <br> • stone aluguel net revenue <br> • stone adesao net revenue <br> • stone pix pos revenue <br> • stone boleto banking revenue <br> • ton net cof revenue <br> • ton net cof revenue ex adesao tapton floating <br> • ton mdr net revenue <br> • ton rav net revenue
| temp_payments_revenue_monthly_results_edit_pagarme         | 21:00                  | [Query](./consultas_agendadas/receita/temp_payments_revenue_monthly_results_edit_pagarme.sql) | Temp - Principais receitas (Pagarme)| • • stone net cof revenue <br> • stone net cof revenue ex adesao <br> • stone mdr net revenue <br> • stone rav net revenue <br> • stone cof <br> • stone aluguel net revenue <br> • stone adesao net revenue <br> • stone pix pos revenue <br> • stone boleto banking revenue <br> • ton net cof revenue <br> • ton net cof revenue ex adesao tapton floating <br> • ton mdr net revenue <br> • ton rav net revenue <br> • ton cof <br> • ton adesao net revenue <br> • ton pix pos revenue <br> • ton tap on phone revenue <br> • pagarme net cof revenue <br> • partner program net cof revenue <br> • partner program net cof revenue ex adesao <br> • partner program mdr net revenue <br> • partner program rav net revenue <br> • partner program aluguel net revenue <br> • partner program adesao net revenue <br> • pagarme smb net cof revenue <br> • pagarme smb receita liquida trx <br> • pagarme smb receita de aluguel <br> • pagarme smb receita de adesao <br> • pagarme smb outras receitas <br> • pagarme grandes contas receita net cof <br> • pagarme grandes contas receita liquida trx <br> • pagarme grandes contas receita de aluguel <br> • pagarme grandes contas receita de adesao <br> • pagarme grandes contas outras receitas


#### Smart Pos

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| smart_pos_ton_monthly_results         | 21:00                  | [Query](./consultas_agendadas/smart_pos/smart_pos_ton_monthly_results.sql) | Resultado Smart POS| • affilliation month <br> • first offer <br> • current offer <br> • active clients <br> • tpv <br> • receita transacional <br> • receita adesao <br> • receita net cof


#### Tap on Phone

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| tap_on_phone_ton_monthly_results       | 21:00                  | [Query](./consultas_agendadas/tap_phone/tap_on_phone_ton_monthly_results.sql) | Resultado Tap on Phone|• active clients <br> • new clients <br> • new clients tpv <br> • churn clients <br> • churned tpv <br> • reactivated clients <br> • reactivated tpv <br> • migrated clients <br> • migrated tpv <br> • tpv <br> • transactions <br> • tpv antecipado <br> • dx <br> • receita mdr <br> • receita liquida mdr <br> • receita rav <br> • receita liquida rav <br> • receita transacional <br> • receita liquida transacional <br> • cost of funding <br> • receita net cof <br> • receita liquida net cof|
| tap_on_phone_ton_tiered_monthly_results_v2        | 21:15                  | [Query](./consultas_agendadas/tap_phone/tap_on_phone_ton_tiered_monthly_results.sql) | Resultado Tap on Phone por tier| • tier tpv <br> • client group <br> • tap cohort <br> • ton cohort <br> • transaction type <br> • active clients <br> • new active clients <br> • churn clients <br> • reactivated clients <br> • new active clients tpv <br> • churned tpv <br> • reactivated tpv <br> • tpv <br> • transactions <br> • prepaid tpv <br> • dx calculado <br> • dx <br> • cost of funding <br> • net mdr revenue <br> • prepayment revenue <br> • transactional revenue <br> • net cof revenue


#### Tpv

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| payments_mtd_pmtd_pytd         | 22:00                  | [Query](./consultas_agendadas/tpv/payments_mtd_pmtd_pytd.sql) | Resultado do TPV - dia| • active clients <br> • new clients <br> • new clients tpv <br> • churn clients <br> • churned tpv <br> • reactivated clients <br> • reactivated tpv <br> • migrated clients <br> • migrated tpv <br> • tpv <br> • transactions <br> • tpv antecipado <br> • dx <br> • receita mdr <br> • receita liquida mdr <br> • receita rav <br> • receita liquida rav <br> • receita transacional <br> • receita liquida transacional <br> • cost of funding <br> • receita net cof <br> • receita liquida net cof|

#### Whatsapp Pay

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| whatsapp_pay_stone_monthly_results         | 22:00                  | [Query](./consultas_agendadas/whatsapp_pay/whatsapp_pay_stone_monthly_results.sql) | Resultado dos principais KPIS| • active clients <br> • tpv <br> • receita netmdr <br> • receita liquida netmdr <br> • prepayment active clients <br> • receita bruta rav <br> • receita liquida rav <br> • receita liquida transacional <br> • cof <br> • receita net cof


#### Liquidação Diaria

| Nome da Tabela                              | Horário de Atualização | Link para Query       | Descrição da Tabela   | Indicadores |
|---------------------------------------------|------------------------|-----------------------|-----------------------|-------------|
| dim_client_liquidacao_diaria         | 20:00                  | [Query](./consultas_agendadas/liquidacao_diaria/dim_client_liquidacao.sql) | Informações por documento| • CustomerDocument <br> • ClientKey <br> • PrepaymentType <br> • acquirer_activation_cohort <br> • acquirer_activation_date <br> • config_cohort <br> • config_date <br> • activation_cohort <br> • activation_date|
| temp_d1_d0_stone_tiered_monthly_results         | 20:00                  | [Query](./consultas_agendadas/liquidacao_diaria/temp_d1_d0_stone_tiered_monthly_results.sql) | Resultado dos principais KPIS| • tier_tpv <br> • acquirer_cohort <br> • activation_cohort <br> • request_channel <br> • prepayment_type <br> • active_clients <br> • new_active_clients <br> • churn_clients <br> • reactivated_clients <br> • migrated_clients <br> • new_active_clients_tpv <br> • churned_tpv <br> • reactivated_tpv <br> • migrated_tpv <br> • tpv <br> • transactions <br> • charged_tpv <br> • fee_free_tpv <br> • estimated_cost_tpv <br> • estimated_additional_cof <br> • estimated_net_revenue <br> • estimated_additional_net_cof_revenue|


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


## :mailbox_with_mail: Contato

Para falar conosco, nossas portas (virtuais) estão sempre abertas:

- :e-mail: E-mail [Duda](mailto:maria.mota@stone.com.br) | [Picotti](mailto:matheus.picotti@stone.com.br)
- :speech_balloon: Slack  [Duda](https://stonepgto.slack.com/team/U063SSKP4J3) | [Picotti](https://stonepgto.slack.com/team/U0684GLJL12)
