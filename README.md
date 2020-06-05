# Repaso de VueJS

## Instalar/Actualizar Vue
`$ npm install -g @vue/cli` (en linux puede hacer falta la palabrita mágia `sudo`)
y luego, para conocer la versión de Vue instalada:
`$ vue --version`

## Crear un proyecto nuevo
`$ vue create app-name` (reemplazar el `app-name` con el nombre que quieras para la app)
> Dato: si pensás usar git (que deberías), por defecto ya viene inicializado y commiteado.  
> Asique si además, querés subirlo a GitHub, GitLab, Bitbucket o similar, solo tenés que correr:  
> `$ git remote add origin https://...{blablabla}.git`  
> y pushearlo.  

### Durante la creación
- Seleccionar configuración manual y marcar `Router` y `Vuex`
- Marcar `Y` en `use hisroty mode?`
- Al resto enter hasta que empiece a crear el esquelero de la app.

## Ejecutar para ver que todo anda
`$ npm run serve`
compila, levanta el server y en el browser vamos a:
`http://localhost:8080/`

## Instalar Bootstrap-Vue
Ejecutar:  
`$ vue add bootstrap-vue`
- cuando pregunte `Use babel/polyfill? (Y/n)` poner `Y`
- Componentes en [este link](https://bootstrap-vue.org/docs/components)
## Rutas
Se declaran en el archivo `router/index.js`, dentro de `const routes = []` y hay dos formas de hacerlo:
1. La primera forma carga el componente al inicio de la app, asique es recomendable solo hacerlo con ciertas páginas, como el `Home`
```
{
    path: '/',
    name: 'Home',
    component: Home
}
```
2. La otra forma es la más recomendada para el común de las páginas ya que carga el HTML y el JavaScript al momento de llamar a la página
```
{
    path: '/about',
    name: 'About',
    component: () => import('../views/About.vue')
}
```
**Todas las rutas que vayamos a necesitar se declaran acá y se corresponden con un archivo de la carpeta `views`**

## Vistas y Componentes
Tienen la misma estructura y la misma extensión, pero se utilizan de distinta forma y son llamados de distinta forma
- Las vistas van en `views` y son llamadas al acceder a las distintas rutas.
- Los componentes van en `components` (wow, que sorpresa!) y son llamados por las vistas o por otros componentes.

### Estructura
Es la misma para ambos casos, son 3 partes, la del HTML, la del JavaScript y la de CSS
```
<template>
  Acá van las etiquetas HTML, componentes, etc. (lo que se va a ver)
</template>

<script>
  Acá va el código en JS, llamadas a componentes, etc.
</script>

<style>
  Los estilos en CSS (o LESS o lo que sea)
</style>
```
`template` vendría a ser la única obligatoria (_creo_), las otras 2 son opcionales.

#### Tag `template`
Dentro del tag debe haber una sola etiqueta (por ejemplo un `div`), y dentro de esta armar la vista del componente.
Por ejemplo, el `template` de `App.vue` podría ser:
```
<template>
  <div id="app">
    <navigation-bar />
    <div class="container">
      <router-view />
    </div>
  </div>
</template>
```
Todo está dentro de un `div`, el cual contiene un componente llamado `navigation-bar` (para que aparezca en todas las vistas) y dentro de un `div` con clase `container` (de bootstrap, para darle un mejor estilo) se van a cargar todas las `views`.

**Para usar componentes hay que importarlos dentro del tag `script`**

#### Tag `script`
Dentro de este tag se importan los componentes, se coloca la lógica de comportamiento de la vista/componente actual, métodos, datos, lifecycle functions, etc.  
Un simple ejemplo de este tag para el caso del template anterior (para `App.vue`) sería:
```
<script>
import Navigation from "@/components/bootstrap/Navigation.vue";
export default {
  components: {
    "navigation-bar": Navigation,
  },
};
</script>
```
Primero importo el componente `Navigation` que está dentro de `components/bootstrap` (cree esa carpera bootstrap para ordenar los componentes que creo a partir de los que provee bootstrap).  
Después lo defino para usarlo en el `template` con el tag `navigation-bar`, y recién ahí funcionaría el tag del ejemplo de template anterior

#### Tag `style`
Muy obvio, acá se definen las clases CSS (o lenguaje de estilo elegido)
Ejemplo:
```
<style>
h1 {
  color:red;
}
</style>
```
Esto haría que el texto de las etiquetas h1 sea rojo (horrible :p).  

# A los bifes.. el TP del profesor
## Listado de los platos en el `Home`
Las imágenes están en la carpeta `public/data/images` y el JSON en `public/data/json`
Empezando por el tag `script`, tendría una estructura básica como la siguiente:
```
<script>
//acá van los imports (de los componentes)
//import MyComponent from "@/path/to/MyComponent.vue"

export default {
  name: "Home",
  //De esta propiedad solo encontré que es obligatoria para componentes recursivos (?)
  //La borré y andaba todo igual, pero al final la dejé :p

  components: {
    //Acá definimos los tags para utilizar los componentes importados
    //"my-component": MyComponent  
  },

  mounted(){
    //Este es como el constructor, acá llamamos a los métodos definidos
    //más abajo que necesitamos que se ejecutan cuando se llama al componente
    //this.getData()
  },

  data() {
    return {
      //Entiendo que acá se definen variables, como en este caso, un array vacío
      //platosData: [],
    }
  },

  methods: {
    //acá se definen los métodos que pueden ser llamados en cualquier momento
    /*
    async getPlatos() {
      const res = await fetch("data/json/platos.json");
      const resJson = await res.json();
      console.log(resJson);
      this.platosData = resJson.platos;
    }
    */
  }
};
</script>
```
Como todavía no creo ningun componente para mostrar cada plato, los voy a listar para probar que funciona la lectura del JSON.  
 - Voy a tener un método `getData()` para obtener los datos del JSON que se va a llamar al inicio, por lo tanto lo llamo desde el método `mounted()`
```
mounted(){
  this.getData()
}
```
- Ese método va a tomar los datos del JSON y los va a settear en un array vacío
```
data() {
    return {
      platosData: [],
    }
}
```
- Finalmente, dentro de `methods` defino el método `getData()`:
```
methods: {
  async getData() {
    const res = await fetch("data/json/platos.json");
    const resJson = await res.json();
    console.log(resJson);
    this.platosData = resJson.platos;//tiene que ser .platos por la estructura del JSON
  }
}
```
