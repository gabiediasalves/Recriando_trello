<template>
  <div class="cardView">
    <slot/>
  </div>
</template>

<script>
export default{
  name: 'cardView'
}
</script>

<style scoped>
.cardView{
  background: var(--color-white);
  padding: 1.4rem;
  border-radius: 0.4rem;
  box-shadow: 0 1px 0 rgba(9, 30, 66, 0.25);
  font-size: 1.6rem;
  margin-bottom: 0.8rem;
  cursor: pointer;
}
</style>