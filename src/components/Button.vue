<template>
  <button :class="{'active-tab': activeTab}" :data-type="type">
    <slot/>
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    type: String,
    activeTab: Boolean
  }
};
</script>

<style lang="scss" scoped>
button {
  cursor: pointer;
  &[data-type="tab-buttons"] {
    height: 40px;
    color: #ffffff;
    font-size: 10px;
    border: 0;
    border-bottom: 3px solid #272727;
    background:#272727;
    transition: all 0.2s ease;
    flex-basis: 50%;

    &.active-tab {
      border-bottom: 3px solid #a672ff;
    }
  }
  &[data-type="down"] {
    width: 40px;
    height: 40px;
    background: #a672ff;
    border-radius: 50%;
    border: 0;
    position: absolute;
    margin: 0 auto;
    left: 0;
    right: 0;
    bottom: 20px;
  }
  &[data-type="new-message"] {
    width: 40px;
    height: 40px;
    background: #eb5d76;
    border-radius: 50%;
    border: 0;
    position: absolute;
    margin: 0 auto;
    left: 0;
    right: 0;
    bottom: 20px;
    color: #ffffff;
    font-weight: bold;
  }
}
</style>
