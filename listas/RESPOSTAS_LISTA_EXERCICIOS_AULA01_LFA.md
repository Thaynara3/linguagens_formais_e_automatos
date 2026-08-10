# Lista de Exercícios — Aula 01

## Linguagens Formais e Autômatos

**Tema:** sintaxe, semântica e análise de código  
**Professor:** Murillo Edson de Carvalho Souza
**Aluno(a):** Thaynara Ramos Soares 
**Turma:** ENGCDM3B-MDCO78 **Data:** 10/08/2026

---

## Objetivos

Ao concluir esta lista, você deverá ser capaz de:

- diferenciar sintaxe e semântica;
- reconhecer problemas de escrita, concordância e ordenação;
- classificar erros básicos em trechos de código;
- explicar como o contexto altera o significado;
- distinguir um erro detectado pelo compilador de um erro lógico;
- ordenar as etapas iniciais do processamento realizado por um compilador.

## Orientações

1. Leia cada enunciado com atenção.
2. Não apresente apenas a classificação: escreva uma justificativa curta.
3. Nos exemplos de programação, considere a seguinte pseudolinguagem:
   - `inteiro`, `real` e `lógico` representam tipos;
   - `:=` é o operador de atribuição;
   - variáveis precisam ser declaradas antes do uso;
   - a forma condicional é `se condição então comando`.
4. Quando mais de uma classificação for defensável, indique o critério utilizado.

> **Nota conceitual:** na língua natural, um problema como “vou corre” é mais precisamente um erro gramatical ou de forma verbal. Na análise de compiladores, **erro léxico** possui um sentido técnico: ocorre quando uma sequência de caracteres não pode ser reconhecida como um token válido.

---

## Exercício 1 — Classificação em linguagem natural

Classifique cada sentença utilizando uma das categorias:

- **A — Adequada:** construção sintaticamente adequada no português usual;
- **B — Problema sintático:** problema de ordem, concordância ou estrutura;
- **C — Problema de formação/escrita:** palavra escrita ou flexionada de forma inadequada para o contexto.

| Item | Sentença | Classificação | Justificativa |
|---:|---|:---:|---|
| 1 | “As flores são belas.” | A | Construção sintaticamente adequada no português usual. |
| 2 | “As flores é bela.” | B | Problema sintático (sujeito no plural com verbo e adjetivo no singular. |
| 3 | “Vou corre hoje no parque.” | C | Problema de formação/escrita (uso de forma conjugada incorreto, o certo seria "correr" ou invés de "corre"). |
| 4 | “Água bebeu José.” | B | Problema sintático (Problema de ordem nos termos). |
| 5 | “O aluno acabou a prova.” | A | Construção sintaticamente adequada no português atual. |

### Questões complementares

1. A sentença do item 4 é impossível em português ou apenas incomum na ordem mais frequente? Explique.

   **Resposta:**  
  Apenas incomum, pois a ordem dos fatores está inversa. Apesar da estranheza gramatical, é possível compreender a mensagem (de que foi José que bebeu a água), mostrando que a semântica e comunicação funcionam. 

2. Reescreva todas as sentenças problemáticas de maneira adequada ao português usual.

   **Resposta:**  
   2. A flor é bela. / As flores são belas.
   3. Vou correr hoje no parque.
   4. José bebeu água.

---

## Exercício 2 — Sintaxe e semântica na programação

Analise os trechos abaixo. Classifique o problema predominante como:

- **S — Sintático:** a estrutura não segue a gramática da pseudolinguagem;
- **M — Semântico:** a estrutura pode ser reconhecida, mas seus elementos não são válidos ou compatíveis;
- **V — Válido:** não há erro considerando apenas as regras fornecidas.

> Alguns compiladores podem classificar determinadas situações em fases diferentes. Considere as regras da pseudolinguagem apresentadas no início da lista.

### Item 1

```text
45 := a;
```

Classificação: S

Justificativa:  
O lado esquerdo de uma atribuição precisa ser um local para armazenar o valor, e não um valor fixo.
O correto seria: a:= 45;

### Item 2

```text
então (a < 10) se;
```

Classificação: S

Justificativa:  
O "então" e "se" estão inversas.
O correto é: se (a < 10) então;

### Item 3

```text
inteiro soma;
soma := 4.5;
```

Classificação: M

Justificativa:  
A estrutura está bem escrita, mas a incompatibilidade em soma que só aceita números inteiros, e 4.5 é um ponto flutuante.
O correto seria: inteiro soma;
                 soma := 4;

### Item 4

```text
media := 10.0;
```

Considere que `media` não foi declarada anteriormente.

Classificação: M

Justificativa:  
Sem a declaração da variável ocasionará num erro de variável inexistente, pois o compilador não reconhece o tipo e nem existência de média.

### Item 5

```text
real media;
media := 10.0;
```

Classificação: V

Justificativa:  
Correto. A variável foi declarada corretamente como real e antes de receber o valor 10.0 que também é um tipo real.

### Item 6

```text
se a < 10 então
    a := a + 1;
```

Considere que `a` foi declarada como inteira.

Classificação: V

Justificativa:  
Correto. A sintaxe (se ... então) e a instrução de atribuição foram usadas de forma que seguem a gramática do pseudolinguagem. 

---

## Exercício 3 — Ambiguidade e contexto

Explique a classe gramatical e o significado da palavra destacada em cada frase.

### Caso A — “caminho”

1. “Eu **caminho** todos os dias.”
2. “O **caminho** é longo.”

**Explicação:**  
1. Remete a uma ação de caminhar (verbo)
2. Remete a um trajeto ou via (substantivo)

### Caso B — “colher”

1. “Vou **colher** flores.”
2. “A **colher** caiu no chão.”

**Explicação:**  
1. Remete a ação de colher/recolher/pegar (verbo)
2. Remete ao utensílio de cozinha (substantivo)

### Caso C — programação

Observe os trechos:

```text
inteiro soma;
soma := 10;
```

```text
função soma(inteiro a, inteiro b)
    retorne a + b;
fim
```

1. O que o nome `soma` representa em cada trecho?
2. Que informações o compilador precisa consultar para interpretar corretamente esse nome?

**Resposta:**  
1. No primeiro, a soma está destinada a guardar um número inteiro (identificador). Já no segundo, recebe 2 parâmetros e retorna um valor.
2. O compilador precisa consultar a tabela de símbolos, onde fica salvo os escopos, categoria da identidade e tipo de identificador.

### Debate

Por que um compilador precisa considerar declarações, tipos e escopos para decidir se um código está correto?

**Anotações:**  
Porque na análise sintática garante apenas que as palavras estão na ordem estruturalmente aceitas pela gramática. Precisam que faça sentido para a memória e lógica do computador, é necessária a análise semântica contextual (tabela de símbolos, checagem de escopo e tipos).

---

## Exercício 4 — Validade e erros lógicos

Um aluno desenvolveu um programa para conceder **10% de aumento** ao salário de um funcionário. O código deveria multiplicar o salário por `1.1`, mas foi escrito assim:

```text
real salario;
real novoSalario;

novoSalario := salario * 11;
```

O programa é aceito pelo compilador e executado normalmente.

Responda:

1. O trecho está sintaticamente correto? Justifique.

   **Resposta:**  
   Sim. A estrutura tem todas as regras gramaticais da pseudolinguagem (declaração de variáveis no formato <tipo> <nome> e atribuição no formato <variável> := <expressão>)

2. Há incompatibilidade de tipos ou uso de variável não declarada no trecho apresentado?

   **Resposta:**  
   Não. As variáveis salario e novoSalario foram declaradas como real, e a expressão salario * 11 resulta em um valor numérico compatível.

3. O programa realiza o objetivo proposto? Justifique.

   **Resposta:**  
   Não. Ao multiplicar por 11, ele calcula 1100% do valor. Para conceder 10% o correto seria multiplicar por 1.1.

4. Classifique o problema como erro sintático, erro semântico estático ou erro lógico.

   **Resposta:**  
   Erro lógico. 

5. Corrija a linha responsável pelo problema.

```text

novoSalario := salario * 1.1

```

---

## Exercício 5 — Ordem de processamento

Organize as etapas abaixo na ordem didática mais comum de um compilador:

- análise semântica;
- análise léxica (*scanner*);
- análise sintática (*parser*).

### Parte A — Lista numerada

1. __________________________________________________________________________
2. __________________________________________________________________________
3. __________________________________________________________________________

### Parte B — O que cada etapa recebe e produz?

| Etapa | O que analisa? | Exemplo de problema detectado |
|---|---|---|
| Análise léxica | Sequência de caracteres no código-fonte para agrupá-los em tokens | Caractere inválido. Ex: let a @ 5; |
| Análise sintática | Sequência de tokens para verificar se respeitam a gramática | Ausência de parênteses ou delimitadores. Ex: se então a := 1; |
| Análise semântica | O significado, tipos, declarações e coerência das estruturas da árvore sintática | Incompatibilidade de tipos ou variáveis não declarada. Ex: inteiro x := "texto"; |

### Parte C — Fluxograma

Desenhe um fluxo contendo os seguintes elementos:

```text
Código-fonte → Análise Léxica → tokens → Análise Sintática → estrutura sintática
            → Análise Semântica → código validado para as próximas etapas
```

### Questão de reflexão

Por que a análise semântica normalmente depende dos resultados das análises léxica e sintática?

**Resposta:**  
Porque a análise semântica precisa de uma estrutura hierárquica já validada (a árvore sintática montada a partir dos tokens) para associar os operados aos seus operando e verificar regras de contexto. Não faz sentido analisar o significado de uma sentença cuja forma (tokens e gramática) está quebrada.

---

## Desafio opcional — Crie seus próprios exemplos

Crie três pequenos exemplos:

1. uma frase ou código com problema de escrita/tokenização;
2. uma construção com erro sintático;
3. um programa sintaticamente válido, mas com erro lógico.

Para cada exemplo, apresente a classificação e a justificativa.

---

## Síntese

Complete:

- **Léxico** está relacionado a reconhecimento e formação de tokens/palavras a partir dos caracteres..
- **Sintaxe** está relacionada a estrutura, organização e regras de arranjo gramatical dos tokens.
- **Semântica** está relacionada ao significado, coerência de tipos e contexto das instruções.
- **Erro lógico** ocorre quando o programa roda sem erros, mas produz um resultado diferente do objetivo pretendido.

