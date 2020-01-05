<template>
    <briup-fulllayout title="常用地址">
    <!-- 已封装好的，点击我的地址，下边没有导航栏 -->
    <van-list>
  <van-cell
    v-for="item in addresses"
    :key="item.id"
    :title="item.province+' '+item.city+' '+item.area+' '+item.address"/>
</van-list>
<br>
<van-button block type="default" @click="toAdressEditHandler">  添加
</van-button>
    </briup-fulllayout>
</template> 

<script>
import {get} from '../../../http/axios'
import {mapState} from 'vuex'
export default{
    data(){
        return{
            addresses:[]
        }
    },
    computed:{
        //对象
        ...mapState("user",["info"])//用哪个user就是谁的信息
    },

    created(){
        this.loadAddress();
    },
    methods:{
        loadAddress(){
            let id=this.info.id;//哪个user
            let url="/address/findByCustomerId?id="+id;
            get(url).then((response)=>{
                this.addresses=response.data;
            })
        },
        //跳转到地址编辑页的处理函数
        toAdressEditHandler(){
            //编程跳转
            this.$router.push("/manager/address_edit");
        }
    }

}
</script>