# kinect-2-libras

Esta aplicação possui o objetivo de mapear gestos da Língua Brasileira de Sinais
(LIBRAS), capturados através do Microsoft Kinect (V2) e salvar os dados em formato
compatível com softwares de aprendizado de máquina.

##Introdução

A API [Kinect-Finger-Tracking](https://github.com/LightBuzz/Kinect-Finger-Tracking.git)
desenvolvida e disponibilizada por [LightBuzz Software](https://github.com/LightBuzz/)
fornece pontos que representam as extremidades de cada um dos 5 dedos da mão, todos mapeados
diretamente pelo Kinect. Seu princípio de cálculo é aproximar os pontos extremos através de
um *Convex Hull*.

Para o reconhecimento de gestos estáticos em LIBRAS é necessário capturar a posição da
mão "alvo" e reconhecer padrões para conseguir inferir o gesto observado. Porém, unicamente
com os pontos fornecidos pela API torna-se impraticável tal atividade. Uma das possíveis
solução é "simular" os efeitos do sensor [Leap Motion](https://www.leapmotion.com/) através
do Kinect, e assim capturar mais pontos na mão.

#Pontos de Interesse

Inicialmente foi utilizada uma informação fornecida pelo próprio Kinect, o centro da mão:
![Centro da mão](https://github.com/inessadl/kinect-2-libras/blob/master/images/01-centerPoint.png)

Para obter um dos pontos fornecidos pelo *Leap Motion*, que consiste no encontro entre as
falanges médias e as falanges proximais, é necessário utilizar-se do ponto central da mão.
Obtendo esta informação, é possível calcular o Ponto Médio entre a ponta de cada dedo
com o centro da mão:

![Localização das falanges da mão](https://github.com/inessadl/kinect-2-libras/blob/master/images/02-exam.png)

![Área de cálculo das falanges](https://github.com/inessadl/kinect-2-libras/blob/master/images/03-calculate.png  )

Uma vez com a área de cálculo definida, a extração desses pontos se dá através da angulação
na qual eles se encontram. Esta serve para corrigir perturbações que ocorrem pela diferença de
*posição do dedo médio* em relação ao demais e do ângulo em que cada um se econtra em relação
ao centro. Por fim, tem-se os seguintes pontos calculados:

![Ponto das Falanges](https://github.com/inessadl/kinect-2-libras/blob/master/images/04-falanges.png)

Com a obtenção dos pontos, cada um segue a seguinte ordem de extração:

![Ponto das Falanges](https://github.com/inessadl/kinect-2-libras/blob/master/images/05-recordedOrder.png)

# Classificação

Para a realização da classificação dos gestos através dos pontos calculados acima,
foram utilizados em um primeiro momento 4 implementações diferentes, são elas:

- SVM One-vs.-one (Kernel=linear)
- SVM One-vs.-rest
- Decision Tree
- Stochastic Gradient Descent

## Contribuidores

* Inessa Luerce [@inessadl](https://github.com/inessadl)
* Lucas Tortelli [@lmtortelli](https://github.com/lmtortelli)

## Referências

- [LightBuzz/Kinect-Finger-Tracking](https://github.com/LightBuzz/Kinect-Finger-Tracking)
- [LightBuzz/Vitruvius](https://github.com/LightBuzz/Vitruvius)
- [Scikit-Learn: Machine Learning in Python](http://scikit-learn.org/)

## License

Licensed under the [Apache License, Version 2.0](https://github.com/inessadl/kinect-2-libras/blob/master/LICENSE)
