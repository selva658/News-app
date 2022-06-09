<template>

<div class="div">
    <div class="time">
    <h5 class="time">{{(publish.split(/[TZ]/ ).join(' '))}}</h5>
</div>

<div class="expand">
    <button @click="showExpand">Expand</button>
</div>

    <h5 class="title">{{title}}.</h5>

<div class="img"><img :src="imgurl"/></div>
    <a :href="url"><div class="description" v-html="description"></div></a>
    <div v-if="expand">
       <h5 class="expandc">Author:{{author}}</h5>
       <h5 class="expandc">Source:{{content}}</h5>
       <a :href="url" target="_blank"><p>see more</p></a>
    </div>
</div>

</template>

<script>

export default{
  props:['publish','description','url','title','imgurl','author','content'],
  data(){
    return{
      expand:false,
    }
  },
  methods:{
     showExpand(){
     this.expand=!this.expand
   }
  }
}
</script>

<style scoped>
table,tr,td{
    border-collapse: collapse;
    border:1px solid black
}
.div{
  border:1px solid rgb(141, 136, 136);
  /* box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px; */
  margin-bottom:20px ;
  border-radius: 5px;
  padding: 5px;
}
.time{
  margin-top:-1px;
  color: #475774;
}
.title{
  margin-top: -20px;
  color:#475774;
}

.img img{ 
  height: 8vh;
}
.img{
  display: inline-block;
  width: 10%;
  vertical-align: top;
}
.description{
  display: inline-block;
   vertical-align: top;
   width: 80%;
   color:#475774;
   font-size: 15px;
}
.description:hover{
  text-decoration: underline;
  color: #475774;
}
input{
  margin-left: 80%;
  margin-bottom: 20px;
  height: 4vh;
  width: 19%;
  border-radius: 5px;
}
.time,.expand{
  display: inline-block;
}
.expand{
  margin-left: 80%;
  cursor: pointer;
}
.expandc{
   color: #475774;
}
@media screen and (max-width:500px) {
  .img img{
    width: 70px;
  }
  .description{
    margin-left: 10%;
  }
  .expand button{
   margin-top: -13%;
   position:absolute;
   width:60px
  }
}
@media screen and (min-width: 402px) and (max-width: 500px) {
.expand button{
   margin-top: -12%;
   position:absolute;
   width:60px
  }
}
</style>>
