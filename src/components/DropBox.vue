<script>
export default {
  name: 'DropBox',
  props: {
    list: {
      type: Array,
      required: true
    },
    index: {
      type: Number,
      required: false,
      default: 0
    }
  },
  data() {
    return {
      // In case the selected item index is not passed we need to assigned
      // it to the first item
      selected: this.list[this.index ?? 0],
      active: false,
      // CSS wont let us have an animation from height 0 to auto, we got
      // to set the height of the drop down list to the height of a
      // single element multiplied to the amount of the items in the
      // list. In the future we should remove this magic number and
      // have a const declaration at the top, but for now we dont want
      // to spend anymore time on this task.
      listCount: this.list.length,
    }
  },
  methods: {
    debug(event) {
      console.log(event)
    },
    setActive(value) {
      // Lets check if the item is not already selected and do stuff only
      // in that case. Would love to rewrite it with an early return.
      if (value !== this.list[this.index]) {
        this.$emit('selected', this.list.indexOf(value))
        console.log(this.list.indexOf(value))
      }
    }
  }
}
</script>

<template>
  <div class="dropbox">
    <button @click="active = !active" @blur="active = false">
      {{list[index]}}
    </button>
    <ul class="list" :class="{ 'active': active }">
      <li v-for="item in this.list"
        @click="setActive(item)"
        :class="{ 'selected': item === list[index] }">
        {{item}}
      </li>
    </ul>
  </div>
</template>

<style scoped>
.dropbox {
  position: relative;
  height: 2rem;
  width: 8rem;

  display: flex;
  flex-direction: column;
}

.dropbox > * {
  cursor: pointer;
}

.dropbox > button {
  height: 100%;
  width: 100%;
  padding-left: 0.4rem;

  border: 1px solid black;
  
  background-color: rgb(203, 230, 255);
  background-image: url(../assets/drop.svg);
  background-repeat: no-repeat;
  background-position: right;

  text-align: left;

  transition: 0.2s;
}

.dropbox > button:hover {
  background-color: rgb(184, 214, 241);
}

.list {
  z-index: 1000;
  top: 2rem;

  position: absolute;
  overflow: hidden;

  height: 0;
  width: 100%;
  padding-left: 0;

  background-color: aliceblue;
  border: 1px solid black;
  /* Have to use this weird work around to make it tidy */
  border-top: 0;
  border-bottom: 0;

  transition: 0.2s;
}

.list > li {
  height: 2rem;
  padding-left: 0.5rem;

  display: flex;
  align-items: center;
}

/* Have to use this weird work around to make it tidy */
.list > li:last-of-type {
  border-bottom: 1px solid black;
}

.list > li:hover {
  background-color: rgb(184, 214, 241);
}

.active {
  height: v-bind(listCount * 2 + 'rem');
}

.selected {
  background-color: rgb(209, 228, 245);
}

@media (min-width: 1024px) {}
</style>
