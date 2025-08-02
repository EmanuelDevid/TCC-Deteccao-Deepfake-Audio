# Detecção de Deepfakes de Áudio com Wavelets e CNNs

Este repositório contém os códigos-fonte desenvolvidos para o Trabalho de Conclusão de Curso "Detecção de Áudios Falsos Através de Wavelets e Redes Neurais Convolucionais", do curso de Engenharia da Computação da Universidade Federal do Ceará (UFC), Campus Sobral.

O objetivo do projeto é avaliar uma metodologia que combina a Transformada Wavelet Contínua (CWT) para extração de características e a arquitetura de Rede Neural Convolucional (CNN) MobileNet para a classificação de áudios como reais ou falsos.

---

## Estrutura do Repositório

O projeto está dividido em dois notebooks principais que devem ser executados em sequência:

1.  `Escalogramas.ipynb`: Responsável pelo pré-processamento dos áudios e geração dos escalogramas.
2.  `MobileNetV2.ipynb`: Responsável pelo treinamento, validação e teste do modelo de CNN.

---

## Pré-requisitos

O ambiente de execução utilizado foi o **Google Colab Pro** com aceleração por GPU. A base de dados utilizada deve ser previamente baixada e organizada no Google Drive.

* **Base de Dados:** [FoR (Fake-or-Real) Dataset](https://bil.eecs.yorku.ca/datasets/)
    * A versão utilizada foi a `for-2seconds`.
    * A estrutura de pastas esperada no Google Drive é a seguinte:
        ```
        /MyDrive/FoR/for-2sec/for-2seconds/
        ├── training/
        │   ├── fake/
        │   └── real/
        ├── testing/
        │   ├── fake/
        │   └── real/
        └── validation/
            ├── fake/
            └── real/
        ```

---

## Como Executar

### Passo 1: Geração dos Escalogramas

Execute o notebook **`Escalogramas.ipynb`**.

* **Objetivo:** Converter os arquivos de áudio `.wav` da base FoR em imagens `.png` (escalogramas).
* **Configuração:** Dentro do notebook, você deve configurar duas variáveis principais:
    * `output_base_path`: O caminho no seu Google Drive onde as imagens geradas serão salvas (ex: `.../Datasets_Scalograms/Morl`).
    * `wavelet`: A família de wavelet a ser utilizada (`'morl'`, `'cmor1.5-1.0'` ou `'mexh'`).
* **Execução:** Este notebook deve ser executado **três vezes**, uma para cada família de wavelet, ajustando as variáveis `output_base_path` e `wavelet` a cada execução.

### Passo 2: Treinamento do Modelo de CNN

Execute o notebook **`MobileNetV2.ipynb`**.

* **Objetivo:** Treinar, validar e testar o modelo MobileNet com os escalogramas gerados no passo anterior.
* **Configuração:** Na primeira célula do notebook, configure a variável `base_path` para apontar para a pasta de escalogramas que você deseja usar (ex: `.../Datasets_Scalograms/Morl`).
* **Execução:** Este notebook também deve ser executado **três vezes**, uma para cada conjunto de escalogramas gerado.
* **Saídas:** Ao final da execução, todos os resultados, incluindo o modelo treinado (`.keras`), o histórico de treinamento (`.json`), os arrays de predição (`.npy`) e os gráficos de desempenho, serão salvos na pasta `Training_Results_MobileNet_Accuracy` dentro do respectivo diretório da wavelet.

