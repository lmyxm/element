<template>
     <div>
        <i class="ac" v-show="!show_yzm" >{{text_yzm}} </i>
    	<i class="ac" v-show="show_yzm" @click="getCode">获取验证码</i>
     </div>
</template>

<script>
export default {
    name:'',
    data(){
        return {
            show_yzm: true,
            text_yzm: '',
            timer: null,
        }
    },
    created(){},
    methods:{   
       getCode(){
            const TIME_COUNT = 60;
            if (!this.timer) {
            this.text_yzm = TIME_COUNT;
            this.show_yzm = false;
            this.timer = setInterval(() => {
            if (this.text_yzm > 0 && this.text_yzm <= TIME_COUNT) {
                this.text_yzm--;
                } else {
                this.show_yzm = true;
                clearInterval(this.timer);
                this.timer = null;
                }
            }, 1000)
            }
        } 
    }
}
</script>
