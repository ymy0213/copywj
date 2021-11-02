<template>
  <div class="home">
    <h3>add todo</h3>
      <input type="text" class="inp" placeholder="请输入...." v-model="input"  @keydown.enter="add">
      <button class='but' @click="add">添加</button>
      <h4>筛选:
          <select name="" id="se" @change="sek">
            <option :value="msg.length" checked>{{msg.length}}</option>
            <option value="150">150</option>
            <option value="50">50</option>
            <option value="10">10</option>
          </select>
      </h4>
      <div>
        <ul class="lb">
          <li :class="{ahha:mm==index}" v-for="(item,index) in list" :key="'a'+index" @click="djnr(index)">{{item}}</li>
        </ul>
      </div>
      <div>
        <h4>代办事项:</h4>
        <ul class="list_con">
          <li v-for="(item,index) in msg" :key="index">{{item.title}}</li>
        </ul>
        <div v-if="mm==0" class="lb_cent">
          <div v-for="(item,index) in msms" :key="'b'+index" @click="item.completed=!item.completed">
            <div class="lb">
              <div class="lb_nr">
                <div :class='{"bac":item.completed}'>{{item.title}}</div>
              </div>
            </div>
          </div>
      <div v-if="msms.length==0">暂无内容</div>
    </div>
        </div>
        
      </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Home',
  data(){
    return{
      input:'',
      list:['查看所有','已完成','未完成'],
      msg:[],
      mm:0,
      ms:0
    }
  },  computed:{
    msms(){
      if(this.ms==0){
        this.ms=this.msg.length
      }
      return this.msg.slice(0,this.ms);
    },
  },
  created() {
    axios.get('http://jsonplaceholder.typicode.com/todos').then(res=>{
      this.msg=res.data;
    })
  },
  methods:{
    add(){
      if (this.input==''){
        alert('输入不能为空');
        return;
      }
      this.msg.splice(this.msg.length-1,1);
      this.msg.unshift({title: this.input,completed:false})
      this.input='';
    },
      djnr(index){
      console.log(index)
      this.mm=index;
    },
    sek(){
      this.ms=document.getElementById('se').value
    }
  }
}
</script>
<style scoped>
.home{
  width: 90%;
  background: #EBF8F1;
  text-align: center;
}
.inp{
  width: 50%;
  height: 38px;
  border: 2px solid rgb(132, 230, 149);
  outline: none;
  /* display: flex; */
}
.but{
  height: 42px;
  width: 5%;
}
.lb{
  width: 50%;
  display: flex;
  justify-content: center;
  justify-content:space-around;
  margin: 0 auto;
}
.lb>li{
  margin-top: 20px;
}
h4{
  margin-top: 30px;
}
.list_con{
  width: 60%;
  /* display: flex; */
  justify-content: center;
  justify-content: space-around;
  margin: 0 auto;
}
.list_con>li{
  margin-top: 20px;
  width: 20%;
  height: 50px;
  background: #64B688;
  line-height: 50px;
  float: left;
  justify-content: center;
  margin-left: 40px;
  overflow: hidden;
}
.list_con>li:hover{
  background: navy;
  color: aliceblue;
}
.ahha{
  color: aquamarine;
}
</style>
