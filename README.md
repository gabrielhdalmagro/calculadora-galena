# Calculadora - Rádio de Galena
Ferramenta interativa desenvolvida para auxiliar no dimensionamento prático dos componentes de um Rádio de Galena. Projeto criado para a disciplina de Física 3 (FIS003) da Universidade Tecnológica Federal do Paraná (UTFPR - Campus Toledo).
**Link para acesso da calculadora: https://gabrielhdalmagro.github.io/calculadora-galena/**

---

## Como a calculadora funciona?

### 1. Escolha da Topologia e cálculo do circuito de Sintonia LC
Primeiramente, o usuário define a abordagem do projeto (sintonia por indutor ou capacitor variável). A partir da frequência da portadora desejada ($f_c$) e o valor do capacitor escolhido para o projeto ($C_1$), calcula-se a indutância ideal por meio da equação: $$L = \frac{1}{(2\pi f_c)^2 C_1}$$

### 2. Correção pelo Fator de Nagaoka
No caso de sintonia por **indutor variável**, é necessário dimensionar a bobina que será confeccionada. Diferentemente de casos ideais, as bobinas reais construídas sofrem dispersão de fluxo nas bordas. O script então calcula a razão entre o diâmetro ($D$) e o comprimento ($l$) informados e realiza uma interpolação linear com base na tabela dos coeficientes do Fator de Nagaoka, obtendo o **fator de redução ($k$)**.

### 3. Centralização de sintonia
Para maximizar a usabilidade do rádio, o algoritmo garante que a estação principal seja sintonizada no centro físico do componente de ajuste:
* **Capacitor Variável:** O cálculo utiliza a capacitância média do componente, garantindo sintonia central e curso de ajuste para ambas as direções.
* **Indutor Variável:** O script dimensiona o número de espiras com base em **metade** do comprimento total do tubo ($l/2$). Assim, ao finalizar o enrolamento completo, o cursor deslizante encontrará a ressonância exata no meio da bobina.

### 4. Detector de Envoltória (Demodulador)
A interface calcula os limites para a constante de tempo ($\tau$) do circuito de descarga RC, com base na equação: $$\frac{1}{2\pi f_c} \ll \tau < \frac{1}{2\pi f_m}$$

No modo automático, o sistema adota um valor de **$\frac{2}{3}$** desse intervalo permitido, garantindo assim menor distorção no sinal de áudio.
O código também calcula automaticamente o paralelo de resistores caso seja utilizado um fone/buzzer juntamente com um resistor de carga.

### 5. Geração de Parâmetros (Resumo)
Ao finalizar os cálculos, o sistema compila e exibe um relatório contendo todos os parâmetros elétricos e dimensionais do projeto, prontos para a execução física do mesmo.
