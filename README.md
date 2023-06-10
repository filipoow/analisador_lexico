# Análise Léxica de Código Fonte

## Descrição
Este código realiza a análise léxica de um código fonte fornecido. Ele identifica os tokens presentes no código, aplicando expressões regulares para encontrar padrões específicos.

## Bibliotecas Utilizadas
- pandas
- re

## Funções
### `analisar(codigo)`
Realiza a análise léxica de um código fonte.

#### Parâmetros
- `codigo` (str): O código fonte a ser analisado.

#### Retorno
- `list`: Uma lista de tuplas contendo os tokens encontrados e seus respectivos tipos.

## Exemplo de Uso
```python
# Importando as bibliotecas
import pandas as pd
import re

# Expressões regulares para os tokens
padroes = [(r'\bse\b', 'SE'), (r'\bse nao\b', 'SE NÃO'),
           (r'\benquanto\b', 'ENQUANTO'), (r'\verdadeiro\b', 'BOOLEANO'),
           (r'\bfalso\b', 'BOOLEANO'), (r'\d+', 'NUMERO'),
           (r'[+\-*/]', 'OPERADOR'), (r'[=<>]=?', 'OPERADOR_COMPARACAO'),
           (r'\(', 'ABRE_PARENTESES'), (r'\)', 'FECHA_PARENTESES'),
           (r'#.*', 'COMENTARIO')]

def analisar(codigo):
    """
    Realiza a análise léxica de um código fonte.

    Args:
        codigo (str): O código fonte a ser analisado.

    Returns:
        list: Uma lista de tuplas contendo os tokens encontrados e seus respectivos tipos.
    """
    tokens = []
    for padrao in padroes:
        reg, tipo_token = padrao
        lista = re.findall(reg, codigo)
        tokens.extend([(l, tipo_token) for l in lista])
    return tokens

# Entrada de exemplo
codigo = '''
# iniciando o contador
entrada = 0
verificador = 0
enquanto entrada < 5:
    se entrada == 2:
        verificador = falso
    print(entrada) # printando o contador
    entrada = entrada + 1
'''

# Realizar análise léxica
tokens = analisar(codigo)

# Printando o código fonte
print(f'Código fonte: {codigo}')

# Printando a análise léxica
print('Análise Léxica:')

# Exibir os tokens encontrados
print(pd.DataFrame(tokens, columns=['SIMBOLOS', 'TOKEN']))
