<template>
  <div class="item">
    <div class="item--quantity">
        <button class="buttons" @click="decreaseQuantity(item.id)" :disabled="item.quantity === 0">-</button>
        <span class="number">{{ item.quantity }}</span>
        <button class="buttons" @click="increaseQuantity(item.id)">+</button>
    </div>
    <div class="item--img--container">
        <img class="item--img" :src="imagePath">
    </div>
    <div class="content">
        <h1 class="item--name">{{ item.name }}</h1>
        <a class="item--observation">Adicionar observação</a>
    </div>
    <p class="item--price">{{ item.price | currency }}</p>
  </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
    name: 'CartItem',
    props:{
        item: {}
    },
    filters:{
        currency(value){
            return `R$ ${value.toLocaleString('pt-br', {minimumFractionDigits: 2})}`
        }
    },
    computed:{
        imagePath(){
            return require(`../assets/images/${this.item.id}.png`)
        }
    },
    methods:{
        ...mapActions([
            'increaseQuantity',
            'decreaseQuantity'
        ])
    }
    
}
</script>

<style lang="less" scoped>
    .item{
        display: flex;
        padding: 20px 0;
        border-bottom: 1px solid @light-grey;

        &--quantity{
            display: flex;
            align-items: center;
            padding-right: 40px;

            .number{
                font-size: 18px;
                font-weight: 500;
                color: @yellow;
                width: 28px;
                text-align: center;
            }


            .buttons{
                font-weight: 600;
                font-size: 18px;
                cursor: pointer;
                background: none;
                border: 0;

                &:focus{
                    outline: 0;
                }
            }
        }

        &--img--container{
            border-radius: 9px;
            background: @light-yellow;
            width: 81px;
            height: 66px;
            display: flex;
            align-items: center;
        }

        &--img{
            width: 100%;
            display: block;
            margin: auto;
        }

        &--name{
            font-weight: 600;
            font-size: 18px;
            margin: 0;
        }

        &--observation{
            font-weight: 500;
            font-size: 12px;
            color: @dark-grey;
            text-decoration: underline;
        }

        .content{
            flex-grow: 1;
            padding: 0 20px;
        }

        &--price{
            font-weight: 600;
            font-size: 18px;
            line-height: 27px;
            color: @yellow;
        }
    }

</style>