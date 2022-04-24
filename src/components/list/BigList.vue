<template>
  <div>
    <div class="bigList">
      <div
        v-for="itemData in itemDatas"
        :key="itemData.id"
        class="big-list-item"
        v-bind:class="{ close: itemData.isHidden }"
      >
        <ListItem
          v-bind:id="itemData.id"
          :name="itemData.name"
          :isHidden="itemData.isHidden"
          :itemDatas="itemDatas"
          @clickOpen="clickOpen"
          @clickClose="clickClose"
          @clickDelete="clickDelete"
          @clickInsert="clickInsert"
        ></ListItem>
      </div>
    </div>
    <button @click="clickAdd" class="add-button">增加</button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import ListItem from "@/components/list/ListItem.vue"; // @ is an alias to /src

@Component({
  components: {
    ListItem,
  },
  data() {
    return {
      maxId: 2,
      itemDatas: [
        { id: 1, name: "333", isHidden: true },
        { id: 2, name: "333444", isHidden: false },
      ],
    };
  },
  methods: {
    clickOpen(val) {
      (this as any).itemDatas.forEach((element: any) => {
        if (element.id === val) {
          return (element.isHidden = false);
        }
      });
    },
    clickClose(val) {
      (this as any).itemDatas.forEach((element: any) => {
        if (element.id === val) {
          return (element.isHidden = true);
        }
      });
    },
    clickDelete(val) {
      (this as any).itemDatas.forEach((element: any, number: number) => {
        if (element.id === val) {
          (this as any).itemDatas.splice(number, 1);
        }
      });
      console.log((this as any).itemDatas);
    },
    clickAdd() {
      (this as any).itemDatas.push({
        id: (this as any).maxId + 1,
        name: "name",
        isHidden: false,
      });
      (this as any).maxId += 1;
      console.log((this as any).itemDatas);
    },
    clickInsert(val) {
      try {
        (this as any).itemDatas.forEach((element: any, number: number) => {
          if (element.id === val) {
            (this as any).itemDatas.splice(number, 0, {
              id: (this as any).maxId + 1,
              name: (this as any).maxId + 1,
              isHidden: false,
            });
            throw new Error("End Loop");
          }
        });
      } catch (e: any) {
        (this as any).maxId += 1;
        console.log((this as any).itemDatas);
        return;
      }
    },
  },
})
export default class BigList extends Vue {}
</script>
<style scoped lang="scss">
.bigList {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  width: 100%;
}
.big-list-item {
  width: 100%;
}
.big-list-item.close {
  display: inline-block;
  width: 7%;
}
.add-button {
  margin: 30px;
  width: 80%;
}
</style>
