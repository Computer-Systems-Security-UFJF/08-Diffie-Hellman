# 08-Diffie-Hellman

Implementação simples da troca de chaves Diffie-Hellman em um notebook Jupyter
([`diffie_hellman.ipynb`](diffie_hellman.ipynb)), usando apenas o Python padrão.

## Como funciona

1. As duas partes combinam publicamente um primo `p` e uma raiz primitiva `g` módulo `p`.
2. Um lado escolhe um segredo `a` e envia `A = g^a mod p`.
3. O outro lado escolhe um segredo `b` e envia `B = g^b mod p`.
4. Quem tem `a` calcula `s = B^a mod p`; quem tem `b` calcula `s = A^b mod p`. Os dois valores são iguais.

O notebook também verifica que `p` é primo e que `g` é raiz primitiva
(`g^((p-1)/q) mod p != 1` para todo fator primo `q` de `p - 1`).

## Valores usados

| Variável | Valor | Tipo |
|---|---|---|
| `p` | 2147483647 (= 2^31 - 1) | público, primo |
| `g` | 7 | público, raiz primitiva módulo `p` |
| `a` | 123456789 | privado (lado A) |
| `b` | 987654321 | privado (lado B) |
| `A = g^a mod p` | 510444705 | público (enviado pelo lado A) |
| `B = g^b mod p` | 1018773341 | público (enviado pelo lado B) |
| `s = B^a mod p = A^b mod p` | 366175671 | segredo compartilhado |

Fatores primos de `p - 1`: 2, 3, 7, 11, 31, 151, 331.

## Como rodar

Ambiente gerenciado com [uv](https://docs.astral.sh/uv/):

```bash
uv sync
uv run python -m ipykernel install --user --name diffie-hellman --display-name "Python (diffie-hellman)"
```

Depois abra `diffie_hellman.ipynb` e selecione o kernel **Python (diffie-hellman)**
(ou aponte para `.venv/bin/python`).

Para executar sem abrir o editor:

```bash
uv run jupyter nbconvert --to notebook --execute --inplace diffie_hellman.ipynb
```
