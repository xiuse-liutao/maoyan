<template>
    <div id="movie" class="page">
        <app-head title="猫眼电影"></app-head>
        <div class="sub-head">
            <city></city>
            <div class="nav">
                <ul>
                    <li v-for="(navItem, index) in navList" :key="index" :class="{active: index==navIndex}" @click="selectLi(index)">
                        {{navItem}}
                    </li>
                </ul>
            </div>
            <div class="search-icon">
                <img src="../../assets/search.png" alt="">
            </div>
        </div>


        <keep-alive>
            <!-- 正在热映部分 -->
            <moviePlaying v-if="navIndex == 0"></moviePlaying>

            <!-- 即将上映部分 -->
            <movieComing v-else-if="navIndex == 1"></movieComing>            
        </keep-alive>
    </div>
</template>

<script>
// 引入请求数据的方法

import moviePlaying from '../../components/movie/moviePlaying'
import movieComing from '../../components/movie/movieComing'
export default {
    name: 'movie',
    components:{
        moviePlaying,
        movieComing
    },
    data() {
        return {
            navList: ['正在热映', '即将上映'],
            navIndex: 0
        }
    },
    methods: {
        selectLi(index){
            this.navIndex = index;
        }
    },
    created(){
        // console.log(this.$store.state.city);
    }
}
</script>

<style lang="scss" scoped>
.sub-head {
    width: 100%;
    height: .88rem;;
    position: absolute;
    top: 1rem;
    border-bottom: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    font-size: .30rem;
    box-sizing: border-box;
    .nav {
        flex: 1;
        height: .88rem;
        color: #666;
        ul{
            display: flex;
            justify-content: space-around;
            height: .87rem;
            li{
                box-sizing: border-box;
                line-height: .87rem;
                margin: 0 .24rem;
                font-weight: 600;
                &.active{
                    border-bottom: 3px solid red;
                    color: red;
                }
            }
        }
    }
    .search-icon {
        width: .9rem;
        height: .8rem;
        padding: .2rem;
        box-sizing: border-box;
    }
}
</style>

