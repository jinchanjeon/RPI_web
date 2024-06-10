<template>
    <div>
        <div class="eventId">{{eventId}}</div>
        <div class="description">{{description}}</div>
        <img src="http://192.168.100.221:5000/video_feed" width="320" height="240">
        <!-- 라즈베리파이 ip주소 -->
    </div>
</template>
<script>
    export default {
        name: 'video-stream',
        data(){
            return{
                eventId:'ttt',
                description:'ttt'
            }
        },
        created(){
            //이 컴포넌트가 생성될 때 소켓 이벤트를 실행함
            this.$socket.on('smart',(data)=>{this.displayEvent(data)})
        },
        methods:{
            displayEvent(data){
                console.log(JSON.stringify(data))
                this.eventId=data.eventId;
                this.description=data.description;                
            }
        }
    }
</script>
