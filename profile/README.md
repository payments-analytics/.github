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
### Índice Payments Analytics - Produtos
  - [RAV](1.RAV)
  - [Boleto](2.Boleto)
  - [Pix](3.Pix)
  - [Link](4.Link)
  - [Tap on Phone](5.TaponPhone)
  - [DCC](6.DCC)
  - [Adesão](7.Adesão)


#### 1.RAV
|**Marca**|**Descrição da Tabela**| **Colunas**| **Dimensões** |
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
|**Marca**|**Descrição da Tabela**| **Colunas**| **Dimensões** |
|---------|-------------|-----------------|--------------|
| Stone| Resultado boleto stone por mês: `payments_analytics.boleto_monthly_results` | • Soma dos valores recebidos de boletos emitidos na conta Stone e liquidados: `gmv` <br> <br> • Contagem de boletos emitidos na conta Stone que foram liquidados: `transactions` <br> <br> • Contagem de boletos emitidos na conta Stone (pagos ou não): `issued_boleto` | • **Mês:** `reference_month` |
| Stone | Resultado boleto stone por mês: `payments_analytics.boleto_tiered_monthly_results` |  • Soma dos valores recebidos de boletos emitidos na conta Stone e liquidados: `gmv` <br> <br> • Contagem de boletos emitidos na conta Stone que foram liquidados: `transactions` <br> <br> • Contagem de boletos emitidos na conta Stone (pagos ou não): `issued_boleto` | • **Mês:** `reference_month` |
| Pagarme | Resultado receita pagarme por dia : `payments_analytics.pagarme_revenue_daily_results` | • Receita boleto refund: `receita_boleto_refund` <br> <br> • Receita boleto: `receita_boleto` |• **Dia:** `date_ref`|
| Pagarme | Resultado receita pagarme por Mês : `payments_analytics.pagarme_revenue_daily_results` | • Receita boleto refund: `receita_boleto_refund` <br> <br> • Receita boleto: `receita_boleto` |• **Mês:** `mes_ref`|
| Pagarme e Stone | Resultado GMV por Mês : `payments_analytics.payments_gmv_monthly_results` | • Net TPV Boleto PSP SMB: `Boleto_PSP_SMB` <br> <br> • Net TPV Boleto PSP KA: `Boleto_PSP_KA` <br> <br> • Net TPV Boleto GTW SMB: `Boleto_Gtw_SMB` <br> <br> • Net TPV Boleto GTW KA: `Boleto_Gtw_KA` <br> <br> •Soma dos valores recebidos de boletos emitidos na conta Stone e liquidados: `Boleto_Stone`| • **Mês:** `mes`|
| Stone | Resultado de receita payments: `payments_analytics.payments_net_cof_revenue` | • Receita gerada pela cobrança de tarifa sobre boletos emitidos na conta Stone e liquidados (R$): `stone_boleto_banking_revenue` | • **Mês:** `reference_month` |

#### :bulb: 2.1 Casos de uso
- Analisar a eficiência na conversão de boletos emitidos em boletos liquidados por mês:
``` sql
SELECT
  reference_month
  , SUM (transactions)/ SUM(issued_boleto) AS taxa_conversao
FROM dataplatform-prd.payments_analytics.boleto_tiered_monthly_results
GROUP BY 1
```
- Analisar a variação de boletos emitidos em 2022 vs 2023 (mês a mês) :
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
- Analisar o net tpv de boletos PSP e Gateway:
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
|**Marca**|**Descrição da Tabela**|**Colunas**|**Dimensões**|
|---------|-----------------------|-----------|-------------|
|Pagarme | Resultado receita pagarme por dia: `payments_analytics.pagarme_revenue_daily_results` | • Receita Pix: `receita_pix` | • **Dia:** `date_ref` |
|Pagarme | Resultado receita pagarme por mês: `payments_analytics.pagarme_revenue_daily_results` | • Receita Pix: `receita_pix` | • **Mês:** `mes_ref` |
|Stone, Ton e Pagarme| Resultado GMV:`payments_analytics.payments_gmv_monthly_results` | • PIX recebido Stone: `Pix_POS_Stone` <br><br> • PIX recebido Ton:`Pix_POS_Ton` <br><br> • PIX recebido Pagarme SMB: `Pix_Pagarme_SMB` <br><br> • PIX recebido Pagarme KA: `Pix_Pagarme_KA` | • **Mês:** `mes` |
|Stone e Ton| Resultado receita payments por mês: `payments_analytics.payments_net_cof_revenue`| • Receita Pix Stone: `stone_pix_pos_revenue` <br><br> • Receita Pix Ton: `ton_pix_pos_revenue`|  • **Mês:** `reference_month` |
|Stone| Resultado pix stone por mês: `payments_analytics.pix_pos_stone_monthly_results`| • Volume de transações via pix QR Code dinâmico gerado no POS : `pix_in_dynamic_pos_trx` <br><br> • Valor total das transações via pix QR Code dinâmico gerado no POS: `pix_in_dynamic_pos_tpv` <br><br> • Receita de taxas de transações via pix QR Code dinâmico gerado no POS: `pix_in_dynamic_pos_revenue` <br><br> • Contagem de transações que entraram na conta através de pix via QR Code estático: `pix_in_dynamic_pos_charged_trx`|  • **Mês:** `reference_month` |
|Ton| Resultado pix ton por mês: `payments_analytics.pix_pos_stone_monthly_results`| • Volume de transações via pix QR Code dinâmico gerado no POS : `pix_in_dynamic_pos_trx` <br><br> • Valor total das transações via pix QR Code dinâmico gerado no POS: `pix_in_dynamic_pos_tpv` <br><br> • Receita de taxas de transações via pix QR Code dinâmico gerado no POS: `pix_in_dynamic_pos_revenue` <br><br> • Contagem de transações que entraram na conta através de pix via QR Code estático: `pix_in_dynamic_pos_charged_trx`|  • **Mês:** `reference_month` |

#### :bulb: 3.1 Casos de uso
- Analisar o valor de receita pix de Stone e Ton:
``` sql
SELECT
    reference_month
    , SUM(stone_pix_pos_revenue) AS receita_pix_stone
    , SUM(ton_pix_pos_revenue) AS receita_pix_ton
FROM dataplatform-prd.payments_analytics.payments_net_cof_revenue
GROUP BY 1
```
- Analisar os valores das transações e o volume de transações:
``` sql
SELECT
    reference_month
    , SUM(pix_in_dynamic_pos_trx) AS qtd_transacoes_pix
    , SUM(pix_in_dynamic_pos_tpv) AS valor_transacoes_pix
FROM dataplatform-prd.payments_analytics.pix_pos_stone_monthly_results
GROUP BY 1
```

#### 4.Link
|**Marca**|**Descrição da Tabela**|**Colunas**|**Dimensões**|
|---------|-----------------------|-----------|-------------|
|Stone| Resultado de link stone: `payments_analytics.payment_link_stone_monthly_results` | • Base Ativa Link: `active_clients` <br><br> • Valor total das transações link: `tpv` <br><br> • Receita Net Cof: `receita_net_cof`| • **Mês:** `reference_month` |
|Ton| Resultado de link stone: `payments_analytics.payment_link_stone_monthly_results` | • Base Ativa Link: `active_clients` <br><br> • Valor total das transações link: `tpv` <br><br> • Receita Net Cof: `receita_net_cof`| • **Mês:** `reference_month` |
|Stone Ton| Resultado GMV: `payments_analytics.payments_gmv_monthly_results` | • TPV Link Ton: `TPV_Link_Ton` <br><br> • TPV Link Stone: `TPV_Link_Stone`| • **Mês:** `mes` |

#### :bulb: 4.1 Casos de uso
- Analisar os valores de TPV Link Ton e Stone:
``` sql
SELECT
    mes
    , SUM(TPV_Link_Ton) AS TPV_Link_Ton
    , SUM(TPV_Link_Stone) AS TPV_Link_Stone
FROM dataplatform-prd.payments_analytics.payments_gmv_monthly_results
GROUP BY 1
```

#### 5.Tap on Phone
|**Marca**|**Descrição da Tabela**|**Colunas**|**Dimensões**|
|---------|-----------------------|-----------|-------------|
|Tap on Phone|Resultado GMV: `payments_analytics.payments_gmv_monthly_results` | • TPV Tap on Phone: `TPV_Tap_Ton` | • **Mês:** `mes` |
|Tap on Phone|Receita Payments: `payments_analytics.payments_net_cof_revenue_monthly_results` | • Receita Tap on Phone: `ton_tap_on_phone_revenue` | • **Mês:** `reference_month` |
|Tap on Phone| Resultado Tap on Phone: `payments_analytics.tap_on_phone_ton_monthly_results`| • Base Ativa Tap on Phone: `active_clients` <br><br> • Valor total das transações Tap on Phone: `tpv` <br><br> • Receita Net Cof: `receita_net_cof` | • **Mês:** `reference_month` |

#### :bulb: 5.1 Casos de uso
- Analisar a base ativa de Tap on Phone:
``` sql
SELECT
    reference_month
    , SUM(active_clients) AS base_ativa_tap
FROM dataplatform-prd.payments_analytics.tap_on_phone_ton_monthly_results
GROUP BY 1
```
#### 6.DCC
|**Marca**|**Descrição da Tabela**|**Colunas**|**Dimensões**|
|---------|-----------------------|-----------|-------------|
|Stone| Resultado Stone DCC: `payments_analytics.dcc_stone_monthly_results` | • Receita estimada: `estimated_revenue` |• **Mês:** `reference_month` |

#### :bulb: 6.1 Casos de uso
- Analisar receita DCC:
``` sql
SELECT
    reference_month
    , SUM(estimated_revenue) AS estimated_revenue
FROM dataplatform-prd.payments_analytics.dcc_stone_monthly_results
GROUP BY 1
```

#### 7.Adesão
|**Marca**|**Descrição da Tabela**|**Colunas**|**Dimensões**|
|---------|-----------------------|-----------|-------------|
|Pagarme| Resultado de receita por dia: `payments_analytics.pagarme_revenue_daily_results` | • Receita de Adesão: `receita_adesao` |• **Dia:** `date_ref`|
|Pagarme| Resultado de receita por mês: `payments_analytics.pagarme_revenue_daily_results` | • Receita de Adesão: `receita_adesao` |• **Mês:** `mes_ref`|
|Stone, Ton e Pagarme| Resultado de receita por mês: `payments_analytics.payments_net_cof_revenue_monthly_results` | • Receita de Adesão Stone: `stone_adesao_net_revenue` <br><br> • Receita de Adesão Ton: `ton_adesao_net_revenue` <br><br> • Receita de Adesão Partner Program: `partner_program_adesao_net_revenue` |• **Mês:** `reference_month`|

#### :bulb: 7.1 Casos de uso
- Analisar receita de adesão partner program:
``` sql
SELECT
  reference_month
  , SUM(partner_program_adesao_net_revenue) AS receita_adesao_partner_program
FROM dataplatform-prd.payments_analytics.payments_net_cof_revenue_monthly_results
GROUP BY 1
```
### Índice Payments Analytics - Budget 2024
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

## :mailbox_with_mail: Contato

Para falar conosco, nossas portas (virtuais) estão sempre abertas:

- :e-mail: E-mail [Duda](mailto:maria.mota@stone.com.br) | [Picotti](mailto:matheus.picotti@stone.com.br)
- :speech_balloon: Slack  [Duda](https://stonepgto.slack.com/team/U063SSKP4J3) | [Picotti](https://stonepgto.slack.com/team/U0684GLJL12)
