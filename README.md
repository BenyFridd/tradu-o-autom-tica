**Pergunta 1: Tente valores diferentes do argumento `num_examples` na função `load_data_nmt`. Como isso afeta os tamanhos dos vocabulários do idioma de origem e do idioma de destino?**

Ao variar o valor de `num_examples` na função `load_data_nmt`, você altera a quantidade de exemplos (pares de frases) usados para construir os vocabulários. Isso afeta os tamanhos dos vocabulários da seguinte forma:

- **Valores Maiores de `num_examples`:**  
  Quando um número maior de exemplos é utilizado, mais palavras únicas são encontradas tanto no idioma de origem (por exemplo, inglês) quanto no idioma de destino (por exemplo, francês). Por exemplo, em um experimento, com `num_examples = 600`, o vocabulário do inglês atingiu aproximadamente 10.012 palavras e o do francês cerca de 14.592 palavras. Isso ocorre porque a maior diversidade de sentenças tende a incluir uma variedade maior de termos, aumentando o tamanho dos vocabulários.

- **Valores Menores de `num_examples`:**  
  Ao reduzir o número de exemplos, há uma quantidade menor de palavras únicas sendo capturadas durante o pré-processamento. Assim, os vocabulários para ambos os idiomas serão significativamente menores, pois muitos termos que apareceriam apenas em um conjunto maior de dados não estão presentes. Essa redução pode levar a um vocabulário mais compacto, mas também pode limitar a capacidade do modelo de lidar com palavras menos frequentes ou com maior variabilidade.

Portanto, o tamanho do vocabulário é diretamente influenciado pela quantidade de dados utilizados: quanto maior o número de exemplos, maior será o vocabulário, o que pode impactar tanto a capacidade de generalização do modelo quanto o tempo e a complexidade do treinamento.

---

**Pergunta 2: O texto em alguns idiomas, como chinês e japonês, não tem indicadores de limite de palavras (por exemplo, espaço). A tokenização em nível de palavra ainda é uma boa ideia para esses casos? Por que ou por que não?**

Para idiomas como chinês e japonês, a tokenização em nível de palavra (baseada em espaços) não é recomendada, e isso se deve aos seguintes motivos:

- **Ausência de Delimitadores Explícitos:**  
  Diferente do inglês ou do francês, que utilizam espaços para separar palavras, o chinês e o japonês apresentam sequências contínuas de caracteres sem delimitadores claros. Como resultado, uma tokenização direta baseada em espaços não consegue segmentar adequadamente as palavras, gerando tokens que podem não representar unidades linguísticas significativas.

- **Segmentação Inadequada:**  
  Sem uma segmentação apropriada, a divisão do texto pode resultar em um vocabulário mal definido e em representações que não capturam corretamente a semântica ou a morfologia do idioma. Isso prejudica o desempenho de tarefas como a tradução automática, onde a precisão na identificação das unidades lexicais é crucial.

- **Soluções Mais Adequadas:**  
  Para esses idiomas, são preferíveis abordagens alternativas, como:
  - **Tokenização em Nível de Caracteres:**  
    Onde cada caractere é tratado como uma unidade. Embora possa aumentar o comprimento das sequências, essa abordagem evita erros de segmentação.
  - **Métodos de Tokenização Subpalavra:**  
    Técnicas como Byte Pair Encoding (BPE) ou SentencePiece podem dividir o texto em unidades menores (subpalavras), capturando melhor as estruturas linguísticas e reduzindo o tamanho do vocabulário.
  - **Ferramentas Especializadas:**  
    Utilizar ferramentas de segmentação específicas, como Jieba para chinês e MeCab para japonês, que aplicam métodos estatísticos e regras linguísticas para identificar corretamente as fronteiras das palavras.

Portanto, para chinês e japonês, a tokenização em nível de palavra sem segmentação prévia não é eficaz. Métodos que consideram a segmentação apropriada ou que operam em unidades menores (subpalavras ou caracteres) são essenciais para uma representação mais precisa e para o sucesso de aplicações em processamento de linguagem natural.
