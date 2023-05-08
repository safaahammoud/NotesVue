<script lang="ts" setup>
  const today = new Date().toLocaleString();
</script>

<template>
  <div class="card">
    <slot></slot>

    <slot name="date">{{ today }}</slot>
  </div>
</template>


<style lang="css" scoped>
.card {
  width: 225px;
  min-height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  margin-right: 20px;
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow-wrap: break-word;
}
</style>