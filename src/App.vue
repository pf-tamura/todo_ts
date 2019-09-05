<template>
  <div id="app">
    <Header v-on:scurrent="current = $event" :counter="todos.length"></Header>
    <Main
      class="main"
      :computedTodos="computedTodos"
      v-on:state="doChangeState($event)"
      v-on:id="SortByItem($event)"
      v-on:remove="doRemove($event)"
    ></Main>
    <Sort v-on:sselect="select = $event" :select="select"></Sort>
    <Form v-on:notify="todos = $event"></Form>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import Main from "./components/Main.vue";
import Sort from "./components/Sort.vue";

@Component({
  components: {
    Header,
    Form,
    Main,
    Sort
  }
})
export default class App extends Vue {
  count: number = 10;
  todos: any[] = [];
  current: number = -1;
  select: number = 0;

  get computedTodos(): any[] {
    const self = this;
    const list: any[] = this.todos.filter(function(el: any) {
      return self.current < 0 ? true : self.current === el.state;
    }, this);

    list.sort(function(a, b): any {
      switch (self.select) {
        case 0:
          return a.id < b.id ? -1 : 1;
        case 1:
          return a.id < b.id ? 1 : -1;
        case 2:
          return a.dateEnd < b.dateEnd ? -1 : 1;
        case 3:
          return a.dateEnd < b.dateEnd ? 1 : -1;
        case 4:
          return a.Comment < b.Comment ? -1 : 1;
        case 5:
          return a.Comment < b.Comment ? 1 : -1;
      }
    });

    return list;
  }

  doChangeState(item: any): void {
    item.state = !item.state ? 1 : 0;

    if (item.state === 1) {
      item.dateEnd = new Date().getTime();
      return;
    }
    item.dateEnd = -1;
  }

  doRemove(item: any): void {
    var index = this.todos.indexOf(item);
    this.todos.splice(index, 1);
  }

  SortByItem(item: any): void {
    let select = this.select;
    switch (item) {
      case 0:
        if (select === 0) this.select = 1;
        else this.select = 0;
        break;
      case 1:
        if (select === 4) this.select = 5;
        else this.select = 4;
        break;
      case 4:
        if (select === 2) this.select = 3;
        else this.select = 2;
        break;
    }
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.main {
  text-align: center;
  margin-left: 500px;
}
</style>
