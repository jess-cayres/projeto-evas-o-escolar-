# Projeto de Análise de Dados: Evasão Escolar no Ensino Médio Público

Este repositório contém o diagnóstico analítico, os scripts de tratamento e o painel de visualização de dados dedicados ao mapeamento do abandono escolar no Ensino Médio brasileiro, utilizando como base os Indicadores Educacionais do INEP (2022).

##  Acesso à Visualização de Dados (Dashboard)
O painel interativo foi desenvolvido no Looker Studio e pode ser acessado publicamente através do link abaixo:
*  [Acesse aqui o Dashboard Interativo no Looker Studio]((https://datastudio.google.com/reporting/2ba14ec6-9ebf-47ff-976c-39238b756e9f))

---

##  Documentação do Projeto

### 1. Coleta de Dados
O processo de coleta de dados foi estruturado de forma automatizada com foco em transparência e reprodutibilidade. A base de dados primária corresponde aos Indicadores Educacionais por Município do ano de 2022, mantidos pelo Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira (INEP/Censo Escolar). 

A extração foi efetuada programaticamente em ambiente Python (Google Colab) por meio da API e do repositório gerenciado pela iniciativa *Base dos Dados*, utilizando a biblioteca integrada ao Google BigQuery. O script realizou consultas estruturadas via SQL diretamente na nuvem para isolar as taxas de rendimento específicas do Ensino Médio Regular.

### 2. Modelagem e Tratamento
Após a ingestão inicial, os dados brutos foram submetidos a uma etapa de engenharia e modelagem descritiva no Pandas. O primeiro passo consistiu no tratamento de dados ausentes utilizando a remoção de registros nulos na variável alvo para mitigar distorções causadas por municípios sem registros validados no ano corrente.

Considerando que a tabela original continha exclusivamente a chave numérica municipal do IBGE (`id_municipio`), foi desenvolvida uma modelagem de enriquecimento geográfico. O algoritmo extraiu os dois primeiros dígitos do identificador municipal (que correspondem ao código nativo de cada Unidade Federativa pelo padrão do IBGE) e mapeou esses valores contra um dicionário estático contendo as siglas dos estados (`sigla_uf`). Por fim, o modelo gerou um arquivo otimizado em formato Excel (`.xlsx`), formato ideal para consumo no ecossistema de Business Intelligence (Looker Studio).

### 3. Conclusões e Insights Estratégicos
A análise exploratória dos dados confirmou que a evasão escolar no Ensino Médio público segue um padrão alarmante de afunilamento, revelando que o primeiro ano letivo é o verdadeiro ponto de ruptura na trajetória dos estudantes. Estatisticamente, a taxa de abandono no 1º ano é substancialmente superior àquela registrada nos anos subsequentes, o que comprova que o período de transição vindo do Ensino Fundamental é onde o jovem se encontra mais vulnerável às pressões socioeconômicas para deixar a escola e ingressar precocemente no mercado de trabalho.

Essa vulnerabilidade financeira ganha contornos geográficos nítidos quando observamos as disparidades regionais no painel analítico: os estados localizados nas regiões Norte e Nordeste concentram as maiores taxas médias de abandono do país, evidenciando que os municípios com menores índices de IDH e menor renda per capita sofrem de forma muito mais severa com a perda de seus alunos. 

Diante desse cenário diagnosticado pelos dados, qualquer intervenção governamental ou pedagógica eficaz deve abandonar o caráter generalista e passar a atuar de forma cirúrgica. Isso significa que programas de transferência de renda e assistência estudantil precisam ter seus recursos e critérios de elegibilidade focados de maneira massiva no primeiro semestre do 1º ano, período crítico de maior risco de abandono, além de implementar um sistema de alerta prévio e busca ativa focado prioritariamente nos municípios que hoje lideram o topo do ranking de evasão.

---

##  Tecnologias Utilizadas
* **Python / Pandas:** Limpeza, engenharia de recursos (recursos geográficos) e tratamento de nulos.
* **SQL (Google bigquery):** Extração otimizada de dados públicos via API *Base dos Dados*.
* **Excel (.xlsx):** Formato de modelagem de dados para portabilidade.
* **Looker Studio:** Desenvolvimento de Business Intelligence e visualização de dados em nuvem.
