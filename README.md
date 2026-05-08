# Fundamentos da Entrada, Conversão e Transformação de Dados em C#

## Introdução

Uma das maiores dificuldades de quem está começando programação não é “decorar sintaxe”.

É compreender:

* o que entra
* o que o sistema espera
* o que precisa ser transformado
* e o que sai depois do processamento

Programar é, essencialmente, construir sistemas de transformação.

Todo software profissional faz isso:

```text
Entrada → Validação → Conversão → Processamento → Saída
```

Desde um caixa eletrônico até uma IA.

Em C#, isso aparece logo nos primeiros contatos com:

* `Console.ReadLine()`
* conversões (`Parse`, `Convert`)
* tratamento de erros
* validações
* funções
* fluxo de execução
* composição de chamadas
* manipulação de tipos

Mas existe algo ainda mais importante:

> Um desenvolvedor júnior costuma pensar apenas em “fazer funcionar”.
>
> Um desenvolvedor sênior pensa:
>
> * que tipo de dado está chegando
> * qual o risco da entrada
> * quais falhas podem ocorrer
> * como proteger o fluxo
> * como transformar dados com segurança
> * como tornar o sistema resiliente

Essa é a evolução mental que construiremos aqui.

---

# CAPÍTULO 1 — O que é uma Entrada de Dados

## O conceito mais importante do início da programação

Quando o usuário digita algo:

```csharp
Console.ReadLine();
```

o computador NÃO sabe:

* se é número
* texto
* data
* CPF
* moeda
* temperatura
* senha
* JSON
* comando

Ele recebe apenas:

```text
texto (string)
```

---

## Visualizando mentalmente

```text
Usuário digita:
25

Computador recebe:
"25"
```

Isso ainda NÃO é um número.

É apenas texto contendo caracteres numéricos.

---

## Primeira percepção crítica

Observe:

```csharp
string idade = Console.ReadLine();
```

O usuário pode digitar:

```text
25
vinte
abc
@
999999999999999999999
```

O sistema aceitará tudo.

Porque:

```text
ReadLine() → retorna string
```

---

# CAPÍTULO 2 — O Fluxo da Transformação

## O verdadeiro pipeline de dados

```text
Entrada
↓
Leitura
↓
Validação
↓
Conversão
↓
Processamento
↓
Saída
```

---

## Exemplo simples

```csharp
Console.Write("Digite sua idade: ");

int idade = int.Parse(Console.ReadLine());

Console.WriteLine($"Você tem {idade} anos.");
```

---

## O que realmente acontece

```text
Console.ReadLine()
↓
retorna "25"
↓
int.Parse("25")
↓
transforma em 25
↓
armazena em idade
↓
WriteLine exibe
```

---

# CAPÍTULO 3 — Composição e Aninhamento

## Conceito de composição

Você pode passar o retorno de uma função diretamente para outra.

Exemplo:

```csharp
int numero = int.Parse(Console.ReadLine());
```

Aqui temos:

```text
ReadLine()
↓
retorna string
↓
Parse recebe string
↓
converte para int
↓
resultado é armazenado
```

---

## Visualização arquitetural

```text
┌──────────────┐
│ ReadLine()   │
└──────┬───────┘
       ↓
┌──────────────┐
│ int.Parse()  │
└──────┬───────┘
       ↓
┌──────────────┐
│ variável     │
└──────────────┘
```

---

# CAPÍTULO 4 — Conversões Fundamentais

## 1. Texto → Inteiro

```csharp
int idade = int.Parse(Console.ReadLine());
```

---

## 2. Texto → Decimal

```csharp
double altura = double.Parse(Console.ReadLine());
```

---

## 3. Texto → Booleano

```csharp
bool ativo = bool.Parse(Console.ReadLine());
```

Entrada válida:

```text
true
false
```

---

## 4. Texto → Data

```csharp
DateTime data = DateTime.Parse(Console.ReadLine());
```

---

# CAPÍTULO 5 — O Problema Real: Falhas

## O mundo real é caótico

Usuários erram.

Muito.

Exemplo:

```csharp
int idade = int.Parse(Console.ReadLine());
```

Se o usuário digitar:

```text
vinte
```

o sistema quebra.

---

## O erro

```text
System.FormatException
```

---

## Pensamento sênior

O problema não é “converter”.

O problema é:

```text
como proteger o fluxo contra entradas inválidas
```

---

# CAPÍTULO 6 — Conversões Seguras

## TryParse()

Esse é um divisor de águas.

```csharp
int.TryParse(Console.ReadLine(), out int idade);
```

---

## O que acontece

```text
Tenta converter
↓
Se conseguir:
    retorna true
↓
Se falhar:
    retorna false
```

---

## Forma profissional

```csharp
Console.Write("Digite sua idade: ");

bool sucesso = int.TryParse(Console.ReadLine(), out int idade);

if (sucesso)
{
    Console.WriteLine($"Idade válida: {idade}");
}
else
{
    Console.WriteLine("Valor inválido.");
}
```

---

# CAPÍTULO 7 — Evolução do Pensamento

## Júnior

```text
“Como converto?”
```

---

## Pleno

```text
“Como valido?”
```

---

## Sênior

```text
“Como garanto integridade do fluxo?”
```

---

# CAPÍTULO 8 — Tipos de Conversão

# Conversão Explícita

Quando você diz exatamente o que quer converter.

```csharp
int numero = int.Parse("10");
```

---

# Conversão Implícita

Quando o C# faz automaticamente.

```csharp
int numero = 10;
double valor = numero;
```

Aqui:

```text
int → double
```

não perde informação.

---

# Casting

Conversão manual entre tipos.

```csharp
double valor = 10.8;

int inteiro = (int)valor;
```

Resultado:

```text
10
```

A parte decimal é descartada.

---

# Convert

Outra forma muito usada.

```csharp
int numero = Convert.ToInt32(Console.ReadLine());
```

---

# Diferença importante

## Parse

Exige valor válido.

---

## Convert

Pode lidar com `null`.

---

# CAPÍTULO 9 — Tratamento de Erros

# try/catch

Forma clássica de proteção.

```csharp
try
{
    int idade = int.Parse(Console.ReadLine());

    Console.WriteLine(idade);
}
catch
{
    Console.WriteLine("Entrada inválida.");
}
```

---

# Visão arquitetural

```text
Entrada
↓
Tentativa de conversão
↓
Erro?
 ├─ sim → tratamento
 └─ não → continua fluxo
```

---

# CAPÍTULO 10 — Entrada Encadeada Moderna

## Código compacto

```csharp
Console.WriteLine($"Olá, {Console.ReadLine()}!");
```

---

## O que ocorre internamente

```text
ReadLine()
↓
retorna string
↓
interpolação monta texto
↓
WriteLine exibe
```

---

# Evolução elegante

```csharp
Console.WriteLine($"Resultado: {int.Parse(Console.ReadLine()) * 2}");
```

Fluxo:

```text
entrada
↓
conversão
↓
processamento matemático
↓
saída
```

---

# CAPÍTULO 11 — O Conceito Mais Importante da Formação

## Todo sistema é transformação de estado

Quando um usuário:

* faz login
* compra algo
* envia mensagem
* agenda consulta
* transfere dinheiro

o sistema está:

```text
recebendo dados
↓
validando
↓
convertendo
↓
transformando estado
↓
gerando saída
```

---

# CAPÍTULO 12 — Engenharia Mental Aplicada

## Como arquitetos pensam

Antes de escrever código, um arquiteto pensa:

```text
O que entra?
↓
Qual tipo?
↓
Pode falhar?
↓
Quem valida?
↓
Onde converte?
↓
Quem é responsável?
↓
Como registrar erro?
↓
Como proteger domínio?
```

---

# Exemplo de pensamento profissional

## Cenário

Usuário digita valor monetário.

Problemas possíveis:

```text
"100"
"100,50"
"R$ 100"
"cem reais"
""
null
```

---

## Pensamento crítico

```text
Qual formato aceitar?
↓
Qual cultura regional?
↓
Decimal usa ponto ou vírgula?
↓
Sistema deve corrigir automaticamente?
↓
Erro deve bloquear?
```

Isso é engenharia de software.

---

# CAPÍTULO 13 — Fluxos Complexos

# Exemplo de pipeline profissional

```csharp
Console.Write("Digite seu salário: ");

string entrada = Console.ReadLine();

bool valido = decimal.TryParse(entrada, out decimal salario);

if (!valido)
{
    Console.WriteLine("Salário inválido.");
    return;
}

decimal imposto = salario * 0.15m;

Console.WriteLine($"Imposto: {imposto:C}");
```

---

# Visualização mental

```text
Usuário
↓
digita texto
↓
TryParse tenta converter
↓
falhou?
 ├─ sim → interrompe
 └─ não → continua
↓
processa regra
↓
gera saída
```

---

# CAPÍTULO 14 — Formação de Mentalidade Sênior

## Um sistema robusto precisa:

* prever falhas
* validar entradas
* impedir estados inválidos
* proteger regras de negócio
* transformar dados com segurança
* ser legível
* ser previsível
* ser resiliente

---

# CAPÍTULO 15 — Exercícios de Engenharia Mental

# Exercício 1

Faça um sistema que:

* peça idade
* valide
* converta
* diga se a pessoa é maior de idade

---

# Exercício 2

Receba altura e peso.

Calcule IMC.

Mas:

* valide números inválidos
* impeça divisão por zero

---

# Exercício 3

Receba data de nascimento.

Calcule idade aproximada.

---

# Exercício 4

Receba salário.

Converta corretamente usando `decimal`.

Aplique aumento.

---

# Exercício 5

Crie um fluxo resiliente:

```text
enquanto usuário errar:
    pedir novamente
```

---

# Conclusão

Programação não é sobre decorar comandos.

É sobre:

```text
modelar pensamento
↓
estruturar fluxo
↓
transformar dados
↓
proteger estados
↓
resolver problemas
```

E todo grande desenvolvedor evolui assim:

```text
Sintaxe
↓
Lógica
↓
Fluxo
↓
Modelagem
↓
Arquitetura
↓
Pensamento sistêmico
```

Esse é o verdadeiro caminho da engenharia de software moderna em C#.
