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
### Índice Payments Analytics 
  - [RAV](####1.RAV)
  - [Boleto](####2.Boleto)
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

#### 1.RAV
|**Marca**|**Descrição da Tabela**   | **Colunas**      | **Dimensões** |
|---------|-------------|-----------------|------------------|
|Pagarme|Receita diária pagarme: `payments_analytics.pagarme_revenue_daily_results`| • Receita líquida de RAV: `receita_rav_liquida` | • **Dia:** `date_ref` <br> • **Operacao:** PAGARME - SMB e PAGARME - GRANDES CONTAS|
|Pagarme|Receita mensal pagarme: `payments_analytics.pagarme_revenue_results`|• Receita líquida de RAV: `receita_rav_liquida`| • **Mês:** `mes_ref` <br> • **Operacao:** PAGARME - SMB e PAGARME - GRANDES CONTAS|
|Stone  | Resultado mensal Link Stone: `payments_analytics.payment_link_stone_monthly_results` | • Receita bruta RAV: `receita_bruta_rav` <br> • Receita líquida de RAV: receita_liquida_rav |• **Mês:** `reference_month`|
|Stone  | Resultado mensal Link Stone por Tier: `payments_analytics.payment_link_stone_tiered_monthly_results` | • Receita bruta RAV: `receita_bruta_rav` <br> • Receita líquida de RAV: receita_liquida_rav |• **Mês:** `reference_month` <br> • **Tier:** `tier_tpv`|
| Ton |Resultado mensal Ton: `payments_analytics.payment_link_ton_monthly_results` |• Receita bruta RAV: `receita_rav` <br> • Receita líquida de RAV: receita_liquida_rav | • **Mês:** `reference_month`|
| Ton |Resultado mensal Ton por Tier: `payments_analytics.payment_link_ton_tiered_monthly_results` |• Receita bruta RAV: `receita_rav` <br> • Receita líquida de RAV: `receita_liquida_rav` | • **Mês:** `reference_month` <br> • **Tier:** `tier_tpv`|
| Stone, Ton e Pagarme | Resultado mensal receita payments: `payments_analytics.payments_net_cof_revenue_monthly_results` | • Receita Net Rav Stone: `stone_rav_net_revenue` <br> •  Receita Net Rav Ton: `ton_rav_net_revenue` <br> • Receita Net Rav Partner Program: partner_program_rav_net_revenue |• **Mês:** `reference_month` |
| Ton | Resultado mensal TapTon: `payments_analytics.tap_on_phone_ton_monthly_results` |•  Receita bruta RAV: `receita_rav` <br> • Receita líquida de RAV: `receita_liquida_rav` |• **Mês:** `reference_month` |


#### :bulb: 1.1 Casos de uso
- Analisar a receita líquida RAV de Link Stone nos últimos 6 meses por Segmento:
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

- Analisara receita RAV mensal do produto TAP TON e determinar a participação em relação a receita net cof:
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
|**Marca**|**Descrição da Tabela**   | **Colunas**      | **Dimensões** |
|---------|-------------|-----------------|--------------|
| Stone| Resultado boleto stone por mês: `payments_analytics.boleto_monthly_results` | • Soma dos valores recebidos de boletos emitidos na conta Stone e liquidados: `gmv` <br> <br> • Contagem de boletos emitidos na conta Stone que foram liquidados: `transactions` <br> <br> • Contagem de boletos emitidos na conta Stone (pagos ou não): `issued_boleto` | • **Mês:** `reference_month` |
| Stone | Resultado boleto stone por mês e Tier: `payments_analytics.boleto_tiered_monthly_results` |  • Soma dos valores recebidos de boletos emitidos na conta Stone e liquidados: `gmv` <br> <br> • Contagem de boletos emitidos na conta Stone que foram liquidados: `transactions` <br> <br> • Contagem de boletos emitidos na conta Stone (pagos ou não): `issued_boleto` | • **Mês:** `reference_month` <br> <br> • **Tier:** `tier_tpv` |
| Pagarme | Resultado receita pagarme por dia : `payments_analytics.pagarme_revenue_daily_results` | • Receita boleto refund: `receita_boleto_refund` <br> <br> • Receita boleto: `receita_boleto` |• **Dia:** `date_ref`|
| Pagarme | Resultado receita pagarme por Mês : `payments_analytics.pagarme_revenue_daily_results` | • Receita boleto refund: `receita_boleto_refund` <br> <br> • Receita boleto: `receita_boleto` |• **Mês:** `mes_ref`|
| Pagarme | Resultado GMV por Mês : `payments_analytics.payments_gmv_monthly_results` | • Net TPV Boleto PSP SMB: `Boleto_PSP_SMB` <br> <br> • Net TPV Boleto PSP KA: `Boleto_PSP_KA` <br> <br> • Net TPV Boleto GTW SMB: `Boleto_Gtw_SMB` <br> <br> • Net TPV Boleto GTW KA: `Boleto_Gtw_KA` <br> <br> •Soma dos valores recebidos de boletos emitidos na conta Stone e liquidados: `Boleto_Stone`|• **Mês:** `mes_ref`|

## :mailbox_with_mail: Contato

Para falar conosco, nossas portas (virtuais) estão sempre abertas:

- :e-mail: E-mail [Duda](mailto:maria.mota@stone.com.br) | [Picotti](mailto:matheus.picotti@stone.com.br)
- :speech_balloon: Slack  [Duda](https://stonepgto.slack.com/team/U063SSKP4J3) | [Picotti](https://stonepgto.slack.com/team/U0684GLJL12)
