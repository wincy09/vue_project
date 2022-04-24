<template>
  <div class="list-view">
    <BigList></BigList>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import BigList from "@/components/list/BigList.vue"; // @ is an alias to /src

@Component({
  components: {
    BigList,
  },
})
export default class ListView extends Vue {}
</script>
<style scoped lang="scss">
.list-view {
  min-width: 650px;
}
</style>
