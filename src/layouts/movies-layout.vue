<template lang="html">
  <section class="movies-layout container">
    <h1>List Movies</h1>
    <div class="input-group">
      <div class="input-group-prepend">
        <span class="input-group-text">Filer by Title</span>
      </div>
      <input type="text"
      class="form-control"
      placeholder="Filter by Title"
      aria-label="Filter"
      v-model="search"
      >
    </div>
    <Table
      :rows="infoPage"
      :headers="headers"
    />
    <div class="mt-3" v-if="info">
      <b-pagination
        size="sm"
        v-model="currentPage"
        :per-page="pageSize"
        :total-rows="infoFiltered.length"
        @change="genPage"
        first-number
        align="right">
      </b-pagination>
    </div>
  </section>
</template>

<script>

import axios from 'axios';
import Table from '../components/table.vue';

export default {
  name: 'MoviesLayout',
  components: {
    Table,
  },
  props: [],
  mounted() {

  },
  data() {
    return {
      info: [],
      infoFiltered: [],
      infoPage: [],
      fieldFilter: 'title',
      headers: null,
      search: '',
      pageSize: 15,
      currentPage: 1,
      totalPages: 0,
    };
  },
  methods: {
    genPage(page) {
      this.paginate(this.infoFiltered, this.pageSize, page);
    },
    paginate(array, pageSize, pageNumber) {
      this.infoPage = array.slice((pageNumber - 1) * pageSize, pageNumber * pageSize);
    },
    filterList(val) {
      if (val) {
        this.infoFiltered = this.info.filter(
          (row) => row[this.fieldFilter].toLowerCase().includes(val.toLowerCase()),
        );
      } else {
        this.infoFiltered = this.info;
      }
      this.genPage(this.currentPage);
    },
  },
  watch: {
    search(newVal) {
      this.filterList(newVal);
    },
  },
  computed: {
  },
  created() {
    axios
      // .get('/resources/movies.json')
      .get('https://raw.githubusercontent.com/getmanfred/codechallenges/main/vue/movies.json')
      .then((response) => {
        this.paginate(response.data, this.pageSize, this.currentPage);
        this.info = response.data;
        this.infoFiltered = this.info;
        this.headers = Object.keys(this.info[0]);
      }, (error) => {
        console.log(error);
      });
  },
};
</script>

<style scoped lang="scss">
</style>
