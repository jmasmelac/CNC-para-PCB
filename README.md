# Implementación de dispositivo CNC a partir de GRBL

Este proyecto describe el desarrollo e implementación de una máquina CNC diseñada para fabricar placas de circuito impreso (PCB) utilizando el firmware de código abierto **GRBL**. Se documenta la construcción física, los materiales utilizados, la configuración de software y pruebas experimentales realizadas.

## Tabla de contenido

1. [Introducción](#introducción)
2. [Marco teórico](#marco-teórico)
3. [Solución propuesta](#solución-propuesta)
4. [Desarrollo del dispositivo](#desarrollo-del-dispositivo)
5. [Pruebas experimentales](#pruebas-experimentales)
6. [Conclusiones](#conclusiones)

---

## Introducción

El proyecto surge como solución a los problemas relacionados con el tiempo de desarrollo de PCBs, especialmente en casos donde los errores de diseño generan retrasos significativos. La propuesta incluye una máquina CNC capaz de reducir los tiempos de fabricación de prototipado mediante herramientas accesibles de hardware y software.

**Objetivo principal**: Crear un dispositivo CNC para la fabricación de PCBs, optimizando el desarrollo mediante software libre como GRBL y componentes fácilmente disponibles.

---

## Marco teórico

### Breve contexto histórico

Las máquinas CNC tienen sus orígenes en la década de 1980, evolucionando con tecnologías más accesibles gracias a microcontroladores como el **ATmega328p** y módulos de drivers como el **DRV8825**. Actualmente, dispositivos con el GRBL permiten la implementación de sistemas CNC de bajo costo y alta precisión para aplicaciones específicas como la creación de PCBs.

### Hardware empleado

- Microcontrolador: [Arduino UNO](https://docs.arduino.cc/resources/datasheets/A000066-datasheet.pdf).
- Shield CNC: [CNC Shield 3-ejes](https://www.handsontec.com/dataspecs/cnc-3axis-shield.pdf).
- Drivers: [DRV8825](https://www.pololu.com/product/2133).
- Motores: NEMA 17.

---

## Solución propuesta

La solución consiste en diseñar una máquina CNC con las siguientes características:

- Área de fresado adaptable según los requisitos.
- Uso del software **GRBL** para procesar instrucciones en formato G-code.
- Componentes modulares y accesibles para facilitar la implementación y calibración.

**Implementación física**:

- Chasis de madera.
- Sistema de ejes con motores paso a paso NEMA 17.
- Fuente de alimentación integrada para todos los componentes.

**Diagrama de bloques**:  
![diagrama de bloques CNC](https://i.imgur.com/sm5t3Yl.png)

---

## Desarrollo del dispositivo

El desarrollo abarca:

1. Montaje estructural

El montaje estructural de la máquina CNC se realizó utilizando materiales económicos y accesibles, priorizando la estabilidad y precisión necesarias para el fresado de PCBs. Los componentes principales incluyen:

- **Base y chasis**: Construidos con MDF contrachapado, elegido por su precio y facilidad de manipulación.
- **Ejes y guías**: Barras metálicas utilizadas como ejes para los movimientos X, Y y Z, asegurando un desplazamiento suave y preciso.
- **Soportes estructurales**: Diseñados para soportar los motores y el husillo, garantizando una alineación adecuada durante el funcionamiento.

**Imagen del montaje estructural inicial**:
![Montaje estructural CNC](https://i.imgur.com/tB0gZWe.jpg)

Este diseño fue optimizado para facilitar el ensamblaje, con un enfoque en mantener los costos bajos sin comprometer la funcionalidad básica del dispositivo.

2. **Sistema eléctrico**:

   - Configuración de motores, drivers y fuentes.
   - Calibración de pasos por eje y ajustes de corriente:

- ```math
  V_{ref} = I_{Max} \times 5 \times R_s
  ```

- ```math
  I_{Max} = 1.7 \, \text{A}, \quad R_s = 0.1 \, \Omega
  ```

- ```math
  V_{ref} = 1.7 \times 5 \times 0.1 = 850 \, \text{mV}
  ```

- Para una operación al 70%:

  ```math
  V_{ref} = 0.7 \times 850 = 595 \, \text{mV}
  ```

- Pasos por revolución:

  ```math
  \frac{360}{1.8} = 200
  ```

- Avance por revolución:

  ```math
  \frac{200}{4} = 50 \, \text{pasos/mm}
  ```

- Calibración de pasos para ajustes de dimensiones:

  ```math
  \text{Pasos} = \frac{\text{dimensión requerida} \times \text{pasos por mm}}{\text{dimensión obtenida}}
  ```

- si se  desea hacer lo mismo teniendo en cuenta la division de pasos por milímetro que permiten los drivers, se divide el 1.8 en el numero de micro pasos que se configuro en el driver de cada eje en especifico, estos micro pasos se dan en  (2, 4, 8, 16, y 32) dependiendo del driver

---

## Pruebas experimentales

1. **Prueba en superficies de papel**:
   - Resultado inicial con un lapicero sobre cinta de papel.
   - ![Imgur](https://i.imgur.com/DA0Un5S.jpg)

2. **Prueba en placa de cobre**:
   - Uso de la CNC para trazar en cobre con vectorización mejorada.
   - ![Imgur](https://i.imgur.com/N8tYTGU.jpg)

3. **prueba con el motor implementado**:

   - Resultado con el motor implementado (placa de dimensiones 2.5cm 1.5cm) sin limpiar
   - ![Resultado de pcb](https://i.imgur.com/PJTkkYW.jpg)
   - https://i.imgur.com/i9RbGPb.mp4
   

---

## Conclusiones

- La implementación del proyecto demuestra que, aunque inicial, los resultados son prometedores para la fabricación de PCBs con bajos costos y buen rendimiento.
- El costo total de los materiales fue de aproximadamente **1,156,750 COP** a fecha de 2022.
- La flexibilidad del diseño permite adaptaciones para mejoras futuras.

---

## Referencias

- [Repositorio oficial de GRBL](https://github.com/grbl/grbl)
- [Especificaciones del DRV8825](https://www.pololu.com/product/2133)
- [Datasheet del Arduino UNO](https://docs.arduino.cc/resources/datasheets/A000066-datasheet.pdf)

