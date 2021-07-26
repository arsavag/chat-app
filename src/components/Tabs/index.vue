<template>
  <div class="tabs">
    <Button
      type="tab-buttons"
      v-for="(tab,index) in data"
      :key="tab.title"
      :active-tab="currentIndex === index"
      @click.native="toggleTab(index)"
      >
        {{tab.title}}
    </Button>
  </div>
</template>

<script>
import Button from '../Button';
import tabsData from './tabsData';
export default {
  name: "Tabs",
  components: {
    Button
  },
  data() {
    return {
      currentIndex: 0,
      data: [...tabsData]
    }
  },
  methods: {
    toggleTab: function(index) {
      this.currentIndex = index;
      this.$emit('currentIndex', this.currentIndex);
    },
  }
};
</script>

<style lang="scss" scoped>
div.tabs {
  width: 100%;
  display: flex;

}
</style>