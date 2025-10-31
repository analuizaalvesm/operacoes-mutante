# Laboratório: Teste de Mutação com a "Calculadora Mutante"

Bem-vindo ao trabalho prático de Teste de Mutação. O objetivo deste projeto é usar a ferramenta StrykerJS para avaliar e fortalecer uma suíte de testes que, à primeira vista, parece boa.

## Contexto

Este repositório contém uma biblioteca de cálculos simples. A suíte de testes inicial em `__tests__/` foi projetada para ter uma alta **cobertura de código**, mas esconde fraquezas que só o **teste de mutação** pode revelar.

Sua missão é atuar como um engenheiro de qualidade para encontrar essas fraquezas e escrever testes mais robustos para corrigi-las.

## Tarefas

1.  **Prepare o ambiente:** Clone o repositório e rode `npm install`.
2.  **Análise Inicial:**
    - Rode `npm test` para ver os testes passando.
    - Rode `npm run coverage` e anote o percentual de cobertura.
3.  **Análise de Mutação:**
    - Configure o StrykerJS (`npx stryker init`).
    - Execute a análise com `npx stryker run` (ou `npm run mutate` após configurar o script).
    - Abra o relatório HTML e analise os **mutantes que sobreviveram**.
4.  **Aprimore os Testes:**
    - Para cada mutante sobrevivente, entenda por que ele não foi "morto".
    - Adicione novos testes em `__tests__/operacoes.test.js` focados em asserções mais específicas para matar esses mutantes.
5.  **Validação Final:**
    - Rode o Stryker novamente e verifique se sua pontuação de mutação aumentou, idealmente para mais de 95%.

## Setup

### 1. Preparação Inicial

```bash
npm install
```

### 2. Executar Testes com Cobertura

```bash
npm run test -- --coverage
```

Este comando executa os testes e gera um relatório de cobertura de código, mostrando quais linhas foram testadas.

### 3. Executar Teste de Mutação

```bash
npx stryker run
```

Este comando executa o teste de mutação com StrykerJS, que cria mutantes do código e verifica se os testes conseguem detectá-los.

### 4. Analisar Resultados

- **Cobertura de código**: Verifica se o código foi executado
- **Teste de mutação**: Verifica se os testes são eficazes em detectar mudanças no comportamento do código
- Compare os resultados para identificar onde os testes precisam ser melhorados
- Acesse o relatório detalhado em `docs/mutation.html`

### Resumo das Melhorias Implementadas

Durante este projeto, foram identificadas várias deficiências na suíte de testes original através do teste de mutação. As principais melhorias implementadas incluíram:

#### **Testes de Validação de Entrada e Casos Extremos:**

**Função `raizQuadrada` (Testes 6.1, 6.2):**

- **Adicionado:** Teste para raiz quadrada de 0 (caso de borda)
- **Adicionado:** Validação de erro para números negativos
- **Motivo:** Cobrir branches de validação de entrada que não eram testados

**Função `fatorial` (Testes 8.1, 8.2, 8.3):**

- **Adicionado:** Teste para fatorial de 0 (retorna 1)
- **Adicionado:** Teste para fatorial de 1 (retorna 1)
- **Adicionado:** Validação de erro para números negativos
- **Motivo:** Garantir cobertura completa dos casos base e validação de entrada

**Função `mediaArray` (Teste 9.1):**

- **Adicionado:** Teste para array vazio (retorna 0)
- **Motivo:** Cobrir branch de tratamento de array vazio

#### **Testes de Tratamento de Erros e Validações:**

**Função `maximoArray` (Teste 11.1):**

- **Adicionado:** Validação de erro para array vazio
- **Motivo:** Testar comportamento de erro em condições inválidas

**Função `minimoArray` (Teste 12.1):**

- **Adicionado:** Validação de erro para array vazio
- **Motivo:** Garantir consistência no tratamento de arrays vazios

**Função `inverso` (Teste 40.1):**

- **Adicionado:** Validação de erro para divisão por zero (inverso de 0)
- **Motivo:** Cobrir branch de validação crítica

**Função `medianaArray` (Teste 47.3):**

- **Adicionado:** Validação de erro para array vazio
- **Motivo:** Completar cobertura de casos de erro

#### **Testes de Comportamento Dual (True/False):**

**Função `isPar` (Teste 15.1):**

- **Adicionado:** Teste para número ímpar (retorna false)
- **Motivo:** Cobrir ambos os branches da função booleana

**Função `isImpar` (Teste 16.1):**

- **Adicionado:** Teste para número par (retorna false)
- **Motivo:** Garantir cobertura completa de branches booleanos

**Funções de Comparação (Testes 44.1, 45.1, 46.1):**

- **Adicionado:** Testes para casos onde comparações retornam false
- **Motivo:** Cobrir todos os branches condicionais

#### **Testes de Algoritmos Complexos:**

**Função `clamp` (Testes 36.1, 36.2):**

- **Adicionado:** Teste para valor menor que mínimo (fixa no mínimo)
- **Adicionado:** Teste para valor maior que máximo (fixa no máximo)
- **Adicionado:** Testes para valores nos limites exatos
- **Motivo:** Cobrir todos os branches da lógica de limitação

**Função `isDivisivel` (Testes 37.1, 37.2):**

- **Adicionado:** Teste para não divisibilidade (retorna false)
- **Adicionado:** Teste para divisor zero (comportamento especial do JS)
- **Motivo:** Cobrir todos os caminhos de execução

**Função `isPrimo` (Testes 33.1, 33.2):**

- **Adicionado:** Testes para números <= 1 (não primos)
- **Adicionado:** Teste para número composto (não primo)
- **Motivo:** Cobrir todas as condições da verificação de primalidade

#### **Testes de Conversão e Cálculos Específicos:**

**Funções de Conversão de Temperatura (Testes 38.1, 39.1):**

- **Adicionado:** Testes com valores diferentes dos casos triviais (0°C, 32°F)
- **Motivo:** Verificar se as fórmulas estão corretas para outros valores

**Função `medianaArray` (Testes 47.1, 47.2, 47.4, 47.5):**

- **Adicionado:** Testes para arrays pares e ímpares
- **Adicionado:** Testes para arrays desordenados
- **Motivo:** Verificar algoritmo de ordenação e cálculo correto da mediana

**Função `produtoArray` (Teste 10.1):**

- **Adicionado:** Teste para array vazio (retorna 1 - elemento neutro)
- **Motivo:** Cobrir caso base da multiplicação

### Comparativo de Métricas

| Métrica                  | Antes  | Depois  | Variação |
| ------------------------ | ------ | ------- | -------- |
| % Mutation Score Total   | 73.71% | 100.00% | +26.29%  |
| % Mutation Score Covered | 78.11% | 100.00% | +21.89%  |
| Mutantes Mortos          | 153    | 124     | -29      |
| Mutantes Sobreviventes   | 44     | 0       | -44      |
| Sem Cobertura            | 12     | 0       | -12      |

### Melhoria na Cobertura de Código

| Métrica         | Antes  | Depois | Variação |
| --------------- | ------ | ------ | -------- |
| Statements      | 85.41% | 100%   | +14.59%  |
| Branches        | 58.82% | 100%   | +41.18%  |
| Functions       | 100%   | 100%   | 0%       |
| Lines           | 98.64% | 100%   | +1.36%   |
| Uncovered Lines | 12     | 0      | -12      |

Os resultados demonstram uma evolução significativa na qualidade da suíte de testes. O aumento de 26.29% no mutation score total indica que os testes refatorados são muito mais eficazes em detectar mudanças no comportamento do código. A eliminação completa dos mutantes sobreviventes (de 44 para 0) mostra que todos os cenários críticos agora estão adequadamente cobertos.

Particularmente notável é a melhoria de 41.18% na cobertura de branches, evidenciando que os novos testes abordam caminhos de execução que anteriormente não eram validados. Essa melhoria garante que o código seja não apenas executado durante os testes, mas também que seu comportamento seja rigorosamente verificado em todas as condições possíveis.

## 7. Recursos Adicionais

### Documentação e Referências

- **Documentação Oficial do StrykerJS**: https://stryker-mutator.io/docs/
- **Manual de Mutantes do Stryker**: https://stryker-mutator.io/docs/mutation-testing-elements/supported-mutators/
- **Relatório**: [Análise de Eficácia de Testes com Teste de Mutação](docs/Relatório%20-%20Análise%20de%20Eficácia%20de%20Testes%20com%20Teste%20de%20Mutação.pdf)
