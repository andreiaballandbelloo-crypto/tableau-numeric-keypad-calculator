# 🧮 Calculadora Numérica no Tableau (Keyboard as a Parameter)

Uma calculadora funcional (soma, subtração, multiplicação, divisão e
porcentagem) construída **inteiramente com parâmetros e campos calculados**
no Tableau — sem nenhuma extensão, script externo ou Hyper API. O "teclado"
é uma planilha comum com marcas em grid, e cada clique atualiza o estado da
conta através de ações de parâmetro.

Baseado na técnica clássica ["Keyboard as a Parameter"],
adaptada de um teclado alfabético (com Shift/Caps Lock) para um teclado
numérico com operações matemáticas.

## Como funciona (resumo)

O Tableau não guarda estado entre cliques — a solução é usar **4 parâmetros**
como se fossem variáveis, recalculadas a cada clique por **4 campos
calculados** e escritas de volta por **4 ações de parâmetro** disparadas ao
mesmo tempo:

```
clique na tecla
   ├─► Novo Display     → pDisplay      (número no visor)
   ├─► Novo Operando1   → pOperando1    (1º número da conta)
   ├─► Novo Operador    → pOperador     (operador pendente: + - × ÷)
   └─► Nova Entrada     → pNovaEntrada  (se o próximo dígito começa um número novo)
```

Um 5º campo (`Resultado`) faz a conta em si quando `=` ou `%` são
pressionados, e um 6º campo (`Expressão Visor`) monta o texto exibido na
tela (ex: `500 × 62`).

## Funcionalidades

- ✅ Soma, subtração, multiplicação e divisão
- ✅ Porcentagem com fechamento automático (`500 × 62 %` → `310`, sem apertar `=`)
- ✅ Ponto decimal
- ✅ Troca de sinal (`+/-`)
- ✅ Backspace
- ✅ Limpar (`C`)
- ✅ Mensagem de instrução quando o visor está vazio
- ✅ Proteção contra divisão por zero

## Estrutura do repositório

```
├── Calculadora_Numerica.twbx              # workbook do Tableau (arquivo principal)
├── data/
│   └── aux_teclado.xlsx          # fonte de dados do teclado (grid 4x5)
└── README.md
```

## Parâmetros

| Parâmetro | Tipo | Valor inicial | O que guarda |
|---|---|---|---|
| `pDisplay` | String | `0` | número sendo digitado / mostrado no visor |
| `pOperando1` | String | *(vazio)* | primeiro número da conta |
| `pOperador` | String | *(vazio)* | operador pendente (`+`, `-`, `×`, `÷`) |
| `pNovaEntrada` | Booleano | Falso | se o próximo dígito começa um número novo |

> Todos configurados como **Valores permitidos: Todos** (nunca "Lista") —
> são preenchidos pelas ações de parâmetro, não digitados manualmente.

## Como usar

1. Baixe o `.twbx` deste repositório. Abra no Tableau Desktop.
2. Ou acesse o link do Tableau Public:
https://public.tableau.com/views/Calculadora_17855540775970/Calculadora?:language=pt-BR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link
3. Clique nas teclas do grid para digitar e operar — o resultado aparece
   na planilha de visor.


