# Projeto de Binarização de Imagens com OpenCV

Este é o primeiro projeto de binarização de imagens utilizando a biblioteca OpenCV. O objetivo é aplicar diferentes etapas de processamento em uma imagem para convertê-la em uma representação binária e combinar os resultados.

---

## Etapas do Projeto

### 1. Importação das Bibliotecas
As bibliotecas necessárias para executar o código:

```python
import cv2 as cv
import numpy as np
```

### 2. Carregamento da Imagem
Carregamos uma imagem de um objeto (por exemplo, uma bola) para iniciar o processamento:

```python
img = cv.imread('pelota.jpg')
cv.imshow('pelota', img)
cv.waitKey(0)
```

---

### 3. Conversão para Tons de Cinza
Convertemos a imagem original para tons de cinza:

```python
img_cinza = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('img_cinza', img_cinza)
cv.waitKey(0)
```

---

### 4. Aplicando o Filtro Gaussiano
Aplicamos um filtro Gaussiano para suavizar a imagem:

```python
imagem_suave = cv.GaussianBlur(img_cinza, (7, 7), 0)
cv.imshow('imagem_suave', imagem_suave)
cv.waitKey(0)
```

---

### 5. Binarização da Imagem
Convertemos a imagem suavizada para o formato binário:

- **Binarização Normal**:
  
```python
t, img_bin = cv.threshold(imagem_suave, 160, 255, cv.THRESH_BINARY)
cv.imshow('img_bin1', img_bin)
cv.waitKey(0)
```

- **Binarização Invertida**:

```python
t_2, img_bin_2 = cv.threshold(imagem_suave, 160, 255, cv.THRESH_BINARY_INV)
cv.imshow('img_bin2', img_bin_2)
cv.waitKey(0)
```

---

### 6. Combinação dos Resultados
Combinamos os resultados das duas binarizações utilizando o OpenCV e o NumPy:

```python
resultado = np.vstack([
    np.hstack([imagem_suave, img_bin]),
    np.hstack([img_bin, cv.bitwise_and(img_cinza, img_cinza, mask=img_bin)])
])
```

---

### 7. Redimensionando o Resultado
Reduzimos o tamanho da imagem combinada para facilitar a visualização:

```python
escala = 0.1  # Fator de escala
largura = int(resultado.shape[1] * escala)
altura = int(resultado.shape[0] * escala)
dimensoes = (largura, altura)

resultado_redimensionado = cv.resize(resultado, dimensoes, interpolation=cv.INTER_AREA)
```

---

### 8. Exibição Final
Exibimos o resultado final redimensionado:

```python
cv.imshow('Resultado Redimensionado', resultado_redimensionado)
cv.waitKey(0)
cv.destroyAllWindows()
```

---

## Requisitos
- Python 3.6+
- OpenCV
- NumPy

Para instalar as dependências, execute:

```bash
pip install opencv-python-headless numpy
```

---

## Como Executar
1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/seu-repositorio.git](https://github.com/AlexNocua/Binariza-o-de-imagens/
   ```

2. Execute o script:
   ```bash
    bin_imagems.ipynb
   ```

Certifique-se de que o arquivo `pelota.jpg` está no mesmo diretório do script ou qualquer outra imagem.

---

## Resultado Esperado
Uma janela será exibida com a combinação das imagens:
1. Imagem original.
2. Imagem em tons de cinza.
3. Imagem suavizada.
4. Imagens binarizadas e a combinação das mesmas.

---

