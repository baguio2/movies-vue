<template lang="html">
  <section class="mt-3">
    <table class="table table-sm table-bordered">
      <thead>
        <tr>
          <th class="w-col table__header-title"
            v-for="(col, index) in headers" :key="`col-${index}`">
            <a href="#" @click="sortTable(col)">
              {{ col }}
              <i v-if="col == sortColumn" class="arrow"
              :class="[ascending ? 'arrow--up' : 'arrow--down']"></i>
            </a>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) in listRows" :key="`row-${index}`">
          <td class="w-col" v-for="(col, index) in headers" :key="`cell-${index}`">
            {{ row[col] }}
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script lang="js">

export default {
  name: 'Table',
  props: {
    rows: {
      type: Array,
    },
    headers: {
      type: Array,
    },
  },
  mounted() {

  },
  // eslint-disable-next-line vue/no-shared-component-data
  data() {
    return {
      listRows: [],
      ascending: false,
      sortColumn: '',
      rowsCopy: [],
    };
  },
  methods: {
    sortTable(col) {
      if (this.sortColumn === col) {
        this.ascending = !this.ascending;
      } else if (col) {
        this.ascending = true;
        this.sortColumn = col;
      }

      const filledRows = this.listRows.filter((row) => !!row[this.sortColumn]);
      const emptyRows = this.listRows.filter((row) => !row[this.sortColumn]);
      const { ascending } = this;

      const listRows = filledRows.sort((a, b) => {
        if (a[this.sortColumn] > b[this.sortColumn]) {
          return ascending ? 1 : -1;
        }
        if (a[this.sortColumn] < b[this.sortColumn]) {
          return ascending ? -1 : 1;
        }
        return 0;
      });

      this.listRows = listRows.concat(emptyRows);
    },
  },
  watch: {
    rows(newVal) {
      this.listRows = newVal;
      this.sortTable();
    },
  },
};
</script>

<style scoped lang="scss">
.table {
  &__header-title {
    a {
      display: flex;
      width: 100%;
      justify-content: center;
      align-items: center;
    }
  }

  .arrow {
    width: 0;
    height: 0;
    border-left: 5px solid transparent;
    border-right: 5px solid transparent;
    border-bottom: 5px solid;
    margin-left: 8px;
    &--up {
      transform: rotate(0deg);
      -webkit-transform: rotate(0deg);
    }
    &--down {
      transform: rotate(180deg);
      -webkit-transform: rotate(180deg);
    }
  }
  @media (min-width: 576px) {
    .w-col {
      min-width: 80px;
    }
  }
}
</style>
