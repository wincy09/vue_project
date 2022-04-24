<template>
  <div class="itemList">
    <button v-if="isHidden" v-on:click="clickOpen">展开</button>
    <div v-if="!isHidden" class="item-detail">
      <div class="item-detail-name">{{ name }}</div>
      <div class="item-action">
        <button @click="clickInsert">插入</button>
        <button @click="clickClose">折叠</button>
        <button @click="clickDelete">删除</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class ListItem extends Vue {
  @Prop() private id: number | undefined;
  @Prop() private name: string | undefined;
  @Prop() private isHidden!: boolean;
  @Prop() private itemDatas!: any;

  public clickOpen() {
    this.$emit("clickOpen", this.id);
  }
  public clickClose() {
    console.log("233");
    this.$emit("clickClose", this.id);
  }
  public clickDelete() {
    console.log("233");
    this.$emit("clickDelete", this.id);
  }
  public clickInsert() {
    console.log("233");
    this.$emit("clickInsert", this.id);
  }
}
</script>

<style scoped lang="scss">
.itemList {
  position: relative;
  width: 100%;
  display: flex;
  justify-content: flex-start;
}
.item-detail {
  margin: 20px 0;
  border: 1px solid black;
  display: flex;
  flex-direction: row;
  min-height: 100px;
  width: 100%;
}
.item-detail-name {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.item-action {
  min-height: 100px;
  right: 10px;
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  button {
    display: block;
  }
}
</style>
