<template>
  <div class="autocomplete">
    <input
      class="input-box"
      v-model="search"
      @input="onChange"
      @keydown.down="onArrowDown"
      @keydown.up="onArrowUp"
      @keydown.enter="onEnter"
      @keyup.delete="changeHandler"
      @focus="$event.target.select()"
      autofocus="autofocus"
      type="text"
      id="textbox"
    />
    <ul v-show="isOpen" class="autocomplete-results">
      <li
        v-for="(result, i) in results"
        :key="i"
        @click="setResult(result)"
        class="autocomplete-result"
        :class="{ 'is-active': i === arrowCounter }"
      >
        {{ result }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "SearchAutocomplete",

  mounted() {
    document.addEventListener("click", this.handleClickOutside);
  },
  destroyed() {
    document.removeEventListener("click", this.handleClickOutside);
  },

  props: {
    items: {
      type: Array,
      required: false,
      default: () => [],
    },
  },
  data() {
    return {
      search: "",
      results: [],
      isOpen: false,
      arrowCounter: -1,
    };
  },

  methods: {
    changeHandler() {
      if (this.search === "") {
        this.isOpen = false;
        this.arrowCounter = -1;
      }
    },
    filterResults() {
      this.results = this.items.filter(
        (item) => item.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      );
    },
    onChange() {
      this.filterResults();
      this.isOpen = true;
      this.arrowCounter = 0;
    },
    setResult(result) {
      this.search = result;
      this.isOpen = false;
      setTimeout(function () {
        document.getElementById("textbox").select();
      }, 100);
    },
    handleClickOutside(event) {
      this.isOpen = false;
      if (!this.$el.contains(event.target)) {
        this.arrowCounter = -1;
      }
    },
    onArrowDown() {
      if (this.arrowCounter < this.results.length) {
        this.arrowCounter = this.arrowCounter + 1;
      }
    },
    onArrowUp() {
      if (this.arrowCounter > 0) {
        this.arrowCounter = this.arrowCounter - 1;
      }
    },
    onEnter() {
      this.search = this.results[this.arrowCounter];
      this.arrowCounter = -1;
      this.isOpen = false;
      setTimeout(function () {
        document.getElementById("textbox").select();
      }, 100);
    },
  },
};
</script>

<style>
.autocomplete {
  font-size: 32;
  position: fixed;
  top: 25%;
  left: 40%;
}

.autocomplete-results {
  padding: 0;
  margin: 0;
  border: 1px solid #eeeeee;
  min-height: 1em;
  max-height: 200em;
  overflow: auto;
}

.autocomplete-result {
  list-style: none;
  text-align: center;
  padding: 4px 2px;
  cursor: pointer;
}

.autocomplete-result.is-active,
.autocomplete-result:hover {
  background-color: #4aae9b;
  color: white;
}

.input-box {
  font-size: 32pt;
}
</style>