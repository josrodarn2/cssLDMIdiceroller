# 🎲 Dice Roller - Generador de Dados Aleatorios

Un generador de números aleatorios interactivo con una interfaz moderna y visualmente atractiva. Perfecto para juegos de rol, juegos de mesa, o cualquier situación que requiera lanzamientos de dados aleatorios.

## ✨ Características

### 🎯 Funcionalidades Principales

- **Lanzamiento de Dados Personalizado**: Introduce cualquier fórmula de dados en formato estándar (XdY+Z)
- **Dados Estándar**: Soporta todos los dados comunes de juegos de rol:
  - d4 (4 caras)
  - d6 (6 caras)
  - d8 (8 caras)
  - d10 (10 caras)
  - d12 (12 caras)
  - d20 (20 caras)
- **Dados Personalizados**: Cualquier dado desde d2 hasta d1000
- **Modificadores**: Suma o resta valores al resultado total
- **Múltiples Dados**: Lanza varios dados del mismo tipo a la vez
- **Lanzamiento de Moneda**: Función especial para cara o cruz
- **Historial de Lanzamientos**: Todos los resultados se guardan en pantalla
- **Botones Rápidos**: Acceso directo a los dados más utilizados

### 🎨 Diseño y UX

- **Interfaz Moderna**: Diseño retro-futurista con gradientes vibrantes
- **Animaciones Fluidas**: Efectos visuales en botones y resultados de dados
- **Responsive**: Optimizado para desktop, tablet y móvil
- **Feedback Visual**: Cada dado se muestra individualmente con animación
- **Validación de Entrada**: Mensajes de error claros y útiles

## 🚀 Uso

### Formato de Comandos

La sintaxis para lanzar dados sigue el formato estándar de juegos de rol:

```
XdY+Z
```

Donde:
- **X** = Número de dados a lanzar (1-100)
- **Y** = Número de caras del dado (2-1000)
- **Z** = Modificador opcional (puede ser positivo o negativo)

### Ejemplos de Uso

| Comando | Descripción |
|---------|-------------|
| `1d6` | Lanza un dado de 6 caras |
| `2d10` | Lanza dos dados de 10 caras |
| `3d8+5` | Lanza tres dados de 8 caras y suma 5 |
| `4d6-2` | Lanza cuatro dados de 6 caras y resta 2 |
| `1d20+3` | Lanza un d20 con +3 de bonificación |
| `2d4` | Lanza dos dados de 4 caras |

### Métodos de Lanzamiento

1. **Campo de Texto**: Escribe la fórmula y presiona "LANZAR" o Enter
2. **Botones Rápidos**: Click en cualquier dado predefinido (d4, d6, d8, d10, d12, d20, 2d6)
3. **Lanzamiento de Moneda**: Botón especial "MONEDA" para cara o cruz

## 📊 Visualización de Resultados

Cada lanzamiento muestra:
- ✅ La fórmula utilizada
- ✅ Cada dado individual con su resultado
- ✅ La suma de los dados (antes del modificador)
- ✅ El modificador aplicado (si existe)
- ✅ El resultado total final

## 🛠️ Tecnologías Utilizadas

- **HTML5**: Estructura semántica
- **CSS3**: 
  - Flexbox y Grid para layouts
  - Gradientes y efectos visuales
  - Animaciones CSS
  - Media queries para responsive design
- **JavaScript Vanilla**: 
  - Generación de números aleatorios
  - Validación de fórmulas con RegEx
  - Manipulación del DOM
  - Gestión de eventos

## 📱 Compatibilidad

### Navegadores Soportados
- ✅ Chrome/Edge (último)
- ✅ Firefox (último)
- ✅ Safari (último)
- ✅ Opera (último)

### Dispositivos
- ✅ Desktop (1920px+)
- ✅ Laptop (1366px+)
- ✅ Tablet (768px+)
- ✅ Móvil (320px+)

## 🎮 Casos de Uso

### Juegos de Rol (RPG)
- Dungeons & Dragons
- Pathfinder
- Call of Cthulhu
- Cualquier sistema que use dados poliédricos

### Juegos de Mesa
- Dados rápidos para cualquier juego
- Resolución de conflictos
- Decisiones aleatorias

### Educación
- Probabilidad y estadística
- Aprendizaje de matemáticas
- Experimentos aleatorios

### General
- Toma de decisiones
- Sorteos
- Generación de números aleatorios

## 📝 Características Técnicas

### Validación
- Rango de dados: 1-100 dados por lanzamiento
- Rango de caras: 2-1000 caras por dado
- Detección de formato inválido
- Mensajes de error descriptivos

### Rendimiento
- Sin dependencias externas
- Carga instantánea
- Animaciones optimizadas con CSS
- Código JavaScript eficiente

### Accesibilidad
- Navegación por teclado (Enter para lanzar)
- Contraste de colores adecuado
- Texto legible en todos los tamaños
- Estructura semántica HTML

## 🔧 Instalación

No requiere instalación. Simplemente:

1. Descarga el archivo `dice-roller.html`
2. Ábrelo en cualquier navegador web moderno
3. ¡Empieza a lanzar dados!

## 💡 Tipografías

- **Bebas Neue**: Títulos y botones (estilo display)
- **Courier Prime**: Texto y números (estilo monoespaciado)

Ambas fuentes se cargan desde Google Fonts.

## 🎨 Paleta de Colores

```css
--primary: #FF6B35   /* Naranja vibrante */
--secondary: #004E89 /* Azul oscuro */
--accent: #F7B801    /* Amarillo dorado */
--dark: #1A1423      /* Fondo oscuro */
--light: #F4F4F9     /* Texto claro */
--success: #06D6A0   /* Verde éxito */
```

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Siéntete libre de usar, modificar y distribuir.

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Si tienes ideas para mejorar el proyecto:

1. Fork el proyecto
2. Crea una rama para tu función
3. Commit tus cambios
4. Push a la rama
5. Abre un Pull Request

## 📞 Soporte

Si encuentras algún bug o tienes sugerencias, por favor abre un issue en el repositorio.

---

**Desarrollado con ❤️ para la comunidad de jugadores y entusiastas de los dados**

🎲 ¡Que tengas buenos lanzamientos! 🎲
