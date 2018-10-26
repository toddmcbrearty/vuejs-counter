<template>
    <div class="counter" @click="toggleCount">
        <font-awesome-icon 
          :icon="[getPrefix, icon]" 
          :color="getIconColor" 
        />
        <span class="count" v-show="showCount" v-text="count"></span>
        <span class="post-text" v-show="postText !== ''" v-html="postText"></span>
    </div>
</template>

<script>
export default {
  name: 'Counter',

  props: {
    icon: {
      type: String,
      default: 'heart',
    },
    count: {
      type: Number,
      default: 0,
    },
    isCounted: {
      type: Boolean,
      default: false,
    },
    colors: {
      type: Object,
      default: () => {
        return {
          counted: 'red',
          uncounted: 'red',
        };
      },
    },
    showCount: {
      type: Boolean,
      default: true,
    },
    postText: {
      type: String,
      default: '',
    },
  },

  data() {
    return {
      counted: false,
    };
  },

  created() {
    this.counted = this.isCounted;
  },

  methods: {
    toggleCount() {
      const count = this.counted ? this.count + 1 : this.count - 1;

      this.counted = !this.counted;

      this.$emit('count-updated', count);
    },
  },

  computed: {
    getIconColor() {
      return this.counted ? this.colors.counted : this.colors.uncounted;
    },

    getPrefix() {
      return this.counted ? 'far' : 'fas';
    },
    getPostText() {
      return this.postText !== ''
        ? `<span class="post-text">${this.postText}</span>`
        : '';
    },
  },
};
</script>

<style lang="scss" scoped>
.counter {
  cursor: pointer;
  font-size: 1em;

  .count {
    font-size: 1em;
    margin-left: 0.8rem;
  }

  .post-text {
    margin-left: 0.3rem;
  }
}
</style>