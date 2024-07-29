<script setup>
  const name = "Pablo";
  const micolor = "color:blue";
  const arrayColores = ["blue", "red", "green", "white"];
  const activo = true;
  const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];
  const arrayFrutas2 = [
    {
      id: 1,
      name: "Manzana",
      price: "$1.00",
      description: "Una manzana",
      stock: 0,
    },
    
    {
      id: 2,
      name: "Pera",
      price: "$2.00",
      description: "Una pera",
      stock: 10,
    },
    {
      id: 3,
      name: "Naranja",
      price: "$3.00",
      description: "Una naranja",
      stock: 20
    },
  ];
  const objetoFrutas = [
    {
      id: 1,
      name: "Manzana",
      price: "$1.00",
      description: "Una manzana"
    }
  ];
  //metodos - methods
  const handleClick = () => {
    console.log("me diste click");
  };
  //metodos - methods

  const handleClick2 = () => {
    alert("me diste click");
  };
  const handleClick3 = (mensaje) => {
    console.log(mensaje);
  };
  //*********************Reactividad */
  import { ref, computed } from "vue";
  const counter = ref(0);
  const increment = () => {
    console.log('aumentar contador');
    alert('Aumentar contador');
    counter.value++;
  };
  const decrement = () => {
    console.log('aumentar contador');
    alert('Disminuir contador');
    counter.value--;
  };
  const reset = () => {
    console.log('aumentar contador');
    alert('Reset contador');
    counter.value = 0;
  };
  const add = () => {
    arrayFavoritos.value.push(counter.value);
  }
  //**************************************** */
  // funciones computadas
  const classCounter = computed(() => {
    if (counter.value === 0) {
      return 'zero';
    }

    if (counter.value > 0) {
      return 'positivo';
    }

    if (counter.value < 0) {
      return 'negativo';
    }
  });

  //**************************************** */
  // Práctica final */

  const arrayFavoritos = ref([]);
  const bloquearBtn = computed(() => {
    const numSearch = arrayFavoritos.value.find(num => num === counter.value);
    if (numSearch === 0) return true;
    return numSearch ? true : false;
  })
</script>

<template>
  <div class="container">
    <h1 class="text-center">
      Hola {{ name.toUpperCase() }}
    </h1>
    <br>
    <h2 class="text-center">
      {{ arrayColores }}
    </h2>

    <h2 v-bind:style="micolor">
      Soy azul
    </h2>

    <h3 :style="`color: ${arrayColores[1]}`">
      Colores con array
    </h3>

    <h3>
      {{ activo ? 'estoy activo' : 'Estoy inactivo' }}

    </h3>
    <p v-if:="activo">Estoy activo</p>
    <p v-else>Estoy inactivo</p>


    <h3 v-show="activo">Estoy indeciso v-show</h3>
    <br>
    <p>Recorriendo un array con v-for</p>
    <ul>
      <li v-for="color in arrayColores"> {{color}}
      </li>
    </ul>
    <ul>
      <li v-for="(fruta,index) in arrayFrutas">
        :key="index"
        {{index}} - {{fruta}}
      </li>
    </ul>

    <br>
    <h3>Array de objetos</h3>
    <ul>
      <li v-for="fruta2 in arrayFrutas2" :key="fruta2.id">
        {{ fruta2.name}} - {{ fruta2.price }} - {{ fruta2.description }}

      </li>
    </ul>
    <br>
    <h3>Objeto fruta</h3>
    {{ objetoFrutas }}
    <ul>
      <li v-for="(value,propiedad,index) in objetoFrutas" :key="id">
        {{ index }}- {{ propiedad }}: {{ value }}

      </li>
    </ul>
    <br>
    <h3>Recorrido array con v-if</h3>
    <ul>
      <li v-for="item in arrayFrutas2" key="item.name">
        <span v-if="item.stock > 0">
          {{ item.name }} - {{ item.price }}
        </span>


      </li>
    </ul>
    <br>
    <h3>
      Mejor solucion:
    </h3>
    <ul>
      <template v-for="fruta in arrayFrutas2" :key="fruta.name">
        <li v-if="fruta.stock > 0">
          {{ fruta.name }} - {{ fruta.price }}
        </li>
      </template>
    </ul>
    <br>
    <h3> ********************************************</h3>
    <h3>Eventos</h3>

    <button v-on:click="handleClick">Activame</button>
    <button @:click="handleClick">Activame2</button>
    <button @:click="handleClick3('mensaje 1 eventos')">Activame2</button>
    <button v-on:click="handleClick2">Activame</button>
    <br>
    <h3>Modificadores</h3>
    <button v-on:click.right.prevent="handleClick3('texto right')">Activame right</button>
    <button v-on:click.middle="handleClick3 ('Texto middle')">Activame middle</button>
    <button v-on:click.left="handleClick3 ('texto left')">Activame left</button>
    <br>
    <h3>**********************************************</h3>
    <h3>Reactividad</h3>
    <h2 :class="counter >0 ? 'positivo' : 'negativo'">{{ counter }}</h2>

    <button @click="decrement">Disminuir</button>
    <button @click="reset">Reset</button>
    <button @click="increment">Aumentar</button>

    <h3>**********************************************</h3>
    <h3>Computadas</h3>
    <h2 :class="classCounter">{{ counter }}</h2>
    <button @click="decrement">Disminuir</button>
    <button @click="reset">Reset</button>
    <button @click="increment">Aumentar</button>

    <br><br>

    <h3>**********************************************</h3>
    <h3>Práctica final</h3>
    <div class="container text-center">
      <h2 :class="classCounter">{{ counter }}</h2>
      <div class="btn-group">
        <button @click="decrement" class="btn btn-danger">Disminuir</button>
        <button @click="reset" class="btn btn-secondary">Reset</button>
        <button @click="increment" class="btn btn-success">Aumentar</button>
        <button @click="add" :disabled="bloquearBtn" class="btn btn-primary">Añadir</button>
      </div>

      <br>
      {{ arrayFavoritos }}

      <ul>
        <li v-for="(num,index) in arrayFavoritos" :key="index">
          {{ num }}
        </li>
      </ul>
    </div>
  </div>

</template>

<style>
  h1 {
    color: brown;
  }

  .positivo {
    color: green;
  }

  .negativo {
    color: red;
  }

  .zero {
    color: black;
  }
</style>