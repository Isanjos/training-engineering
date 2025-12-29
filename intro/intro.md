# Oracle Cloud Infrastructure Fast Track - For Data Engineering

## Resumo

A **arquitetura de medalhão** é um modelo que organiza os dados em etapas progressivas — **Bronze, Prata e Ouro** —, facilitando a jornada de **dados brutos até insights de alto valor**. Essa estrutura garante **qualidade, rastreabilidade e confiabilidade**, permitindo que as empresas tomem decisões mais seguras e que modelos de **Inteligência Artificial** sejam alimentados com dados consistentes.

![Arquitetura Medalhão em Detalhes - Um fluxograma vertical dividido em três seções que representam a Arquitetura Medalhão: "Bronze" para dados brutos, "Prata" para dados processados, e "Ouro" para dados otimizados. Os dados fluem de "Origem de Dados" passando por cada etapa até a "Análise de Dados" e "Machine Learning e Inteligência Artificial", indicando o processo desde a coleta até a análise e insights.](./images/arquitetura-medalhao.png)

Dentro dessa jornada, o **Oracle Cloud Infrastructure Data Flow** atua como o motor de processamento que dá vida à arquitetura medalhão. Sendo uma solução **serverless baseada em Apache Spark**, ele permite trabalhar com **big data em larga escala** de forma simples e eficiente. Com **processamento em tempo real**, **interface intuitiva** e **integração fluida aos fluxos de trabalho**, o Data Flow viabiliza análises complexas sem a sobrecarga de infraestrutura, garantindo **produtividade, escalabilidade e governança de dados** em cada camada da arquitetura.

![A imagem ilustra a arquitetura medalhão no Oracle Cloud Infrastructure (OCI), mostrando como os dados fluem desde diferentes fontes (streaming, arquivos, weblogs e sensores) até seu consumo final. No OCI Data Flow, eles passam pelas camadas de Bronze (dados brutos), Prata (dados limpos) e Ouro (dados preparados), utilizando aplicações e sessões Spark ou clusters SQL. Todo o processo é apoiado pelo OCI Data Catalog (metadados) e pelo OCI Object Storage (armazenamento), garantindo governança e organização. Por fim, os dados enriquecidos podem alimentar bancos de dados (ADW, ExaCS, MySQL Heatwave, NoSQL, DBCS, OCI DMS) ou modelos de machine learning, sendo consumidos por diferentes perfis de usuários, como engenheiros de dados, cientistas de dados e analistas SQL.](images/oci-data-flow.png)

Nos tópicos a seguir, você poderá explorar em detalhe como essa arquitetura está estruturada e como cada camada contribui para gerar valor.

### *Sobre esse Workshop*

O objetivo principal deste laboratório é capacitar e aperfeiçoar as competências associadas à utilização de serviços de **Lakehouse para lidar com Big Data**, abrangendo todas as etapas desde a **aquisição inicial dos dados** até a sua transformação em **insights avançados** e **relatórios detalhados**.

Adotando a estrutura de arquitetura medalhão, que se segmenta nas camadas **Bronze , Prata (Silver) e Ouro (Gold)**, os participantes serão encorajados a investigar, ajustar e aperfeiçoar os dados durante as diversas fases do seu ciclo de vida.

**Todas as práticas estão descritas em detalhes e não necessitam de qualquer conhecimento prévio para serem executadas.**

Em caso de dúvidas ou necessidade de suporte, os participantes poderão entrar em contato com a equipe responsável pela criação e edição dos laboratórios, com informações de contato disponíveis ao final de cada etapa.

***Tempo estimado para o Workshop:* 4 Horas**


*Objetivos*

Por meio deste guia, iremos fornecer laboratórios práticos de:

- Configuração e Implementação do Ambiente
- Configuração do Data Flow Studio
- Manipulação de Dados
- Consumo de Dados no Data Lake
- Visualização de Dados

## O que é a Arquitetura Medalhão?

Na era dos dados, o diferencial não está apenas em coletar informações, mas em organizar e transformar esse ativo em vantagem competitiva. A arquitetura de medalhão oferece um caminho claro para evoluir de dados brutos até insights estratégicos, garantindo qualidade, confiança e valor a cada etapa.

Neste laboratório você aprenderá a transformar dados brutos em informações valiosas, avançando por três etapas fundamentais conhecidas como **Bronze, Prata e Ouro**. 

Essa divisão reflete a jornada de maturidade dos dados: do estado inicial, ainda cru e desorganizado, até o nível mais refinado, em que passam a gerar insights estratégicos e confiáveis para apoiar decisões e resultados de negócio.

![Arquitetura Medalhão em Detalhes - Um fluxograma vertical dividido em três seções que representam a Arquitetura Medalhão: "Bronze" para dados brutos, "Prata" para dados processados, e "Ouro" para dados otimizados. Os dados fluem de "Origem de Dados" passando por cada etapa até a "Análise de Dados" e "Machine Learning e Inteligência Artificial", indicando o processo desde a coleta até a análise e insights.](./images/arquitetura-medalhao.png)

---
🥉 <span style="color:#cd7f32">Bronze</span>

**Descrição:**  Imagine a coleta de dados como o início da mineração: metais recém-extraídos, ainda brutos. Assim são os dados nesta fase — capturados em sua forma original de fontes como sensores IoT, registros de transações, logs de sistemas ou redes sociais.

**Processos:** Neste ponto inicial, os dados são simplesmente mantidos em estado bruto com segurança, aguardando etapas futuras onde serão refinados e transformados para uso.

---
🥈 <span style="color:silver">Prata</span>


**Descrição:** Como no processo de purificação do metal, os dados passam por limpeza e organização, tornando-se consistentes e confiáveis. Este processo é vital para remover erros e redundâncias, assegurando dados de alta qualidade para análise.

**Processos:** Erros e duplicações são removidos, formatos padronizados e a base preparada para análises confiáveis.

---
🥇 <span style="color:#ffd700">Ouro</span>

**Descrição:** Na etapa final da metalurgia, o metal é refinado até atingir sua forma mais valiosa, podendo até ser combinado para criar ligas mais fortes. Da mesma forma, os dados em sua fase Ouro são enriquecidos e transformados em informações de alto valor, integrados a outras fontes e submetidos a análises avançadas que revelam insights estratégicos e apoiam decisões críticas.

**Processos:** Neste estágio, utilizam-se técnicas de mineração de dados — o processo de explorar grandes volumes de informação para identificar padrões e correlações ocultas —, além de business intelligence e aprendizado de máquina, para transformar dados em conhecimento prático, prever tendências e orientar decisões estratégicas.


| Camada    | Nome              | Objetivo                                                                                                                                                                                             |
| --------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🥉 Bronze | Dados Brutos      | • Coleta de dados em estado original, vindos de várias fontes. <br> • Armazenamento seguro, mantendo os dados exatamente como foram recebidos. <br> • Preservação para auditoria e rastreabilidade.  |
| 🥈 Prata  | Dados Processados | • Remoção de erros, duplicações e inconsistências. <br> • Padronização e organização para facilitar leitura e uso. <br> • Preparação dos dados para análises mais detalhadas.                        |
| 🥇 Ouro   | Dados Otimizados  | • Enriquecimento com informações adicionais e contexto. <br> • Combinação de diferentes dados para gerar visões consolidadas. <br> • Aplicação de análises avançadas para extrair insights valiosos. |



## Por que utilizar a arquitetura medalhão?

A arquitetura de medalhão ajuda a construir um **ecossistema de dados organizado, confiável e fácil de expandir**. Isso é fundamental para aproveitar o poder da análise de dados e da inteligência artificial, gerando vantagem em um mercado cada vez mais orientado por informações.

![Benefícios da Arquitetura Medalhão - Um diagrama circular com seis ícones interconectados. Cada ícone representa um benefício da Arquitetura Medalhão: "Segregação de dados brutos e processados", "Prontidão analítica", "Melhoria da qualidade e integridade dos dados", "Otimização para modelos de IA", "Dashboards eficientes", e "Escalabilidade e governança".](.\images\beneficios-medalhao.png)

✅ **Separação clara das camadas:**
Os dados são divididos em níveis — Bronze, Prata e Ouro — o que permite trabalhar com informações brutas, intermediárias e refinadas ao mesmo tempo, sem confusão.

✅ **Mais qualidade nos dados:**
A cada etapa, os dados são revisados, limpos e padronizados. Isso garante que erros e duplicações sejam eliminados antes de chegar à análise.

✅ **Dados prontos para Inteligência Artificial:**
Como os modelos de IA precisam de dados de qualidade, essa estrutura garante que eles recebam informações já tratadas e confiáveis, aumentando a precisão e a velocidade dos resultados.

✅ **Dashboards mais eficientes:**
Na camada Ouro, os dados estão prontos para gerar painéis claros e atualizados, ajudando na tomada de decisão rápida e segura.

✅ **Escalabilidade e organização:**
A arquitetura é fácil de expandir, pois cada camada pode ser ajustada sem afetar as outras. Além disso, facilita a governança, mostrando claramente como os dados evoluem até se tornarem insights.

✅ **Prontidão para análise:**
No estágio final, os dados já estão preparados e confiáveis, permitindo que equipes de negócio extraiam insights valiosos com menos esforço e maior precisão.

## Arquitetura do Workshop

![Arquitetura usada neste workshop.](./images/arquitetura-workshop.gif)

### *Sobre o Oracle Cloud Infrastructure Data Flow*

O **OCI Data Flow** será o **principal serviço** utilizado neste workshop. Ele é uma **plataforma em nuvem para análise de dados** que simplifica o uso do **Apache Spark em grande escala**.

Por estar **totalmente na nuvem**, elimina a necessidade de **configurar e manter clusters**, permitindo que desenvolvedores e cientistas de dados foquem no que realmente importa: **processar e transformar informações**.

Com o **Data Flow**, é possível:

* **Executar tarefas em paralelo**, aproveitando o poder distribuído do Spark.
* Fazer **análises de big data diretamente nas fontes**, sem complicações de infraestrutura.
* **Integrar facilmente** a ferramenta a fluxos de trabalho existentes, pela **interface intuitiva** ou por **APIs**.
* **Processar dados em tempo real** com Spark Streaming, garantindo informações sempre atualizadas para análises e decisões rápidas.

Em resumo, o **OCI Data Flow une escala, simplicidade e eficiência**, ajudando a **transformar dados em valor** sem a sobrecarga de gerenciar infraestrutura.

## Saiba Mais

Português:
- [Documentação do Oracle Cloud Infrastructure Data Flow](https://docs.oracle.com/pt-br/iaas/data-flow/using/home.htm)

Inglês:
- [Documentação do Oracle Cloud Infrastructure Data Flow](https://docs.oracle.com/en-us/iaas/data-flow/using/home.htm)
- [Saiba mais sobre o Data Flow - Vídeo](https://www.oracle.com/br/big-data/data-flow/?ytid=U-8TRHD_UOc)
- [O que há de novo](https://docs.oracle.com/en-us/iaas/releasenotes/services/data-flow/)
- [Arquiteturas de referência](https://docs.oracle.com/en/solutions/oci-big-data-flow/index.html#GUID-D84476CE-4063-4884-B2EC-793A921A4638)

## Autoria

- *Created By/Date* - Thais Henrique, Heloisa Escobar, Isabelle Anjos, Janeiro 2024
- *Last Updated By* - Isabelle Anjos, Outubro 2025
