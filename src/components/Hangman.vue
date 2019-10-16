<template>
  <div class="container">
    <h1 class="title">Jeu du pendu</h1>
    <h3 class="subtitle result"></h3>
    <div class="columns is-mobile is-centered">
      <div class="column" v-for="(letter, index) in randomWordArray" v-bind:key="index"></div>
    </div>
    <div class="buttons is-centered">
      <button v-for="(letter, index) in letters" v-bind:key="index"
         v-on:click="check(letter, index)" class="button letter">{{ letter }}</button>
    </div>
    <div>
      <h2 class="subtitle">Il vous reste {{ lives }} essais.</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Hangman',
  data() {
    return {
      words: [
        'Patate',
        'Escargot',
        'Sauce',
        'Illustration',
        'Xylophone',
        'Orange',
        'Meringue',
        'Art',
        'Ville',
      ],
      randomWord: null,
      randomWordArray: [],
      letters: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'],
      lives: 3,
    };
  },
  created() {
    // get a random word from the word array defined above
    this.randomWord = this.words[Math.floor(Math.random() * this.words.length)];
    this.randomWordArray = this.randomWord.toLowerCase().split('');
  },
  methods: {
    // checks if the letter clicked is in the hidden word or not and places it in the spaces if so
    check(letter, index) {
      const btnClicked = document.querySelectorAll('.letter')[index];
      btnClicked.disabled = true;
      if (this.randomWordArray.includes(letter.toLowerCase())) {
        btnClicked.style.background = 'green';
        for (let i = 0; i < this.randomWordArray.length; i += 1) {
          if (this.randomWordArray[i] === letter.toLowerCase()) {
            document.querySelectorAll('.column')[i].innerHTML = letter;
          }
        }
      } else {
        btnClicked.style.background = 'red';
        this.lives -= 1;
      }
      this.verifyState();
    },
    // checks if the user ran out of lives or if the hidden word was found
    verifyState() {
      if (this.lives === 0) {
        this.disableButtons();
        document.querySelector('.result').innerHTML = `Vous avez perdu... Le mot était ${this.randomWord.toLowerCase()}.`;
      } else if (!Array.from(document.querySelectorAll('.column')).some(space => space.innerHTML === '')) {
        this.disableButtons();
        document.querySelector('.result').innerHTML = 'Bravo! Vous avez gagné.';
      }
    },
    // disables every button (used when the user wins or loses)
    disableButtons() {
      document.querySelectorAll('.letter').forEach((button) => {
        button.disabled = true; // eslint-disable-line no-param-reassign
      });
    },
  },
};
</script>

<style scoped lang="scss">
  .column {
    border-bottom: 1px solid black;
    margin: 50px 10px;
    max-width: 40px;
  }
  button:disabled {
    cursor: default;
  }
</style>
