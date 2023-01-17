<template>
    <div class="category-menu" >
        <ul>
            <li v-for="category in categoryList" :key="category.id" @click="onCategoryClick(category.id)" :class="{'active': isActive(category.id)}">
                <component :is="category.icon"/>
                <p>{{ category.label }}</p>
            </li>
        </ul>
    </div>
</template>

<script>

import Pizza from '../assets/icons/pizza.svg';
import Combo from '../assets/icons/french-fries.svg';
import Deserts from '../assets/icons/ice-cream.svg';
import Drinks from '../assets/icons/smothie.svg';
import Burguer from '../assets/icons/food.svg';

export default{
    name: 'CategoryMenu',
    components:{
        Pizza, 
        Combo,
        Deserts,
        Drinks,
        Burguer,
    },
    data(){
        return{
            categoryList:[
                {label: 'Pizza', icon: 'Pizza', id:'pizza'},
                {label: 'Combos', icon: 'Combo', id:'combo'},
                {label: 'Doces', icon: 'Deserts', id:'deserts'},
                {label: 'Bebidas', icon: 'Drinks', id:'drinks'},
                {label: 'Burguers', icon: 'Burguer', id:'burguers'}
            ],
            selectedCategory: ''
        }
    },
    mounted(){
        this.onCategoryClick('pizza');
    },
    methods: {
        onCategoryClick(id){
            this.selectedCategory = id;
            this.$store.dispatch('changeCategory', id)
        },
        isActive(id){
            return this.selectedCategory === id;
        }
    }
}
</script>

<style lang="less" scoped>

.category-menu{
    width: 130px;
    height: 100vh;
    background: white;

    display: flex;
    align-items: center;

    ul{
        list-style: none;
        padding: 0;
        width: 100%;

        li{
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 102px;
            padding: 0;
            cursor: pointer;
            
            &:hover{
                p{
                    color: @yellow;
                    transition: .3s ease-in-out;
                }
                svg{
                    path{
                        fill: @yellow;
                        transition: .3s ease-in-out;
                    }
                }
            }

            p{
                margin-bottom: 0;
                margin-top: 8px;
                font-weight: 500;
                font-size: 14px;
                color: @dark-grey;
            }

            &.active{
                background: @yellow;
                border-radius: 8px;

                p{
                    color: @pink;
                }

                svg{
                    path{
                        fill: @pink;
                    }
                }
            }

            svg{
                path{
                    fill: @dark-grey;
                }
            }
        }
    }

    @media @tablets{
        width: 100%;
        height: fit-content;

        ul{
            display: flex;
            justify-content: start;
            margin: 8px;
            overflow: scroll;

            li{
                min-width: 78px;
            }
        }
    }
}

</style>