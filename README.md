<div align="center" style="display: flex; justify-content: center; gap: 20px;">
  <a href="https://vuejs.org/" target="_blank">
    <img src="./src/assets/vue.svg" width="120" alt="Vue Logo" />
  </a>

  <a href="https://tailwindcss.com/" target="_blank">
    <img src="https://upload.wikimedia.org/wikipedia/commons/d/d5/Tailwind_CSS_Logo.svg" width="120" alt="Tailwind CSS Logo" />
  </a>

  <a href="https://vitejs.dev/" target="_blank">
    <img src="./public/vite.svg" width="120" alt="Vite Logo" />
  </a>
</div>

## Descripción

Este es un proyecto frontend para crear una interfaz gráfica para **Ollama** en un entorno local, utilizando **Vue 3**, **TypeScript**, **Tailwind CSS** y **Vite**. El objetivo es proporcionar una forma sencilla y eficiente de interactuar con Ollama a través de una interfaz moderna y bien diseñada.

## Comandos para Ejecutar el Proyecto

### Instalación de Dependencias
Primero, asegúrate de instalar todas las dependencias del proyecto:

```bash
$ npm install
```
## Ejecutar el Proyecto

Para iniciar el servidor de desarrollo y ver tu proyecto en el navegador, ejecuta:

```bash
# Modo desarrollo
$ npm run dev
```

Esto iniciará Vite, y podrás ver la interfaz en http://localhost:5173/ o la URL que se indique en la terminal.

### Comando para Procesar los Estilos con Tailwind CSS
Para compilar los estilos de Tailwind y generar un archivo CSS optimizado, utiliza el siguiente comando:

```bash
# Compilar los estilos de Tailwind
$ npx tailwindcss -i ./src/assets/styles/tailwind.css -o ./src/style.css --watch
```

Este comando hace lo siguiente:

- ``-i ./src/assets/styles/tailwind.css``: Especifica el archivo de entrada donde se encuentran las directivas de Tailwind.

- ``-o ./src/style.css``: Especifica el archivo de salida donde se generará el CSS procesado.
- ``--watch``: Activa el modo de observación, lo que significa que Tailwind actualizará automáticamente el archivo de salida cada vez que detecte cambios en los archivos relacionados (por ejemplo, tailwind.css o tus archivos de Vue).

Esto te permitirá desarrollar con las clases de utilidad de Tailwind sin necesidad de ejecutar el comando manualmente cada vez que realices cambios.

## Licencia

Este proyecto está bajo la licencia [MIT](https://github.com/nestjs/nest/blob/master/LICENSE).