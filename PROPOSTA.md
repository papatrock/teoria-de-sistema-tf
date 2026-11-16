# Proposta do Trabalho Final: CI1220 Teoria de Sistemas (2026/2)

> Documento-guia do grupo. Antes de escrever qualquer seção, conferir se ela segue o que está aqui.
> Última atualização: 14/11/2026

---

## 1. Ideia geral em um parágrafo

Um hospital é um **sistema aberto sociotécnico**: pessoas, tecnologias, normas e informação
interagem e trocam com o ambiente (pacientes, fornecedores, nuvem, governo). Quando esse hospital
passa a depender de **IA clínica** e de **nuvem híbrida**, surgem perturbações novas: o modelo de IA
perde desempenho porque o perfil de pacientes mudou (*drift*), ou o serviço em nuvem fica fora do ar.
Essas perturbações **não ficam presas na TI**: elas se propagam para a assistência, a administração
e o financeiro. O trabalho usa os conceitos da disciplina (sistema, infosfera, entropia, cibernética,
realimentação, variedade requisita) para mostrar **por que** isso acontece e **como** um plano de
segurança e continuidade pode manter o sistema estável. Para isso, aplica a análise a um hospital
hipotético, o **Hospital Geral Vida Plena (HGVP)**.

**Pergunta do trabalho:** como a Teoria de Sistemas ajuda a estruturar a governança de IA e a
resiliência em nuvem híbrida de um hospital, de forma que uma falha em um componente não comprometa
o funcionamento do todo?

**Tese que queremos sustentar:** segurança é uma **propriedade emergente do sistema**, e não de uma
ferramenta isolada. Por isso, a resposta precisa combinar controles técnicos, humanos e
organizacionais (variedade requisita) e precisa de mecanismos de realimentação que detectem desvios e
corrijam o sistema (cibernética).

---

## 2. Como o trabalho se encaixa no enunciado

O enunciado pede um trabalho sobre **um dos títulos da lista**, com referências de **2022 a 2026**,
"de artigos científicos e/ou de experiências técnicas (colocando a sustentação teórica)".

- **Títulos atendidos:** *Governança de IA em sistemas corporativos* (eixo principal) e *Segurança
  em ambientes multicloud e híbridos* (eixo complementar). Também tocamos *Marco Legal de IA no
  Brasil* (PL 2338/2023), mas só como contexto regulatório.
- **O hospital é o caso de aplicação, não o tema.** O tema é governança de IA e nuvem híbrida
  analisadas como sistema; o HGVP é o "laboratório" onde os conceitos são aplicados.

### Conteúdos da disciplina que o trabalho usa

| Conteúdo da disciplina (lista da professora) | Onde aparece no trabalho |
|---|---|
| Sistemas: conceitos e estruturas; **Infosfera (Floridi)**; sistemas computacionais | 2.1: hospital como sistema aberto inserido na infosfera |
| **Entropia** | 2.4: entropia/ruído (Shannon) e desorganização do sistema; fadiga de alertas como ruído |
| Requisitos de estabilidade; **casos emblemáticos** | 2.2 e 2.3 (realimentação, homeostase, variedade requisita); cenários baseados em casos reais (seção 3.7) |
| Sistemas de TI, organizacionais e normativos | 3.1 a 3.3: subsistemas do HGVP (assistencial, administrativo, tecnológico, financeiro) e camada normativa |
| **Indicadores/parâmetros para a segurança do sistema** | 3.5: indicadores como realimentação; só o *que* medir e *como* definir a meta, nunca valores inventados |
| **LGPD** aplicada à TI | 2.5 e 3.6: dado de saúde como dado sensível; comunicação de incidente (ANPD 15/2024) |
| Planos corporativos de mitigação de riscos | 3.5: plano de segurança |
| **Planos de continuidade**: caracterização e estruturas | 3.6 |
| Análise dos planos pelos **eixos**: treinamentos, comunicações, mapeamentos, infraestrutura, tecnologias, regramentos internos, investimentos, monitoramentos | **Proposta: organizar o plano (3.5) por esses 8 eixos** e mapear cada eixo às funções do NIST CSF 2.0 |
| Eventos e riscos que provocam problemas nos sistemas | 3.4 (riscos) e 3.7 (cenários de falha) |

---

## 3. De onde partimos

### Versão 1 (tf-antigo-1): reprovada na apresentação

Críticas da professora:
1. **Estrutura fora do lugar:** o hospital era descrito antes da teoria; a fundamentação tinha 3
   páginas e misturava conceitos com normas.
2. **O grupo não sabia de onde vinham os dados:** os quadros eram quase todos "elaboração do grupo".
3. **Números inventados no hospital fictício:** 450 leitos, matriz P×I, RTO/RPO, metas de 99,95%,
   falsos alertas de 15% → 65%. Ela disse que **nem era para pôr valores** no hospital fictício.
4. Referências fora da faixa de 2022 a 2026 e normas ISO pagas que ninguém leu.

### Versão 2 (tf-antigo-2): reescrita de um colega

- **Acertos aproveitados:** ordem teoria → literatura → metodologia → aplicação; regras de
  rastreabilidade (Quadro 3); não fixar RTO/RPO, mas explicar o método para defini-los; cenário de
  sepse sem percentuais inventados.
- **Problemas:** manteve os "450 leitos"; texto longo (40 páginas, 9 capítulos); citação colada no
  fim de quase todo parágrafo; **3 referências não existem** (Kruse 2026, Wang 2026, Shahrour 2026).

### Versão final (esta)

Mantém o tema e o hospital, mas:
- toda referência tem arquivo em `referencias/` e foi conferida (ver `referencias/LISTA.md`);
- nenhum número descreve o HGVP;
- todo conceito do Capítulo 2 é usado no Capítulo 3, e o que não for usado sai;
- os cenários partem de **casos reais documentados**, e não de situações inventadas.

---

## 4. Metodologia

### 4.1 Tipo de pesquisa
Qualitativa, bibliográfica e documental, de caráter **propositivo**. Não houve coleta de dados em
hospital real, entrevistas nem experimentos. O HGVP é um **cenário hipotético de aplicação**.

### 4.2 Seleção das fontes
- **Conceitos da disciplina:** obras clássicas, por serem a fonte original dos conceitos
  (Bertalanffy, Wiener, Ashby, Shannon), mais Leveson (segurança como propriedade emergente) e
  Floridi (infosfera). Essas ficam fora da faixa 2022–2026 por serem a origem dos conceitos, e isso
  é dito explicitamente no texto.
- **Estado atual do problema:** artigos revisados por pares de 2022 a 2026, de preferência revisões
  sistemáticas ou de escopo (Ewoh 2024, Qureshi 2026, Martin 2026, Anian 2025, Svandova 2024,
  Abbas 2025, Sahiner 2023, Freeman 2026, Hassan 2025, Ray 2026, Fallon 2024).
- **"Experiências técnicas"** (termo do enunciado): frameworks e documentos oficiais (NIST CSF 2.0,
  NIST AI RMF, HICP 2023, TIC Saúde 2024, LGPD, Resolução ANPD 15/2024, Portaria MS 7.678/2025).
- **Exceção justificada:** Finlayson et al. (2021), por ser o registro do caso real que sustenta o
  cenário de IA.

### 4.3 Regras de rastreabilidade (respondem a "de onde veio isso?")

| Tipo de informação | Regra | Exemplo |
|---|---|---|
| Conceito teórico | Citar a fonte original | Variedade requisita (Ashby, 1956) |
| Dado do mundo real | Número só com fonte, no mesmo trecho, e descrevendo o mundo real | "Modelos de IA para sepse relatam AUC entre 0,79 e 0,96 (Abbas et al., 2025)" |
| Obrigação legal | Citar o artigo da norma e dizer se está vigente | Comunicação à ANPD em 3 dias úteis (Res. 15/2024, art. 6º) |
| Característica do HGVP | **Só qualitativa**, justificada pela literatura ("é comum que hospitais...") | "O HGVP usa PEP integrado ao laboratório", apoiado na TIC Saúde 2024 |
| Meta ou parâmetro (RTO, RPO, metas) | **Não fixar valor.** Descrever o método para defini-lo | "O RTO do PEP seria definido por análise de impacto com a área clínica" |
| Cenário de falha | Transpor um caso real documentado para o HGVP | Michigan/Epic sepse (Finlayson, 2021) → cenário de drift no HGVP |
| Proposta do grupo | Identificar como proposta e indicar o conceito ou fonte que a justifica | "Propõe-se um comitê de IA (realimentação), conforme Freeman et al. (2026)" |

### 4.4 Como a análise é feita
Para cada parte do hospital seguimos a mesma sequência:
**conceito (cap. 2) → como ele aparece no HGVP → qual risco ele revela → qual controle o plano propõe.**

---

## 5. Onde queremos chegar

### 5.1 Produto final
Um texto de cerca de 20 a 25 páginas, nas normas UFPR (modelo LaTeX), contendo:
1. Fundamentação teórica enxuta, em que cada conceito é usado depois.
2. Caracterização sistêmica do HGVP: atores, estrutura, fluxos de informação e subsistemas, sem
   números.
3. Mapa de riscos com a fonte que sustenta cada risco.
4. Plano de segurança e continuidade organizado pelos 8 eixos da disciplina.
5. Dois cenários de falha:
   - **Ransomware**, como perturbação externa que se propaga entre subsistemas (base: Martin 2026);
   - **Drift em IA de triagem de sepse**, como perturbação vinda do ambiente que gera realimentação
     positiva (excesso de alertas → fadiga → menos atenção ao alerta verdadeiro) (base: Finlayson
     2021, Sahiner 2023, Ray 2026, Fallon 2024).
6. Conclusão sistêmica e limitações.

### 5.2 Critérios de "pronto" (checklist antes de entregar)
- [ ] Toda citação tem arquivo em `referencias/` e está no `.bib`.
- [ ] Nenhum número descreve o HGVP.
- [ ] Todo conceito do cap. 2 aparece no cap. 3.
- [ ] Todo quadro tem fonte que não seja só "elaboração do grupo"; quando for nosso, diz "com base em…".
- [ ] Qualquer membro do grupo consegue responder "de onde veio isso?" para qualquer frase.
- [ ] Os 8 eixos da disciplina aparecem no plano.
- [ ] Referências recentes (2022–2026) são a maioria; os clássicos estão justificados.

---

## 6. Estrutura do texto

| Cap./Seção | Conteúdo | Conceitos/fontes principais |
|---|---|---|
| 1 Introdução | Contexto, problema, objetivo, organização | TIC Saúde 2024, Ewoh 2024 |
| 2.1 Sistema, ecossistema e infosfera | Sistema aberto, fronteira, subsistemas, equifinalidade, propriedade emergente, infosfera | Bertalanffy, Leveson, Floridi |
| 2.2 Cibernética e realimentação | Controle, feedback negativo e positivo, homeostase | Wiener (1970), Leveson |
| 2.3 Variedade requisita | "Só variedade absorve variedade" | Ashby |
| 2.4 Informação, entropia e atributos | Fonte, canal, ruído, entropia; CID e demais atributos; princípios da LGPD | Shannon, LGPD |
| 2.5 Segurança e governança de IA em saúde | Vulnerabilidades sociotécnicas; gestão de risco; governança de IA; drift; nuvem; legislação | Ewoh, Qureshi, NIST CSF, NIST AI RMF, Freeman, Hassan, Sahiner, Portaria 7.678, ANPD, Gonçalves |
| 3.1 Método | Seção 4 deste documento (regras de rastreabilidade) | — |
| 3.2 Caracterização do HGVP | Perfil qualitativo; hospital como sistema aberto | TIC Saúde, Bertalanffy |
| 3.2 Atores | Internos e externos | — |
| 3.3 Estrutura e fluxos | Sistemas, IoMT, nuvem híbrida, interoperabilidade, subsistemas | Anian, Svandova |
| 3.4 Riscos | Categorias, com a fonte de cada risco | Ewoh, Qureshi, Martin |
| 3.5 Plano | 8 eixos da disciplina ↔ NIST CSF; indicadores como realimentação | NIST, Ashby, Wiener |
| 3.6 Continuidade e compliance | Continuidade; LGPD/ANPD; requisito → controle → evidência | ANPD, LGPD |
| 3.7 Cenários | Ransomware; drift em IA de sepse | Martin; Finlayson, Sahiner, Abbas, Ray, Fallon |
| 4 Considerações finais | Resposta à pergunta, limitações, trabalhos futuros | — |

**Ordem de escrita:** cap. 2 (pronto) → cap. 3 (rascunho pronto em 14/11; revisar após a aula de 16/11) → 4 → 1 → resumo.

> A numeração do cap. 3 no LaTeX ficou: 3.1 Método, 3.2 Caracterização, 3.3 Atores, 3.4 Estrutura e fluxos, 3.5 Riscos, 3.6 Plano (8 eixos), 3.7 Continuidade e compliance, 3.8 Cenários.

---

## 7. Pendências

- [ ] **Decidir** se o plano é organizado pelos 8 eixos da professora (recomendado) ou pelas funções do NIST CSF.
- [ ] **Decidir** o título final (sugestão: manter o subtítulo "com foco em governança de IA e resiliência em nuvem híbrida").
- [ ] **Floridi (infosfera):** conseguir uma referência; a disciplina cita, mas ainda não temos arquivo.
- [ ] Baixar Ray 2026, Fallon 2024, HICP 2023 e Leveson 2011 (ver `LISTA.md`).
- [ ] Confirmar a edição do Bertalanffy (Wiener: *Cibernética e Sociedade*, Cultrix, 1970, decidido).
- [ ] Achar um artigo de 2022 a 2026 específico sobre nuvem/híbrido em saúde.
- [ ] Confirmar a situação atual do PL 2338/2023 na ficha de tramitação.
- [ ] As categorias de risco do esqueleto (equipe, tecnologia, protocolos…) vieram das versões
      antigas, não do enunciado: confirmar a origem ou trocar pelos "eventos e riscos" da disciplina.
