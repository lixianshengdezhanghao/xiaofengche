## 1.通过点击事件将字母传递给父组件City.vue

~~~
<ul class="nav">
            <li 
            @click="handleClick"
            v-for="(item,index) of cities" :key="index" >{{index}}</li>
</ul>
export default {
    name:"CityWord",
    props:['cities'],
    methods:{
        handleClick(event){
            this.$emit("changeWord",event.target.innerText)
        }
    }
}
</script>
~~~

## 2.在City.vue里接收传递过来的参数

~~~~
<city-word :cities="cities" @changeWord="handleWord"></city-word>

data() {
    return {
      hotCities: [],
      cities: [],
      //在data中定义letter接收子组件传递过来的参数
      letter:""
    };
},
methods:{
    handleWord(word){
       this.letter = word
    }
}
~~~~

## 3.letter传递给List.vue组件

~~~
//通过city.vue的属性传递
<city-list :hotCities="hotCities" :cities="cities" :letter="letter"></city-list>
~~~

## 4.在list.vue组件中接收接收传递过来的参数

~~~
props: ["hotCities", "cities","letter"]
~~~

## 5.通过watch属性,侦听letter值的变化

~~~
watch:{
      letter(){
          console.log(this.letter)
      }
  }
~~~

## 6.结合better-scroll组件让元素滚动到对应的位置

~~~
//1.给要滚动的DOM  ref属性
<p class="title" :ref="index">{{index}}</p>
//2.通过watch属性滚动到对应的位置
watch:{
      letter(){
          var elment = this.$refs[this.letter][0];
          this.scroll.scrollToElement(elment)
	}
}
~~~

