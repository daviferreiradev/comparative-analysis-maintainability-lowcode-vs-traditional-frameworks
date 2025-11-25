# Análise Comparativa de Manutenibilidade e Tempo de Resolução de Issues: Plataformas Low-Code Open Source vs. Frameworks Web Tradicionais

Estudo empírico comparando a eficiência de manutenção (tempo de resolução de issues) entre Plataformas Low-Code Open Source (e.g., Appsmith, Budibase, ToolJet) e Frameworks Web Tradicionais (e.g., React, Vue.js, NestJS).

# Plano de Experimento – Scoping e Planejamento

## 1. Identificação básica

### 1.1 Título do experimento
Análise Comparativa de Manutenibilidade e Tempo de Resolução de Issues: Plataformas Low-Code Open Source vs. Frameworks Web Tradicionais.

### 1.2 ID / código
`EXP-TCC-2025-LCT` (Low-Code vs Traditional Analysis)

### 1.3 Versão do documento e histórico de revisão
* **v1.0** (21/11/2025): Revisão do plano inicial, definição de hipóteses e escopo de mineração de dados.
* **v1.1** (25/11/2025): Escopo, Objetivo, Stakeholders/Impacto, Riscos de alto nível, premissas e critérios de sucesso

### 1.4 Datas (criação, última atualização)
* **Criação:** 21/11/2025
* **Última atualização:** 25/11/2025

### 1.5 Autores (nome, área, contato)
* **Davi José Ferreira:** Estudante de Engenharia de Software - davi.ferreira.1408962@sga.pucminas.br

### 1.6 Responsável principal (PI / dono do experimento)
* **Davi José Ferreira:** Pesquisador Principal.

### 1.7 Projeto / produto / iniciativa relacionada
Este experimento compõe o trabalho final de "Proposta de Experimento para TCC" da disciplina de Medição e Experimentação em Engenharia de Software.

---

## 2. Contexto e problema

### 2.1 Descrição do problema / oportunidade
O desenvolvimento Low-Code promete acelerar a entrega de software através de abstração e interfaces visuais. No entanto, existe uma lacuna no entendimento sobre a **manutenibilidade interna** das próprias plataformas que oferecem esses recursos.

O problema investigado é se a complexidade arquitetural e o alto acoplamento inerentes às plataformas Low-Code Open Source resultam em um ciclo de correção de defeitos mais lento em comparação com frameworks web tradicionais baseados em código ("Pro-Code"), que tendem a ser mais modulares. A oportunidade é fornecer evidências empíricas para CTOs e arquitetos sobre a sustentabilidade e agilidade de evolução dessas ferramentas a longo prazo.

### 2.2 Contexto organizacional e técnico
O experimento ocorrerá no contexto de **Software Livre (Open Source)** hospedado no GitHub. O estudo caracteriza-se como **Mineração de Repositórios de Software (MSR)**.
* **Ambiente:** Repositórios públicos de alta relevância (>10k stars).
* **Tecnologias:** Python (para scripts de coleta), GitHub REST API (fonte de dados).
* **Domínio:** Ferramentas de desenvolvimento de software (Developer Tools).

### 2.3 Trabalhos e evidências prévias (internos e externos)
A principal fundamentação para este estudo baseia-se no mapeamento sistemático realizado por **Khorram et al. (2020)**, intitulado *"Problems and opportunities in low-code development"*.
* **Evidência:** Os autores identificaram que a **manutenibilidade** é um dos desafios técnicos mais críticos e citados na adoção de plataformas Low-Code, devido às dificuldades de versionamento e à complexidade oculta gerada pela abstração.
* **Lacuna:** Embora o estudo de Khorram aponte o problema de forma qualitativa através da literatura, há uma escassez de estudos empíricos que quantifiquem essa dificuldade comparando diretamente a **eficiência do processo de manutenção** (*Issue Tracking*) entre os repositórios de plataformas Low-Code e os de frameworks tradicionais.

### 2.4 Referencial teórico e empírico essencial
O desenho experimental fundamenta-se nos seguintes conceitos:
1.  **Manutenibilidade (ISO/IEC 25010):** Capacidade do produto de software ser modificado de forma eficaz e eficiente.
2.  **Issue Resolution Time (Tempo de Resolução):** Métrica proxy amplamente aceita na indústria e academia para medir esforço de manutenção e complexidade oculta.
3.  **Dívida Técnica:** O custo implícito de retrabalho causado pela escolha de uma solução fácil (ou arquiteturalmente complexa) agora, em vez de uma abordagem melhor que levaria mais tempo.
4.  **Arquitetura Monolítica vs. Modular:** A premissa teórica de que plataformas Low-Code tendem a ser monólitos acoplados (interface + lógica + dados), dificultando a isolação e correção de falhas.

---

## 3. Objetivos e questões (Goal / Question / Metric)

### 3.1 Objetivo geral (Goal template)
Analisar a **manutenibilidade** (focando em tempo de resolução de issues e esforço de alteração) de **Plataformas Low-Code Open Source** comparadas a **Frameworks Web Tradicionais**, com o propósito de **avaliar a eficiência de manutenção e evolução**, sob a perspectiva de **Arquitetos de Software e Gestores de Tecnologia**, no contexto de **projetos de código aberto hospedados no GitHub**.

### 3.2 Objetivos específicos
*   **O1:** Comparar a velocidade de correção de defeitos (bug fixing) entre os dois tipos de tecnologia.
*   **O2:** Analisar a complexidade das alterações necessárias para correções (esforço de código).
*   **O3:** Avaliar a estabilidade das correções (incidência de reabertura de issues ou regressões).
*   **O4:** Investigar o engajamento da comunidade no processo de manutenção (dependência do core team).

### 3.3 Questões de pesquisa e 3.4 Métricas associadas (GQM)

| Objetivo | Questão de Pesquisa | Métricas Associadas |
| :--- | :--- | :--- |
| **O1. Velocidade** | **Q1.1** Qual é a diferença no Tempo Médio de Resolução (MTTR) de bugs entre plataformas Low-Code e frameworks tradicionais? | - MTTR (Mean Time to Resolution)<br>- Issue Age (para issues abertas) |
| | **Q1.2** A distribuição do tempo de fechamento de issues varia significativamente entre os grupos (cauda longa de bugs complexos)? | - Issue Close Time Percentiles (P50, P90, P99)<br>- Std Dev of Close Time |
| | **Q1.3** Qual é o tempo mediano de vida de um bug crítico? | - Critical Bug Resolution Time<br>- Critical Bug Count |
| **O2. Esforço** | **Q2.1** Qual é o tamanho médio dos commits (churn) associados a correções de bugs em cada grupo? | - Code Churn (Lines Added + Deleted)<br>- Commit Count per Issue |
| | **Q2.2** Quantos arquivos são modificados em média para resolver uma issue (dispersão da mudança)? | - Files Changed Count<br>- Directory Spread (pastas afetadas) |
| | **Q2.3** O tamanho do patch (linhas adicionadas/removidas) difere significativamente entre os grupos? | - Patch Size (Bytes)<br>- Hunks Count |
| **O3. Estabilidade** | **Q3.1** Qual a taxa de reabertura de issues (bugs que voltaram)? | - Reopen Rate<br>- Reopen Count |
| | **Q3.2** Qual a proporção de issues marcadas como "wontfix" ou "invalid"? | - Invalid Issue Rate<br>- Wontfix Issue Rate |
| | **Q3.3** Qual a frequência de issues linkadas a commits de "revert"? | - Revert Commit Rate<br>- Regression Label Count |
| **O4. Comunidade** | **Q4.1** Qual o tempo médio para a primeira resposta da equipe/comunidade em uma nova issue? | - Time to First Response<br>- Time to First Triage |
| | **Q4.2** Qual a proporção de issues resolvidas por contribuidores externos vs. time core? | - External Contributor Ratio<br>- Core Team Commit Ratio |
| | **Q4.3** Qual o número médio de participantes na discussão de um bug? | - Comment Count<br>- Unique Commenters Count |

### Tabela de Definição de Métricas

| Métrica | Descrição | Unidade |
| :--- | :--- | :--- |
| **MTTR (Mean Time to Resolution)** | Tempo médio decorrido entre a abertura e o fechamento de uma issue classificada como bug. | Horas / Dias |
| **Issue Age** | Tempo decorrido desde a abertura até o momento atual para issues ainda abertas. | Dias |
| **Issue Close Time Percentiles** | Valores de tempo de fechamento abaixo dos quais se encontram 50%, 90% e 99% das observações. | Dias |
| **Std Dev of Close Time** | Desvio padrão do tempo de fechamento, indicando a variabilidade do processo de correção. | Dias |
| **Critical Bug Resolution Time** | Tempo de resolução específico para issues com labels de alta prioridade (e.g., `critical`, `high`). | Horas |
| **Code Churn** | Soma de linhas de código adicionadas e removidas nos commits associados à issue. | Linhas de Código (LOC) |
| **Commit Count per Issue** | Número total de commits vinculados a uma única issue. | Quantidade (Inteiro) |
| **Files Changed Count** | Número de arquivos únicos modificados nos commits da issue. | Quantidade (Inteiro) |
| **Directory Spread** | Número de diretórios distintos que contêm arquivos modificados na correção. | Quantidade (Inteiro) |
| **Patch Size** | Tamanho total em bytes do diff gerado pela correção. | Bytes |
| **Reopen Rate** | Porcentagem de issues que foram reabertas após terem sido fechadas. | Porcentagem (%) |
| **Invalid Issue Rate** | Porcentagem de issues fechadas com labels indicando inválido (`invalid`, `duplicate`). | Porcentagem (%) |
| **Revert Commit Rate** | Porcentagem de correções que resultaram em um commit posterior de reversão (`revert`). | Porcentagem (%) |
| **Time to First Response** | Tempo decorrido entre a abertura da issue e o primeiro comentário de um membro (não autor). | Horas |
| **External Contributor Ratio** | Proporção de issues resolvidas (PR mergeado) por usuários que não são mantenedores do repositório. | Porcentagem (%) |
| **Comment Count** | Número total de comentários na thread da issue. | Quantidade (Inteiro) |
| **Unique Commenters Count** | Número de usuários distintos que participaram da discussão da issue. | Quantidade (Inteiro) |

---

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo (incluído e excluído)
*   **Incluído:**
    *   Análise de issues fechadas e commits associados (via link na issue) em repositórios públicos do GitHub.
    *   Foco estrito em issues classificadas semanticamente como "bug", "fix" ou "defect" através de labels ou mineração de texto no título.
    *   Repositórios com mais de 10.000 estrelas para garantir relevância e maturidade de processo.
*   **Excluído:**
    *   Issues de "feature request", "enhancement", documentação ou dúvidas (questions).
    *   Repositórios privados ou plataformas Low-Code proprietárias (sem acesso ao código fonte).
    *   Análise de qualidade de código estática (SonarQube) não está no escopo principal deste estudo de *processo*, mas sim a métrica de *tempo e esforço*.

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)
*   **Tipo de Organização:** Projetos Open Source mantidos majoritariamente por empresas comerciais (e.g., Appsmith Inc., Vercel, Facebook/Meta) com forte apoio da comunidade.
*   **Tipo de Projeto:** Ferramentas de desenvolvimento de software (Developer Tools), caracterizadas por alta complexidade técnica.
*   **Perfil de Experiência:** Desenvolvedores profissionais, mantenedores core e contribuidores open source distribuídos globalmente.

### 4.3 Premissas
*   As issues estão corretamente etiquetadas (labels como `bug`, `fix`, `type:bug`) nos repositórios selecionados, permitindo a filtragem automática.
*   O link entre issues e Pull Requests/Commits é rastreável na maioria dos casos (via "Closing keywords" do GitHub).
*   A API do GitHub permanecerá estável e acessível durante o período de coleta de dados.

### 4.4 Restrições
*   **Limitação de API:** O GitHub impõe um limite de 5.000 requisições por hora para usuários autenticados, o que pode prolongar o tempo de coleta.
*   **Tempo:** O experimento deve ser concluído dentro do semestre letivo.
*   **Acesso:** Impossibilidade de entrevistar os desenvolvedores para entender o contexto qualitativo de cada bug ("caixa preta").

### 4.5 Limitações previstas
*   **Viés de seleção:** Os repositórios escolhidos podem não representar todo o universo Low-Code/Tradicional, limitando a generalização (validade externa).
*   **Qualidade dos dados:** Issues podem ter sido fechadas sem correção real, ou correções feitas sem link explícito, gerando ruído nos dados.

---

## 5. Stakeholders e impacto esperado

### 5.1 Stakeholders principais
*   **CTOs e Decisores de Tecnologia:** Responsáveis pela escolha de stack tecnológica em empresas.
*   **Arquitetos de Software:** Interessados na manutenibilidade arquitetural e dívida técnica de longo prazo.
*   **Equipes de Desenvolvimento:** Interessados em saber se a ferramenta facilita ou dificulta o dia a dia de correções.
*   **Pesquisadores de Engenharia de Software:** Interesse na validação empírica de métricas de manutenção em novos paradigmas de desenvolvimento.

### 5.2 Interesses e expectativas dos stakeholders
*   **Decisores:** Esperam dados quantitativos para justificar o ROI e avaliar o risco de "lock-in" de manutenção difícil a longo prazo com Low-Code.
*   **Arquitetos:** Buscam evidências de que a abstração do Low-Code não cobra um preço alto demais em complexidade de manutenção.
*   **Pesquisador:** Espera identificar padrões distintos de evolução entre os dois paradigmas e publicar os resultados.

### 5.3 Impactos potenciais no processo / produto
*   **No Experimento:** A execução é passiva (mineração de dados históricos), portanto não há impacto direto nos produtos ou equipes analisadas.
*   **Pós-Experimento:** Os resultados podem influenciar diretrizes de adoção de Low-Code na indústria, potencialmente desencorajando o uso para sistemas críticos se a manutenibilidade for comprovadamente pior, ou validando a tecnologia caso seja equivalente/melhor.

---

## 6. Riscos de alto nível, premissas e critérios de sucesso

### 6.1 Riscos de alto nível (negócio, técnicos, etc.)
*   **Risco Técnico (Médio):** Dificuldade em normalizar dados entre repositórios com processos diferentes (ex: taxonomias de labels inconsistentes).
    *   *Mitigação:* Criar um mapa de equivalência de labels para cada repositório antes da análise.
*   **Risco de Dados (Alto):** Baixa quantidade de links explícitos entre Issue e Commit em alguns projetos, reduzindo a amostra para métricas de esforço (churn).
    *   *Mitigação:* Utilizar heurísticas de busca textual em mensagens de commit (e.g., "fixes #123") se os links diretos forem escassos.

### 6.2 Critérios de sucesso globais (go / no-go)
*   Coleta de pelo menos **1.000 issues válidas** (classificadas como bug e fechadas) de cada grupo (Low-Code vs Tradicional).
*   Capacidade de responder a pelo menos **80% das Questões de Pesquisa** com significância estatística (p-value < 0.05).
*   Identificação de pelo menos **3 repositórios comparáveis** em cada categoria.

### 6.3 Critérios de parada antecipada (pré-execução)
*   Se, durante a análise exploratória inicial, for identificado que menos de **10% das issues** possuem links rastreáveis para commits/PRs, a análise de "esforço de código" (Objetivo O2) será abortada ou reescopada, mantendo-se apenas a análise temporal (Objetivo O1), pois a mineração manual seria inviável pelo tempo disponível.