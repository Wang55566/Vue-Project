<template>
  <div>
    {{ testMessage }}
    {{ duplicateText }}
    {{ total }}
    {{ responseData.title }}
  </div>
</template>

<script>
  export default {
    data() {
      return {
        testMessage: "TestComponent",
        responseData: {},
      }
    },
    methods: {
      printMessage() {
        return this.testMessage
      },
      fetchData() {
        fetch('https://jsonplaceholder.typicode.com/posts/1')
        .then(res => {
            if(!res.ok) {
              throw new Error('fetch data does not succeed')
            }
            return res.json()
          }
        ).then(
          data => {
            this.responseData = data
            this.$emit('dataFetched', data)
          }
        ).catch(error => {
          console.error("Error Message:", error)
        })
      }
    },
    computed: {
      duplicateText() {
        return this.testMessage + this.testMessage
      }
    },
    props: {
      total: {
        type: Number
      }
    },
    mounted() {
      this.fetchData()
      console.log("mounted stage")
    }
  }
</script>
