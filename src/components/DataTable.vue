<template>
  <div>
    <table
      class="table"
    >
      <thead class="table__head">
        <tr class="table__row">
          <th
            class="table__headerTitle"
            v-for="title in dataTitles"
            :key="title.sortField"
            @click="switchSort(title.sortField)"
          >
            <span> {{ title.name }} </span>
            <i :class="[sortType > 0 && sortField === title.sortField ? 'filterButton' : 'filterButton_active']"></i>
          </th>
        </tr>
      </thead>
      <tr
        v-for="item in sorted"
        :key="item.id"
        class="table__row"
      >
        <td 
          v-for="title in dataTitles"
          :key="title.sortField"
          class="table__cell"> {{ item[title.sortField] instanceof Date ?
          formatDate(item[title.sortField]) : item[title.sortField] }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  mounted() {
    this.list = this.dataList
  },
  props: {
    dataList: {
      type: Array,
      required: true
    },
    dataTitles: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      list: [],
      sortField: null,
      sortType: 1
    }
  },
  computed: {
    sorted() {
      let items = this.list;
      if (this.sortField === null) {
        return items;
      }
      return items.sort((left, right) => {
        let leftValue = left[this.sortField];
        let rightValue = right[this.sortField];
        if ((typeof leftValue) === 'string') {
          leftValue = leftValue.length;
          rightValue = rightValue.length;
        }
        if (leftValue > rightValue) {
          return this.sortType;
        }
        if (leftValue < rightValue) {
          return this.revertSortType;
        }
        return 0;
      });
    },
    revertSortType() {
      return this.sortType > 0 ? -1 : 1;
    }
  },
  methods: {
    switchSort(sortField) {
      this.sortField = sortField;
      this.sortType = this.revertSortType;
    },
    formatDate(date) {
      let dd = date.getDate();
      if (dd < 10) dd = '0' + dd;

      let mm = date.getMonth() + 1;
      if (mm < 10) mm = '0' + mm;

      let yy = date.getFullYear();
      if (yy < 10) yy = '0' + yy;

      return yy + '-' + mm + '-' + dd;
    }
  }
}
</script>

<style scoped>
.table {
  width: 1160px;
  height: 600px;
  margin: 0 auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.table__head {
  position: sticky;
  top: 0;
  left: 0;
  z-index: 1;
  border: 1px solid black;
  background-color: antiquewhite;
}
.table__row {
  height: 80px;
  border: 1px solid black;
}
.filterButton {
  background-image: url(/src/assets/images/arrowSort.svg);
  width: 8px;
  height: 8px;
  background-repeat: no-repeat;
  border: none;
  margin-left: 10px;
  display: inline-block;
}
.filterButton_active {
  background-image: url(/src/assets/images/arrowSort.svg);
  width: 8px;
  height: 8px;
  background-repeat: no-repeat;
  border: none;
  margin-left: 10px;
  color: #29277d;
  transform: rotate(180deg);
  display: inline-block;
}
.table__headerTitle {
  border: 1px solid black;
  cursor: pointer;
}
.table__cell {
  border: 1px solid black;
  text-align: center;
  min-height: 40px;
}
</style>
