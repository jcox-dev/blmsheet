<template>
<div>
  <div class="filters p-3 mb-2">
    <p>Discover artists, producers and labels...</p>    
    <a class="btn btn-bc-blue text-white" v-on:click="shuffleRandom">
    <svg class="bi bi-shuffle" width="1em" height="1em" viewBox="0 0 16 16" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
      <path fill-rule="evenodd" d="M12.646 1.146a.5.5 0 0 1 .708 0l2.5 2.5a.5.5 0 0 1 0 .708l-2.5 2.5a.5.5 0 0 1-.708-.708L14.793 4l-2.147-2.146a.5.5 0 0 1 0-.708zm0 8a.5.5 0 0 1 .708 0l2.5 2.5a.5.5 0 0 1 0 .708l-2.5 2.5a.5.5 0 0 1-.708-.708L14.793 12l-2.147-2.146a.5.5 0 0 1 0-.708z"/>
      <path fill-rule="evenodd" d="M0 4a.5.5 0 0 1 .5-.5h2c3.053 0 4.564 2.258 5.856 4.226l.08.123c.636.97 1.224 1.865 1.932 2.539.718.682 1.538 1.112 2.632 1.112h2a.5.5 0 0 1 0 1h-2c-1.406 0-2.461-.57-3.321-1.388-.795-.755-1.441-1.742-2.055-2.679l-.105-.159C6.186 6.242 4.947 4.5 2.5 4.5h-2A.5.5 0 0 1 0 4z"/>
      <path fill-rule="evenodd" d="M0 12a.5.5 0 0 0 .5.5h2c3.053 0 4.564-2.258 5.856-4.226l.08-.123c.636-.97 1.224-1.865 1.932-2.539C11.086 4.93 11.906 4.5 13 4.5h2a.5.5 0 0 0 0-1h-2c-1.406 0-2.461.57-3.321 1.388-.795.755-1.441 1.742-2.055 2.679l-.105.159C6.186 9.758 4.947 11.5 2.5 11.5h-2a.5.5 0 0 0-.5.5z"/>
    </svg>
    Random Shuffle
    </a>
  <hr>
    <p>Or filter by name, genre or location...</p>

    <form class="d-flex justify-content-center">
      <div class="d-flex flex-row flex-wrap justify-content-center">
        <div class="input-group input-group-sm d-flex justify-content-center">
          <input placeholder="Search by name" type="text" class="form-control" id="name-filter" v-model="filters.name">
          <a @click="filters.name = ''" v-if="filters.name !== ''">&times;</a>
        </div>
        <div class="input-group input-group-sm">
          <div>
          <select class="custom-select" v-model="filters.genre" :disabled="filters.name !== ''">
            <option value="">All Genres</option>
            <option v-for="genre in genresData" :value="genre" :key="genre">
                {{ genre }}
            </option>
          </select>
          </div>
        </div>
        <LocationTypeAhead :filters="filters" class="location-filter"/>
      </div>
    </form>
  </div>
  <div :class="{ 'alphabet-filter': true, disabled: filters.name }">
  <ul class="mt-3 mb-3 mb-0">
      <li v-on:click="filters.first_letter = null" :class="{ 'd-inline text-uppercase h4 letter mr-3': true, active: filters.first_letter === null }">All</li>
      <li v-for="letter in alphabet" :key="letter" v-on:click="filters.first_letter = letter; filters.name = ''" :class="{ 'd-inline text-uppercase h4 letter': true, active: letter === filters.first_letter }" >
        {{ letter }}
      </li>
  </ul>
  </div>

  </div>
</template>

<script>
import axios from 'axios';
import LocationTypeAhead from '@/components/LocationTypeAhead.vue'

export default {
  name: 'Filters',
  props: {
    filters: Object,
  },
  components: {
    LocationTypeAhead
  },
  mounted(){
    this.fetchGenres();
  },
  data: function() {
    return {
      genresData: [],
      locationsData: [],
      alphabet: 'abcdefghijklmnopqrstuvwxyz#'.split(''),
    }
  },
  methods: {
    fetchGenres(){
        this.$emit('loading', true)
        axios.get('/api/genres')
        .then((response) => {
            this.genresData = response.data
            this.$emit('loading', false)
        })
    },
    shuffleRandom(){
      this.$parent.fetchRandom();
    }
  }
}
</script>

<style scoped lang="scss">
  $bc-blue: #0064b5;

  .letter {
    cursor: pointer;
    @media (prefers-color-scheme: dark) {
      color: rgba(255,255,255, 0.5);
    }
   
    &:hover, &.active {
      color: $bc-blue;
      @media (prefers-color-scheme: dark) {
        color: white;
      }
    }

     @media (prefers-color-scheme: light) {
      color: rgba(0,0,0, 0.5);
      &:hover {
        color: black;
      }
    }
  }

  select {
    width: 100% !important;
    height: 100%;
    background-color: transparent;
    border-color: rgba(255,255,255,0.5);
  }

  .input-group, .location-filter {
    width: 200px;
    // width: 100%;
    height: 40px !important;
    margin:10px ;
    input, /deep/div, /deep/ div input {
      height: 100%;
      width: 100%;
      background-color: transparent;
      border-color: rgba(255,255,255,0.5);
    }
  }
  select, option {text-transform:capitalize !important;}

  .input-group div {
    margin:auto;
  }
  .input-group {
    position: relative;
    input {
      z-index: 2;
    }
    a {
      z-index: 3;
      cursor: pointer;
      position: absolute;
      right: 10px;
      top: 0px;
      line-height: 40px;
      font-size: 22px;
    }
  }



  .alphabet-filter {
    overflow-x:scroll;
    transition:opacity 0.2s;
    ul {
      padding-left: 0;
      min-width:710px;
    }
    &.disabled {
      opacity:0.3;
      pointer-events: none;
    }
  }

  .btn-bc-blue {
    background-color: $bc-blue;
    border: 1px solid $bc-blue;
    @media (prefers-color-scheme: dark) {
      background-color: transparent;
      border: 1px solid white;
    }
  }

  @media (prefers-color-scheme: dark) {
    .filters {
      border: 1px solid rgba(255,255,255,0.3);
      background-color: transparent;
    }
    select, input, /deep/div, /deep/ div input {
      background-color: transparent;
      color: white !important;
      border-color: rgba(255,255,255,0.5);
    }
    select:disabled {
      background-color: transparent;
      opacity: 0.7;
    }
    hr {
      background-color: rgba(255,255,255,0.3);
    }
  }

  @media (prefers-color-scheme: light) {
    .filters {
      background-color: white;
      color: black;
    }
    select, input, /deep/ div input {
      background-color: #f9f9f9 !important;
    }
     select, input, /deep/div, /deep/ div input {
      color: black !important;
      border-color: black !important;
    }
    select:disabled {
      opacity: 1;
    }
    hr {
      background-color: #f7f7f7;
    }
  }

</style>
