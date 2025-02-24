# Motor Faults Detection

## Como Usar

1. Instalar esse repositório utilizando o seguinte comando:

```bash
git clone https://github.com/rafaelgreca/motor-faults-detection.git
```

2. Criar um arquivo `.env` na pasta raíz do projeto e criar duas variáveis (`KAGGLE_USERNAME` e `KAGGLE_KEY`).

Exemplo:

```bash
KAGGLE_USERNAME=username
KAGGLE_KEY=key
```

Para ter acesso aos valores dessas variáveis, é necessário estar logado na sua conta do Kaggle e depois acessar o link: https://www.kaggle.com/settings. Encontre a sessão de `API` e clique em `Criar Novo Token`.

3. Crie um novo ambiente virtual com o `conda` utilizando o comando a seguir:

```bash
conda create --name motor-faults python=3.11 && conda activate motor-faults
pip install -r requirements.txt
```

4. Abra o notebook `main.ipynb` e rode as células sequencialmente.

## Justificativas

- Pré-processamento:
    - **Downsampling**: Diminuir a taxa de aquisição das amostras e diminuir os arrays para conseguir treinar o modelo na GPU.
    - **FFT**: É a técnica mais conhecida na área de processamento de sinais e que tem como principal objetivo transformar um sinal no domínio do tempo para o domínio da frequência. A principal justificativa para essa etapa é que os sinais no domínio da frequência geralmente são mais valiosos do que no domínio do tempo (cada nível de desbalanceamento pode ter uma faixa de frequência dominante diferente).
    - **Dividir em janelas**: Além da sua necessidade na utilização de um modelo LSTM, dividir os sinais em janelas (com os conceitos de `window_size` e `stride`) ajuda a diminuir o tamanho dos vetores e a criar mais amostras de dados.
- Modelo:
    - **LSTM**: Devido a sua facilidade de implementação, o modelo LSTM é um dos modelos mais conhecidos e utilizados em dados de séries temporais. Porém, possui alguns pontos negativos: o seu treinamento não é paralelizável, requer mais memória para treinar e a etapa de treinamento é lenta; para entradas muito grandes o modelo tende a "esquecer" o que viu nos valores iniciais (vanishing gradient problem); necessita de um grande conjunto de dados disponível para o treinamento; é mais propensa ao overfiting.