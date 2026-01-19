# pg_pie 🥧 

**pg_pie** es una función de PostgreSQL que permite "dibujar" gráficos circulares y medidores de porcentaje directamente en tu terminal usando `psql`.



## 🚀 ¿Qué hace diferente a pg_pie?

A diferencia de las barras de progreso lineales, `pg_pie` utiliza coordenadas cartesianas y lógica trigonométrica para determinar qué píxel (carácter) debe pintarse, permitiendo crear visualizaciones circulares altamente personalizables.

## 🛠️ Instalación

1. Asegúrate de tener instalada la dependencia `notice_color.sql` (disponible en este repo).
2. Ejecuta el script principal:
```bash
   psql -d tu_db -f sql/pg_pie.sql

```

## 📊 Parámetros de la Función

La función `print_cube` (puedes renombrarla a `pg_render_pie`) acepta los siguientes parámetros:

| Parámetro | Tipo | Descripción |
| --- | --- | --- |
| `p_width` / `p_height` | Integer | Dimensiones del lienzo en la terminal. |
| `p_percentage` | Integer | El valor a representar (0-100). |
| `p_character_circle` | String | El carácter para el área no completada. |
| `p_character_percentage` | String | El carácter para el área completada. |
| `p_color_circle` | String | Color del fondo del círculo. |
| `p_color_percentage` | String | Color del sector del porcentaje. |

## 💡 Ejemplos de Visualización

Puedes crear diferentes estilos cambiando los caracteres y colores:

```sql
-- Estilo Smileys
SELECT print_cube(
    p_width => 35, 
    p_height => 20, 
    p_percentage => 60, 
    p_character_circle => '☻', 
    p_character_percentage => '☺'
);

```

### Animación en tiempo real

Puedes integrar esto en tus procesos de carga para ver cómo se llena el círculo conforme avanza una tarea técnica.

## 🧠 Lógica Matemática

El script calcula el ángulo de cada carácter relativo al centro usando la función `atan2()`:


Esto permite una precisión matemática en la representación del porcentaje.

