<template>
  <div class="container-fluid pb-5">
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

    <div class="duel-grid pb-5">
      <div class="player-1">
        <div class="d-flex align-items-center justify-content-center">
          <h2 class="orbitron text-center">
            {{ duelistOne.name ? duelistOne.name : 'Duelista 1' }}
          </h2>
          <div class="">
            <button
              class="btn btn-raised rounded-circle py-1 px-2 mx-2"
              :class="isDarkTheme ? 'btn-uv' : 'btn-crimson'"
              @click="getDuelistOne(duelists)"
            >
              <font-awesome-icon :icon="['fas', 'rotate']" />
            </button>
          </div>
        </div>

        <img
          :src="
            duelistOne.avatar
              ? duelistOne.avatar
              : 'https://i.imgur.com/L6kUdv4.jpg'
          "
          class="duelist-avatar shadow mb-3"
          alt=""
        />
        <div class="d-flex justify-content-center align-items-center">
          <h2 class="orbitron text-center">Decks</h2>
          <div class="">
            <button
              class="btn btn-raised rounded-circle py-1 px-2 mx-2"
              :class="isDarkTheme ? 'btn-uv' : 'btn-crimson'"
              @click="getDeckDuelistOne(duelistOne.decks)"
            >
              <font-awesome-icon :icon="['fas', 'rotate']" />
            </button>
          </div>
        </div>

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
                <h3 class="orbitron text-light text-center">Decks</h3>
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
        <div class="d-flex align-items-center justify-content-center">
          <h2 class="orbitron text-center">
            {{ duelistTwo.name ? duelistTwo.name : 'Duelista 2' }}
          </h2>
          <div class="">
            <button
              class="btn btn-raised rounded-circle py-1 px-2 mx-2"
              :class="isDarkTheme ? 'btn-uv' : 'btn-crimson'"
              @click="getDuelistTwo(duelists)"
            >
              <font-awesome-icon :icon="['fas', 'rotate']" />
            </button>
          </div>
        </div>
        <img
          :src="
            duelistTwo.avatar
              ? duelistTwo.avatar
              : 'https://i.imgur.com/L6kUdv4.jpg'
          "
          class="duelist-avatar shadow mb-3"
          alt=""
        />
        <div class="d-flex justify-content-center align-items-center">
          <h2 class="orbitron text-center">Decks</h2>
          <div class="">
            <button
              class="btn btn-raised rounded-circle py-1 px-2 mx-2"
              :class="isDarkTheme ? 'btn-uv' : 'btn-crimson'"
              @click="getDeckDuelistTwo(duelistTwo.decks)"
            >
              <font-awesome-icon :icon="['fas', 'rotate']" />
            </button>
          </div>
        </div>

        <div class="px-4">
          <div
            class="card card-raised card-background mx-auto view-anchor"
            style="max-width: 450px"
          >
            <img
              :src="
                deckDuelistTwo.img
                  ? deckDuelistTwo.img
                  : 'https://i.imgur.com/L6kUdv4.jpg'
              "
              class="card-background-image-featured"
              alt=""
            />
            <div class="mask pattern-1"></div>
            <div
              class="card-img-overlay d-flex flex-column justify-content-center"
            >
              <div v-if="deckDuelistTwo.name">
                <h2 class="orbitron text-light text-center stroke">
                  <strong>{{ deckDuelistTwo.name }}</strong>
                </h2>
              </div>
              <div v-else-if="duelistTwo.decks" class="">
                <p
                  v-for="(deck, i) in duelistTwo.decks"
                  :key="i"
                  class="orbitron text-light"
                >
                  <strong>
                    {{ deck.name }}
                  </strong>
                </p>
              </div>

              <div v-else>
                <h3 class="orbitron text-light text-center">Decks</h3>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- <pre>{{ duelistOne }}</pre> -->
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
      duelistTwo: {},
      deckDuelistTwo: {},
    }
  },
  computed: {
    ...mapGetters(['isDarkTheme']),
  },

  mounted() {
    // this.getDuelistOne(this.duelists)
    // this.getDuelistTwo(this.duelists)
  },

  methods: {
    duelistRandomizer(duelists) {
      return duelists[Math.floor(Math.random() * duelists.length)]
    },

    getDuelistOne(duelists) {
      const duelist = this.duelistRandomizer(duelists)

      if (Object.keys(this.duelistOne).length > 0) {
        this.duelistOne = {}
      }

      setTimeout(() => {
        if (duelist !== this.duelistTwo && Object.keys(duelist).length > 0) {
          this.duelistOne = duelist
          return this.duelistOne
        } else {
          return this.getDuelistOne(duelists)
        }
      }, 250)
    },

    getDeckDuelistOne(decks) {
      const randomDeck = decks[Math.floor(Math.random() * decks.length)]
      console.log(randomDeck)
      this.deckDuelistOne = randomDeck
    },

    getDuelistTwo(duelists) {
      const duelist = this.duelistRandomizer(duelists)

      if (Object.keys(this.duelistTwo).length > 0) {
        this.duelistTwo = {}
      }

      setTimeout(() => {
        if (duelist !== this.duelistOne && Object.keys(duelist).length > 0) {
          this.duelistTwo = duelist

          return this.duelistTwo
        } else {
          return this.getDuelistTwo(duelists)
        }
      }, 250)
    },

    getDeckDuelistTwo(decks) {
      const randomDeck = decks[Math.floor(Math.random() * decks.length)]
      console.log(randomDeck)
      this.deckDuelistTwo = randomDeck
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
  width: 225px;
  height: 225px;
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
