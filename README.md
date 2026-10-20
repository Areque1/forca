# Jogo da Forca em C

Jogo da forca para o terminal, escrito em C. O programa sorteia uma palavra secreta de um arquivo de texto e o jogador tenta adivinhá-la letra por letra antes de ser enforcado.

```
  _______
 |/      |
 |      (_)
 |      \|/
 |       |
 |      / \
 |
_|___

M E L _ _ _ _ A
```

## Arquivos

| Arquivo        | Descrição                                                  |
|----------------|------------------------------------------------------------|
| `forca.c`      | Código-fonte do jogo                                       |
| `forca.h`      | Cabeçalho com a constante `TAMANHO_PALAVRA` e os protótipos |
| `palavras.txt` | Banco de palavras usado no sorteio                         |

## Como compilar e jogar

É preciso ter um compilador C, como o GCC.

```bash
gcc forca.c -o forca
./forca
```

No Windows, execute `forca.exe`. Rode o programa na mesma pasta do `palavras.txt`, pois o arquivo é aberto pelo caminho relativo.

## Regras

1. Uma palavra é sorteada do `palavras.txt`.
2. A cada rodada, a forca e a palavra são desenhadas, com `_` no lugar das letras ainda não descobertas.
3. Digite uma letra. O jogo informa se ela existe na palavra.
4. Cada letra errada acrescenta uma parte ao boneco: cabeça, tronco, braços e pernas.
5. Você **ganha** ao descobrir todas as letras e **perde** ao acumular 5 erros.

Ao final aparece um troféu (vitória) ou uma caveira junto com a palavra secreta (derrota).

## Adicionando palavras

Ao fim de cada partida o jogo pergunta:

```
Você deseja adicionar uma nova palavra no jogo (S/N)?
```

Responda `S` (maiúsculo) e digite a nova palavra em letras maiúsculas. Ela é gravada no final do `palavras.txt` e o contador da primeira linha é atualizado.

Você também pode editar o arquivo à mão. O formato é:

```
3
MELANCIA
MELAO
MORANGO
```

A primeira linha guarda a quantidade de palavras e cada linha seguinte guarda uma palavra. Se adicionar palavras manualmente, atualize o número da primeira linha.

## Estrutura do código

| Função              | O que faz                                                         |
|---------------------|-------------------------------------------------------------------|
| `abertura()`        | Mostra o título do jogo                                           |
| `escolhepalavra()`  | Lê o `palavras.txt` e sorteia a palavra secreta com `rand()`      |
| `desenhaforca()`    | Desenha a forca conforme os erros e mostra a palavra parcial      |
| `chuta()`           | Lê uma letra do jogador e a registra no vetor `chutes`            |
| `letraexiste()`     | Verifica se uma letra está na palavra secreta                     |
| `jachutou()`        | Verifica se uma letra já foi chutada                              |
| `chuteserrados()`   | Conta quantos chutes não estão na palavra                         |
| `ganhou()`          | Retorna 1 quando todas as letras foram descobertas                |
| `enforcou()`        | Retorna 1 quando há 5 ou mais erros                               |
| `adicionapalavra()` | Pergunta e grava uma nova palavra no banco                        |

## Limitações conhecidas

- **Diferencia maiúsculas de minúsculas:** as palavras estão em maiúsculas, então digite os chutes em maiúsculas (`a` não acerta `A`).
- **Chutes repetidos contam de novo:** repetir uma letra errada soma mais um erro.
- **Limite de chutes:** o vetor `chutes` guarda até 26 letras.
- **Tamanho da palavra:** no máximo 19 caracteres (`TAMANHO_PALAVRA` é 20).
