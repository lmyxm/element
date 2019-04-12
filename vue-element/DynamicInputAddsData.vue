<template>
  <div>
    <div class="header">
      <i class="icon" @click="toback"></i>
      <p class="title">产品报修</p>
    </div>
    <ul class="main">
      <div class="btn_icon">
        <i class="icon_minus" @click="ClassList_minus"></i>
        <i @click="ClassList_plus"></i>
      </div>
      <div class="inner">
        <ul class="list">
          <li class="ac">
            <input type="text" placeholder="请输入设备号或扫码录入" maxlength="13" v-model="shebeihao">
            <i class="jia" @click="deviceNumber_plus"></i>
            <i></i>
            <div class="xuhao">
              <ol>
                <li v-for="(list,index) in deviceNumber" :key="index">
                  {{list.name}}
                  <span @click="deviceNumber_minus(index)"></span>
                </li>
              </ol>
            </div>
          </li>
        </ul>
        <ul class="list" v-for="(numlist,i) in ClassList" :key="i">
          <li class="ac">
            <input type="text" placeholder="请输入设备号或扫码录入" v-model="numlist.shebeihao_class" >
            <i class="jia" @click="deviceNumber_plus_class(i)"></i>
            <i></i>
            <div class="xuhao">
              <ol>
                <li v-for="(numlist_class,i_num) in numlist.list" :key="i_num">
                  {{numlist_class.name}}
                  <span @click="deviceNumber_minus_class(i,i_num)"></span>
                </li>
              </ol>
            </div>
          </li>
        </ul>
        <div class="jixing" @click="toDeviceType">
          <p>请选择设备机型</p>
          <span class="miaosu">123</span>
          <u></u>
        </div>
        <div class="jixing" @click="tofaultType">
          <p>请选择故障类型</p>
          <span class="miaosu">123</span>
          <u></u>
        </div>
      </div>
      <textarea class="details" maxlength="200" placeholder="请输入故障描述"></textarea>
    </ul>
    <div class="sendbtn mt3" @click="toconfirm">下一步</div>
  </div>
</template>

<script>
export default {
  name: "usertion",
  data() {
    return {
      shebeihao: "",
      msg: "12323122333",
      //基础组
      newitems: {
        name: "",
        sex: "",
        msg: ""
      },
      deviceNumber: [],
      //基础组

      //添加组
      ClassList: [],
      //添加组  数据
      deviceNumber_class: []
    };
  },
  methods: {
    //返回上一页
    toback() {
      this.$router.go(-1);
    },
    //设备类型选择
    toWriteHospital() {
      this.$router.push({
        path: "/writehospital"
      });
    },
    //进入填写医院选择
    toDeviceType() {
      this.$router.push({
        path: "/devicetype"
      });
    },
    tofaultType() {
      this.$router.push({
        path: "/faultType"
      });
    },
    toconfirm() {
      this.$router.push({
        path: "/writehospital"
      });
    },

    //＋＋   添加组
    ClassList_plus() {
      this.ClassList.push({ "title":"", "shebeihao_class":"", list:[] });
    },
    //--    减去组
    ClassList_minus() {
      this.ClassList.splice(this.ClassList.length - 1, 1);
      console.log(this.ClassList);
    },

    //＋＋   添加设备号
    deviceNumber_plus() {
      if (this.shebeihao == "") return;
      this.deviceNumber.push({ name: this.shebeihao, sex: "", msg: "" });
      this.shebeihao = "";
    },
    //--     减去设备号
    deviceNumber_minus(index) {
      this.deviceNumber.splice(index, 1);
    },
    //按钮添加的  子类
    //＋＋
    deviceNumber_plus_class(n) {
      if (this.ClassList[n].shebeihao_class == "") return;
      this.ClassList[n].list.push({ name: this.ClassList[n].shebeihao_class, sex: "", msg: "" });
      this.ClassList[n].shebeihao_class = "";
    },
    //--
    deviceNumber_minus_class(n,index) {
        this.ClassList[n].list.splice(index, 1);
    }
  }
};
</script>
<style scoped>
.posibtn {
  position: absolute;
  bottom: 1rem;
  left: 0;
}

.main {
  margin: 0 0.34rem;
}
.main .btn_icon {
  width: 6.92rem;
  height: 1.03rem;
}
.main .btn_icon i {
  float: right;
  display: block;
  width: 0.47rem;
  height: 0.47rem;
  background: url("../../assets/icon_plus.png") no-repeat;
  background-size: 100% 100%;
  margin-top: 0.29rem;
}
.main .btn_icon .icon_minus {
  background: url("../../assets/icon_minus.png") no-repeat;
  background-size: 100% 100%;
  margin-left: 0.16rem;
}

.inner {
  width: 6.92rem;
  height: auto;
}
.inner .list {
  width: 6.92rem;
  height: auto;
  margin-bottom: 0.5rem;
}
.inner .list li {
  width: 6.88rem;
  background: #fff;
  margin-bottom: 0.16rem;
  position: relative;
}

.inner .list li input {
  width: 4.8rem;
  height: 0.95rem;
  line-height: 0.97rem;
  background: #fff;
  margin-left: 0.28rem;
  color: #919191;
}

.inner .list li p {
  width: 5.62rem;
  height: 0.97rem;
  line-height: 0.97rem;
  background: #fff;
  margin-left: 0.28rem;
  font-size: 0.26rem;
  color: #919191;
}
.inner .list li i {
  display: block;
  width: 0.49rem;
  height: 0.5rem;
  background: url("../../assets/erweima.png") no-repeat;
  background-size: 100% 100%;
  position: absolute;
  top: 0.25rem;
  right: 0.25rem;
}

.inner .list li .jia {
  background: url("../../assets/icon_jia02.png") no-repeat;
  background-size: 100% 100%;
  top: 0.25rem;
  right: 1.1rem;
}

.inner .list li u {
  display: block;
  width: 0.17rem;
  height: 0.28rem;
  background: url("../../assets/arrow_r.png") no-repeat;
  background-size: 100% 100%;
  position: absolute;
  top: 0.35rem;
  right: 0.3rem;
}
.inner .list .ac {
  padding-top: 0.01rem;
  font-size: 0.3rem;
  padding-bottom: 0.5rem;
}

.inner .list .miaosu {
  position: absolute;
  top: 0;
  left: 2.4rem;
  width: 3.9rem;
  line-height: 0.95rem;
  height: 0.95rem;
  font-size: 0.3rem;
  color: #919191;
  text-align: right;
}

.main .details {
  padding: 0.3rem;
  width: 6.27rem;
  height: 3.4rem;
  line-height: 0.38rem;
  background: #fff;
  color: #919191;
}
.mt3 {
  margin-top: 1rem;
  margin-bottom: 1rem;
}

.inner .xuhao ol li {
  width: 2rem;
  height: 0.49rem;
  line-height: 0.49rem;
  padding: 0 0.55rem 0 0.2rem;
  border: 1px #999999 solid;
  border-radius: 0.25rem;
  font-size: 0.24rem;
  color: #998bd6;
  display: inline-block;
  vertical-align: top;
  margin: 0.37rem 0 0 0.35rem;
  position: relative;
}
.inner .xuhao ol li span {
  display: block;
  width: 0.26rem;
  height: 0.26rem;
  background: url("../../assets/cha.png") no-repeat;
  background-size: 100% 100%;
  position: absolute;
  top: 0.13rem;
  right: 0.25rem;
}

.inner .jixing {
  width: 6.88rem;
  background: #fff;
  margin-bottom: 0.16rem;
  position: relative;
}
.inner .jixing p {
  width: 5.62rem;
  height: 0.97rem;
  line-height: 0.97rem;
  background: #fff;
  margin-left: 0.28rem;
  font-size: 0.26rem;
  color: #919191;
}

.inner .jixing .miaosu {
  position: absolute;
  top: 0;
  left: 2.4rem;
  width: 3.9rem;
  line-height: 0.95rem;
  height: 0.95rem;
  font-size: 0.3rem;
  color: #919191;
  text-align: right;
}

.inner .jixing u {
  display: block;
  width: 0.17rem;
  height: 0.28rem;
  background: url("../../assets/arrow_r.png") no-repeat;
  background-size: 100% 100%;
  position: absolute;
  top: 0.35rem;
  right: 0.3rem;
}
</style>

