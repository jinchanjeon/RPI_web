<template>
  <div id="app">
            <v-btn color="blue darken-1" text @click="btnClick($event)">LED ON</v-btn>
            <v-btn color="blue darken-1" text @click="btnClick($event)">LED OFF</v-btn>
            <v-btn color="blue-darken-1" text @click="btnClick($event)">열림</v-btn>
            <v-btn color="blue-darken-1" text @click="btnClick($event)">닫힘</v-btn>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    data () {
        return {
            urlinfo:'http://localhost:8000/devices/',
            urldevice:'http://192.168.100.221:5000/' 
        }
    },
    created(){
        this.$bus.$on('deviceSelected',this.refleshData)
    },
    methods: {
        refleshData(data) {
            axios.get(this.urlinfo+data.deviceId) //서버에 요청하기
            .then((res) => {
                console.log(res.data); //성공시
                this.items = res.data;
            })
            .catch((err) => {
                alert('에러 발생: ' + err); //에러 발생
            });          
        },
        btnClick($event){
            if($event.target.innerHTML == "LED ON"){
                axios.get(this.urldevice+'led?state=on');   
                this.$socket.emit('ledon')
            }
            if($event.target.innerHTML == "LED OFF"){
                axios.get(this.urldevice+'led?state=off'); 
                this.$socket.emit('ledoff')   
            }
            if($event.target.innerHTML == "닫힘"){
                axios.get(this.urldevice+'close');
                this.$socket.emit('close')
            }
            if($event.target.innerHTML == "열림"){
                axios.get(this.urldevice+'open');
                this.$socket.emit('open')
            }
        }
  }
}
</script>
<style scoped>
  div{
    margin:0 5px 0 5px;
  }
</style>