<template>
  <div class="container">
   <div class="col-span-12 w-full flex-col">
    <div class="w-full h-full" style="background-color:black;">
    </div>
   </div>
  </div>
</template>

<script>

export default {
  name: 'Main',
  data() {
    return {
      nothing: 'hi',
    }
  },
  methods: {
    hi() {
      this.currentPage = 'hi';
    },
  },
}
</script>

<style lang="scss" scoped>
.container{
display: grid;
grid-template-columns: repeat(12, minmax(0, 1fr));
height: 98vh;
width:100%;
margin:0;
overflow: auto;
}
</style>
