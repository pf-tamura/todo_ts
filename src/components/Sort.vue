<template>
  <div>
    <h3>並び変え</h3>
    <label v-for="sort in sorts" class="bbb" v-bind:key="sort.value">
      <input
        type="radio"
        v-model="select"
        v-bind:value="sort.value"
        v-on:click="s_select(sort.value)"
      />
      {{ sort.type }}
    </label>
    <span></span>
  </div>
</template>

<script lang="ts" type="module">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";

@Component
export default class Sort extends Vue {
  @Prop() select!: number;
  sorttodo: any[] = [];
  sorts: Object[] = [
    { value: 0, type: "id順" },
    { value: 1, type: "id順(降順)" },
    { value: 2, type: "完了日順" },
    { value: 3, type: "完了日順(降順)" },
    { value: 4, type: "アルファベット順" },
    { value: 5, type: "アルファベット降順" }
  ];

  @Emit()
  s_select(select: number): number {
    return select;
  }
}
</script>