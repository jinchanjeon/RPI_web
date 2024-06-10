<template>
            <v-container fluid>
                <v-row>
                    <v-col>
                        <device-table/>
                    </v-col>
                    <v-col>
                        <google-map/>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col>
                        <data-table/>
                    </v-col>
                    <v-col>
                        <v-row>
                            <device-control/>
                        </v-row>
                            <current-weather/>
                        <v-row>
                        </v-row>
                    </v-col>
                </v-row>
                <v-row>
                    <video-stream/>
                </v-row>
            </v-container>
</template>

<script>
import DeviceTable from '../components/DeviceTable';
import DataTable from '../components/DataTable';
import GoogleMap from '../components/GoogleMap';
import DeviceControl from '../components/DeviceControl';
import CurrentWeather from '../components/CurrentWeather';
import VideoStream from '../components/VideoStream';

export default {
  name: 'App',
  components: {
    DeviceTable,
    DataTable,
    DeviceControl,
    CurrentWeather,
    GoogleMap,
    VideoStream
  },
  data () {
        return {
            urldevice:'http://192.168.100.221:5000/' 
        }
    },
  created(){
    this.$socket.on('ledonres',function(){
        alert('불이 켜졌습니다');   
    });
    this.$socket.on('ledoffres',function(){
        alert('불이 꺼졌습니다');   
    });
    this.$socket.on('closeres',function(){
        alert('문이 닫혔습니다');   
    });
    this.$socket.on('openres',function(){
        alert('문이 열렸습니다');   
    });

    this.$socket.on('smart',function(data){
        alert(JSON.stringify(data));
        console.log(data)
    });
    this.$socket.on('rint',function(data){
        alert(JSON.stringify(data));
    });
  }
}
</script>