<script lang="ts">
import {
  defineComponent,
  onMounted,
  reactive,
  toRefs,
} from '@vue/composition-api'
import Logo from '@/components/Logo.vue'
import axios from 'axios'

const URL = 'http://localhost:9010'

type State = {
  response: any
}

const initialState = (): State => ({
  response: '',
})
export default defineComponent({
  components: {
    Logo,
  },
  setup() {
    const state = reactive<State>(initialState())

    const publicFunc = async () => {
      const token = localStorage.getItem('token')
      const auth = {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${token}`,
      }
      const params = {
        name: 'sakamoto',
      }

      try {
        const res = await axios.post(`${URL}/private`, params, {
          headers: auth,
        })
        console.log(res, 'res')
        state.response = res.data
      } catch (error) {
        console.log(error)
      }
    }

    onMounted(async () => {
      await publicFunc()
    })

    return {
      ...toRefs(state),
    }
  },
})
</script>

<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">jwt_p</h1>
      <h3>{{ response }}</h3>
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
