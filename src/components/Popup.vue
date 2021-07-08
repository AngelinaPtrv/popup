<template>
  <div class="popup">
    <div class="popup__wrap">
      <div>
      <div class="header__wrap">
        <span class="header">Налоговый вычет</span>
        <div class="close">
          <span
              class="close__img"
              @click="doVisiblePopup"
          ></span>
        </div>
      </div>
        <span class="popup__info">
          Используйте налоговый вычет чтобы погасить ипотеку досрочно. Размер налогового вычета составляет 13% от своего
          официального годового дохода.
        </span>
      <div class="popup__input">
        <span>Ваша зарплата в месяц</span>
        <input
            type="text"
            placeholder="Введите данные"
            v-model="value"
            :class="err ? 'error' : ''"
        />
        <span v-if="err" style="color: #dc3131">Введите число</span>
        <span
            class="text__button"
            @click="doVisibleCheckboxes"
        >Рассчитать</span>
      </div>
      <div
          class="popup__checkboxes"
          :class="activeCheckboxes ? 'active' : 'notactive'">
        <span class="checkboxes__header">Итого можете внести в качестве досрочных:</span>
        <div
            v-for="(item, index) in recoupment"
            :key="index"
            class="checkbox__item"
        >
          <input
              type="checkbox"
              class="checkbox"
              :id="`checkbox${index}`"
          >
          <label :for="`checkbox${index}`">{{item}} рублей</label>
          <span style="opacity: 0.5">&ensp;в {{index+1}}-ый год</span>
        </div>
      </div>
      <div class="popup__selection">
        <span>Что уменьшаем?</span>
        <div>
          <button class="tags-active">Платеж</button>
          <button class="tags-notactive">Срок</button>
        </div>
      </div>
    </div>
      <button class="button-red">Добавить</button>
    </div>
  </div>
</template>

<script>

export default {
  name: "Popup",

  props: ['toVisible'],

  data() {
    return {
      activeCheckboxes: false,
      value: null,
      recoupment: [],
      err: false
    }
  },

  computed: {
    salary() {
      return +this.value
    }
  },

  methods: {
    doVisiblePopup() {
      this.toVisible()
    },

    doVisibleCheckboxes() {
      if (this.salary) {
        this.activeCheckboxes = true;
        this.calculateRecoupment();
      } else {
        this.err = true
      }
    },

    calculateRecoupment() {
      this.recoupment = [];
      let payment = this.salary * 12 * 0.13;
      let years = Math.floor(260000 / payment + 1);
      for (let i = 0; i < years-1; i++) {
        this.recoupment.push(payment);
      }
      let remainder = 260000 % payment;
      this.recoupment.push(remainder)
    }
  },

  watch: {
    salary() {
      this.err = false;
    }
  }
}
</script>

<style scoped>
.popup {
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: start;
  overflow: scroll;
}

.popup__wrap {
  display: flex;
  flex-direction: column;
  background-color: #fff;
  border-radius: 30px;
  width: 38vw;
  padding: 32px;
  margin-top: 120px;
}

.header__wrap {
  display: flex;
  justify-content: space-between;
  margin-bottom: 16px;
}

.header {
  font-family: 'Lab-Grotesque-Medium', sans-serif;
  font-size: 28px;
}

.close {
  position: relative;
}

.close__img {
  position: absolute;
  right: 10px;
  top: -14px;
}

.close__img:hover {
  cursor: pointer;
}

.close__img:before, .close__img:after {
  position: absolute;
  left: 10px;
  content: ' ';
  height: 18px;
  width: 2px;
  background-color: #EA0029;
}

.close__img:before {
  transform: rotate(45deg);
}

.close__img:after {
  transform: rotate(-45deg);
}

.popup__info {
  display: block;
  font-family: 'Lab-Grotesque-Light', sans-serif;
  font-size: 14px;
  color: #808080;
  line-height: 24px;
  margin-bottom: 24px;
}

.popup__input {
  font-family: 'Lab-Grotesque-Medium', sans-serif;
  font-size: 14px;
  display: flex;
  flex-direction: column;
  margin-bottom: 28px;
}

.popup__selection {
  font-family: 'Lab-Grotesque-Medium', sans-serif;
  font-size: 14px;
  margin-bottom: 40px;
  margin-top: 20px;
  display: flex;
  flex-direction: row;
}

.button-red {
  width: 100%;
}

.popup__checkboxes {
  font-family: 'Lab-Grotesque-Light', sans-serif;
  font-size: 14px;
}

.active {
  display: block;
}

.notactive {
  display: none;
}

.checkboxes__header {
  font-family: 'Lab-Grotesque-Medium', sans-serif;
  font-size: 14px;
}

.checkbox__item {
  border-bottom: 1px solid #DFE3E6;
  padding: 22px 0;
  display: flex;
  align-items: center;
}

.error {
  border: 1px solid #dc3131;
}

@media (max-width: 1200px){
  .popup__wrap {
    width: 58vw;
  }
}

@media (max-width: 650px) {
  .popup__selection {
    flex-direction: column;
  }

  .popup__selection button {
    margin: 10px 10px 10px 0;
  }
}

@media (max-width: 450px) {
  .popup {
    background-color: #fff;
  }

  .popup__wrap {
    margin-top: 0;
    border-radius: 0;
    width: 100vw;
    height: 100vh;
    justify-content: space-between;
  }

}
</style>