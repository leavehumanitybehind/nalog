<template>
  <form
    class="card__form"
    @submit.prevent="calculatePay()"
    :class="{ 'form-group--error': $v.salary.$error }"
  >
    <label> Ваша зарплата в месяц</label>
    <input
      v-model.lazy="$v.salary.$model"
      placeholder="Введите данные"
      @blur="$v.salary.$touch()"
    />
    <div v-if="$v.salary.$error">
      <span class="error" v-if="!$v.salary.required">
        Это поле обязательно к заполнению
      </span>
      <span class="error" v-if="!$v.salary.minValue">
        Некорректные данные
      </span>
    </div>

    <button type="submit">Рассчитать</button>
  </form>
</template>
<script>
import Vue from "vue";
import Vuelidate from "vuelidate";
import { required, integer, minValue } from "vuelidate/lib/validators";
Vue.use(Vuelidate);
export default {
  name: "Form",
  data() {
    return {
      salary: "",
      payments: "",
    };
  },
  validations: {
    salary: {
      required,
      integer,
      minValue: minValue(1),
    },
  },
  methods: {
    calculatePay() {
      this.payments = [];
      const flatPrice = 2000000;
      const year = 12;
      const tax = 0.13;
      const yearTax = this.salary * year * tax;
      const maxTax = flatPrice < 2000000 ? flatPrice * tax : 260000;
      let sum = yearTax;

      if (!this.$v.$invalid) {
        if (yearTax > maxTax) {
          this.payments.push(maxTax);
        } else {
          for (let i = 1; i <= 4; i++) {
            if (maxTax - sum <= yearTax) {
              let remainingPay = maxTax - sum;
              this.payments.push(Math.round(remainingPay));
            } else {
              this.payments.push(Math.round(sum / i));
              sum = sum + yearTax;
            }
          }
        }
        this.pay();
      }
    },
    pay() {
      this.$emit("pay", { payments: this.payments });
    },
  },
};
</script>
<style>
.alert {
  font-size: 12px;
}

.card__form {
  display: flex;
  flex-direction: column;
}
.card__form input {
  padding: 10px;
  border: 1px solid #bec5cc;
  outline: none;
}

.card__form input::placeholder {
  color: #bec5cc;
}
.card__form input:hover {
  border-color: black;
}

.card__form input:active {
  border-color: #dfe3e6;
}

.card__form input:disabled {
  border-color: #808080;
}

.form-group--error input {
  border: 1px solid #ea0029;
}

.error {
  color: #ea0029;
  font-weight: normal;
  font-size: 10px;
  line-height: 12px;
}

.card__form label {
  font-weight: bold;
  margin-bottom: 8px;
}

.label span {
  padding-left: 5px;
}

.card__form button {
  max-width: 76px;
  color: #ea0029;
  margin: 8px 0 24px;
  font-weight: bold;
}

.card__form button:hover {
  color: #f53a31;
}

.card__form button:active {
  color: #ea0029;
}
</style>
