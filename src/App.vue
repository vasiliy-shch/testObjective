<template>
  <div class="body">
    <SelectComponent
      v-model="selectedItem"
      :items="options"
      placeholder="Выберите название региона"
    />
    <DataTable
      class="fixedHeight"
      :data-list="preparedData"
      :data-titles="titles"
    />
  </div>
</template>

<script>
import SelectComponent from '/src/components/SelectComponent.vue'
import DataTable from '/src/components/DataTable.vue'
export default {
  components: {
    SelectComponent,
    DataTable
  },
  data () {
    return {
      selectedItem: null,
      options: [
        {
          id: 1,
          title: 'Слон'
        },
        {
          id: 2,
          title: 'Бегемот'
        },
        {
          id: 3,
          title: 'Зебра'
        },
        {
          id: 4,
          title: 'Жираф'
        },
        {
          id: 5,
          title: 'Лев'
        }
      ],
      data: [
        {
          id: 1,
          number: 421,
          developer: 'PRINZIP',
          deadline: '2006-08-10T19:21:32',
          type: 'Студия',
          floor: 3,
          square: 100.3
        },
        {
          id: 2,
          number: 73,
          developer: 'Брусника',
          deadline: '2007-08-09T18:31:42',
          type: '2-к',
          floor: 5,
          square: 10.3
        },
        {
          id: 3,
          number: 122,
          developer: 'TEN',
          deadline: '2001-08-09T18:31:42',
          type: '3-к',
          floor: 7,
          square: 103
        },
        {
          id: 4,
          number: 1,
          developer: 'PRINZIP',
          deadline: '2010-08-09T18:31:42',
          type: 'Студия',
          floor: 1,
          square: 100.3
        },
        {
          id: 5,
          number: 72,
          developer: 'Брусника',
          deadline: '2030-08-09T18:31:42',
          type: '2-к',
          floor: 2,
          square: 10.3
        },
        {
          id: 6,
          number: 23,
          developer: 'TEN',
          deadline: '2005-08-09T18:31:42',
          type: '3-к',
          floor: 2,
          square: 103
        },
        {
          id: 7,
          number: 5,
          developer: 'PRINZIP',
          deadline: '2005-08-09T18:31:42',
          type: 'Студия',
          floor: 2,
          square: 100.3
        },
        {
          id: 8,
          number: 2,
          developer: 'Брусника',
          deadline: '2005-08-09T18:31:42',
          type: '2-к',
          floor: 2,
          square: 10.3
        },
        {
          id: 9,
          number: 97,
          developer: 'TEN',
          deadline: '2005-08-09T18:31:42',
          type: '3-к',
          floor: 2,
          square: 103
        },
        {
          id: 10,
          number: 34,
          developer: 'PRINZIP',
          deadline: '2005-08-09T18:31:42',
          type: 'Студия',
          floor: 2,
          square: 100.3
        },
        {
          id: 11,
          number: 1,
          developer: 'Брусника',
          deadline: '2005-08-09T18:31:42',
          type: '2-к',
          floor: 2,
          square: 10.3
        },
        {
          id: 12,
          number: 88,
          developer: 'TEN',
          deadline: '2005-08-09T18:31:42',
          type: '3-к',
          floor: 2,
          square: 103
        }
      ],
      appartamentTypes: [
        {
          name: 'Студия',
          weight: 1
        },
        {
          name: '2-к',
          weight: 2
        },
        {
          name: '3-к',
          weight: 3
        },
      ],
      titles: [
        {
          sortField: 'number',
          name: 'Номер'
        },
        {
          sortField: 'developer',
          name: 'Девелопер'
        },
        {
          sortField: 'deadline',
          name: 'Срок'
        },
        {
          sortField: 'typeWeight',
          name: 'Тип'
        },
        {
          sortField: 'floor',
          name: 'Этаж'
        },
        {
          sortField: 'square',
          name: 'Площадь'
        },
      ]
    }
  },
  computed: {
    preparedData() {
      return this.data.map((item) => {
        const type = this.appartamentTypes.find((i) => i.name === item.type)
        const deadline = new Date(item.deadline)
        return {
          ...item,
          deadline,
          typeWeight: type != undefined ? type.weight : 0
        }
      })
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

html, body {
    margin: 0;
    font-family: 'Montserrat', sans-serif;
    min-width: 1200px;
    max-width: 100%;
    padding: 0;
    height: 100%;
    min-height: 100%;
}
#app {
    font-family: 'Montserrat', sans-serif;
}
.fixedHeight {
  width: 1200px;
  height: 600px;
  overflow-y: scroll;
  margin: 0 auto;
}
</style>
