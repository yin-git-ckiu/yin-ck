<template>
  <div id="home"> 
    <input type="text" v-model="text" @input="inp">
    <div class="foot">
        <div class="lbhead">
            <div @click="num">编号 <num><img src="/arrow-red.png" alt="" :class="state?'down':''"></num></div>
            <div class="lbname"> 名称</div>
            <div @click="price">价格<num><img src="/arrow-red.png" alt="" :class="state1?'down':''"></num></div>
        </div>
        <div class="lbfoot">
            <ul>
              <li v-for="(ele) in list" :key="ele.id">
                  <span>{{ele.id}}</span>
                  <span class="lbna">{{ele.goods_name}}</span>
                  <span>{{ele.price}}</span>
              </li>
            </ul>
        </div>
        <div class="lbdd">
            <div>每页<input type="text" v-model="num1" @input="change">条，共10条</div>
            <!-- 翻页组件 -->
            <div>
                <cl v-for="(ele,index) in Math.ceil(10/num1)" :key="index" @click.native="clc(index)">{{index+1}}</cl>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import num from '../components/num'
import cl from '../components/cl'
export default {
  components: {
    num,
    cl,
  },
  data() {
    return {
      list:[],
      list1:[],
      text:'',
      num1:10,
      num2:[],
      state:true,
      state1:true,
    }
  },
  methods: {
    clc(num){
      console.log(5555)
          this.list=this.list1.slice(num*this.num1,(num+1)*this.num1)
    },
    change(){
      if(this.num1==''){
        this.num1=0
      }{
        this.list=this.list1.slice(0,this.num1)
      }
        
    },
    inp() {
        this.list=this.list1.filter(ele=>{
          return ele.goods_name.includes(this.text)
        })
    },
    price(){
      console.log(1111)
this.state1=!this.state1
      if(this.state1){
        this.list=this.list.sort((a,b)=>{
        return (a.price-b.price)
      })
      }else{
         this.list=this.list.sort((a,b)=>{
        return (b.price-a.price)
      })
      }
    },
    num(){
      
      this.state=!this.state
      if(this.state){
        this.list=this.list.sort((a,b)=>{
        return (a.id-b.id)
      })
      }else{
         this.list=this.list.sort((a,b)=>{
        return (b.id-a.id)
      })
      }
     
    }
  },
  mounted () {
    this.$axios({
      url:'./data.json'
    }).then(res=>{
      console.log(res.data.data)
      this.list1=res.data.data
      this.list=this.list1
    })
  },

}
</script>

<style lang="scss">
.down {
 
  transform: rotate(180deg);
}
img{
  width: 30px;
  height: 30px;
}
  #home{
    width: 100%;
    position: relative;
    input{
      width: 400px;
      height: 40px;
    }
    .lbdd{
      width: 100%;
      height: 60px;
      // background-color: saddlebrown;
      position: absolute;
      left: 0;
      bottom: 0;
      display: flex;
      padding-right: 20px;
      justify-content: space-between;
      
      input{
        width: 50px;
        height: 20px;
      }
    }
    .foot{
      width: 100%;
      height: 80vh;
      background-color: bisque;
        .lbhead{
          width: 100%;
          height: 60px;
          line-height: 60px;
          background-color: aqua;
          display: flex;
          text-align: center;
          div{
              width: 25%;
          }
          .lbname{
            width: 50%;
          }
        }
        .lbfoot{
          width: 100%;
          height: 100%;
          ul{
            width: 100%;
            height: 100%;
            li{
              width: 100%;
              height: 30px;
              line-height: 30px;
              background-color: red;
              margin-bottom: 5px;
              display: flex;
              text-align: center;
              span{
                width: 25%;
                height: 100%;
              }
              .lbna{
                width: 50%;
              }
            }
          }
        }
    }
  }
</style>