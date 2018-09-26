<template>
    <div class="search" v-on:mouseenter="focusInput">
      <i class="icon fas fa-search"/>
      <form v-on:submit.prevent="onSubmit">
          <input type="text" class="input" ref="input" v-model="search"/>
      </form>
      <item  v-for="item in results" v-bind:key="item.id" v-bind:title="item.title" />
    </div>
</template>

<script>
import ResultItem from './ResultItem';
const TODO_API = 'https://jsonplaceholder.typicode.com/todos';
export default {
    data: function(){
        return{
            search:'',
            results: []
        }
    },
    components:{
        item : ResultItem,
    },
    methods: {
      focusInput() {
        console.log('DEBUG');
        this.$refs.input.focus();
    },
    unfoucusInput(){
        this.$refs.input;blur();
    },
    onSubmit(){
        fetch(TODO_API)
          .then(res => res.json())
          .then(json => json.filter(el => el.title.indexOf(this.search) >= 0))
          .then((results) => {this.results = results;});
    },
  },
};
</script>

<style>
    .search {
        max-width: 40px;
        background: #FFF;

        padding: 12px;

        border-radius:5px;
        transition: 500ms ease-in-out;
    }

    .search:hover {
        max-width: 200px;
    }
    .icon {
        color: #0663DF;
    }

    .input{
        display: inline-block;
        width: 0px;
        

        outline:none;

        border: none;
        border-bottom: 1px solod black;
        transition: 450ms ease-in-out;

        caret-color: #76A7F6;
        color: #76A7F6;
    }
    form{
        display: inline;
    }

    .search:hover .input{
        width: calc(100% - 22px);
    }
</style>
