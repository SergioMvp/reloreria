
<template>

   <h1 class="title">Slider 3D con puro CSS</h1>

<div class="container__slider">

    <div class="container">
        <input type="radio" name="slider" id="item-1" checked>
        <input type="radio" name="slider" id="item-2">
        <input type="radio" name="slider" id="item-3">

        <div class="cards">
            <label class="card" for="item-1" id="selector-1">
                <img src="./assets/Speedmaster.jpg">
            </label>
            <label class="card" for="item-2" id="selector-2">
                <img src="./assets/Omega.jpg">
            </label>
            <label class="card" for="item-3" id="selector-3">
                <img src="./assets/Sitiopriv.jpg">
            </label>
            

        </div>
    </div>

</div>
<br>
<br>
<br>
<br>
<br>
<br>

  
<header>


 
  <div class="carrito" id="carrito">
    <div class="header-carrito">
                <h2>Tu Carrito</h2>
            </div>
      

          <button class="bookmarkBtn" @click="abrirModal ">
           <span class="IconContainer"> 
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"> <g> <path fill="none" d="M0 0h24v24H0z"/> <path d="M7 8V6a5 5 0 1 1 10 0v2h3a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V9a1 1 0 0 1 1-1h3zm0 2H5v10h14V10h-2v2h-2v-2H9v2H7v-2zm2-2h6V6a3 3 0 0 0-6 0v2z"/> </g> </svg></span>
            <p class="text">{{ carrito.length }}  </p>
          </button>
          
        <div class="modal" v-if="mostrarTabla">
          <div class="carrito-item">
            <h3 class="agregado">Agregados</h3>
            <div class="table-container">
              <table>
                <thead>
                  <tr>
                    <th>Imagen</th>
                    <th>Nombre</th>
                    <th>Precio</th>
                    <th>Cantidad</th>
                    <th>Sub total</th>
                    <th>Eliminasr</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(item, index) in carrito" :key="index">
                    <td><img :src="item.img" class="modal-img" width="80px" alt="Producto"></td>
                    <td>{{ item.nombre }}</td>
                    <td>{{ formatoMoneda(item.precio) }}</td> 
                    <td class="ctn">
                      <button @click="menos(item)">➖</button>
                      {{ item.cantidad }}
                      <button @click="mas(item)">➕</button>
                    </td>
                    <td>{{ calcularSubtotal(item) }}</td>
                    <td>
                      <button class="btn5" @click="eliminarProducto(index)">❌</button>
                    </td>
                  </tr>
                  <div class="">
                  <tr>
                    <td colspan="2">Total:</td>
                    <td>{{ calcularTotal() }}COP</td>
                  </tr>
                  <button class="btn4" @click="cerrarModal">Cerrar</button>
              <button class="btn4" @click="limpiarModal">Limpiar</button>
                </div>
                </tbody>
              </table>
              <!-- <button class="btn-pagar" @click="cerrarModal">Cerrar</button>
              <button class="btn-pagar" @click="limpiarModal">Limpiar</button> -->
            </div>
          </div>
        </div>
      </div>

  </header>
    
      <!-- <section class="contenedor">
        <div v-for="(tarjetas, i) in filtroTarjeta" :key="i" class="contenedor_items">
        
          <div class="item">
              <span class="titulo_item">{{ tarjetas.nombre }}</span>
              <img class="img_item" :src="tarjetas.img" alt="">
              <h1 class="precio_item">precio: {{ tarjetas.Modelo }}</h1>
              <h1 class="info">cantidad: {{ tarjetas.cantidad }}</h1>
              <div class="icon">
            
              </div>
               <div class="carrito2">
                 <h1 class="info">{{ formatoMoneda(tarjetas.precio) }}</h1>
                   <br>
                 <button class="Btn"  @click="agregarCarrito(tarjetas)">Pay
                    <svg class="svgIcon" viewBox="0 0 576 512"><path d="M512 80c8.8 0 16 7.2 16 16v32H48V96c0-8.8 7.2-16 16-16H512zm16 144V416c0 8.8-7.2 16-16 16H64c-8.8 0-16-7.2-16-16V224H528zM64 32C28.7 32 0 60.7 0 96V416c0 35.3 28.7 64 64 64H512c35.3 0 64-28.7 64-64V96c0-35.3-28.7-64-64-64H64zm56 304c-13.3 0-24 10.7-24 24s10.7 24 24 24h48c13.3 0 24-10.7 24-24s-10.7-24-24-24H120zm128 0c-13.3 0-24 10.7-24 24s10.7 24 24 24H360c13.3 0 24-10.7 24-24s-10.7-24-24-24H248z"></path></svg>
                 </button>
               </div>
          </div>
        </div>
    
   
      </section> -->

      <section class="contenedor">
  <div class="contenedor_items">
    <div v-for="(tarjetas, i) in filtroTarjeta" :key="i" class="item">
      <span class="titulo_item">{{ tarjetas.nombre }}</span>
      <img class="img_item" :src="tarjetas.img" alt="">
      <h1 class="precio_item"></h1>
      <div class="carrito2">
        <h1 class="info">{{ formatoMoneda(tarjetas.precio) }}</h1>
        <button class="Btn" @click="agregarCarrito(tarjetas)">BUY
          <svg class="svgIcon" viewBox="0 0 576 512"><path d="M512 80c8.8 0 16 7.2 16 16v32H48V96c0-8.8 7.2-16 16-16H512zm16 144V416c0 8.8-7.2 16-16 16H64c-8.8 0-16-7.2-16-16V224H528zM64 32C28.7 32 0 60.7 0 96V416c0 35.3 28.7 64 64 64H512c35.3 0 64-28.7 64-64V96c0-35.3-28.7-64-64-64H64zm56 304c-13.3 0-24 10.7-24 24s10.7 24 24 24h48c13.3 0 24-10.7 24-24s-10.7-24-24-24H120zm128 0c-13.3 0-24 10.7-24 24s10.7 24 24 24H360c13.3 0 24-10.7 24-24s-10.7-24-24-24H248z"></path>
            <!-- ... (código del icono) ... -->
          </svg>
        </button>
      </div>
    </div>
  </div>
</section>

</template>



<script setup>
  
// import g2d from "./assets/"
import { ref, computed } from "vue";
const tarjeta = ref([
  { nombre: "Rolex Submariner",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/14/68/12/63/14681263_23919085_1000.jpg" },

   { nombre: "ROLEX GMT MASTER II 50 YEAR",
   precio: "200000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/16/10/55/06/16105506_37053911_1000.jpg" },

   { nombre: "ROLEX GMT MASTER II",
   precio: "800000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/21/00/16/96/21001696_50991315_1000.jpg" },

   { nombre: "ROLEX DAYTONA",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/20/07/32/12/20073212_45253278_1000.jpg" },

   { nombre: "VERSACE SPORT TECH",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/17/45/90/82/17459082_42151980_1000.jpg" },

   { nombre: "VERSACE ICON ACTIVE",
   precio: "400000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/19/02/89/00/19028900_43460559_1000.jpg" },

   { nombre: "VERSACE GRECA GLAM",
   precio: "700000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/20/24/49/86/20244986_50287979_1000.jpg" },

   { nombre: "VERSACE DV ONE",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/20/31/87/16/20318716_50530757_1000.jpg" },

   { nombre: "GUCCI-TIMELESS WATCH",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/13/31/79/82/13317982_14922630_1000.jpg" },

   { nombre: "GUCCI DIVE",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/13/76/24/48/13762448_16859936_1000.jpg" },

   { nombre: "GUCCI 25H",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/17/44/31/67/17443167_36150784_1000.jpg" },

   { nombre: "GUCCI DIVE",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/18/82/55/22/18825522_41690261_1000.jpg" },

   { nombre: "PHPL HIGH-CONIC",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/19/43/52/44/19435244_43568353_1000.jpg" },

   { nombre: "PP HIGH-CONIC II",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/17/72/42/64/17724264_41109705_1000.jpg" },

   { nombre: "PHPL HIGH-CONIC",
   precio: "100000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/19/43/52/40/19435240_43569502_1000.jpg" },

   { nombre: "PHPL HIGH-CONIC",
   precio: "10000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/19/43/52/41/19435241_50322817_1000.jpg" },

   { nombre: "FERRAGAMO SALVATORE",
   precio: "300000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/17/45/77/71/17457771_41416158_1000.jpg" },

   { nombre: "FERRIER FERRAGAMO",
   precio: "19000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/17/45/85/59/17458559_39653370_1000.jpg" },

   { nombre: "FERRAGAMO F-80 TITANIUM",
   precio: "10000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/19/03/57/11/19035711_43463700_1000.jpg" },

   { nombre: "FERRAGAMO 1927",
   precio: "30000000", 
   cantidad: "1",  
   img:"https://cdn-images.farfetch-contents.com/19/03/57/10/19035710_43448920_1000.jpg" },
   

  
]);
const carrito = ref([]);
const mostrarTabla = ref(false);
const terminoBusqueda = ref('');

const filtroTarjeta = computed(() => {
  return terminoBusqueda.value === ''
    ? tarjeta.value
    : tarjeta.value.filter(item => item.nombre.toLowerCase().includes(terminoBusqueda.value.toLowerCase()));
});

const agregarCarrito = (item) => {
  carrito.value.push(item);
  item.agregado = true;
};

const eliminarProducto = (index) => {
  const removedItem = carrito.value.splice(index, 1)[0];
  removedItem.agregado = false;

  const tarjetaIndex = tarjeta.value.findIndex(item => item.nombre === removedItem.nombre);
  if (tarjetaIndex !== -1) {
    tarjeta.value[tarjetaIndex].cantidad = "1";
  }
};



const limpiarModal = () => {
  carrito.value.forEach(item => {
    item.agregado = false;
    item.cantidad = 1;
  });
  carrito.value = [];
  /* cerrarModal() */
};

const abrirModal = () => {
  mostrarTabla.value = true;
};

const cerrarModal = () => {
  mostrarTabla.value = false;
};

const mas = (item) => {
  item.cantidad++;
};

const menos = (item) => {
  if (item.cantidad > 0) {
    item.cantidad--;
  }
};

const calcularSubtotal = (item) => {
  return formatoMoneda(parseFloat(item.precio) * item.cantidad);
};

const calcularTotal = () => {
  let total = 0;
  for (const item of carrito.value) {
    total += parseFloat(item.precio) * item.cantidad;
  }
  return formatoMoneda(total);
};

const formatoMoneda = (item2) => {
  const formatter = new Intl.NumberFormat("es-CO", {
    style: "currency",
    currency: "COP",
    minimumFractionDigits: 0,
  });
  return formatter.format(item2);
};





</script>
