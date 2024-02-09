<template>
  <div class="select">
    <div v-if="!isEdit" @click="show">
      <div class="selectForm">
          <span class="selectForm__topTitle selectForm__topTitle_visible"
            v-show="isSelected"
          >
            {{ placeholder }}
          </span>
          <span class="selectForm__title" :class="isSelected ? 'selectForm__title_selected' : ''">
            {{ title }}
          </span>
          <button class="selectForm__button selectForm__button_deRotate"></button>
      </div>
    </div>
    <div v-else-if="isEdit" @click="hide">
      <div class="selectForm__selectList">
        <div class="selectForm selectForm_inList">
          <span class="selectForm__title">{{ title }}</span>
          <button class="selectForm__button selectForm__button_rotate"></button>
        </div>
        <div class="selectForm__list">
          <div
            v-for="item in items"
            :key="item.id"
            :class="['selectForm__listItem', 
              isSelected && modelValue.id === item.id ?
              'selectForm__selectedListItem' : '']"
            @click="select(item)"
          >
            <span class="selectedForm__listItemTitle">{{ item.title }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    placeholder: {
      type: String,
      default: 'Выберете элемент'
    },
    modelValue: {
      type: Object,
      default: null
    }
  },
  emits: ['update:modelValue'],
  data () {
    return {
      isEdit: false,
    }
  },
  computed: {
    isSelected() {
      return !(this.modelValue === null);
    },
    title() {
      return this.isSelected ? this.modelValue.title : this.placeholder;
    }
  },
  methods: {
    show () {
      this.isEdit = true;
    },
    hide () {
      this.isEdit = false;
    },
    select (item) {
      this.$emit('update:modelValue', item);
      this.hide();
    }
  }
}
</script>

<style scoped>
.select {
  min-height: 200px;
}
.selectForm {
  position: relative;
  display: flex;
  width: 220px;
  height: 25px;
  margin: 50px auto 0;
  border: 1px solid #F968bf;
  border-radius: 5px;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}
.selectForm__title {
  padding: 5px;
  font-size: 12px;
  color: rgba(41, 39, 125, 0.40);
  width: 100%;
}
.selectForm__title_selected {
  color: #29277d;
}
.selectForm__button {
  background-image: url(/src/assets/images/arrowSelect.svg);
  width: 16px;
  height: 16px;
  border: none;
  background-color: white;
  color:  #5F88F4;
  margin-right: 5px;
  cursor: pointer;
}
.selectForm__button_rotate {
  animation: rotation 0.3s linear 1;
  animation-fill-mode: forwards;
}
@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(180deg);
  }
}
.selectForm__button_deRotate {
  animation: deRotation 0.3s linear 1;
  animation-fill-mode: forwards;
}
@keyframes deRotation {
  from {
    transform: rotate(180deg);
  }
  to {
    transform: rotate(0deg);
  }
}
.selectForm__selectList {
  display: flex;
  flex-direction: column;
  width: 220px;
  margin: 50px auto 0;
  border: 1px solid #F968bf;
  border-radius: 5px;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}
.selectForm_inList {
  border: none;
  border-bottom: 1px solid #F968bf;
  border-radius: 0;
  margin: 0;
}
.selectForm__list {
  font-size: 12px;
  color: #29277d;
  width: 100%;
}
.selectForm__listItem {
  cursor: pointer;
}
.selectForm__listItem:hover {
  background-color: #DADEFE;
  transition: background-color 0.25s, color 0.15s;
}
.selectForm__listItem {
    padding: 5px;
}
.selectedForm__listItemTitle {
  margin: 2px 5px;
}
.selectForm__selectedListItem {
  background-color: #DADEFE;
  color: #F968bf;
}
.selectForm__topTitle {
    font-size: 8px;
    position: absolute;
    top: -10px;
    left: 0;
    display: none;
    color: rgba(41, 39, 125, 0.40);
}
.selectForm__topTitle_visible {
    display: block;
}
</style>
