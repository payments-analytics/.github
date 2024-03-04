# 🌟 Bem-vindo à Payments Analytics! 🌟


## 💡 Sobre
A missão do nosso repositório é centralizar todas as queries de análise de resultados que utilizamos no BigQuery e RedShift. Nosso objetivo é criar um catálogo abrangente de informações e queries prontas, especificamente voltadas a payments.

![image](https://github.com/payments-analytics/.github/assets/154369193/1bac58eb-51c7-41e3-9d67-041031b6fdd0)

## 🚀 Nossos Projetos

- **[pay-gestao-negocio-analytics-queries](https://github.com/payments-analytics/pay-gestao-negocio-analytics-queries)**:
  - 📊 Queries rotineiras para consultas no BigQuery, Metabase e Redshift.
- **[pay-gestao-negocio-looker-queries](https://github.com/payments-analytics/pay-gestao-negocio-looker-queries)**
  - 📈 Queries para dashboards do Looker Studio.
- **[pay-gestao-negocio-scheduled-queries](https://github.com/payments-analytics/pay-gestao-negocio-scheduled-queries)**
  - 🗓 Queries agendadas do Dataset `payments_analytics` no BigQuery.
- **[pay-gestao-scripts](https://github.com/payments-analytics/pay-gestao-scripts)**
  - 📜 Scripts para o dia a dia do time.

## 🧭 Guia de Análise  
Este guia é focado em ilustrar como realizar consultas fundamentais e identificar as tabelas chave no dataset de pagamentos para uma análise dos produtos. Vamos explorar as principais tabelas e como utilizá-las em consultas estratégicas para obter insights.
### Índice
  - [RAV](#bigquery)
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

#### 1.RAV
|**Marca**|**Descrição da Tabela**   | **Colunas**      | **Dimensões** |
|---------|-------------|-----------------|--------------|
|Pagarme|Receita diária pagarme: `payments_analytics.pagarme_revenue_daily_results`| • Receita líquida de RAV: `receita_rav_liquida` | • **Dia:** `date_ref` <br> • **Operacao:** PAGARME - SMB e PAGARME - GRANDES CONTAS|
|Pagarme|Receita mensal pagarme: `payments_analytics.pagarme_revenue_results`|• Receita líquida de RAV: `receita_rav_liquida`| • **Mês:** `mes_ref` <br> • **Operacao:** PAGARME - SMB e PAGARME - GRANDES CONTAS|
|Stone  | Resultado mensal Link Stone: `payments_analytics.payment_link_stone_monthly_results` | • Receita bruta RAV: `receita_bruta_rav` <br> • Receita líquida de RAV: receita_liquida_rav |• **Mês:** `reference_month`|
|Stone  | Resultado mensal Link Stone por Tier: `payments_analytics.payment_link_stone_tiered_monthly_results` | • Receita bruta RAV: `receita_bruta_rav` <br> • Receita líquida de RAV: receita_liquida_rav |• **Mês:** `reference_month` <br> • **Tier:** `tier_tpv`|
| Ton |Resultado mensal Ton: `payments_analytics.payment_link_ton_monthly_results` |• Receita bruta RAV: `receita_rav` <br> • Receita líquida de RAV: receita_liquida_rav | • **Mês:** `reference_month`|
| Ton |Resultado mensal Ton por Tier: `payments_analytics.payment_link_ton_tiered_monthly_results` |• Receita bruta RAV: `receita_rav` <br> • Receita líquida de RAV: `receita_liquida_rav` | • **Mês:** `reference_month` <br> • **Tier:** `tier_tpv`|
| Stone, Ton e Pagarme | Resultado mensal receita payments: `payments_analytics.payments_net_cof_revenue_monthly_results` | • Receita Net Rav Stone: `stone_rav_net_revenue` <br> •  Receita Net Rav Ton: `ton_rav_net_revenue` <br> • Receita Net Rav Partner Program: partner_program_rav_net_revenue |• **Mês:** `reference_month` |
| Ton | Resultado mensal TapTon: `payments_analytics.tap_on_phone_ton_monthly_results` |•  Receita bruta RAV: `receita_rav` <br> • Receita líquida de RAV: `receita_liquida_rav` |• **Mês:** `reference_month` |

##### 💡 1.1 Casos de uso





## 📬 Contato

Para falar conosco, nossas portas (virtuais) estão sempre abertas:

- 📧 E-mail [Duda](mailto:maria.mota@stone.com.br) | [Picotti](mailto:matheus.picotti@stone.com.br)
- 💬 Slack  [Duda](https://stonepgto.slack.com/team/U063SSKP4J3) | [Picotti](https://stonepgto.slack.com/team/U0684GLJL12)

