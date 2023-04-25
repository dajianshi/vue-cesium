/*
* @Author: 大剑师兰特（xiaozhuanlan），还是大剑师兰特（CSDN）
* @此源代码版权归大剑师兰特所有，可供学习或商业项目中借鉴，未经授权，不得重复地发表到博客、论坛，问答，git等公共空间或网站中。
* @Email: 2909222303@qq.com
* @First published in xiaozhuanlan.com
* @Second published in CSDN
* @First published time: 2023-04-09
*/
<template>
    <div class="container">
        <h3>vue+cesium: 加载czml文件,显示图形</h3>
        <p>大剑师兰特, 还是大剑师兰特</p>
        <h4>
            <el-button type="primary" size='mini' @click="loadFile()">加载czml文件</el-button>
        </h4>
        <div id="vue-cesium"></div>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                viewer: null,
            }
        },
        methods:{
            loadFile(){
                this.viewer.dataSources.add(  //加载Vehicle.czml
                    Cesium.CzmlDataSource.load("../sampledata/Vehicle.czml")
                ).then((dataSource) => {
                    this.viewer.flyTo(dataSource.entities);
                });
            },
        },
        mounted() {
			Cesium.Ion.defaultAccessToken = this.$root.cesiumToken; //自己的token
            this.viewer = new Cesium.Viewer("vue-cesium", {
                vrButton: false,
                geocoder: false,
                selectionIndicator: false,
                animation: true,
                timeline: true,
                // baseLayerPicker:false,
                navigationHelpButton: false,
                useDefaultRenderLoop: true,
                showRenderLoopErrors: true,
                fullscreenButton: false,
                infoBox: false,
				shouldAnimate: true, //让其运动
            });

          this.viewer.homeButton.container.style.display  = "none"; //顶部的工具栏
          this.viewer.baseLayerPicker.viewModel.selectedImagery = this.viewer.baseLayerPicker.viewModel.imageryProviderViewModels[3];

        }
    }
</script>
<style scoped>
    .container {
        width: 1000px;
        height: 640px;
        margin: 50px auto;
        border: 2px solid rgb(219, 218, 111);
        position: relative;
    }

    #vue-cesium {
        width: 960px;
        height: 470px;
        margin: 0 auto;
        border: 1px solid #42B983;
        position: relative;
    }

    /deep/.cesium-viewer .cesium-widget-credits {
        display: none
    }
</style>