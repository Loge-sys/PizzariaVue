<template>
  <div>
    <div class="main-container">
      <h1>Faça sua pizza do seu jeito:</h1>
      <Form/>
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import Form from '../components/Form.vue'

export default {
  name: 'Home',
  components: {
    Banner,
    Form
  }
}

</script>
