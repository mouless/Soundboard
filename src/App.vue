<template>
  <div id="app">
    <SearchAutocomplete
      :items="[
        'Apple',
        'Apricot',
        'Banana',
        'Dragonfruit',
        'Fig',
        'Grape',
        'Guava',
        'Kiwi',
        'Lemon',
        'Lime',
        'Orange',
        'Mandarine',
        'Mango',
        'Papaya',
        'Passionfruit',
        'Pear',
        'Peach',
        'Pineapple',
        'Plum',
        'Tangerine',
        'Blueberry',
        'Blackberry',
        'Lingonberry',
        'Raspberry',
        'Gooseberry',
        'Mulberry',
        'Strawberry',
        'Watermelon',
      ]"
    />

    <audio controls>
      <source src="@/assets/1337.mp3" type="audio/mpeg" />
      Your browser does not support the audio tag.
    </audio>
  </div>
</template>

<script>
import SearchAutocomplete from "./components/SearchAutocomplete.vue";

export default {
  name: "App",
  components: {
    SearchAutocomplete,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
