# Revisão rápida — Python Modules 03 e 04 (42)

Guia simples para **entender e explicar os exercícios na avaliação**. Baseado no código dos repositórios [python-module-03](https://github.com/viniciusnevescosta/python-module-03) e [python-module-04](https://github.com/viniciusnevescosta/python-module-04).

## Module 03 — Coleções, argumentos e geradores

**Ideia geral:** receber e organizar dados, fazer cálculos e gerar informações sem precisar guardar tudo na memória.

| Exercício | O que faz | O que explicar |
| --- | --- | --- |
| **ex0 — Command Quest** | Mostra os argumentos passados pelo terminal. | `sys.argv` é uma lista de strings; a posição 0 contém o nome/caminho do script e `sys.argv[1:]` contém os argumentos. |
| **ex1 — Score Analytics** | Converte argumentos em pontuações e calcula total, média, maior e menor valor. | `int()` converte texto em número; `try/except ValueError` trata entradas inválidas; `sum`, `len`, `max` e `min` fazem os cálculos. |
| **ex2 — Coordinate System** | Lê coordenadas X, Y e Z e calcula a distância entre dois pontos. | `split(",")` separa a entrada, `float()` converte os valores e uma **tupla** guarda as três coordenadas. A distância é calculada com a fórmula euclidiana em 3D. |
| **ex3 — Achievement Tracker** | Compara conquistas dos jogadores. | **Set (conjunto)** não armazena itens duplicados; `union` junta conquistas, `intersection` encontra as comuns e `difference` mostra as exclusivas ou ausentes. |
| **ex4 — Inventory System** | Lê itens no formato `nome:quantidade` e calcula estatísticas do inventário. | **Dict (dicionário)** guarda pares chave–valor, por exemplo `{"poção": 3}`; `keys()`, `values()` e `update()` acessam e alteram os dados. |
| **ex5 — Data Stream** | Gera eventos aleatórios de jogadores e consome eventos de uma lista. | **Generator** usa `yield` para produzir um valor por vez; `next()` pede o próximo valor. `pop()` retira um elemento da lista. |
| **ex6 — Data Alchemist** | Normaliza nomes, filtra jogadores e monta um placar. | **Comprehensions** criam listas e dicionários de forma concisa, com transformação e filtro. |

### Estruturas de dados: saiba diferenciar

- **List `[1, 2, 2]`:** ordenada, mutável, permite repetidos.
- **Tuple `(1, 2, 3)`:** ordenada, imutável, permite repetidos.
- **Set `{1, 2}`:** conjunto sem elementos repetidos; útil para operações entre grupos.
- **Dict `{"Alice": 100}`:** associa uma chave a um valor; as chaves são únicas.

### Exemplos importantes

```python
# Argumentos: python3 programa.py 10 20
import sys
numeros = [int(x) for x in sys.argv[1:]]

# Operações entre conjuntos
a, b = {1, 2, 3}, {2, 3, 4}
a | b  # união: {1, 2, 3, 4}
a & b  # interseção: {2, 3}
a - b  # diferença: {1}

# Generator: não cria todos os resultados de uma vez
def contar():
    yield 1
    yield 2

gerador = contar()
next(gerador)  # 1
next(gerador)  # 2
```

**Como explicar o `yield`:** diferente de `return`, ele entrega um valor e *pausa* a função; na próxima chamada de `next()`, a execução continua de onde parou. Isso ajuda a processar dados aos poucos.

## Module 04 — Arquivos, streams e gerenciamento de recursos

**Ideia geral:** trabalhar com arquivos de texto, tratar falhas e garantir que os arquivos sejam fechados corretamente.

| Exercício | O que faz | O que explicar |
| --- | --- | --- |
| **ex0 — Ancient Text** | Abre e lê um arquivo informado no terminal. | `open(..., "r", encoding="utf-8")` abre para leitura; `read()` obtém o texto; `try/except/finally` trata erros e fecha o arquivo. |
| **ex1 — Archive Creation** | Lê um arquivo, acrescenta `#` ao final de cada linha e salva em outro arquivo. | Modo `"w"` escreve/cria um arquivo (**sobrescreve** se já existir); `write()` grava texto. |
| **ex2 — Stream Management** | Faz a mesma leitura/transformação/escrita, mas controla a entrada, a saída e os erros. | `sys.stdin` recebe entrada; `sys.stdout` mostra saída normal; `sys.stderr` mostra erros; `flush()` força o envio de dados pendentes do buffer. |
| **ex3 — Vault Security** | Cria uma função para ler ou escrever com tratamento de erros. | `with open(...) as arquivo` gerencia o fechamento automaticamente; a função retorna uma **tupla** `(sucesso, resultado)`. |

### Modos de abertura

- `"r"`: lê arquivo existente.
- `"w"`: escreve, criando ou sobrescrevendo o arquivo.
- `"a"`: acrescenta conteúdo ao final (não usado nesses exercícios, mas é bom conhecer).

### Exemplo: por que usar `with`?

```python
try:
    with open("dados.txt", "r", encoding="utf-8") as arquivo:
        conteudo = arquivo.read()
except OSError as erro:
    print(f"Erro ao ler: {erro}")
```

O **`with` chama o gerenciamento de contexto**, garantindo o fechamento do arquivo ao sair do bloco, inclusive se ocorrer uma exceção. Nos primeiros exercícios, isso é feito manualmente com `finally`.

### Tratamento de erros

- **`try`:** código que pode falhar.
- **`except`:** trata a exceção para o programa não encerrar inesperadamente.
- **`finally`:** executa mesmo que haja erro; útil para liberar recursos.
- **`OSError`:** cobre problemas como arquivo ausente ou falta de permissão.
- **`UnicodeError`:** cobre problemas de codificação/decodificação de texto.

## Perguntas rápidas para a avaliação

**1. Por que `sys.argv` precisa de conversão?**  
Porque os argumentos chegam como strings, mesmo quando parecem números.

**2. Qual a diferença entre lista e set?**  
A lista mantém a sequência e aceita repetidos; o set elimina duplicatas e facilita operações de conjuntos.

**3. Por que usar tupla nas coordenadas?**  
Porque representa um grupo fixo de três valores que não precisa ser alterado.

**4. Qual a diferença entre `yield` e `return`?**  
`yield` produz um valor e pode continuar a execução depois; `return` termina a função.

**5. Por que tratar erros ao abrir arquivos?**  
O arquivo pode não existir, não ter permissão ou apresentar problemas de codificação.

**6. Qual a vantagem de `with` sobre `open()` e `close()` manuais?**  
Reduz a chance de esquecer de fechar o arquivo, mesmo quando acontece um erro.

**7. Qual a diferença entre `stdout` e `stderr`?**  
`stdout` é a saída normal do programa; `stderr` é o canal separado para mensagens de erro.

**8. Para que servem as anotações como `list[int]` e `-> None`?**  
Documentam os tipos esperados e ajudam ferramentas de análise; Python normalmente não obriga esses tipos em tempo de execução.

## Resumo para falar em voz alta

> **Python 03:** pratiquei como receber argumentos, converter e validar dados, trabalhar com listas, tuplas, conjuntos e dicionários, e usar generators e comprehensions para processar informações.
>
> **Python 04:** pratiquei a leitura e escrita de arquivos, a separação entre entrada, saída e erros, o tratamento de exceções e o fechamento seguro de arquivos com `finally` ou `with`.

**Dica:** na avaliação, abra o arquivo de cada exercício e explique *qual dado entra, como ele é processado e qual resultado sai*. Saber justificar a estrutura de dados escolhida vale mais do que decorar o código.
