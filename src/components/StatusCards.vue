<template>
  <div class="wrapper">
    <div class="text-wrap">
      <div class="text-class">{{ heading }}</div>
      <div class="number-class">{{ statNumber }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    heading: String,
    statNumber: Number,
  },
  setup(props) {},
};
</script>

<style scoped>
.wrapper {
  height: 150px;
  width: 150px;
  background: white;
  border-radius: 10px;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  color: black;
  margin: 10px;
  padding: 15px;
}
.wrapper:nth-child(1) {
  background: #224c98;
  color: white;
}
.text-class {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 40px;
}
.number-class {
  font-size: 36px;
  font-weight: bold;
}
.text-wrap {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
</style>
