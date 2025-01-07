# Administrador de Gastos con Vite y Vue.js

Este proyecto es una aplicación web de **gestión de gastos** desarrollada con **Vue 3** y **Vite**. Es el tercer proyecto del curso de [Código con Juan](https://codigoconjuan.com) impartido por **Juan de la Torre**. Puedes acceder a la demo funcional del proyecto en el sitio https://duridev-administrador-gastos-vue3.netlify.app/

## 🚀 Características principales

- **Gestor de Presupuesto**:
  - Permite definir un presupuesto inicial.
  - Actualiza dinámicamente los gastos realizados y el dinero disponible.

- **Gestión de Gastos**:
  - Agrega, edita y elimina gastos.
  - Los gastos se guardan localmente en el navegador para persistencia.

- **Filtrado de Gastos**:
  - Filtra gastos por categoría para un mejor control.

- **Interfaz Amigable**:
  - Diseño limpio y responsivo.

- **Persistencia con Local Storage**:
  - Guarda tanto el presupuesto como los gastos registrados.

## 🔧 Tecnologías Utilizadas

- **Vue 3**: Framework de JavaScript moderno y reactivo.
- **Vite**: Herramienta de desarrollo rápida para aplicaciones Vue.js.
- **CSS**: Estilizado del proyecto.
- **Local Storage**: Para guardar datos localmente en el navegador.

## 📝 Instalación y Configuración

Sigue los pasos a continuación para ejecutar el proyecto localmente:

1. **Clona el repositorio**

```bash
https://github.com/Duridev/admin-gastos-vue.git
```

2. **Instala las dependencias**

```bash
npm install
```

3. **Inicia el servidor de desarrollo**

```bash
npm run dev
```

4. **Abre el proyecto en tu navegador**

```
http://localhost:5173
```

## 🔍 Estructura del Proyecto

El archivo principal **App.vue** maneja la lógica principal de la aplicación. Contiene:

- **Gestor de Presupuesto:** Componente para definir y mostrar el presupuesto.
- **Modal:** Ventana emergente para agregar o editar gastos.
- **Listado de Gastos:** Visualización de los gastos registrados y opción para eliminarlos.

Los principales componentes:

- `Presupuesto.vue`
- `ControlPresupuesto.vue`
- `Gastos.vue`
- `Modal.vue`
- `Filtros.vue`

Además, incluye un archivo `helpers.js` para funciones auxiliares como la generación de IDs.

## 📊 Demostración

Puedes ver el proyecto funcionando en https://duridev-administrador-gastos-vue3.netlify.app/



## 📚 Autor

Desarrollado por [Duridev](https://github.com/duridev). Este proyecto es parte del curso **Código con Juan** de **Juan de la Torre**.


## 🛠️ Licencia

Este proyecto está licenciado bajo la [MIT License](https://opensource.org/licenses/MIT).


