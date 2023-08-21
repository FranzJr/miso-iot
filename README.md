# miso-iot
Modulo 8 - Internet de las cosas - Maestría de la Universidad de los Andes de Ingenieria de Software MISO

### Integrantes
| Nombre                   | Correo                                                          |
| ------------------------ | --------------------------------------------------------------- |
| Wilber Palomino Acosta   | [w.palomino@uniandes.edu.co](mailto:w.palomino@uniandes.edu.co) |
| Franz Rogelez Carvajal | [f.rogelez@uniandes.edu.co](mailto:f.rogelez@uniandes.edu.co)|

## Reto 1

### Caracterización de la variable física (Intensidad Lumínica)

La intensidad lumínica es una medida fundamental en el mundo de la física que se relaciona directamente con el fenómeno de la luz. Esta variable determina la potencia lumínica que se recibe en una superficie por unidad de área. Es vital en diversas aplicaciones, desde sistemas de control de iluminación hasta estudios medioambientales.

Las unidades predominantes para esta medición son:

- **Lúmenes (lm):** Se refiere a la cantidad total de luz visible que emite una fuente en todas las direcciones por segundo.
  
- **Lux:** Es una medida de la intensidad lumínica, que representa los lúmenes por metro cuadrado. Es la cantidad total de luz visible de una fuente que incide sobre un área de superficie específica.

---
### Selección de dispositivo de sensado

Al considerar dispositivos de sensado para medir la intensidad lumínica, se encontraron varias opciones, que van desde fotorresistencias hasta fotodiodos y fototransistores. Cada sensor tiene sus particularidades, como velocidad de respuesta, precisión y rango de operación.

- **Fotorresistencia (LDR):** Es un tipo de resistor cuya resistencia cambia en función de la cantidad de luz que incide sobre él. Presenta una sensibilidad en el rango de longitud de onda de 560nm a 600nm, lo que se asemeja al rango de percepción del ojo humano. Su respuesta es que cuanto más luz recibe, menor es su resistencia.

- **Fotodiodos y Fototransistores:** Aunque ofrecen respuestas más rápidas y pueden tener una mayor precisión, tienden a ser más caros y requieren circuitería adicional para operar de manera óptima.

**Justificación de Selección:** Se optó por utilizar la **Fotorresistencia LDR** (GL5516) para esta implementación. A pesar de tener una respuesta más lenta en comparación con otros sensores, cumple con los requisitos necesarios para esta aplicación. Su bajo costo, facilidad de uso y su curva de respuesta que se asemeja a la del ojo humano lo hacen adecuado para este proyecto. Además, no se requiere una alta precisión ni tiempo de respuesta inmediato para esta aplicación específica.

### Sensor de Intensidad Lumínica con NodeMCU y LDR

### Extensión de la capa de dispositivo

En este proyecto, hemos utilizado una **fotorresistencia LDR**, que disminuye su resistencia a medida que se incrementa la exposición a la luz. Estos sensores tienen una velocidad de respuesta más baja comparada con otros dispositivos, como fotodiodos o fototransistores, y su resistividad puede verse afectada por la temperatura ambiente. Sin embargo, para este proyecto, el LDR es ideal debido a su bajo costo, respuesta adecuada y requisitos específicos del caso de uso.

### Características del LDR
* Sensibilidad en longitud de onda de la luz: 560nm a 600nm.
* Curva de respuesta similar a la del ojo humano.
* A cuanta más luz, menor resistencia.
  
### Implementación

Las imágenes siguientes muestran los resultados de la implementación del LDR con el NodeMCU:

A continuación se muestra los resultados de la implementación del LDR sobre el NodeMCU

![image](https://github.com/FranzJr/miso-iot/assets/961269/c42e8342-454f-4c85-b2ce-56b6fe131f94)

Imagen 1. Respuesta del Monitor Serial

![image](https://github.com/FranzJr/miso-iot/assets/961269/1555bab2-9396-4d79-8ab8-764fcc64afe9)

Imagen 2. Respuesta en REMA de temperatura

![image](https://github.com/FranzJr/miso-iot/assets/961269/12febaeb-a9c2-4aaf-9c77-9b5a62d88e43)

Imagen 3. Respuesta en REMA de humedad

![image](https://github.com/FranzJr/miso-iot/assets/961269/694e2295-7255-4f12-8b85-cf518e7141ab)

Imagen 4. Respuesta en REMA de luminosidad


### Conclusión

Este proyecto demuestra la implementación de un sensor LDR con NodeMCU para medir la intensidad lumínica. Es una solución eficiente y rentable para aplicaciones donde la precisión extrema y la alta velocidad de respuesta no son cruciales. Gracias al NodeMCU, es posible visualizar y enviar los datos recopilados a diferentes plataformas para su análisis y uso posterior.
