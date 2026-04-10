# 03. Framework Reutilizável — Inferência Estatística para Métricas Numéricas

## 1. Objetivo

Este framework tem como objetivo padronizar a análise estatística inferencial de qualquer métrica numérica, permitindo:

- compreender a distribuição dos dados
- extrair amostras
- estimar parâmetros populacionais
- construir intervalos de confiança
- diagnosticar premissas
- escolher entre métodos paramétricos e não paramétricos
- transformar análise estatística em decisão prática

---

## 2. Quando utilizar este framework

Este fluxo é indicado quando desejamos inferir características de uma população a partir de uma amostra, especialmente para métricas como:

- satisfação
- receita
- tempo
- valor
- volume
- score
- nota
- frequência

---

## 3. Estrutura conceitual

### 3.1 Pergunta analítica

A estrutura da pergunta deve seguir este padrão:

> Qual é o valor esperado da métrica `[nome_da_metrica]` para a população de `[unidade_de_analise]`, e qual a incerteza associada a essa estimativa?

**Exemplos:**

- Qual é a média de `NPS` dos clientes ativos?
- Qual é o tempo médio de `atendimento` por chamado?
- Qual é o valor médio de `compra` por pedido?
- Qual é a nota média de `satisfação` por usuário?

---

## 4. Pipeline estatístico reutilizável

### 4.1 Definição da métrica

Antes de iniciar a análise, defina claramente:

- o que será medido
- qual é a unidade de análise
- qual é o período observado
- qual é a escala da métrica
- se há regras de tratamento para valores ausentes ou extremos

**Template:**

- **Métrica:** `[nome_da_metrica]`
- **Unidade de análise:** `[cliente, pedido, ticket, atendimento, usuário...]`
- **Período:** `[jan/2025, últimos 30 dias, trimestre...]`
- **Tipo da variável:** `[discreta ou contínua]`
- **Escala:** `[intervalo válido ou domínio esperado]`

---

### 4.2 Construção ou leitura da base

Nesta etapa, devemos obter uma base contendo ao menos a coluna da métrica.

**Estrutura mínima esperada:**

| id_unidade | metrica |
|-----------|---------|
| 1 | ... |
| 2 | ... |
| 3 | ... |

---

### 4.3 Análise exploratória inicial

Objetivo: entender o comportamento geral dos dados antes da inferência.

#### 4.3.1 Estatísticas descritivas

Avaliar:

- média
- mediana
- desvio padrão
- mínimo e máximo
- quartis
- assimetria
- curtose

#### 4.3.2 Diagnóstico visual

Gerar:

- histograma
- boxplot
- Q-Q plot

#### 4.3.3 Diagnóstico formal

Aplicar:

- teste de normalidade (Shapiro-Wilk, quando fizer sentido)
- análise de outliers
- comparação entre média e mediana

---

### 4.4 Processo de amostragem

Quando não tivermos acesso à população inteira, devemos coletar uma amostra.

Registrar:

- método de amostragem
- tamanho da amostra
- possíveis vieses
- limitações do processo

**Possíveis métodos:**

- amostragem aleatória simples
- amostragem estratificada
- amostragem por conveniência

---

### 4.5 Distribuição amostral

Objetivo: compreender como o estimador se comporta sob repetição do processo de amostragem.

Nesta etapa, simulamos múltiplas amostras e observamos:

- distribuição das médias amostrais
- estabilidade do estimador
- evidência do Teorema Central do Limite

---

### 4.6 Intervalo de confiança

A partir da amostra, construímos uma faixa plausível para o parâmetro populacional.

Registrar:

- estimador utilizado
- nível de confiança
- erro padrão
- margem de erro
- limites do intervalo

---

### 4.7 Diagnóstico de premissas

Antes de escolher o método final, avaliar:

- amostra pequena?
- distribuição assimétrica?
- presença de outliers?
- normalidade plausível?
- variável discreta com forte concentração?
- caudas pesadas?

---

### 4.8 Escolha metodológica

#### Usar t-Student quando:

- a métrica for aproximadamente simétrica
- a amostra não for muito pequena
- não houver outliers severos
- a normalidade for plausível ou o tamanho amostral compensar

#### Usar bootstrap quando:

- a amostra for pequena
- houver assimetria relevante
- houver outliers
- a distribuição for não usual
- houver dúvida sobre robustez do método paramétrico

---

### 4.9 Comparação entre métodos

Quando houver risco estatístico relevante, comparar:

- intervalo via t-Student
- intervalo via bootstrap

Avaliar:

- largura do intervalo
- deslocamento dos limites
- sensibilidade às premissas

---

### 4.10 Tomada de decisão

Conectar o resultado estatístico ao problema real.

Perguntas finais:

- a estimativa é estável?
- a incerteza é aceitável?
- o método escolhido foi adequado aos dados?
- qual decisão pode ser tomada com base nesse intervalo?

---

## 5. Template de documentação por métrica

## 5.1 Contexto

### 5.1.1 O que é a métrica?

### 5.1.2 Por que ela é importante para o negócio?

### 5.1.3 Qual é a unidade de análise?

### 5.1.4 Qual é o período observado?

---

## 5.2 Construção da base

### 5.2.1 Origem dos dados

### 5.2.2 Estrutura da base

### 5.2.3 Tratamento inicial

---

## 5.3 Análise exploratória

### 5.3.1 Estatísticas descritivas

### 5.3.2 Histograma

### 5.3.3 Boxplot

### 5.3.4 Q-Q Plot

### 5.3.5 Teste de normalidade

### 5.3.6 Assimetria e curtose

---

## 5.4 Amostragem

### 5.4.1 Estratégia de amostragem

### 5.4.2 Tamanho da amostra

### 5.4.3 Comparação entre população e amostra

---

## 5.5 Distribuição amostral

### 5.5.1 Simulação de múltiplas amostras

### 5.5.2 Distribuição das médias

### 5.5.3 Interpretação

---

## 5.6 Intervalos de confiança

### 5.6.1 Intervalo com t-Student

### 5.6.2 Interpretação do intervalo

### 5.6.3 Limitações

---

## 5.7 Cenário problemático

### 5.7.1 Amostra pequena

### 5.7.2 Assimetria

### 5.7.3 Outliers

### 5.7.4 Violação de premissas

---

## 5.8 Bootstrap

### 5.8.1 Intuição

### 5.8.2 Reamostragem

### 5.8.3 Intervalo bootstrap

### 5.8.4 Comparação com t-Student

---

## 5.9 Decisão final

### 5.9.1 Método recomendado

### 5.9.2 Justificativa estatística

### 5.9.3 Impacto para o negócio

---

## 6. Template de variáveis reutilizáveis no código

Use sempre nomes genéricos para facilitar reaproveitamento:

- `df`
- `col_metrica`
- `media_pop`
- `media_amostra`
- `desvio_amostra`
- `amostra`
- `medias_amostrais`
- `ic_inf`
- `ic_sup`
- `ic_inf_boot`
- `ic_sup_boot`

---

## 7. Template de código reutilizável

```python
# CONFIGURAÇÃO INICIAL
col_metrica = "nome_da_metrica"
n_amostra = 80
nivel_confianca = 0.95
n_boot = 10000
```

```python
# ESTATÍSTICAS DESCRITIVAS
media = df[col_metrica].mean()
mediana = df[col_metrica].median()
desvio = df[col_metrica].std()

assimetria = stats.skew(df[col_metrica])
curtose = stats.kurtosis(df[col_metrica])

print(f"Média: {media:.3f}")
print(f"Mediana: {mediana:.3f}")
print(f"Desvio padrão: {desvio:.3f}")
print(f"Assimetria: {assimetria:.3f}")
print(f"Curtose: {curtose:.3f}")
```

```python
# HISTOGRAMA
plt.figure(figsize=(10, 5))
plt.hist(df[col_metrica], bins=30, edgecolor="black")
plt.axvline(media, linestyle="--", label="Média")
plt.axvline(mediana, linestyle=":", label="Mediana")
plt.title(f"Distribuição de {col_metrica}")
plt.legend()
plt.show()
```

```python
# BOXPLOT
plt.figure(figsize=(10, 2.5))
plt.boxplot(df[col_metrica], vert=False)
plt.title(f"Boxplot de {col_metrica}")
plt.show()
```

```python
# Q-Q PLOT
plt.figure(figsize=(6, 6))
stats.probplot(df[col_metrica], dist="norm", plot=plt)
plt.title(f"Q-Q Plot de {col_metrica}")
plt.show()
```

```python
# SHAPIRO
subamostra = df[col_metrica].sample(min(500, len(df)), random_state=42)
stat, p_valor = stats.shapiro(subamostra)

print(f"p-valor: {p_valor:.6f}")
```

```python
# AMOSTRAGEM
amostra = df.sample(n=n_amostra, random_state=123)
```

```python
# IC T-STUDENT
n = len(amostra)
media_amostra = amostra[col_metrica].mean()
desvio_amostra = amostra[col_metrica].std(ddof=1)

erro = desvio_amostra / np.sqrt(n)
t_critico = stats.t.ppf((1 + nivel_confianca) / 2, df=n-1)
margem = t_critico * erro

ic_inf = media_amostra - margem
ic_sup = media_amostra + margem

print(f"IC t-Student: ({ic_inf:.3f}, {ic_sup:.3f})")
```

```python
# BOOTSTRAP
medias_boot = []

for _ in range(n_boot):
    reamostra = amostra[col_metrica].sample(n=len(amostra), replace=True)
    medias_boot.append(reamostra.mean())

medias_boot = np.array(medias_boot)

ic_inf_boot = np.percentile(medias_boot, 2.5)
ic_sup_boot = np.percentile(medias_boot, 97.5)

print(f"IC Bootstrap: ({ic_inf_boot:.3f}, {ic_sup_boot:.3f})")
```

---

## 8. Framework de decisão

Use esta lógica prática:

### Escolha `t-Student` se:

- `n >= 30`
- assimetria moderada
- poucos outliers
- distribuição aceitável

### Escolha `Bootstrap` se:

- `n < 30`
- assimetria alta
- outliers relevantes
- forte desvio da normalidade

---

## 9. Checklist final

- [ ] Métrica definida claramente
- [ ] Unidade de análise definida
- [ ] Base validada
- [ ] Estatísticas descritivas calculadas
- [ ] Histograma gerado
- [ ] Boxplot gerado
- [ ] Q-Q plot gerado
- [ ] Normalidade avaliada
- [ ] Amostra coletada
- [ ] Intervalo com t-Student calculado
- [ ] Bootstrap calculado, se necessário
- [ ] Método final justificado
- [ ] Decisão conectada ao negócio

---

## 10. Conclusão

Este framework transforma uma análise estatística isolada em um processo reutilizável, auditável e adaptável para diferentes métricas de negócio.

A principal vantagem não está apenas em reaproveitar código, mas em padronizar o raciocínio analítico:
diagnóstico, inferência, validação e decisão.