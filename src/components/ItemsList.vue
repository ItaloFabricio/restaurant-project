<template>
    <div class="items-list">
      <ItemCard 
        v-for="item in itemsList" :key="item.id"
        :item="item"
      />
    </div>
</template>

<script>

// eslint-disable-next-line no-unused-vars
import axios from 'axios';
import ItemCard from './ItemCard.vue';

export default {
    name: 'ItemsList',
    components:{
      ItemCard
    } ,  
    data() {
        return {
            itemsList: []
        }
    },
    created() {
        axios.get('http://localhost:3000/burguers').then((response) => {
            this.itemsList = response.data;
        });
    }
};

</script>

<style lang="less" scoped>

  .items-list{
    margin: 50px;
    display: flex;

    @media @tablets{
      flex-wrap: wrap;
      margin: 20px;
    }
  }

</style>