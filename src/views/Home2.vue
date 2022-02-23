<template>
  <div class="home">
    <h1>Home</h1>

    <input type="text" v-model="search" />
    <p>search term = {{ search }}</p>

    <div v-for="name in matchingNames" :key="name">
      {{ name }}
    </div>

    <button @click="handleClick">stop watching</button>

    <!-- ## ref vs reactive -->
    <!-- <h2>Refs</h2>

    <p>{{ ninjaOne.name }} - {{ ninjaOne.age }}</p>
    <button @click="updateNinjaOne">Update ninja one</button>

    <h2>Reactive</h2>
    <p>{{ ninjaTwo.name }} - {{ ninjaTwo.age }}</p>
    <button @click="updateNinjaTwo">Update ninja two</button> -->

    <!-- ## normal ref -->
    <!-- <p ref="p">My name is {{name}} and my age is {{age}}</p>
    <button @click="handleClick">click me</button>
    <button @click="age++">add 1 to age</button>
    <input type="text" v-model="name" /> -->
  </div>
</template>

<script>
// import { ref, reactive } from "vue";
import { computed, ref, watch, watchEffect } from "vue";
// @ is an alias to /src

export default {
  name: "Home",
  setup() {
    const search = ref("");
    const names = ref([
      "mario",
      "yoshi",
      "luigi",
      "toad",
      "bowser",
      "koopa",
      "peach",
    ]);

    const stopWatch = watch(search, (value) => {
      console.log("search changed", value);
    });

    const stopEffect = watchEffect(() => {
      console.log("search changed", search.value);
    });

    const matchingNames = computed(() => {
      return names.value.filter((name) => name.includes(search.value));
    });

    const handleClick = () => {
      stopWatch();
      stopEffect();
    };

    return { names, search, matchingNames, handleClick };

    // ## ref vs reactive
    // const ninjaOne = ref({ name: "mario", age: 30 });
    // const ninjaTwo = reactive({ name: "luigi", age: 35 });

    // const updateNinjaOne = () => {
    //   ninjaOne.value.age = 40;
    // };

    // const updateNinjaTwo = () => {
    //   ninjaTwo.age = 45;
    // };

    // return { ninjaOne, updateNinjaOne, ninjaTwo, updateNinjaTwo };

    // ## normal ref

    // const p = ref(null);

    // // let name = "mario";
    // let name = ref("mario");
    // let age = ref(30);

    // const handleClick = () => {
    //   console.log(p, p.value);
    //   p.value.classList.add("test");
    //   p.value.textContent = 'hello, ninjas';

    //   name.value = "luigi";
    //   age.value = 35;
    // };

    // return { name, age, handleClick, p };
  },
};
</script>
