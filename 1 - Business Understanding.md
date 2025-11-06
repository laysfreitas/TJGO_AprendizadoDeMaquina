---
titulo: "CRISP-DM — Fase 1: Business Understanding"
projeto: "Projeção da Taxa de Congestionamento — Justiça Estadual (GO)"
versao: "1.0"
data: "06-11-2025"
autores: "Julio César e Lays de Freitas"
status: "Rascunho"
---

# 1) Resumo
Este trabalho avalia métricas e resultados a partir de dados de processos com **datas de distribuição e baixa**, **comarca, serventia e área de ação**, para **calcular a taxa de congestionamento mensal** e **projetá-la** para **3 meses, 6 meses e 12 meses** em **todas as comarcas do Estado de Goiás**, utilizando **regressão linear** (baseline).

- **Problema de negócio**: falta de visibilidade futura da taxa de congestionamento por unidade jurisdicional e área de ação.
- **Entrega principal**: análise do problema, série histórica, taxa anual por recorte, e **previsões 3/6/12 meses** com faixas de confiança.

---

# 2) Contexto do Negócio
- **Órgão**: Tribunal de Justiça do Estado de Goiás (TJ-GO).
- **Unidades**: comarcas, serventias (varas/juizados) e áreas de ação.
- **Motivação**: direcionar recursos para reduzir congestionamento e prazos, alinhado a metas estratégicas do tribunal.
- **Benefícios esperados**: melhor alocação de magistrados/servidores, transparência e previsibilidade.

---

# 3) Objetivos do Negócio
1. **Disponibilizar previsões** da **taxa de congestionamento** para **100% das comarcas** de GO com **erro absoluto médio (MAE) ≤ x p.p.** em validação temporal.
2. **Identificar as 10 comarcas** com maior **risco de aumento** (tendência > +3 p.p. em 6 meses).

**KPIs primários**: Taxa de congestionamento (mensal)
**KPIs secundários**:

---

# 4) Restrições e Premissas
- **Restrições**:
- **Premissas**:

---

# 5) Critérios de Sucesso & Aceitação
- Métrica implementada.
- **MAE ≤ x p.p.** em validação temporal para 80% das comarcas.
- Painel com **ranking, mapa e tendência**.

---

# 6) Questões de Negócio → Questões Analíticas
- **Negócio**: Quais comarcas tendem a **aumentar** a taxa nos próximos 3/6/12 meses?  
  **Analítica**: Modelar e prever a taxa por série temporal (baseline: regressão linear sobre tendência/sazonalidade).
- **Negócio**: Onde focar recursos no curto prazo?  
  **Analítica**: Ranqueamento por **risco de alta** (variação prevista) + **nível atual** (matriz risco × impacto).
- **Negócio**: A taxa varia por **área de ação** e/ou por **serventia**?  
  **Analítica**: Cortes por área; análise de heterogeneidade e efeitos sazonais.

---

# 7) Objetivos de Data Mining
- **Modelagem preditiva** de séries por comarca/serventia/área de ação.
- **Nowcasting** (último mês) e **forecast** (3/6/12 meses).
- **Explicabilidade**: decomposição de tendência/sazonalidade e fatores correlatos (entradas, baixas, estoque).

---

# 8) Métricas de Avaliação
- **Modelagem**: MAE, RMSE;
- **Negócio**: nº de comarcas em **alerta** (↑ previsto), redução efetiva pós-intervenção (quando houver).
- **Operação**: % séries com previsão válida; latência do processamento; taxa de atualização.

---

# 9) Considerações Legais, Éticas e LGPD
- **Base legal**: execução de política pública e interesse público (art. 7º/23 LGPD).
- **Dados pessoais**: evitar campos desnecessários ou identificadores diretos; **agregação por unidade**.
- **Minimização**: trabalhar com contagens/estados agregados; anonimização quando houver risco de reidentificação.

---

# 10) Plano de Projeto (alto nível)
**Marcos**
1. **Semanas 1**: alinhamento, validação da **definição da taxa** e inventário de dados.
2. **Semanas 2**: construção das séries agregadas e checagens de qualidade.
3. **Semanas 3**: baseline (regressão linear) + backtesting; documentação.
4. **Semanas 4**: painel (mapa, ranking, tendências) e publicação.

**Entregas**: conjunto de séries (CSV/Parquet), modelo v1, dashboard.

---

# 11) Glossário
- **Comarca / Serventia**: divisões administrativas do TJ .
- **Área de ação**: agrupamento por natureza/assunto do processo .
- **Quantidade de Processos Distribuídos**: Essa medida foi obtida através da contagem de datas de entrada dos processos em uma determinada área de ação de uma comarca. A importância de se conhecer essa métrica é que ela permite compreender o volume de demandas que ingressam no sistema judiciário em um determinado período, o que é fundamental para o planejamento e a alocação eficiente de recursos.
- **Quantidade de Processos Baixados**: A quantidade de processos baixados se refere à contagem de datas de processos que foram dadas baixa em uma área de ação de uma comarca, isto é, reflete o número de processos que foram arquivados em um determinado período, permitindo identificar gargalos e melhorar a eficiência e a produtividade. Portanto, seu conhecimento possibilita a implementação de estratégias especéficas como otimização do fluxo de trabalho, capacitação de servidores ou adoção de tecnologias para automatizar tarefas repetitivas.
- **Quantidade de Processos Pendentes**: Esse indicador é o número de processos que ainda estão em aberto, ou seja, em que não foram registradas baixa. Essa métrica permite identificar se há um acúmulo excessivo de demandas, avaliar a eficiência, planejar estratégias e promover transparência no sistema judiciário.
- **Taxa de congestionamento**: A Taxa de Congestionamento permite medir o grau de congestionamento do sistema, isto é, quanto do volume total de processos ainda não foi resolvido. Uma taxa alta indica que uma parcela significativa das demandas está acumulada, o que pode refletir ineficiências, falta de recursos ou gargalos no fluxo de trabalho. Por outro lado, uma taxa baixa sugere que o sistema está conseguindo dar vazão às demandas de forma ágil e eficiente. A taxa de congestionamento foi obtida pela fórmula: Tx. Cong = (nº de processos pendentes / (nº de processos pendentes + nº de processos baixados (últimos 12 meses))). A partir desse índice buscamos a resposta para a hipótese, ou seja, se a transformação de juizados dentro das varas pode ter impactado os processos do Juizado Especial Cível.
- **Nowcasting**: estimativa do período mais recente com dados parciais.
- **Backtesting**: avaliação da previsão em janelas históricas.

---

# 12) Anexos
- Painel (mapa, ranking, tendência).
