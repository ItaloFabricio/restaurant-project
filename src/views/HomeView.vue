<template>
  <div class="home">
    <CategoryMenu />
    <ItemsList />
    <CartShop v-if="isDesktop()"/>
  </div>
</template>

<script>
// @ is an alias to /src
import CategoryMenu from '@/components/CategoryMenu.vue'
import ItemsList from '@/components/ItemsList.vue';
import CartShop from '@/components/CartShop.vue';
import Mixin from '@/mixins/mixins';


export default {
  name: 'HomeView',
  components: {
    CategoryMenu,
    ItemsList,
    CartShop
  },
  mixins: [Mixin]
}

</script>

<style lang="less" scoped>

  .home{
    display: flex;

    @media @tablets{
      flex-direction: column;
    }
  }

</style>


