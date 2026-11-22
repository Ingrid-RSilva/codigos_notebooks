# Impacto do design UX/UI assistido por IA Generativa na experiência e inclusão de usuários finais

Código da análise de dados do Trabalho de Conclusão de Curso (TCC) em Engenharia de Software da Faculdade iCEV (Teresina, 2026).

- **Autora:** Ingrid Ribeiro Silva
- **Orientadoras:** Lia Mariana Nascimento Brito e Karoline Farias

## Sobre a pesquisa

A pesquisa avalia se um material de apoio de UX/UI e acessibilidade, usado no desenvolvimento de interfaces assistido por IA Generativa (ChatGPT, Gemini e Claude), melhora a experiência, a usabilidade e a acessibilidade percebidas por usuários finais, considerando o nível de *expertise* dos profissionais.

O estudo é quase experimental, entre grupos, e tem duas etapas:

1. **Construção das páginas.** 16 profissionais (desenvolvedores e designers de UX/UI) construíram, com IA Generativa, uma *landing page* para uma escola de culinária fictícia. O **G1** (8 participantes) trabalhou sem o material de apoio, e o **G2** (8 participantes) trabalhou com ele. Ao final, cada profissional respondeu a um questionário sobre o processo.
2. **Avaliação das páginas.** As 16 páginas passaram por uma verificação técnica de acessibilidade (axe DevTools e WAVE) e foram testadas por 17 usuários finais, 8 deles com deficiência, daltonismo ou idosos. Ao todo, foram 49 avaliações com tarefas, a escala SUS (*System Usability Scale*) e o questionário UEQ-S (*User Experience Questionnaire*, versão curta).

Hipóteses examinadas no experimento:

- **H1:** profissionais que usam IA sem apoio tendem a confiar nas sugestões da ferramenta sem validá-las com usuários.
- **H2:** o material de apoio melhora a qualidade e a acessibilidade da experiência final.

## Conteúdo do repositório

```
.
├── notebooks/
│   ├── 1_questionario_profissionais.ipynb
│   ├── 2_testes_usuarios.ipynb
│   └── 3_figura_aim_sus.ipynb
├── dados/            # planilhas de respostas (não versionadas; ver "Dados")
├── figuras/          # figuras geradas pelos notebooks (criada automaticamente)
├── requirements.txt
└── README.md
```

| Notebook | O que calcula | Onde aparece no TCC |
| --- | --- | --- |
| `1_questionario_profissionais.ipynb` | Comparação G1 × G2 no questionário final dos profissionais: mediana e intervalo interquartil, teste de Mann-Whitney, delta de Cliff, teste exato de Fisher, correlações de Spearman e correção de Holm | Resultados, seção "Processo de construção pelos profissionais" (Tabela 2) |
| `2_testes_usuarios.ipynb` | Perfil dos usuários, conclusão e facilidade das tarefas, SUS, UEQ-S e confiança; comparação entre grupos por página, comparação dentro de cada usuário (Wilcoxon), resultados por perfil e preferência declarada | Resultados, seção "Testes com usuários finais" (Tabelas 4 e 5) |
| `3_figura_aim_sus.ipynb` | Relação entre o AIM Score do WAVE e o SUS médio de cada página, com o número de violações do axe | Discussão (figura "AIM Score do WAVE e SUS médio de cada página, por grupo") |

Os valores de AIM Score e de violações do axe usados no notebook 3 vêm da verificação técnica feita em 16 nov. 2026 (axe DevTools, axe-core 4.13.0, WCAG 2.1 AA, e WAVE) e estão no próprio código, porque não foram coletados por formulário.

## Métodos estatísticos

Como a amostra é pequena e as escalas são ordinais, a análise usa estatística não paramétrica:

- **Descrição:** mediana e intervalo interquartil (IIQ).
- **Comparação entre grupos:** teste de Mann-Whitney para variáveis ordinais e teste exato de Fisher para proporções, com significância de 5%.
- **Tamanho de efeito:** delta de Cliff (δ), de −1 a +1, positivo quando o G2 tem resultado mais alto.
- **Associação:** correlação de Spearman (ρ).
- **Comparações múltiplas:** correção de Holm.
- **Comparação dentro de cada usuário:** teste de Wilcoxon, entre a média das páginas do G1 e a das páginas do G2 que o usuário avaliou.

Nos testes com usuários, as comparações entre grupos usam a média de cada página (8 por grupo), e não cada avaliação, para não contar o mesmo usuário várias vezes. Todas as análises são exploratórias.

## Como executar

### Requisitos

- Python 3.11 ou superior (testado com Python 3.13 e 3.14)
- Jupyter, ou VS Code com a extensão Jupyter
- Bibliotecas listadas em `requirements.txt`: pandas, numpy, scipy, matplotlib e openpyxl

### Passo a passo

1. Clone o repositório e entre na pasta:

   ```bash
   git clone <url-do-repositório>
   cd <pasta-do-repositório>
   ```

2. (Recomendado) Crie e ative um ambiente virtual:

   ```bash
   python -m venv .venv
   # Windows
   .venv\Scripts\activate
   # Linux/macOS
   source .venv/bin/activate
   ```

3. Instale as dependências:

   ```bash
   python -m pip install -r requirements.txt
   ```

4. Coloque as planilhas de respostas na pasta `dados/`, com os nomes da seção "Dados".
5. Abra os notebooks da pasta `notebooks/`, selecione como *kernel* o Python do ambiente criado e execute todas as células (**Run All**). Os notebooks são independentes e podem ser executados em qualquer ordem.

Se aparecer o erro `ModuleNotFoundError`, o *kernel* selecionado não é o Python em que as bibliotecas foram instaladas. Troque o *kernel* e reinicie o notebook.

## Dados

As planilhas de respostas **não estão neste repositório**. Elas contêm dados pessoais dos participantes, e o Termo de Consentimento Livre e Esclarecido restringe o acesso aos dados individuais à pesquisadora, às orientadoras e à banca avaliadora, em conformidade com a Lei Geral de Proteção de Dados (Lei nº 13.709/2018). Por isso, a pasta `dados/` está no `.gitignore`.

Para executar os notebooks com os dados originais, a pasta `dados/` deve conter:

| Arquivo | Conteúdo |
| --- | --- |
| `Questionario_Final_Grupo_1_respostas.xlsx` | Questionário final dos profissionais do G1 |
| `Questionario_Final_Grupo_2_respostas.xlsx` | Questionário final dos profissionais do G2 |
| `Questionario_Usuario_Final_respostas.xlsx` | Perfil dos usuários finais |
| `Questionario_avaliacao_landing_page_usuario_final_respostas.xlsx` | Avaliação de cada página pelos usuários finais (tarefas, SUS, UEQ-S e comentários) |

As planilhas são as exportações dos formulários do Google Forms, sem edição. Os participantes são identificados por códigos, e cada página recebeu o mesmo código do profissional que a construiu.

## Observações sobre o tratamento dos dados

- **Pontuação da SUS:** nos itens ímpares, a nota é a resposta menos 1; nos pares, 5 menos a resposta. A soma é multiplicada por 2,5, o que gera um escore de 0 a 100.
- **Pontuação do UEQ-S:** as respostas de 1 a 7 são convertidas para a escala de −3 a +3. As médias são consideradas positivas acima de +0,8 e negativas abaixo de −0,8.
