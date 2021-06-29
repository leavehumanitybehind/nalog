<template>
  <div class="reduce__wrapper">
  <span class="reduce__title">Что уменьшаем? </span>
  <div>
    <div class="btn__wrapper">
      <input type="radio" id="radio-1" name="radio" value="pay" checked />
      <label for="radio-1" class="reduce__btn"> Платёж</label>
    </div>

    <div class="btn__wrapper">
      <input type="radio" name="radio" id="radio-2" value="time" />
      <label for="radio-2" class="reduce__btn"> Срок </label>
    </div>
  </div>
  </div>
</template>
<script>
export default {
  name: "RadioButtons",
};
</script>
<style>
.reduce__wrapper {
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  margin-bottom: 40%;
}


.reduce__title {
  font-weight: bold;
  color: black;
  margin-bottom: 24px;
}

@media(min-width: 638px) {
    .reduce__wrapper {
flex-direction: row;  
align-items: center;
margin-bottom: 40px;
    }

    .reduce__title {
  margin-right: 35px;
}
}

.btn__wrapper {
  display: inline-block;
  margin-right: 10px;
}

.btn__wrapper input {
    display: none;
}

.btn__wrapper .reduce__btn {
  padding: 6px 12px;
  border-radius: 50px;
  cursor: pointer;
  background: #eef0f2;
  display: inline-block;
  user-select: none;
}

.btn__wrapper input:checked + .reduce__btn {
  background: linear-gradient(
      255.35deg,
      #dc3131 0.83%,
      rgba(255, 79, 79, 0) 108.93%
    ),
    #ff5e56;
    color: #ffffff;
}

.btn__wrapper .reduce__btn:hover {
  opacity: 0.7;
}
</style>
