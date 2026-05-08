# Engenharia Mental Aplicada à Resolução de Problemas em C#

## Introdução

Os livros antigos de matemática ensinavam algo extremamente poderoso:

```text id="4n7nuh"
situação
↓
interpretação
↓
estruturação
↓
resolução
```

Isso continua sendo exatamente o coração da programação.

A diferença é que agora:

* os problemas são sistemas
* as variáveis são dados
* os cálculos são regras de negócio
* os erros são estados inválidos
* e o código é a formalização do pensamento

---

# O ERRO MAIS COMUM DOS INICIANTES

O iniciante geralmente tenta:

```text id="4n6i9j"
“Qual comando uso?”
```

Mas o desenvolvedor experiente pensa:

```text id="gzsgwo"
“O que está acontecendo nessa situação?”
```

---

# A HABILIDADE MAIS IMPORTANTE

Antes de programar:

```text id="70n15p"
decodifique a realidade
```

---

# EXEMPLO COMPLETO — EVOLUÇÃO DO PENSAMENTO

# Situação-Problema

Uma loja deseja calcular desconto para clientes.

Regras:

* compras acima de R$ 100 recebem 10% de desconto
* abaixo disso não há desconto
* o sistema deve validar entradas inválidas

---

# ETAPA 1 — Entender o problema humano

O que está acontecendo?

```text id="gqbfy9"
Cliente compra algo
↓
Sistema recebe valor
↓
Sistema verifica regra
↓
Sistema calcula desconto
↓
Sistema mostra resultado
```

---

# ETAPA 2 — Encontrar entradas e saídas

## Entrada

```text id="pkwkeb"
valor da compra
```

---

## Saída

```text id="8s58r8"
valor final
desconto aplicado
```

---

# ETAPA 3 — Encontrar possíveis falhas

Pensamento sênior:

O usuário pode digitar:

```text id="7n6d6y"
abc
-50
0
100,50
R$ 300
```

Então precisamos:

* validar
* converter
* impedir valores negativos

---

# ETAPA 4 — Transformar em lógica

```text id="b8xj34"
se valor > 100:
    aplica desconto

senão:
    mantém valor
```

---

# ETAPA 5 — Modelar o fluxo

```text id="zwhm6m"
entrada
↓
validação
↓
conversão
↓
regra de negócio
↓
saída
```

---

# ETAPA 6 — Construir mentalmente antes do código

## Variáveis necessárias

```text id="j7lfjw"
valorCompra
desconto
valorFinal
```

---

# ETAPA 7 — Código Final

```csharp id="zjfwov"
Console.Write("Digite o valor da compra: ");

bool valido = decimal.TryParse(Console.ReadLine(), out decimal valorCompra);

if (!valido || valorCompra < 0)
{
    Console.WriteLine("Valor inválido.");
    return;
}

decimal desconto = 0;

if (valorCompra > 100)
{
    desconto = valorCompra * 0.10m;
}

decimal valorFinal = valorCompra - desconto;

Console.WriteLine($"Desconto: R$ {desconto:F2}");
Console.WriteLine($"Valor final: R$ {valorFinal:F2}");
```

---

# O QUE VOCÊ PRECISA ENXERGAR

O código é apenas a última etapa.

O verdadeiro trabalho foi:

```text id="sh1b75"
compreender
↓
estruturar
↓
validar
↓
proteger
↓
transformar
```

---

# EVOLUÇÃO DO PENSAMENTO

# Nível 1 — Iniciante

```text id="3g3tth"
“Como faço if?”
```

---

# Nível 2 — Júnior

```text id="6e0l6r"
“Como resolvo essa regra?”
```

---

# Nível 3 — Pleno

```text id="lt4f04"
“Quais entradas inválidas existem?”
```

---

# Nível 4 — Sênior

```text id="9h8hgs"
“Como tornar esse fluxo resiliente e sustentável?”
```

---

# COMO TREINAR PENSAMENTO COMPUTACIONAL

Sempre faça estas perguntas:

---

# 1. O que entra?

```text id="8s6o8v"
dados
```

---

# 2. O que o sistema espera?

```text id="x6jyyb"
tipo correto
```

---

# 3. O que pode dar errado?

```text id="v5vrdf"
falhas
```

---

# 4. Qual regra transforma os dados?

```text id="md8m0e"
processamento
```

---

# 5. O que deve sair?

```text id="07r9al"
resultado esperado
```

---

# 6. O sistema é confiável?

```text id="xaqv2w"
proteção do fluxo
```

---

# EXEMPLO 2 — PENSAMENTO MAIS AVANÇADO

# Situação

Uma academia deseja calcular IMC.

---

# Pensamento inicial

## Entradas

```text id="gdujlwm"
peso
altura
```

---

## Fórmula

IMC = \frac{peso}{altura^2}

---

# Problemas possíveis

```text id="u4z0g4"
altura = 0
peso negativo
texto inválido
```

---

# Fluxo correto

```text id="61e0s5"
entrada
↓
validação
↓
conversão
↓
proteção matemática
↓
cálculo
↓
classificação
↓
saída
```

---

# Código

```csharp id="0z43d6"
Console.Write("Digite seu peso: ");
bool pesoValido = double.TryParse(Console.ReadLine(), out double peso);

Console.Write("Digite sua altura: ");
bool alturaValida = double.TryParse(Console.ReadLine(), out double altura);

if (!pesoValido || !alturaValida)
{
    Console.WriteLine("Entrada inválida.");
    return;
}

if (peso <= 0 || altura <= 0)
{
    Console.WriteLine("Valores devem ser positivos.");
    return;
}

double imc = peso / (altura * altura);

Console.WriteLine($"IMC: {imc:F2}");
```

---

# O QUE UM SÊNIOR ENXERGA AQUI

Não apenas “uma conta”.

Mas:

```text id="nd2uk0"
integridade matemática
+
proteção de domínio
+
resiliência
+
confiabilidade
```

---

# AGORA É SUA VEZ — TREINAMENTO

# EXERCÍCIO 1 — Sistema de Média Escolar

Crie um sistema que:

* receba 3 notas
* valide entradas
* calcule média
* diga:

  * aprovado
  * recuperação
  * reprovado

---

# EXERCÍCIO 2 — Controle de Estoque

Uma loja recebe:

* nome do produto
* quantidade
* preço unitário

O sistema deve:

* validar entradas
* impedir valores negativos
* calcular valor total em estoque

---

# EXERCÍCIO 3 — Conversor de Temperatura

Receba temperatura em Celsius.

Converta para Fahrenheit.

Use a fórmula:

F = \frac{9}{5}C + 32

Mas:

* valide entrada
* trate valores absurdos
* permita repetir operação

---

# EXERCÍCIO 4 — Sistema de Login

Receba:

* usuário
* senha

Regras:

* usuário não pode ser vazio
* senha precisa ter ao menos 6 caracteres

Exiba:

```text id="8r3izn"
acesso permitido
```

ou:

```text id="0zvg3x"
acesso negado
```

---

# EXERCÍCIO 5 — Simulador Bancário

O sistema deve:

* receber saldo inicial
* permitir saque
* impedir saldo negativo
* validar entradas inválidas

Depois:

* mostrar saldo final

---

# DESAFIO DE ENGENHARIA MENTAL

Para cada exercício:

NÃO comece codando.

Faça primeiro:

```text id="y7iqzv"
1. O que entra?
2. O que sai?
3. O que pode falhar?
4. Qual regra transforma?
5. Como proteger o fluxo?
6. Quais variáveis existem?
7. Qual sequência lógica?
```

---

# O VERDADEIRO OBJETIVO DA FORMAÇÃO

Você não está aprendendo apenas C#.

Está aprendendo:

```text id="4o8f0w"
estruturação lógica
+
modelagem mental
+
engenharia de fluxo
+
resolução sistemática
+
pensamento computacional
```

E isso vale para:

* software
* arquitetura
* sistemas distribuídos
* APIs
* jogos
* IA
* automações
* empresas
* vida real

Porque programar é:

```text id="hr9tyl"
transformar problemas em estruturas solucionáveis
```
