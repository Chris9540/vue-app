<template>
  <div class="screenlet">
    <div class="screenlet-body">
      <slot>
        Empty Screenlet
      </slot>
    </div>
    <div class="overlay" v-if="loading">
      <div class="loader"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Screenlet",
  props: {
    loading: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
};
</script>
<style scoped>
.screenlet {
  width: 90%;
  margin: 20px 5%;
  background: lightblue;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  min-height: 64px;
}
.overlay,
.screenlet-body {
  grid-column: 1/2;
  grid-row: 1/2;
}
.overlay {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
}
.screenlet-body {
  width: 100%;
  height: 100%;
}

.loader {
  border: 4px solid lightgray;
  border-top: 4px solid darkgray;
  border-radius: 50%;
  width: 28px;
  height: 28px;
  animation: spin 1s linear infinite;
  margin: auto;
}
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
