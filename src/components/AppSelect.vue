<template>
    <div class="select-block">
        <div class="select-block__title" @click="areOptionsVisible = !areOptionsVisible">{{selected}}</div>
        <ul class="select-block__list" v-if="areOptionsVisible">
            <li v-for="option in options" :key="option.value">
                <a href="#" @click.prevent="selectOption(option)">{{option.name}}</a>
            </li>
        </ul>
        <input class="select-block__input" type="hidden" value="Россия">
    </div>
</template>

<script>
    export default {
        name: "AppSelect",
        data() {
          return{
              areOptionsVisible: false
          }
        },
        props: {
            options: {
                type: Array,
                default() {
                    return []
                }
            },
            selected: {
                type: String,
                default() {
                    return '';
                }
            },
        },
        methods: {
            selectOption(option){
                this.$emit('select', option);
            },
            hideSelect(){
                this.areOptionsVisible = false;
            }
        },
        mounted(){
            document.addEventListener('click', this.hideSelect.bind(this), true)
        },
        beforeUnmount(){
            document.removeEventListener('click', this.hideSelect);
        }
    }
</script>

<style>
    .select-block {
        display: inline-block;
        position: relative;
    }
    .select-block.active {
        z-index: 10;
    }
    .select-block__title {
        width: 170px;
        height: 40px;
        line-height: 38px;
        padding: 0 22px 0 10px;
        border-radius: 5px;
        border: 1px solid #ccc;
        background-color: #fff;
        font-size: 14px;
        position: relative;
        cursor: pointer;
        z-index: 1;
    }
    .select-block__title:after {
        content: '';
        display: block;
        width: 0;
        height: 0;
        border-style: solid;
        border-width: 4px 3.5px 0 3.5px;
        border-color: #333 transparent transparent transparent;
        position: absolute;
        top: 50%;
        margin-top: -2px;
        right: 10px;
        transition: all 0.2s ease-in-out;
    }
    .select-block__title.active:after {
        transform: rotate(180deg);
    }
    .select-block__title span {
        overflow: hidden;
        white-space: nowrap;
        display: inline-block;
        width: 100%;
    }
    .select-block__list {
        background-color: #fff;
        position: absolute;
        top: 20px;
        left: 0;
        border-radius: 0 0 5px 5px;
        border: 1px solid #ccc;
        margin: 0;
        padding: 20px 0 5px;
        list-style: none;
        width: calc(100% - 2px);
        max-height: 200px;
        overflow-y: auto;
    }
    .select-block__list li a {
        display: block;
        color: #333;
        padding: 5px 10px;
        text-decoration: none;
    }
    .select-block__list li a:hover {
        background-color: #e3e3e3;
    }
</style>