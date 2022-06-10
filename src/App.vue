<template>
    <h1>News</h1>
    <div class="header">
    <select v-if="select" v-model="dateFrom" @change="getDate">
      <option  value="1">Last Week</option>
      <option  value="2">Last two Week </option>
      <option  value="3">Last Month</option>
    </select>
    <!-- <button v-if="select" class="select" @click="getDate">check</button> -->
    <br>
    <button :style="{visibility:nextPre}" class="next" @click="page1">1</button>
    <button :style="{visibility:nextPre}" class="pages" @click="page2">2</button>
    <button :style="{visibility:nextPre}" class="pages" @click="page3">3</button>
    <button :style="{visibility:nextPre}" class="pages" @click="page4">4</button>
    <button :style="{visibility:nextPre}" class="pages" @click="page5">5</button>
    <input placeholder="Search" v-model="search" v-on:keyup.enter="searchNews">
    </div>



    <div class="p">
<div id="scroll-container">
  <div id="scroll-text">  
    First families lose their land, then their livestock and then their children; that’s the stark reality of life right now in the Horn of Africa, where millions of people have been hit by successive failed rainy seasons.
    <br>
    <br>
    According to UN Children’s Fund UNICEF, hundreds of thousands of Somali children are in desperate need of treatment for life-threatening severe acute malnutrition, more even than during the brutal 2011 famine.
    <br>
     <br>
    Téné Maïmouna Zoungrana, of Burkina Faso, serves with the UN Mission in CAR, MINUSCA. She received the United Nations Trailblazer Award for Women Justice and Corrections Officers at a special ceremony, at UN Headquarters in New York.
    <br>
    <br>
       First families lose their land, then their livestock and then their children; that’s the stark reality of life right now in the Horn of Africa, where millions of people have been hit by successive failed rainy seasons.
    <br>
    <br>
    According to UN Children’s Fund UNICEF, hundreds of thousands of Somali children are in desperate need of treatment for life-threatening severe acute malnutrition, more even than during the brutal 2011 famine.
    <br>
    Téné Maïmouna Zoungrana, of Burkina Faso, serves with the UN Mission in CAR, MINUSCA. She received the United Nations Trailblazer Award for Women Justice and Corrections Officers at a special ceremony, at UN Headquarters in New York.
    <br>
    <br>
       First families lose their land, then their livestock and then their children; that’s the stark reality of life right now in the Horn of Africa, where millions of people have been hit by successive failed rainy seasons.
    <br>
    <br>
    According to UN Children’s Fund UNICEF, hundreds of thousands of Somali children are in desperate need of treatment for life-threatening severe acute malnutrition, more even than during the brutal 2011 famine.
    <br>
  </div>
</div>
    </div>
    
    <div v-if="!loading">
    <HelloWorld v-for="(arr,index) in arrs" 
    :key="arr.title" 
    :publish='arr.publishedAt' 
    :title="arr.title" 
    :imgurl='arr.urlToImage' 
    :url='arr.url' 
    :description='arr.description'
    :author='arr.author'
    :content='arr.source.name'
    :index='index'
    />
    </div>
    <div v-else class="loading">
      <div class="loader"></div>
    </div>
    
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
   data(){
    return {
      arrs:'',
      search:'',
      dateFrom:'',
      date:'',
      count:1,
      select:false,
      nextPre:'visible',
      loading:false
    }
  },
  methods:{
   searchNews(){
    this.loading=true
    axios.get(`https://newsapi.org/v2/everything?q=${this.search}&searchIn=title&sortBy=publishedAt&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
    this.arrs=res.data.articles
    this.select=true
    this.nextPre='hidden'
     this.loading=false
  })
   },
   getDate(){
    if(this.dateFrom==1){
     this.gettingDate(7)
     this.previousweek()
     this.nextPre='hidden'
    }
    else if(this.dateFrom==2){
      this.gettingDate(14)
      this.previousweek()
      this.nextPre='hidden'
    }
    else if(this.dateFrom==3){
       this.gettingDate(30)
       this.previousweek()
       this.nextPre='hidden'
    }
   },
   page1(){
       this.loading=true
       axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&page=1&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
       this.arrs=(res.data.articles)
    //  console.log(this.arrs)
      this.loading=false
       })
   },
  page2(){

       this.loading=true
       axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&page=2&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
       this.arrs=(res.data.articles)
       //console.log(this.arrs)
       this.loading=false
       })
       
   },
   page3(){
       this.loading=true
       axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&page=3&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
       this.arrs=(res.data.articles)
    //  console.log(this.arrs)
       this.loading=false
       })
   },
   page4(){
       this.loading=true
       axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&page=4&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
       this.arrs=(res.data.articles)
    //  console.log(this.arrs)
       this.loading=false
       })
   },
   page5(){
       this.loading=true
       axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&page=5&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
       this.arrs=(res.data.articles)
    //  console.log(this.arrs)
       this.loading=false
       })
   },
   // for getting the past week and past month date
   gettingDate(x){
     let getLastWeek=()=> {
     var today = new Date();
     var lastWeek = new Date(today.getFullYear(), today.getMonth(), today.getDate() - x);
    return lastWeek;
}

    var lastWeek = getLastWeek();
    var lastWeekMonth = lastWeek.getMonth() + 1;
    var lastWeekDay = lastWeek.getDate();
    var lastWeekYear = lastWeek.getFullYear();

    var lastWeekDisplayPadded = ("0000"+lastWeekYear.toString()).slice(-4)+"-" +("00" + lastWeekMonth.toString()).slice(-2) + "-" + ("00" + lastWeekDay.toString()).slice(-2)

    // console.log(lastWeekDisplayPadded);
    this.date=lastWeekDisplayPadded
   },
previousweek(){
  // console.log(this.date)
  this.loading=true
  axios.get(`https://newsapi.org/v2/everything?q=${this.search}&from=${this.date}&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
  this.arrs=res.data.articles
   this.loading=false
    })
}
  },
  created(){
     this.loading=false
     axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&apiKey=23bad7851f3947a6ba7d532f36587735`).then((res)=>{
     this.arrs=(res.data.articles)
    // console.log(res)
     this.loading=false
       })
  }
}
</script>

<style>
body{
  background-image:url(https://img.freepik.com/free-vector/halftone-background-with-circles_23-2148907689.jpg?size=626&ext=jpg&ga=GA1.2.996264456.1654773645);
  background-attachment: fixed;
  margin: 0;
  overflow-x:hidden ;
  background-color: #f0f8fe;
}
input{
  margin-left: 20%;
  margin-bottom: 20px;
  height: 4vh;
  width: 250px;
  border-radius: 5px;
  position:absolute;
  margin-top:23px;
  border:1px solid #6a7891;
  color: #6a7891;
}
input:focus{
   outline: none;
}
h1{
  margin: auto;
  text-align: center;
  color:#6a7891;
  background-color: #f0f8fe;
  border-radius: 5px;
  }
button{
  cursor: pointer;
  height: 5vh;
  width: 80px;
  border-radius: 3px;
  color:#6a7891;
  border:1px solid #f0f8fe
}
.header{
 border:3px solid #6a7891;
 width: 100%;
 position:sticky;
 border-radius:10px;
 top:0;
 z-index: 1;
 background-color: #f0f8fe

 
}
.next{
margin-left: 42%;
margin-top: 20px;
width: 40px;
}
.pages{
 width: 40px;
}
select{
  margin-top: 45px;
  position: absolute;
  height: 3.5vh;
  border-radius: 3px;
  margin-left:67%;
  background-color:white;
  border:1px solid #6a7891;
  color:#6a7891
}
select option:hover{
  background-color: red;
}
select:focus{
   outline: none;
}
.select{
  position: absolute;
  margin-top: 38px;
  margin-left: 120px;

}
.p{
  height: 90vh;
  width: 48%;
  display:inline-block;
  border:1px solid white;
  position: fixed;
  background-color: #f0f8fe;
  margin-top:-3%;
  color:#475774;
}
.loading{
  margin-left: 65%;
  margin-right: auto;
  margin-top: 10%;
  width: 40%;
  justify-content: center;
}


@media screen and (max-width: 500px) {
.next{
  margin-left: 0;
}
input{
  margin-left: 50px;
  width: 140px;
}
}
@media screen and (min-width: 402px) and (max-width: 500px) {
input{
  margin-left: 17%;
}
}
#scroll-container {
  border: 3px solid  #f0f8fe;
  border-radius: 5px;
  height: 80vh;
  overflow: hidden;
}

#scroll-text {
  height: 100%;
 text-align: justify;
  
  /* animation properties */
  -moz-transform: translateY(100%);
  -webkit-transform: translateY(100%);
  transform: translateY(100%);
  
  -moz-animation: my-animation 20s linear infinite;
  -webkit-animation: my-animation 20s linear infinite;
  animation: my-animation 20s linear infinite;
}

/* for Firefox */
@-moz-keyframes my-animation {
  from { -moz-transform: translateY(100%); }
  to { -moz-transform: translateY(-100%); }
}

/* for Chrome */
@-webkit-keyframes my-animation {
  from { -webkit-transform: translateY(100%); }
  to { -webkit-transform: translateY(-100%); }
}

@keyframes my-animation {
  from {
    -moz-transform: translateY(100%);
    -webkit-transform: translateY(100%);
    transform: translateY(100%);
  }
  to {
    -moz-transform: translateY(-100%);
    -webkit-transform: translateY(-100%);
    transform: translateY(-100%);
  }
}

/* loading */

.loader {
  position: relative;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  text-align: center;
  justify-content: center;
  background: linear-gradient(45deg, transparent 40%, skyblue);
  animation: move 0.8s linear infinite;
}
.loader::before {
  position: absolute;
  content: "";
  top: 6px;
  left: 6px;
  right: 6px;
  bottom: 6px;
  background: #242629;
  border-radius: 50%;
  z-index: 2;
}
.loader::after {
  position: absolute;
  content: "";
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background: linear-gradient(45deg, transparent 40%, skyblue);
  filter: blur(20px);
}
@keyframes move {
  to {
    transform: rotate(360deg);
    filter: hue-rotate(360deg);
  }
}

</style>
