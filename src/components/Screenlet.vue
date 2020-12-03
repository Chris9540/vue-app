<template>
  <div class="screenlet">
      <slot>
        Empty Screenlet
      </slot>
  </div>
</template>

<script>
export default {
  name: "Screenlet"
};
</script>
<style scoped>
.screenlet {
  width: 90%;
  margin: 20px 5%;
  background: #444;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  min-height: 64px;
}

</style>
