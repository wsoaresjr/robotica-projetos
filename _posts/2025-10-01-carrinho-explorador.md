---
layout: post
title: "Carrinho Explorador (Ultrassom + Desvio)"
tags: [Arduino, HC-SR04, L298N, OBR]
image: /assets/capas/carrinho-explorador.jpg
repo: https://github.com/wsoaresjr/carrinho-explorador
demo: https://wsoaresjr.github.io/carrinho-explorador/
---

Robô autônomo que mede distância (HC-SR04) e desvia obstáculos usando ponte H L298N. Ideal para introduzir sensores, atuadores e lógica de decisão.

## Materiais
- Arduino UNO R3
- Sensor ultrassônico HC-SR04
- Ponte H L298N
- 2 motores DC + rodas + chassi
- Bateria (ou pack 18650)

## Código
Veja o repositório no GitHub:  
[Repositório no GitHub]({{ page.repo }})

## Próximos passos
- Implementar curvas suaves com PWM  
- Registros de telemetria (distância por tempo)  
- Integração com LCD I2C para debug
