# miso-iot
Modulo 8 - Internet de las cosas - Maestría de la Universidad de los Andes de Ingenieria de Software MISO

### Integrantes
| Nombre                   | Correo                                                          |
| ------------------------ | --------------------------------------------------------------- |
| Wilber Palomino Acosta   | [w.palomino@uniandes.edu.co](mailto:w.palomino@uniandes.edu.co) |
| Franz Rogelez Carvajal | [f.rogelez@uniandes.edu.co](mailto:f.rogelez@uniandes.edu.co)|


# Reto 2

## Enlace del repositorio del código

[Repositorio en GitHub](https://github.com/FranzJr/miso-iot/tree/main/Reto%202)

## Análisis comparativo de los resultados de consumo energético

| Parámetro                                   | Zigbee                     | WiFi                          | LoRa                             |
|---------------------------------------------|----------------------------|-------------------------------|----------------------------------|
| Área de Cobertura                           | Rojo (simulador)           | Verde (simulador)             | Azul (simulador)                 |
| Consumo Energético                          | Agotó más rápido la batería| Agotó más rápido que LoRa     | Consumo menor de energía         |
| Batería Restante después de 1000 Iteraciones| 60%                        | 58%                           | 92%                              |
| Iteraciones antes de agotar la batería      | 2400                       | 3000                          | 16000                            |

### Notas:

- **Área de Cobertura**: Los tres protocolos se identifican con colores diferentes en el simulador. Más visual que funcional.
  
- **Consumo Energético**: Zigbee y WiFi consumen más energía que LoRa. Coherente con la naturaleza de baja potencia y largo alcance de LoRa.

- **Batería Restante después de 1000 Iteraciones**: LoRa es el más eficiente con 92%, seguido de Zigbee (60%) y WiFi (58%).

- **Iteraciones antes de agotar la batería**: LoRa necesita 16000 iteraciones para agotar la batería, en contraste con Zigbee (2400) y WiFi (3000).

La elección del protocolo dependerá de la infraestructura, alcance deseado, densidad de nodos y tasas de transferencia requeridas, entre otros factores.

## Procedimiento del experimento

Se implementaron 21 nodos de tipo sensor. Estos se conectaron en serie con el máximo rango de comunicación para Zigbee y se simuló para mil iteraciones. Cada iteración representa el muestreo del área en busca de un evento natural. Eventos generados independientemente para cada sensor. A pesar del mayor alcance en WiFi y LoRa, se mantuvo la distribución de Zigbee por dos razones:

1. Observar el gasto de batería y las iteraciones del script.
2. Al aumentar el área de distribución, el programa se ejecuta más lento, pudiendo llegar a bloquear CupCarbon.

### Reportes de simulación

- **Zigbee**: Área de cobertura en rojo. Ver imagen 1.
- **WiFi**: Área de cobertura en verde. Ver imagen 2.
- **LoRa**: Área de cobertura en azul. Ver imagen 3. Un sensor en LoRa no mostró su consumo debido a un bloqueo de CupCarbon.

![Image 1](https://lh3.googleusercontent.com/SFgZMS217pndWSXIdZbPpVRQYWCM_IbcNmq4j99Slrfzq8GKaF3XZVP1qmIy5KG7Ud-6idaHOUKN6DmWPCPUHPa4tLcB4RFZd88w-YD-7Vyhq2mGHIxcV4D_r9IbZX8vopBKCzmXlqOhnW55QxCTor8)
**Imagen 1.** Simulación nodos sensor con tecnología Zigbee

![Image 2](https://lh5.googleusercontent.com/Ov1JXXcw6pRC_gziIo3QoNaaJ8I2RTKLDJGDJyDAz_anyb6dJL8ZG-yn70t5EoiERHnWuGwl9EUWFipgP-ya7t82uCFGZJtJEfy8LJWYxDUijShJtS518HeplzFozVVYeOWsg7RovkAi9C2cyFmXeDE)
**Imagen 2.** Gráfica de consumo de energía de un nodo sensor con tecnología Zigbee

![Image 3](https://lh5.googleusercontent.com/SemLADuHoZbfkllrKKnOiyEcEktkRUgNG_gkP7YmNqmBA7m7adjc1-99swq4Z3qR9db41crStcETiuTDKIy3pJifu7-f6nLcz2qA4t84E3s9TrrcudrwPz1Ooebx705AIiUWtidI5wBUgMqv5hljCnY)
**Imagen 3.** Simulación nodos sensor con tecnología WiFi

![Image 4](https://lh3.googleusercontent.com/on9n-8Zbbw8VR1DX1WNHopNQjydSVAdtbWefivms1CpiFpqh4STu9TPQwVzvT2m8PELRx1Vvx7Gt6WdaDVOl165l7DPZDiNyTVY6VSXxoIXvebRNAGS6H1kfZ4LtNUvvVOLcUSCgxROl2jRypcZB1kw)
**Imagen 4.** Gráfica de consumo de energía de un nodo sensor con tecnología WiFi

![Image 5](image-5.png)
**Imagen 5.** Simulación nodos sensor con tecnología LoRa

Los scripts usados para cada Nodo Base y Nodo Sensor se detallan a continuación. La función principal del script es detectar eventos naturales y notificar si el nivel de batería es bajo.

*(Nota: Por simplicidad y formato, se omite el contenido detallado de los scripts. Por favor, revíselo en el repositorio vinculado).*
https://docs.google.com/document/u/1/d/e/2PACX-1vRQX3AtmMSGIlp6kjbNboyYFsbSUKotTXYrDcVpSeg0YLitdnOseuNeRzeVHPJtZIoawIZNkwxYRYlR/pub

## Preguntas

a. **¿Cuál de los protocolos agotó más rápido la batería?**
   Zigbee y WiFi agotaron más rápido que LoRa debido a su naturaleza de mayor potencia.
   
b. **¿Algún estándar no agotó la batería?**
   Todos finalizaron las mil iteraciones sin agotar completamente la batería. Zigbee llegó al 60%, WiFi al 58%, y LoRa al 92%.
   
c. **¿Cuántas iteraciones en promedio tardó en agotar la batería?**
   Zigbee: 2400 (ver imagen 6), WiFi: 3000 (ver imagen 7), LoRa: 16000 (ver imagen 8).

![Image 6](https://lh5.googleusercontent.com/T-7OdEivFJcQJ0PcS2FIjqatbrKMrfqSYv4t-6SOqnWx4-9sxBJLQbf0gfZWcI3HpYdXoH-JyRUTCbNR99gFbIkQ1xebn4vUicyp_iWlQxPObCdi_zZrT3doQ8jsj-jhLKiYLwtFN2pz81uXRdz-kzk)
![Image 7](https://lh3.googleusercontent.com/l0n97VKuWVS7E5tDOecAz0OxcTSDPyvKy_4YmzuTXmetExHDZBstY_xvmtPIKZU6bToCgSDrHPRGMGwoKM2NGXCR_vJZFS_mDbovjnl5mvP3xajBEBUVclYnhvhV-4ue7CDyxoEAxzIclO6DB1-JiPY)
![Image 8](https://lh6.googleusercontent.com/a9QoZL6qgPZUZh824_D7rF1k_HB49kd-ipCNWKp7gv3oTrxdEXXIXlNGrM20SUpSHfFPi-KS6V0gM8AJmxvBxdBminSlgosn9inFaUyb77HuQt4lO1qQqKYAVnhzQzITcfIf7cmj6lFf46xAcQTxVIo)

## Reflexión

Los resultados reflejan las diferencias en diseño y propósito de cada tecnología. Zigbee y WiFi son adecuados para aplicaciones de corta distancia y alta velocidad, mientras que LoRa es ideal donde la eficiencia energética y la cobertura a larga distancia son esenciales. La simulación mostró la superioridad de LoRa en cuanto a eficiencia energética y rango.

---

Espero que esta versión te sea útil. ¡Déjame saber si hay algo más en lo que pueda ayudarte!