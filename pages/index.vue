<template>
  <div class="container-fluid">
    <h1
      class="orbitron mt-3"
      :class="
        isDarkTheme
          ? 'text-light cyber-underline-light'
          : 'text-dark cyber-underline-dark'
      "
    >
      Master Duel - Matchmaker
    </h1>

    <div class="duel-grid">
      <div class="player-1">
        <h2 class="orbitron text-center">
          {{ duelistOne.name ? duelistOne.name : 'Duelista 1' }}
        </h2>
        <img
          :src="
            duelistOne.avatar
              ? duelistOne.avatar
              : 'https://i.imgur.com/L6kUdv4.jpg'
          "
          class="duelist-avatar mb-3"
          alt=""
        />

        <h2 class="orbitron text-center">Decks</h2>

        <div class="px-4">
          <div
            class="card card-raised card-background mx-auto view-anchor"
            style="max-width: 450px"
          >
            <img
              :src="
                deckDuelistOne.img
                  ? deckDuelistOne.img
                  : 'https://i.imgur.com/L6kUdv4.jpg'
              "
              class="card-background-image-featured"
              alt=""
            />
            <div class="mask pattern-1"></div>
            <div
              class="card-img-overlay d-flex flex-column justify-content-center"
            >
              <div v-if="deckDuelistOne.name">
                <h2 class="orbitron text-light text-center stroke">
                  <strong>{{ deckDuelistOne.name }}</strong>
                </h2>
              </div>
              <div v-else-if="duelistOne.decks" class="">
                <p
                  v-for="(deck, i) in duelistOne.decks"
                  :key="i"
                  class="orbitron text-light"
                >
                  <strong>
                    {{ deck.name }}
                  </strong>
                </p>
              </div>

              <div v-else>
                <h3 class="orbitron text-light">Dead Space</h3>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="versus">
        <h2 class="orbitron text-center">VS</h2>
        <span
          class="vertical-divider"
          :class="isDarkTheme ? 'bg-light' : 'bg-dark'"
        ></span>
      </div>
      <div class="player-2">
        <h2 class="orbitron text-center">Duelista 2</h2>
        <img
          src="https://i.imgur.com/To4RzjC.jpg"
          class="duelist-avatar mb-3"
          alt=""
        />

        <h2 class="orbitron text-center">Decks</h2>

        <div class="px-4">
          <div
            class="card card-raised card-background view-anchor mx-auto"
            style="max-width: 450px"
          >
            <img
              src="https://i.imgur.com/L6kUdv4.jpg"
              class="card-background-image-featured"
              alt=""
            />
            <div class="mask pattern-1"></div>

            <div
              class="card-img-overlay text-center d-flex flex-column justify-content-center"
            >
              <h3 class="orbitron text-light">Dead Space</h3>
            </div>
          </div>
        </div>
      </div>
    </div>

    <pre>{{ duelistOne }}</pre>
    <button class="" @click="getDeckDuelistOne(duelistOne.decks)">
      random deck
    </button>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

import dataDuelists from '@/static/duelists.json'
export default {
  name: 'IndexPage',
  data() {
    return {
      duelists: dataDuelists,
      duelistOne: {},
      deckDuelistOne: {},
    }
  },
  computed: {
    ...mapGetters(['isDarkTheme']),
  },

  mounted() {
    this.getDuelistOne(this.duelists)
  },

  methods: {
    getDuelistOne(duelists) {
      const duelist = duelists.filter((obj) => obj.name === 'Ultimate Mercer')
      this.duelistOne = {
        ...duelist[0],
      }
      console.log(this.duelistOne)
      return this.duelistOne
    },

    getDeckDuelistOne(decks) {
      const randomDeck = decks[Math.floor(Math.random() * decks.length)]
      console.log(randomDeck)
      this.deckDuelistOne = randomDeck
    },
  },
}
</script>

<style lang="scss">
.orbitron {
  font-family: 'Orbitron', 'JetBrains Mono', consolas, monospace;
}

.duel-grid {
  display: grid;
  grid-template-columns: auto 100px auto;
  grid-template-rows: auto auto auto;
  grid-template-areas:
    'Player1 Versus Player2'
    'Player1 Versus Player2 '
    'Player1 Versus Player2 '
    'Player1 Versus Player2 '
    'Info Info Info'
    'Footer Footer Footer ';
  padding: 1rem 0.5rem 2rem;
}

.player-1 {
  grid-area: Player1;
  padding: 0.5rem 0;
}

.versus {
  grid-area: Versus;
}

.player-2 {
  grid-area: Player2;
  padding: 0.5rem 0;
}

.vertical-divider {
  width: 4px;
  min-height: 100vh;
  height: 100%;
  /* max-height: 100%; */
  margin: 1rem auto;
  display: block;
}

.duelist-avatar {
  width: 200px;
  height: 200px;
  margin: 0 auto;
  display: block;
  object-fit: cover;
  border-radius: 4px;
}

.stroke {
  text-shadow: -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,
    1px 1px 0 #000;
}
</style>
