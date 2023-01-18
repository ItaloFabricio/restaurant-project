<template>
    <div class="items-list">
      <LoadingScreen v-if="isLoading" />
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
            itemsList: [],
            isLoading: false,
        };
    },
    created() {},
    computed: {
        selectedCategory() {          
                return this.$store.state.selectedCategory;        
        }
    },
    methods: {
        getItemsList() {
            this.isLoading = true;
            this.itemsList = [];
            setTimeout( () => {
                axios.get(`http://localhost:3000/${this.selectedCategory}`).then((response) => {
                    this.itemsList = response.data;
                    this.isLoading = false;
                });
            }, 500);
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
    width: 100%;
    flex-wrap: wrap;

    @media @tablets{
      flex-wrap: wrap;
      margin: 0;
      padding: 20px;
    }
  }

</style>