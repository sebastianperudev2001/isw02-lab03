# Laboratorio 03: Sistema de Gestión de Servicios de Limpieza

## Descripción General

La empresa **LimpioYa S.A.C.** ofrece servicios de limpieza personalizados para **hogares, oficinas y plantas industriales**. Cada tipo de servicio tiene su propia tarifa, duración estimada y condiciones especiales. Además, pueden incluir servicios adicionales como **aromatizante, desinfección o limpieza de vidrios**.

El objetivo de este laboratorio es implementar un sistema en Java que permita:

- Modelar los distintos servicios usando POO.
- Aplicar principios SOLID para mejorar la extensibilidad del sistema.
- Decorar servicios con funcionalidades adicionales usando patrones de diseño.

---

## Objetivos

1. Reforzar conceptos de **encapsulamiento, herencia y polimorfismo**.
2. Aplicar los principios **SRP** y **OCP** del paradigma SOLID.
3. Usar patrones de diseño **creacionales (Factory)** y **estructurales (Decorator)**.

---

## Lógica de negocio

### Entidad: Servicio de Limpieza

Todos los servicios comparten ciertas características comunes:

- `String direccionCliente`
- `double duracionHoras`
- `double tarifaHora`
- `boolean incluyeMateriales`
- `String nombreCliente`

### Tipos de servicios

#### ServicioHogar

- Atributos adicionales:
  - `boolean esApartamento`
- Reglas:
  - Si `esApartamento` es verdadero, se aplica un **descuento del 10%** sobre el precio base.
- Métodos:
  - `double calcularPrecioFinal()` – Aplica el descuento si corresponde.

#### ServicioOficina

- Atributos adicionales:
  - `int cantidadEmpleados`
- Reglas:
  - Se añade **0.1 horas** por cada empleado extra.
  - Al precio final se le aplica el **IGV (18%)**.
- Métodos:
  - `double calcularPrecioFinal()` – Considera el aumento de duración y aplica IGV.

#### ServicioIndustrial

- Atributos adicionales:
  - `double multiplicadorRiesgo`
- Reglas:
  - El servicio solo puede prestarse si `incluyeMateriales` es verdadero.
  - El precio base se multiplica por el `multiplicadorRiesgo`.
- Métodos:
  - `double calcularPrecioFinal()` – Lanza una excepción si no se incluyen materiales, y aplica el multiplicador de riesgo.

> Pro tip: `calcularPrecioFinal` NO DEBERÍA estar en las 3 subclases.

### Reglas adicionales

- Se pueden aplicar **descuentos** basados en:
  - Clientes frecuentes
  - Campañas promocionales
- Se pueden añadir **servicios adicionales** mediante decoración:
  - Aromatizante: suma S/ 5.00 al total
  - Desinfección: suma S/ 15.00 al total
  - Limpieza de vidrios: suma S/ 10.00 al total

---

## Preguntas de desarrollo

### Ejercicio 1 – Programación Orientada a Objetos

Implementa una jerarquía de clases usando herencia para representar los distintos tipos de servicios.

- Crea una clase abstracta `ServicioLimpieza` con atributos comunes y método abstracto `calcularPrecioFinal()`.
- Implementa las subclases `ServicioHogar`, `ServicioOficina` y `ServicioIndustrial`.
- Encapsula correctamente atributos y lógica de negocio usando getters/setters y constructores.

### Ejercicio 2 – Principios SOLID

Aplica el principio de **Responsabilidad Única** y el principio de **Abierto/Cerrado**.

- Crea una interfaz `Descuento` con el método `double aplicarDescuento(double monto)`.
- Implementa al menos dos clases que representen distintos tipos de descuentos:
  - `DescuentoClienteFrecuente`
  - `DescuentoCampania`
- El cálculo del precio final debe permitir inyectar descuentos sin modificar el código del servicio base.

### Ejercicio 3 – Patrón de diseño: Decorator

Aplica el patrón **Decorator** para añadir servicios adicionales a un servicio base.

- Crea una clase abstracta `ServicioAdicional` que implemente o extienda `ServicioLimpieza`.
- Implementa decoradores como:
  - `ConAromatizante`
  - `ConDesinfeccion`
  - `ConLimpiezaVidrios`
- El sistema debe permitir encadenar múltiples decoradores sobre un mismo servicio.

### Ejercicio 4 – Patrón de diseño: Factory

Crea una clase `ServicioFactory` que devuelva una instancia del servicio solicitado en base a un parámetro tipo `String`.

- `ServicioFactory.crearServicio("hogar", ...)`
- Este patrón debe permitir la creación flexible de instancias con sus atributos base.

---

## Entregable

El proyecto Java debe contener:

- Las clases Java correctamente estructuradas por paquetes (por ejemplo: `ServicioLimpieza`, `Descuento`, `Decorator`, `Factory`, etc.).
- Una clase `Main` que incluya ejemplos de uso separados por sección según cada ejercicio:
  - **Ejercicio 01**: Crear e imprimir el precio final de un `ServicioHogar`, `ServicioOficina` y `ServicioIndustrial`.
  - **Ejercicio 02**: Aplicar e imprimir al menos dos descuentos (`ClienteFrecuente`, `Campaña`) sobre un servicio.
  - **Ejercicio 03**: Decorar un servicio con al menos dos servicios adicionales y mostrar el precio final.
  - **Ejercicio 04**: Usar `ServicioFactory` para crear un servicio e imprimir su tipo y datos principales

---
