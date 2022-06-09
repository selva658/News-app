<template>
    <h1>News</h1>
    <div class="header">
    <select v-if="select" v-model="dateFrom">
      <option  value="1">Last Week</option>
      <option  value="2">Last two Week </option>
      <option  value="3">Last Month</option>
    </select>
    <button v-if="select" class="select" @click="getDate">check</button>
    <br>
    <button :style="{visibility:nextPre}" class="next" :disabled="count==1" @click="previous">Previous</button>
    <button :style="{visibility:nextPre}" :disabled="count==5" @click="next">Next</button>
    <input placeholder="Search" v-model="search" v-on:keyup.enter="searchNews">
    </div>
    <HelloWorld v-for="arr in arrs" 
    :key="arr.title" 
    :publish='arr.publishedAt' 
    :title="arr.title" 
    :imgurl='arr.urlToImage' 
    :url='arr.url' 
    :description='arr.description'
    :author='arr.author'
    :content='arr.source.name'/>
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
      nextPre:'visible'
    }
  },
  methods:{
   searchNews(){
    axios.get(`https://newsapi.org/v2/everything?q=${this.search}&searchIn=title&sortBy=publishedAt&apiKey=d80d8c48fff9488aa0efcaf7f7b8f564`).then((res)=>{
    this.arrs=res.data.articles
    this.select=true
    this.nextPre='hidden'
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
   next(){
     if(this.count<6){
       this.count++
       axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&page=${this.count}&apiKey=d80d8c48fff9488aa0efcaf7f7b8f564`).then((res)=>{
       this.arrs=(res.data.articles)
    //  console.log(this.arrs)
       })
     }
   },
   previous(){
     if(this.count==1){
//
     }else{
       this.count--
       axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&page=${this.count}&apiKey=d80d8c48fff9488aa0efcaf7f7b8f564`).then((res)=>{
       this.arrs=(res.data.articles)
    //  console.log(this.arrs)
       })
     }
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
  axios.get(`https://newsapi.org/v2/everything?q=${this.search}&from=${this.date}&apiKey=d80d8c48fff9488aa0efcaf7f7b8f564`).then((res)=>{
  this.arrs=res.data.articles
    })
}
  },
  created(){
     axios.get(`https://newsapi.org/v2/everything?domains=wsj.com&apiKey=d80d8c48fff9488aa0efcaf7f7b8f564`).then((res)=>{
     this.arrs=(res.data.articles)
    //  console.log(this.arrs)
       })
  }
}
</script>

<style>
body{
  background-image:url()
}
input{
  margin-left: 20%;
  margin-bottom: 20px;
  height: 4vh;
  width: 250px;
  border-radius: 5px;
  position:absolute;
  margin-top:23px;
  border:1px solid gray
}
input:focus{
   outline: none;
}
h1{
  margin: auto;
  text-align: center;
}
button{
  cursor: pointer;
  height: 5vh;
  width: 80px;
  border-radius: 3px;
  border:1px solid gray
}
.header{
 border:1px solid rgb(141, 136, 136);
}
.next{
margin-left: 44%;
margin-top: 20px;
}
select{
  margin-top: 45px;
  position: absolute;
  height: 3.5vh;
  border-radius: 3px;
}
.select{
  position: absolute;
  margin-top: 38px;
  margin-left: 120px;
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
</style>
