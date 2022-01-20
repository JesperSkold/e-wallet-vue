<template>
	<main>
    <h1>E-WALLET</h1>
    <h5>ACTIVE CARD</h5>
    <CardList :cards="cards"/>
  </main>
</template>

<script>
import CardList from "../components/CardList.vue";
export default {
	components: {
    CardList
  },
  props: {
    cards: Array
  }
};
</script>

<style lang="scss" scoped>
main{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  h5{
    margin: 0;
    padding: 0;
  }
}
</style>
