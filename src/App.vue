<template>
  <MemoryGame />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import MemoryGame from "./components/deck.vue";
import Form from "./components/form.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    MemoryGame,
    Form,
  },
};
</script>
