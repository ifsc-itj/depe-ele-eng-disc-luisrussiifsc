> toda proposta de tema de projeto de PI3 deve seguir o padrão abaixo.

# Proposta de Tema de PI3

**Título:**  
Desenvolvimento de um Modem Digital Ultrassônico de Baixo Custo para Transmissão de Dados

**Aluno(s):** Nome 1 e Nome 2  
**Orientador:** Prof. Nome

## Objetivo Geral

Desenvolver um modem digital para transmissão de dados utilizando modulação em frequência (M-FSK) de ondas acústicas ultrassônicas.

## Objetivos Específicos

- Programar o algoritmo de modulação no ESP32 para geração do sinal.
- Adaptar o sinal gerado pelo ESP32 para a transmissão acústica.
- Condicionar o sinal recebido para aquisição pelo ESP32.
- Programar o ESP32 para realizar a amostragem do sinal recebido.
- Simular e implementar a estratégia de demodulação mais eficaz.
- Pesquisar e adquirir os componentes necessários para a implementação.
- Integrar todas as etapas do projeto em um sistema funcional.
- Realizar testes de comunicação a uma distância mínima de 5 metros.
- Garantir uma taxa de transmissão de pelo menos 100 bits/s.


## Metodologia

Inicialmente, foram definidos alguns blocos essenciais para o desenvolvimento do sistema, os quais são apresentados a seguir. No entanto, esses blocos podem ser ajustados ao longo do processo, conforme necessário.

### 1. Seleção e Testes do Transdutor Ultrassônico

A partir do levantamento preliminar, serão pesquisados e encomendados transdutores ultrassônicos, responsáveis pela conversão de energia elétrica em mecânica (e vice-versa). A definição das duas frequências de modulação será realizada somente após testes experimentais para obter a função de transferência do transdutor, determinando as frequências ideais para comunicação (espera-se operar próximo de 40 kHz).

### 2. Implementação da Modulação FSK no ESP32

Será implementado um algoritmo de modulação no ESP32 utilizando PWM de 3.3V com frequência variável para gerar o sinal FSK. O tempo de bit será definido por timers do ESP32, sendo detalhado na etapa de demodulação.

### 3. Dimensionamento do Amplificador Classe D

O próximo passo é o projeto de um amplificador Classe D com MOSFETs apropriados para operar nas frequências desejadas. O chaveamento será controlado por um gate driver, visando eficiência e melhor resposta do sistema.

#### 3.1. Circuito de Condicionamento para o Gate Driver

Considerando que o gate driver disponível exige 10V para acionamento, será projetado um circuito de condicionamento para converter o sinal de 3.3V do ESP32 para 10V, usando uma chave eletrônica com BJTs ou MOSFETs.

#### 3.2. Alimentação

Será adquirido um conversor boost para elevar a tensão de alimentação do amplificador (estimada em até 100V). O valor definitivo dependerá dos testes com o transdutor e das limitações do circuito bootstrap do gate driver.

#### 3.3. Filtro Sintonizado

O sinal amplificado passará por um filtro LC sintonizado para garantir uma onda cossenoidal mais pura possível, com componentes dimensionados de acordo com a faixa de frequência de operação.

### 4. Condicionamento do Sinal para Conversão Analógica-Digital

#### 4.1. Pré-Amplificação

O sinal recebido pelo transdutor passará por um pré-amplificador para aumentar sua amplitude sem prejudicar a relação sinal-ruído. Serão testadas abordagens com amplificadores operacionais e JFETs.

#### 4.2. Filtragem

Em seguida, o sinal será processado por um filtro passa-faixa, projetado para selecionar apenas as frequências próximas às de modulação. Serão simuladas topologias Butterworth e Chebyshev, e pode ser necessário adquirir amplificadores operacionais de baixo ruído e alta rejeição de modo comum.

#### 4.3. Condicionamento da Tensão DC

Após a filtragem, será ajustado o nível DC do sinal para garantir que esteja dentro da faixa operacional do ESP32, evitando saturação ou danos ao microcontrolador.

#### 4.4. Sistema de Controle Automático de Ganho (AGC)

Um circuito AGC será implementado para manter o sinal dentro da faixa ideal de entrada do ADC do ESP32, ajustando dinamicamente o ganho. Serão avaliadas soluções usando CIs dedicados ou circuitos analógicos.

### 5. Demodulação Digital

A etapa de demodulação será feita de forma digital, após a amostragem do sinal analógico. O ESP32 será configurado para garantir uma taxa de amostragem suficiente para sinais em torno de 40 kHz, respeitando o critério de Nyquist (pelo menos 80 kHz).

#### 5.1. Conversão Analógica-Digital com o ESP32

Serão otimizadas as configurações do ADC do ESP32 para garantir a amostragem eficiente e a qualidade do sinal para demodulação.

#### 5.2. Estratégias para Identificação das Frequências

Serão testadas abordagens como filtros digitais centrados nas frequências de modulação, medição do nível de energia, Transformada Rápida de Fourier (FFT), algoritmo de Goertzel e multiplicação digital para extração dos símbolos.

#### 5.3. Definição da Taxa de Transmissão

A taxa de transmissão (baud rate) será definida após os testes de demodulação, buscando atingir pelo menos 100 bits/s.

### 6. Prototipagem

As etapas serão inicialmente montadas em protoboard para validação individual, seguidas do desenvolvimento de uma placa de circuito impresso.

### 7. Ambiente de Testes e Validação

Os testes iniciais poderão ser realizados fora da água, mas o objetivo é atingir pelo menos 5 metros de comunicação subaquática (meta futura: 100 metros). A validação será feita por meio da gravação dos sinais demodulados em cartão de memória ou via osciloscópio.



# Cronograma
> crie um projeto no GitHub discriminando as ações e o período em que as mesmas serão realizadas
> coloque dentro do parênteses abaixo o link para o projeto criado

Clique [aqui](https://github.com/users/sergiopetrovcic/projects/8/views/1?layout=roadmap) para acessar o cronograma.

# Lista de Materiais

> Crie uma lista dos materiais que serão necessários para a execução do projeto  
> Utilize preço médio do mercado mesmo que não seja necessário comprar

| Item | Descrição                              | Unidade           | Valor Unitário | Quantidade | Total      |
|------|----------------------------------------|-------------------|---------------:|-----------:|-----------:|
| 01   | Placa de desenvolvimento ESP32         | unid.             |     R$ 55,00   |          1 |   R$ 55,00 |
| 02   | Transdutor piezoelétrico ultrassônico  | unid.             |     R$ 30,00   |          2 |   R$ 60,00 |
| 03   | MOSFET IRF540N ou similar              | unid.             |     R$ 7,00    |          4 |   R$ 28,00 |
| 04   | Gate driver IR2110 ou similar          | unid.             |     R$ 20,00   |          2 |   R$ 40,00 |
| 05   | Conversor boost (DC-DC)                | unid.             |     R$ 35,00   |          1 |   R$ 35,00 |
| 06   | Indutor (100 uH, 2A)                   | unid.             |     R$ 10,00   |          2 |   R$ 20,00 |
| 07   | Capacitor poliéster 100nF/400V         | unid.             |     R$ 2,00    |          4 |    R$ 8,00 |
| 11   | Bateria 12V 7Ah                        | unid.             |   R$ 130,00    |          1 |  R$ 130,00 |
| 12   | Protoboard                             | unid.             |     R$ 25,00   |          1 |   R$ 25,00 |
| 13   | Fios, conectores e jumpers diversos    | conjunto          |     R$ 20,00   |          1 |   R$ 20,00 |

|      |                                        |                   |               |            |            |
|      |                                        |                   |               |            | **R$ 453,00** |



## Unidades Curriculares Envolvidas

- Eletrônica 1 e 2
- Eletrônica de Potência 1
- Sistemas de Comunicação
- Processamento Digital de Sinais
- Microcontroladores
- Programação 1
