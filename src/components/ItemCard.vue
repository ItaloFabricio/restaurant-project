<template>
    <div class="item" @click="addToCart">
        <div class="container">
            <div class="item--tag" v-if="item.offer">Oferta</div>
            <img class="item--img" :src="imagePath" alt="">
        </div>
      <div class="content">
          <h2 class="item--name">{{item.name}}</h2>
          <p class="item--description" >{{item.description}}</p>
          <p class="item--price">{{ item.price | currency }}</p>
      </div>
    </div>
</template>

<script>



export default {
    name: 'ItemCard',
    filters:{
        currency(value){
            return `R$ ${value.toLocaleString('pt-br', {minimumFractionDigits: 2})}`
        }
    },
    props:{
        item:{}
    },
    computed:{
        imagePath(){
            return require(`../assets/images/${this.item.id}.png`);
        }
    },
    methods:{
        addToCart(){
            this.$store.dispatch('addToCart', this.item);
        }
    }
};

</script>

<style lang="less" scoped>

    .item{
        width: 216px;
        height: 290px;
        border-radius: 8px;
        background: white;
        box-shadow: rgba(202, 204, 205, 0.2) 0px 8px 24px;
        position: relative;
        margin: 20px;
        padding: 20px;
        cursor: pointer;

        display: flex;
        flex-direction: column;
        transition: .4s ease-in-out;

        &:hover{
            box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
        }

        &--tag{
            position: absolute;
            background: @pink;
            border-radius: 8px;
            color: white;
            top: 15px;
            right: 15px;
            font-weight: 500;
            font-size: 12px;
            padding: 3px 8px;
        }

        img{
            display: block;
            width: 100%;
            margin: auto;
        }

        &--name{
            font-weight: 600;
            font-size: 18px;
            margin: 0;
        }

        &--description{
            color: @dark-grey;
            font-weight: 300;
            font-size: 12px;
            margin: 0;
        }

        &--price{
            font-weight: 600;
            font-size: 18px;
            color: @yellow;
            margin: 0;
        }

        .content{
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            margin-top: 10px;
        }

        @media @tablets{
            width: 100%;
            height: fit-content;
            border: 1px solid @light-grey;
            display: flex;
            flex-direction: row;
            margin: 10px 0;
            padding: 10px 20px;

            .item--img{
                width: 86px;
                order: 1;
                margin: 0 0 10px 0; 
            }

            &--price{
                text-align: right;
                margin: 5px 0 0 auto;
            }

            &--tag{
                position: static;
                order: 2;
                width: fit-content;
            }

            .content{
                flex-grow: 1;
            }

            .container{
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;
                margin-right: 10px;
            }
        }
    }

   

</style>