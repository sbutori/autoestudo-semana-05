# autoestudo-semana-05


## 1. Tente valores diferentes do argumento num_examples na função load_data_nmt. Como isso afeta os tamanhos do vocabulário do idioma de origem e do idioma de destino?

### Resultados de execução do notebook com diferentes num_examples
```
num_examples=1
X: tf.Tensor(
[[4 0 2 3 3 3 3 3]
 [4 0 2 3 3 3 3 3]], shape=(2, 8), dtype=int32)
valid lengths for X: tf.Tensor([3 3], shape=(2,), dtype=int32)
Y: tf.Tensor(
[[4 0 2 3 3 3 3 3]
 [4 0 2 3 3 3 3 3]], shape=(2, 8), dtype=int32)
valid lengths for Y: tf.Tensor([3 3], shape=(2,), dtype=int32)

num_examples=300
X: tf.Tensor(
[[14 68  0  4  5  5  5  5]
 [16 64  2  4  5  5  5  5]], shape=(2, 8), dtype=int32)
valid lengths for X: tf.Tensor([4 4], shape=(2,), dtype=int32)
Y: tf.Tensor(
[[82  2  4  5  5  5  5  5]
 [14  6  2  4  5  5  5  5]], shape=(2, 8), dtype=int32)
valid lengths for Y: tf.Tensor([3 4], shape=(2,), dtype=int32)

num_examples=1200
X: tf.Tensor(
[[140   7   2   5   6   6   6   6]
 [110 148   0   5   6   6   6   6]], shape=(2, 8), dtype=int32)
valid lengths for X: tf.Tensor([4 4], shape=(2,), dtype=int32)
Y: tf.Tensor(
[[173 320 296   2   4   5   5   5]
 [ 45 347   0   4   5   5   5   5]], shape=(2, 8), dtype=int32)
valid lengths for Y: tf.Tensor([5 4], shape=(2,), dtype=int32)
```

### Resposta
  
O parâmetro num_examples determina a quantidade de exemplos carregados para a modelagem. Conforme o valor de num_examples aumenta (1, 300, 1200), observa-se um aumento na diversidade e complexidade das sequências em X e Y. Por exemplo, com num_examples=1 o comprimento válido de Y é 3. Já com num_examples=1200, o comprimento válido de Y chega a 5, indicando que mais dados e variações de comprimento nas sequências estão sendo incluídos. A mesma situação é observada com X, sendo que com num_examples=1 temos um comprimento válido de 3 e com 300 (ou mais) exemplos o comprimento válido passa a ser 4.

## 2. O texto em alguns idiomas, como chinês e japonês, não tem indicadores de limite de palavras (por exemplo, espaço). A tokenização em nível de palavra ainda é uma boa ideia para esses casos? Por que ou por que não?

### Resposta

A tokenização em nível de palavra não é ideal para idiomas como chinês e japonês, que não possuem delimitadores claros de palavras, como espaços. Esses idiomas apresentam desafios específicos para segmentação, pois os limites de palavras não são facilmente distinguíveis. Por exemplo, em determinado ponto do código, é utilizado espaço para separar os tokens:

```
def tokenize_nmt(text, num_examples=None):
  (...)
  source.append(parts[0].split(' '))
  target.append(parts[1].split(' '))
```

Isso não seria possível em uma linguagem que não usa espaço como delimitador. Em vez disso, a tokenização em nível de caractere ou subpalavra pode ser mais eficaz, permitindo que modelos lidem melhor com as estruturas linguísticas relativamente mais complexas desses idiomas. 

