<script>
import DropBox from './DropBox.vue'
import TextField from './TextField.vue'

export default {
  name: 'Settings',
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  components: { DropBox, TextField },
  data() {
    return {
      theme: this.data.data.theme,
      background: this.data.data.background,
      description: this.data.data.description,
      themeOptions: ['Light','Dark'],
      backgroundOptions: ['Colorful','Solid', 'Image']
    }
  },
  methods: {
    themeChange(value) {
      this.theme = value
    },
    backgroundChange(value) {
      this.background = value
    },
    descroChange(value) {
      this.description = value
    }
  }
}

</script>

<template>
  <div id="window">
    <h2 class="title">Settings</h2>
    <ul class="content">
      <li class="inline">
        <h3>Theme</h3>
        <DropBox
          :list="['Light','Dark']"
          :index="this.theme"
          @selected="themeChange" />
      </li>
      <li class="inline">
        <h3>Background</h3>
        <DropBox
          :list="['Colorful','Solid', 'Image']"
          :index="this.background"
          @selected="backgroundChange" />
      </li>
      <li class="block">
        <h3>Description</h3>
        <TextField
          :content="this.description"
          @description="descroChange" />
      </li>
    </ul>
  </div>
  <div id="state">
    <h3>theme: '{{this.themeOptions[this.theme]}}'</h3>
    <h3>background: '{{this.backgroundOptions[this.background]}}'</h3>
    <h3>description: '{{this.description}}'</h3>
  </div>
</template>

<style scoped>
#state {
  position: fixed;
  top: 0;
  left: 0;

  height: auto;
  width: 18rem;
  padding: 2rem;

  background-color: rgba(0, 0, 0, 0.342);
  color: white;
}

#window {
  width: 30rem;
  min-height: 20rem;
  height: auto;

  border-radius: 5px;
  overflow: hidden;

  background-color: white;
  color: var(--vt-c-black);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
}

.title {
  padding: 0.5rem 1rem;
  background-color: rgb(203, 230, 255);
}

.content {
  padding: 2rem 1.5rem;
}

.content > li {
  display: flex;
  justify-content: space-between;

  border-radius: 5px;

  padding: 0.5rem 1rem;
  margin-bottom: 1rem;

  transition: .2s;
}

.inline {
  align-items: center;
}

.block {
  flex-direction: column;
  align-items: flex-start;
}

@media (min-width: 1024px) {}
</style>
