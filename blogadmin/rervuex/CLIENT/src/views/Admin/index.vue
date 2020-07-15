<template>
   <div>
       <el-container>
           <el-aside width="200">aside</el-aside>
           <el-main>main</el-main>

       </el-container>

   </div>
</template>

<script>
    export default {
        name: "Admin"
    }
</script>

<style scoped lang="less">
    .el-aside{
        height: 100vh;
        background-color: beige;
    }

    .el-main{
        height: 100vh;

    }
</style>