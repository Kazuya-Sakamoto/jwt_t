<script lang="ts">
import { defineComponent, reactive, toRefs } from '@vue/composition-api'
import Logo from '@/components/Logo.vue'
import axios from 'axios'

type State = {
  name: string
  password: string
}

const initialState = (): State => ({
  name: '',
  password: '',
})

export default defineComponent({
  components: {
    Logo,
  },
  setup() {
    const state = reactive<State>(initialState())

    const signUp = async () => {
      const params: State = {
        name: state.name,
        password: state.password,
      }
      const res = await axios.post('http://localhost:9010/signup', params)
      console.log(res, 'res')
    }
    return {
      ...toRefs(state),
      signUp,
    }
  },
})
</script>

<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">jwt_p</h1>
      <div class="links">
        <div class="p-2">
          <label class="" for="">name:</label>
          <input class="ml-2 border-2" type="text" v-model="name" />
        </div>
        <div class="p-2">
          <label for="">pass:</label>
          <input class="ml-4 border-2" type="password" v-model="password" />
        </div>
        <div class="mt-5 ml-2">
          <button
            @click="signUp"
            class="bg-green-500 text-white py-2 px-4 rounded-md font-semibold"
          >
            登録する
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  text-align: left;
}
</style>
