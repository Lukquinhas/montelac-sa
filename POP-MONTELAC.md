# POP-001 — Processo Produtivo Montelac S.A.

| Campo | Informação |
|---|---|
| Código | POP-001 |
| Título | Processo produtivo: da fabricação do chocolate à expedição |
| Versão | 1.0 |
| Data | 22/10/2026 |
| Elaborado por | Lucas Oliveira — Estagiário de Análise de Produção |
| Área | Produção |

---

## 0. Contexto do projeto (leia primeiro)

> **Este é um projeto de portfólio fictício.** A Montelac S.A., seus produtos, pessoas e números são inventados. Todos os dados usados no projeto são simulados e devem respeitar as regras deste documento.

**Cenário:** a Montelac S.A. é uma fábrica de chocolate que mantém todos os seus dados em papel (fichas de produção, apontamentos de turno, controle de estoque, registros de perdas). Isso impede a visualização de KPIs e a definição de estratégia.

**Papel do autor:** Lucas Oliveira foi contratado como estagiário de Análise de Produção para iniciar a transformação digital da empresa. O primeiro passo é estruturar os dados da produção, desde a fabricação do chocolate até os produtos finais.

**Dinâmica do projeto:** a cada novo conhecimento adquirido (cursos, faculdade), o líder direto passa um desafio aplicado à fábrica. O projeto cresce em complexidade ao longo do tempo.

**Instruções para assistentes de IA (Claude Code e similares):**

- Use este documento como fonte da verdade sobre o funcionamento da fábrica.
- Qualquer dado simulado deve respeitar receitas, capacidades, restrições de máquina, setups, regras de tanque, embalagem e formato de lotes descritos aqui.
- Se uma regra necessária não estiver definida aqui, pergunte antes de assumir.
- Consulte a seção 11 para saber quais desafios já foram concluídos.

---

## 1. Objetivo

Padronizar e documentar o funcionamento do processo produtivo da Montelac S.A., servindo como referência para operação, rastreabilidade e geração/validação de dados.

## 2. Escopo

Aplica-se a todas as etapas do processo:

1. Recebimento e dosagem de matérias-primas
2. Fabricação do chocolate (tanque de fabricação)
3. Armazenamento (tanques de armazenamento)
4. Envase (máquinas de produção)
5. Resfriamento
6. Embalagem, paletização e expedição para o depósito

## 3. Definições e siglas

| Sigla / termo | Significado |
|---|---|
| PCP | Planejamento e Controle da Produção. Emite a lista de ordens de produção |
| OP | Ordem de Produção |
| SKU | Código único de produto (tipo de chocolate + tamanho) |
| TF | Tanque de Fabricação |
| TA | Tanque de Armazenamento |
| M1–M4 | Máquinas de envase 1 a 4 |
| Batelada | Uma produção completa do tanque de fabricação |
| Setup | Parada para troca de molde e/ou de chocolate na máquina |
| Purga | Chocolate descartado na limpeza da linha de transferência durante troca de tipo |
| Lote com troca | Lote de armazenamento que recebeu novo tipo de chocolate sobre resíduo permitido |

## 4. Fluxo do processo

```
Matérias-primas → TF-01 (fabricação) → TA-01..TA-06 (armazenamento)
   → tubulação → M1..M4 (envase) → piscina com chiller (resfriamento)
   → embalagem (caixas de 12 kg) → pallet (40 caixas) → depósito → carregamento
```

---

## 5. Fabricação do chocolate

### 5.1 Tipos de chocolate

| Tipo | Código SKU | Código de lote |
|---|---|---|
| Ao leite | AL | 1 |
| Meio amargo | MA | 2 |
| 70% cacau | 70 | 3 |
| Branco | BR | 4 |

### 5.2 Receitas (% em massa por kg de chocolate)

| Matéria-prima | Ao leite | Meio amargo | 70% cacau | Branco |
|---|---|---|---|---|
| Massa de cacau | 12,0 | 45,0 | 60,0 | — |
| Manteiga de cacau | 20,0 | 12,5 | 10,0 | 30,0 |
| Açúcar | 45,0 | 42,0 | 29,5 | 45,0 |
| Leite em pó | 22,0 | — | — | 24,0 |
| Lecitina | 0,5 | 0,5 | 0,5 | 0,5 |
| Aroma de baunilha | 0,5 | — | — | 0,5 |
| **Total** | **100,0** | **100,0** | **100,0** | **100,0** |

### 5.3 Tanque de fabricação (TF-01)

| Parâmetro | Valor |
|---|---|
| Quantidade de tanques | 1 |
| Capacidade | 2.000 kg |
| Ciclo por batelada | 6 h |
| — Dosagem | 1 h |
| — Mistura e conchagem | 4 h |
| — Transferência para TA | 1 h |
| Bateladas máximas por dia | 4 |
| Capacidade máxima diária | 8.000 kg |

**Procedimento:**

1. Receber do PCP a lista de OPs e identificar o tipo de chocolate necessário.
2. Dosar cada matéria-prima conforme a receita (5.2) para a batelada.
3. Executar mistura e conchagem.
4. Gerar o lote de fabricação (seção 8.1).
5. Transferir para um tanque de armazenamento que atenda às regras da seção 6.2.

---

## 6. Armazenamento

### 6.1 Tanques de armazenamento

| Parâmetro | Valor |
|---|---|
| Tanques | TA-01 a TA-06 |
| Capacidade de cada tanque | 5.000 kg |
| Agitação | Contínua |

### 6.2 Regras de uso dos tanques

1. Cada tanque contém **apenas um tipo de chocolate**. Mistura é proibida.
2. Um tanque pode receber outra batelada do **mesmo tipo** a qualquer momento, desde que haja capacidade livre.
3. **Tolerância para troca de tipo:** um tanque só pode receber um tipo diferente se o resíduo do tipo anterior for **≤ 50 kg** (1% da capacidade).
   - Resíduo > 50 kg: transferência **bloqueada**.
   - Resíduo ≤ 50 kg: transferência **permitida**, e o armazenamento é registrado como **lote com troca**.
4. Exemplo: TA-03 com 2.000 kg de chocolate branco (40% da capacidade) **não** pode receber 70% cacau.

---

## 7. Produção (envase)

### 7.1 Tamanhos e SKUs

Tamanhos: **30 g, 100 g, 250 g, 500 g e 1 kg**. Todas as combinações de tipo × tamanho existem, totalizando **20 SKUs**.

Formato do SKU: `MTL-[tipo]-[gramas com 4 dígitos]`

| Tamanho | Ao leite | Meio amargo | 70% cacau | Branco |
|---|---|---|---|---|
| 30 g | MTL-AL-0030 | MTL-MA-0030 | MTL-70-0030 | MTL-BR-0030 |
| 100 g | MTL-AL-0100 | MTL-MA-0100 | MTL-70-0100 | MTL-BR-0100 |
| 250 g | MTL-AL-0250 | MTL-MA-0250 | MTL-70-0250 | MTL-BR-0250 |
| 500 g | MTL-AL-0500 | MTL-MA-0500 | MTL-70-0500 | MTL-BR-0500 |
| 1 kg | MTL-AL-1000 | MTL-MA-1000 | MTL-70-1000 | MTL-BR-1000 |

### 7.2 Capacidade nominal por máquina (kg/h)

| Tamanho | M1 | M2 | M3 | M4 |
|---|---|---|---|---|
| 30 g | 180 | 160 | — | — |
| 100 g | 300 | 280 | 260 | 200 |
| 250 g | 280 | 300 | 340 | 320 |
| 500 g | 220 | 260 | 360 | 380 |
| 1 kg | — | — | — | 450 |

**Restrições:**

- 30 g: somente M1 e M2.
- 1 kg: somente M4.
- 100 g, 250 g e 500 g: todas as máquinas, com eficiências diferentes.
- M1 e M2 são especializadas em itens pequenos; M3 e M4, em itens grandes.

### 7.3 Setup

Ordem de cor (do mais claro para o mais escuro): **Branco → Ao leite → Meio amargo → 70% cacau**

| Tipo de troca | Tempo | Perda de purga |
|---|---|---|
| Só tamanho (troca de molde, mesmo chocolate) | 30 min | 0 kg |
| Só chocolate, do mais claro para o mais escuro | 60 min | 15 kg |
| Só chocolate, do mais escuro para o mais claro | 120 min | 30 kg |
| Troca completa (tamanho + chocolate) | Tempo da troca de chocolate + 30 min | Igual à troca de chocolate |

Exemplos:

- MTL-AL-0100 → MTL-AL-0250: 30 min, 0 kg.
- MTL-AL-0250 → MTL-70-0250: 60 min, 15 kg.
- MTL-70-0250 → MTL-BR-0100: 120 + 30 = 150 min, 30 kg.

### 7.4 Procedimento

1. Receber a OP do PCP (SKU e quantidade).
2. Selecionar uma máquina permitida para o tamanho (7.2).
3. Selecionar um TA que contenha o tipo de chocolate da OP.
4. Executar o setup, se houver mudança de SKU (7.3).
5. Transferir o chocolate pela tubulação do TA até a máquina.
6. Envasar e enviar para o resfriamento.

---

## 8. Rastreabilidade

### 8.1 Lote de fabricação — 7 dígitos

Formato: `AA SS T NN`

| Parte | Significado |
|---|---|
| AA | Ano (2 dígitos) |
| SS | Semana da fabricação |
| T | Código do tipo de chocolate (1 = AL, 2 = MA, 3 = 70, 4 = BR) |
| NN | Sequencial da batelada na semana (01 a 28) |

Exemplo: **2642103** = ano 2026, semana 42, ao leite, batelada 03.

Como existe apenas um TF, o `NN` é único na semana para todos os tipos.

### 8.2 Lote de embalagem — 8 dígitos

Formato: `AA SS 0 NN M`

| Parte | Significado |
|---|---|
| AA | Ano da **fabricação** |
| SS | Semana da **fabricação** |
| 0 | Separador fixo |
| NN | Sequencial da batelada de fabricação (mesmo NN do lote 8.1) |
| M | Máquina de envase (1 a 4) |

Exemplo: **26420031** = batelada 03 da semana 42 de 2026, envasada na M1.

### 8.3 Regras de lote

1. **Calendário:** a semana começa no **domingo às 00:00** (virada de sábado para domingo). A semana 01 é a que contém o dia 1º de janeiro. O `NN` zera a cada nova semana.
2. **Virada de semana:** `AA SS` do lote de embalagem é sempre a semana da **fabricação**, não a do envase. A data real do envase fica registrada na OP.
3. **Tanque com várias bateladas:** o lote de embalagem usa a **batelada mais recente** que entrou no TA de origem. Se uma nova batelada entrar no TA durante uma OP, o lote de embalagem muda a partir desse momento. O sistema registra quais bateladas estavam em cada TA em cada instante.
4. **Lote repetido:** a mesma batelada envasada na mesma máquina em OPs diferentes gera o mesmo lote de embalagem. O lote identifica a origem (batelada + máquina); a OP diferencia as corridas.

### 8.4 Cadeia de rastreio

```
Pallet → Caixa → Lote de embalagem → Máquina → TA de origem
       → Lote de fabricação → Matérias-primas (receita)
```

### 8.5 Registro da OP

Cada OP gera um registro com: número da OP, SKU, quantidade, máquina, TA de origem, lote de fabricação, lote de embalagem, data/hora de início e fim, e número do(s) pallet(s).

---

## 9. Resfriamento

| Parâmetro | Valor |
|---|---|
| Equipamento | Piscina de água resfriada por chiller + esteira |
| Temperatura da água | 8 °C |
| Tempo de travessia | 20 min |
| Saída | Chocolate frio e rígido, pronto para embalar |

---

## 10. Embalagem e expedição

### 10.1 Caixa

Peso líquido padrão: **12 kg** por caixa. Cada caixa contém apenas um SKU.

| Tamanho | Unidades por caixa | Unidades por pallet |
|---|---|---|
| 30 g | 400 | 16.000 |
| 100 g | 120 | 4.800 |
| 250 g | 48 | 1.920 |
| 500 g | 24 | 960 |
| 1 kg | 12 | 480 |

### 10.2 Pallet

| Parâmetro | Valor |
|---|---|
| Caixas por pallet | 40 |
| Produto por pallet | 480 kg |
| Madeira + filme stretch | ~20 kg |
| Peso total | ~500 kg |
| SKUs por pallet | 1 |

### 10.3 Procedimento

1. Receber o chocolate resfriado da esteira.
2. Embalar nas caixas conforme a quantidade por SKU (10.1).
3. Cadastrar no sistema de rastreio com OP, quantidade e lote de embalagem (8.2).
4. Montar o pallet com 40 caixas do mesmo SKU.
5. Destinar o pallet fechado ao depósito, aguardando carregamento.

---

## 11. Histórico de desafios do projeto

| # | Data | Conhecimento aplicado | Desafio | Status |
|---|---|---|---|---|
| — | — | — | Nenhum desafio iniciado | — |

---

## 12. Controle de revisões

| Versão | Data | Descrição |
|---|---|---|
| 1.0 | 22/10/2026 | Criação do documento: fabricação, armazenamento, envase, setup, resfriamento, embalagem e rastreabilidade |
