<template>
  <div class="container col-6">
    <header class="row my-5">
      <h1>MemoFruits</h1>

      <input type="text" v-model="newCard" />
      <p>{{ newCard }}</p>
      <button @click="addCards">Ajouter</button>

      <p>new card :{{ newCardsData }}</p>
      <h2 class="col-12">
        score : {{ score }} <br />
        {{ textAlert }}
      </h2>
    </header>
    <div class="row gap-2">
      <div
        id="board"
        v-for="(card, index) in deck"
        :key="index"
        class="col-3 mx-auto"
      >
        <button
          :class="card.show ? 'show' : ''"
          @click="flipCard(index, card.cardData)"
        >
          <p>{{ card.cardData }}</p>
        </button>
      </div>
    </div>
  </div>
  <button @click="shuffle">Mélanger</button>
</template>

<script>
import form from "./form.vue";
export default {
  components: { form },
  name: "MemoryGame",
  data() {
    return {
      deck: [
        { cardData: "🍌", show: false },
        { cardData: "🍌", show: false },
        { cardData: "🥝", show: false },
        { cardData: "🥝", show: false },
        { cardData: "🍎", show: false },
        { cardData: "🍎", show: false },
      ],
      currentCardData: null,
      firstId: null,
      newCard: "",
      newCardId: 7,
      score: 0,
      maxScore: 3,
      textAlert: "",
    };
  },
  methods: {
    addCards() {
      this.deck.push({ cardData: "" + this.newCard, show: false });
      this.deck.push({ cardData: "" + this.newCard, show: false });
      this.newCard = "";
      this.shuffle(this.deck);
    },
    flipCard(id, cardData) {
      this.deck[id].show = true;

      if (this.currentCardData === null) {
        this.currentCardData = cardData;
        this.firstId = id;
      } else if (cardData === this.currentCardData) {
        this.score++;
        this.textAlert = "GOOD !";

        this.currentCardData = null;
        if (this.score === this.maxScore) {
          setTimeout(() => {
            alert("You won !");
          }, 300);
        }
      } else {
        this.textAlert = "Try Again ! !";
        setTimeout(() => {
          this.deck[this.firstId].show = false;
          this.deck[id].show = false;
        }, 1000);
        this.currentCardData = null;
      }
    },
    shuffle() {
      this.deck.sort(() => Math.random() - 0.5);
      console.log(this.deck);
    },
  },
};
</script>

<style scoped>
#board button {
  overflow: hidden;
  min-width: 200px;
  aspect-ratio: 1/1;
  background-color: rgb(195, 215, 255);
  border-radius: 15px;
  border: 10px solid rgb(17, 100, 182);
}
#board .show {
  background-color: rgb(255, 255, 255);
}

#board button {
  width: max-content;
  max-width: 10%;
  margin: auto;
}

h1 {
  font-weight: bold;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-size: 4em;
}

h2 {
  margin: auto;
  width: max-content;
  border: 2px solid red;
  border-radius: 15px;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}

button p {
  margin-top: 200px;
  font-size: 3em;
  font-weight: bold;
  opacity: 0;
  transition: 0.3s;
}
.show p {
  margin-top: 10px;
  opacity: 1;
}
</style>
