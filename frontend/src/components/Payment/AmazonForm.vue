<template>
  <div class="card-form">
    <div class="col-md-10 m-4">
      <div class="card-input">
        <label for="cardNumber" class="card-input__label">
          Pay amount
        </label>
        <input
          :value="amount"
          autofocus
          id="cardNumber"
          class="card-input__input"
          autocomplete="off"
        />
      </div>
      <button @click="submitCard" class="card-form__button">
        Pay by Amazon
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      amount:1000
    };
  },
  methods: {
    submitCard() {
      alert(`
        ${this.cardNumber}\n
        ${this.name}\n
        ${this.expireMonth}/${this.expireYear}\n
        ${this.cvv}`);
    },
  },
};
</script>

<style scoped lang="scss">
.card-container {
  margin: 30px auto 50px auto;
}

.card-form {
  max-width: 570px;
  margin: auto;
  width: 100%;

  &__inner {
    background: #fff;
    box-shadow: 0 30px 60px 0 rgba(90, 116, 148, 0.4);
    border-radius: 10px;
    padding: 20px;
  }

  &__row {
    display: flex;
    align-items: flex-start;
  }

  &__col {
    flex: auto;
    margin-right: 15px;

    &:last-child {
      margin-right: 0;
    }

    &.-cvv {
      max-width: 150px;
    }
  }

  &__group {
    display: flex;
    align-items: flex-start;
    flex-wrap: wrap;

    .card-input__input {
      flex: 1;
      margin-right: 15px;

      &:last-child {
        margin-right: 0;
      }
    }
  }

  &__button {
    width: 100%;
    height: 55px;
    background: #38a294;
    border: none;
    border-radius: 5px;
    font-size: 22px;
    font-weight: 500;
    box-shadow: 3px 10px 20px 0px rgba(35, 100, 210, 0.3);
    color: #fff;
    margin-top: 20px;
    cursor: pointer;

    &:hover {
      background: darken(#38a294, 5%);
    }
  }
}

.card-input {
  margin-bottom: 20px;
  &__label {
    margin-bottom: 5px;
    color: #1a3b5d;
    width: 100%;
    display: block;
    text-align: left;
  }
  &__input {
    width: 100%;
    height: 40px;
    border-radius: 5px;
    box-shadow: none;
    border: 1px solid #ced6e0;
    transition: all 0.3s ease-in-out;
    font-size: 18px;
    padding: 5px 15px;
    background: none;
    color: #1a3b5d;

    &:hover,
    &:focus {
      border-color: #38a294;
    }

    &:focus {
      box-shadow: 0px 10px 20px -13px rgba(32, 56, 117, 0.35);
    }
    &.-select {
      -webkit-appearance: none;
      background-image: url("/img/select.png");
      background-size: 12px;
      background-position: 90% center;
      background-repeat: no-repeat;
      padding-right: 30px;
    }
  }
}
</style>