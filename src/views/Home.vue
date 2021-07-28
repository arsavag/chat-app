<template>
  <div class="home">
    <div data-name="aside-box">
      <Tabs @currentIndex="currentIndex = $event"/>
      <div data-name="tabs-content" ref="tabsContent">
        <Chat 
          @newMessageLength="newMessage = $event" 
          :new-message="newMessage"
          v-if="currentIndex === 0"/>
        <Speaker v-if="currentIndex === 1"/>
      </div>
      <Button v-if="showButton && !newMessage" @click.native="scrollDown" type="down">
        <Icon icon="down-arrow"/>
      </Button>
      <Button v-if="showButton && newMessage" @click.native="scrollDown" type="new-message">
        <p>{{newMessage}}</p>
      </Button>
    </div>
  </div>
</template>

<script>
import Tabs from '@/components/Tabs';
import Chat from '@/components/Chat';
import Speaker from '@/components/Speaker';
import Button from '@/components/Button';
import Icon from '@/components/Icon';
export default {
  name: 'Home',
  components: {
    Tabs,
    Chat,
    Speaker,
    Button,
    Icon
  },
  data() {
    return {
      currentIndex: 0,
      showButton: false,
      newMessage: 0,
      scrolling: false
    }
  },
  watch:{
    'newMessage': function() {
      this.$nextTick(() => {
        console.log(this.$refs.tabsContent.scrollTop);
        if(this.$refs.tabsContent.scrollTop >= this.$refs.tabsContent.scrollHeight - (this.$refs.tabsContent.offsetHeight + this.$refs.tabsContent.scrollTop)) {
          this.$refs.tabsContent.scrollTop = this.$refs.tabsContent.scrollHeight;
        }
      })
    }
  },
  mounted: function() {
    this.scrollDown()
    let lastScrollTop = 0
    this.$refs.tabsContent.addEventListener('scroll', () => {
      this.scrolling = true
      let scrollTop = this.$refs.tabsContent.scrollTop;
      if (scrollTop > lastScrollTop){
        if(this.$refs.tabsContent.offsetHeight + this.$refs.tabsContent.scrollTop >= this.$refs.tabsContent.scrollHeight) {
          this.showButton = false;
          this.newMessage = 0;
        }
      } else {
        this.showButton = true;
      }
      lastScrollTop = scrollTop;
    });
  },
  methods: {
    scrollDown: function() {
      this.$refs.tabsContent.scrollTop = this.$refs.tabsContent.scrollHeight;
      this.showButton = false;
      this.newMessage = 0;
    }
  }
};
</script>
<style lang="scss" scoped>
div.home {
  div[data-name="aside-box"] {
    width: 320px;
    height: 530px;
    background: #272727;
    margin: 0 auto;
    position: relative;
    
    div[data-name="tabs-content"] {
      height: calc(100% - 40px);
      padding: 0 20px 0;
      overflow-y: auto;
      transition: all 0.4s ease;
      
      &::-webkit-scrollbar {
        width: 6px;
      }

      /* Track */
      &::-webkit-scrollbar-track {
        background: #272727;
      }

      /* Handle */
      &::-webkit-scrollbar-thumb {
        background: #272727;
          border-radius: 4px;
      }
      &:hover {
        &::-webkit-scrollbar-thumb {
          background: #a672ff;
        }
      }
      
    }
  }
}
</style>