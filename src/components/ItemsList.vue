<template>
    <div class="items-list">
      <LoadingScreen />
      <ItemCard 
        v-for="item in itemsList" :key="item.id"
        :item="item"
      />
    </div>
</template>

<script>

import axios from 'axios';
import ItemCard from './ItemCard.vue';
import LoadingScreen from './LoadingScreen.vue';

export default {
    name: 'ItemsList',
    components:{
      ItemCard,
      LoadingScreen
    } ,  
    data() {
        return {
            itemsList: []
        };
    },
    created() {},
    computed: {
        selectedCategory: {
            get() {
                return this.$store.state.selectedCategory;
            }
        }
    },
    methods: {
        getItemsList() {
            axios.get(`http://localhost:3000/${this.selectedCategory}`).then((response) => {
                this.itemsList = response.data;
            });
        }
    },
    watch: {
        selectedCategory() {
            this.getItemsList();
        }
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