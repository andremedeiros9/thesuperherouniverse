<template>
  <div id="app">
    <main>
      <div class="title">The Superhero Universe</div>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Search character..."
          v-model="query"
          @keypress="fetchCharacter"
        />
      </div>
      <div class="character-box" v-if="typeof character.results != 'undefined'">
        <div class="superhero-name" v-for="hero in character.results" v-bind:key="hero">
          {{ hero.name }}
          <button>
            <img v-bind:src="hero.image.url" />
          </button>
        </div>
      </div>
    </main>
    <section class="new-view">
      <div class="character-description" v-if="typeof character.results != 'undefined'"></div>
    </section>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      acess_token: "",
      url_base: "http://localhost:8080/api/3326108260779442",
      query: "",
      character: {}
    };
  },
  methods: {
    fetchCharacter(e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}/search/${this.query}`)
          .then(res => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.character = results;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-image: url("./assets/background-image.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

.title {
  font-size: 60px;
  color: white;
  text-align: center;
  font-style: italic;
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  text-align: center;
  font-style: italic;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 16px 16px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.8);
  box-shadow: 0px 0px 8px 3px paleturquoise;

  text-align: center;
  font-style: inherit;
}

main {
  min-height: 100vh;
  padding: 25px;
}

.character-box {
  display: flex;
  flex-wrap: wrap;
  margin: 0px -15px;

  text-align: center;
}

.superhero-name {
  width: 33.333%;
  display: flex;
  flex-direction: column;
  min-width: 200px;
  padding: 60px;

  color: paleturquoise;
  text-align: center;
  font-weight: 600;
  font-size: 50px;

  align-content: center;
}
.superhero-name img {
  display: block;
  width: 100%;
  cursor: pointer;
  border-radius: 8px 8px 8px 8px;
}

button:focus {
  box-shadow: 0px 0px 16px 6px paleturquoise;
  border-radius: 8px 8px 8px 8px;
}
</style>
