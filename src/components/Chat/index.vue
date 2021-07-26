<template>
  <div class="chat">
    <ul>
      <li
        v-for="(item,index) in chatData.slice(0, count)"
        :key="`${item.message}-${index}`">
          <div data-name="item-header">
            <p>{{item.name}}</p>
            <p>{{item.createdAt}}</p>
          </div>
          <p data-name="message">{{item.message}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import chatData from './chatData.json';
export default {
  name: "Chat",
  props: {
    newMessage: Number
  },
  data() {
    return {
      chatData: [...chatData],
      count: 12,
    }
  },
  mounted: function() {
    setInterval(() => {
      this.count++;
      this.newMessage++;
      this.$emit('newMessageLength', this.newMessage);
    }, 5000);
  },
};
</script>

<style lang="scss" scoped>
div.chat {
  width: 100%;
  height: 100%;
  position: relative;
  ul {
    padding: 0;
    margin: 0;
    width: 100%;
    list-style-type: none;
    li {
      padding: 20px 0 5px;
      p {
        color: #ffffff;
        font-size: 12px;
        margin: 0;
      }
      div[data-name="item-header"] {
        display: flex;
        justify-content: space-between;
        p {
          &:first-child {
            font-weight: bold;
          }
        }
      }
      p[data-name="message"] {
        margin-top: 8px;
      }
    }
  }
  button {
    
  }
}
</style>