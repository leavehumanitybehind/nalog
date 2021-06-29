<template>
  <div class="card__wrapper">
    <div class="card">
      <button class="close__btn" @click="$emit('close')"></button>
      <h2 class="card__title">Налоговый вычет</h2>
      <p class="card__desc">
        Используйте налоговый вычет чтобы погасить ипотеку досрочно. Размер
        налогового вычета составляет не более 13% от своего официального
        годового дохода.
      </p>
      <Form @pay="onPayments" />
      <form id="form" @submit.prevent="sendForm">
        <div v-if="pays.length" class="card__list">
          <p class="card__notification">
            Итого можете внести в качестве досрочных:
          </p>
          <div v-for="(pay, index) in pays" :key="index" class="card__item">
            <input
              type="checkbox"
              name="checkbox"
              class="checkbox"
              :id="index"
              checked
            />
            <label :for="index" class="label">
              {{ format(pay) }} рублей
              <span class="year__pay">
                в {{ index + 1 + declOfNum(index + 1) }} год
              </span>
            </label>
          </div>
        </div>
        <RadioButtons />
        <button type="submit" class="add__btn">Добавить</button>
      </form>
    </div>
  </div>
</template>
<script>
import Form from "./Form.vue";
import RadioButtons from "./RadioButtons.vue";
export default {
  name: "Card",
  props: ["isMain"],
  components: { Form, RadioButtons },
  data() {
    return {
      pays: "",
      alert: false,
      titles: ["-ый", "-ой", "-ий"],
    };
  },
  methods: {
    onPayments(data) {
      this.pays = data.payments;
    },
    format: function (num) {
      return num
        .toString()
        .split(/(?=(?:\d{3})+(?:\.|$))/g)
        .join(" ");
    },
    sendForm() {
      console.log(this.checked);
    },
    declOfNum: function (num) {
      const value = Math.abs(num) % 100;
      let numb = value % 10;
      if (value == 3) return this.titles[2];
      if (numb == 2 || (numb >= 6 && numb <= 9)) return this.titles[1];
      if (numb == 1) return this.titles[0];
      return this.titles[0];
    },
  },
};
</script>
<style>
.card__item {
  border-bottom: 1px solid #dfe3e6;
}

.card__notification {
  font-weight: bold;
  font-size: 14px;
  line-height: 24px;
  margin: 16px 0;
}

.card__wrapper {
  width: 100%;
  background: #f1f1f1;
}
button {
  cursor: pointer;
  background: inherit;
  border: none;
}

.card {
  background: #ffffff;
  padding: 16px 32px;
  text-align: left;
  font-weight: normal;
  font-size: 14px;
  line-height: 24px;
  position: relative;
  min-height: 100%;
}
.card__title {
  font-weight: bold;
  font-size: 28px;
  line-height: 40px;
  margin-bottom: 16px;
}

.card__desc {
  color: #808080;
  margin-bottom: 24px;
  font-weight: normal;
  font-size: 12px;
  line-height: 16px;
}

.add__btn {
  background: linear-gradient(
      255.35deg,
      #dc3131 0.83%,
      rgba(255, 79, 79, 0) 108.93%
    ),
    #ff5e56;
  box-shadow: 0px 0px 24px rgba(234, 0, 41, 0.33);
  border-radius: 6px;
  color: white;
  font-size: 16px;
  padding: 16px 0;
  position: absolute;
  bottom: 3%;
  left: 0;
  right: 0;
  margin: auto;
  width: 90%;
}

.close__btn {
  position: absolute;
  right: 10%;
  top: 3%;
}

.close__btn::after {
  content: "";
  position: absolute;
  width: 18px;
  height: 18px;
  background: url("../assets/close.svg") no-repeat center center;
}

@media (min-width: 668px) {
  .card__wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5% 0;
  }

  .card {
    border-radius: 30px;
    max-width: 552px;
    padding: 32px;
    min-height: auto;
    margin: auto;
  }

  .card__title {
    font-size: 18px;
    line-height: 24px;
  }
  .card__desc {
    font-size: 14px;
    line-height: 24px;
  }

  .add__btn {
    width: 100%;
    position: static;
    text-align: center;
  }

  .close__btn {
    top: 7%;
  }

  .close__btn::after {
    width: 30px;
    height: 30px;
  }
}

.add__btn:hover {
  background: #ea0029;
}
.add__btn:active {
  background: #ea0029;
  box-shadow: 0px 0px 24px rgba(234, 0, 41, 0.33);
}
.add__btn:disabled {
  background: #bec5cc;
}

.close__btn:hover::after,
.close__btn:active::after {
  opacity: 0.6;
}

.checkbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
}
.checkbox + .label {
  display: inline-flex;
  align-items: center;
  user-select: none;
  position: relative;
  padding: 16px 0;
}
.checkbox + .label::before {
  content: "";
  display: inline-block;
  width: 20px;
  height: 20px;
  border: 1px solid #d8d8d8;
  margin-right: 12px;
  border-radius: 6px;
}

.checkbox:checked + .label::before {
  background-position: center;
  border-color: inherit;
}

/* стили при наведении курсора на checkbox */
.checkbox:not(:disabled):not(:checked) + .label:hover::after {
  left: 1px;
}
/* стили для активного состояния чекбокса (при нажатии на него) */
.checkbox:not(:disabled):checked + .label::before {
  background-image: url("../assets/mdi_done.svg");
  background-repeat: no-repeat;
  border: none;
  width: 22px;
  height: 22px;
}
/* стили для чекбокса, находящегося в фокусе */
.checkbox:hover + .label::before {
  border-color: black;
}
/* стили для чекбокса, находящегося в фокусе и не находящегося в состоянии checked */
.checkbox:focus:not(:checked) + .label::before,
.checkbox:hover:not(:checked) + .label::before {
  border-color: black;
}
/* стили для чекбокса, находящегося в состоянии disabled */
.checkbox:disabled + .label::before {
  background-image: url("../assets/mdi_disabled.svg");
}

.year__pay {
  opacity: 0.7;
}
</style>
