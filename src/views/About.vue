<template>
	<div class="container">
		<h3>显示各种图形(一)
			<div class="cuclife">
				<el-button type="primary" size="mini" @click="removeAll">清空</el-button>
				<el-button type="primary" size="mini" @click="showpoint">Point</el-button>
				<el-button type="primary" size="mini" @click="showBox">Box</el-button>
				<el-button type="primary" size="mini" @click="showCircle">Circle</el-button>
				<el-button type="primary" size="mini" @click="showEllipse">Ellipse椭圆</el-button>
				<el-button type="primary" size="mini" @click="showCorridor">Corridor走廊</el-button>
				<el-button type="primary" size="mini" @click="showCylinder">Cylinder圆柱</el-button>
				<el-button type="primary" size="mini" @click="showCone">Cone圆锥</el-button>
			</div>
		</h3>
		<div id="vue-gis"></div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				viewer: null,
				positionArr: [-90, 30, 3000]
			}
		},
		methods: {
			removeAll() {
				this.viewer.entities.removeAll()
			},
			showpoint() {
				this.removeAll();
				let position = this.viewer.entities.add({
					position: Cesium.Cartesian3.fromDegrees(this.positionArr[0], this.positionArr[1], this.positionArr[2]),
					point: {
						pixelSize: 10,
						color: Cesium.Color.YELLOW
					}
				});
				// this.viewer.zoomTo(position);  
			},
			showBox() {
				this.removeAll();
				this.viewer.entities.add({
					name: 'Blue box',
					position: Cesium.Cartesian3.fromDegrees(this.positionArr[0], this.positionArr[1], this.positionArr[2]),
					box: {
						dimensions: new Cesium.Cartesian3(400000.0, 800000.0, 5000000.0),
						material: Cesium.Color.RED
					}
				});
			},
			showCircle() {
				this.removeAll();
				this.viewer.entities.add({
					position: Cesium.Cartesian3.fromDegrees(this.positionArr[0], this.positionArr[1], this.positionArr[2]),
					name: 'Green circle at height',
					ellipse: {
						semiMinorAxis: 300000.0,
						semiMajorAxis: 300000.0,
						height: 2000000.0,
						material: Cesium.Color.GREEN
					}
				});
			},
			showEllipse() {
				this.removeAll();
				this.viewer.entities.add({
					position: Cesium.Cartesian3.fromDegrees(this.positionArr[0], this.positionArr[1], this.positionArr[2]),
					name: '上海地面站',
					ellipse: {
						semiMinorAxis: 250000.0,
						semiMajorAxis: 400000.0,
						material: Cesium.Color.RED.withAlpha(0.8),
						height: 2000000.0,
						outline: true,
						outlineColor: Cesium.Color.BLUE
					},
					description:'divID55555555555555555555'
				});
				
			},
			showCorridor() {
				this.removeAll();
				this.viewer.entities.add({
				name: 'Red corridor on surface with rounded corners and outline',
				corridor: {
					positions: Cesium.Cartesian3.fromDegreesArray([
																	-90.0, 30.0,
																	-95.0, 30.0,
																	-95.0, 35.0
					]),					
					width: 100000.0,
					material: Cesium.Color.RED.withAlpha(0.9),
					outline: true,
					outlineColor: Cesium.Color.RED
				}
			});
			},
			showCylinder(){
				this.removeAll();
				this.viewer.entities.add({
					position: Cesium.Cartesian3.fromDegrees(this.positionArr[0], this.positionArr[1], this.positionArr[2]),
					name: 'Perple ellipse on surface with outline',
					cylinder: {
					    length: 4000000.0,
					    topRadius: 800000.0,
					    bottomRadius: 800000.0,
					    material: Cesium.Color.GREEN.withAlpha(0.5),
					    outline: true,
					    outlineColor: Cesium.Color.DARK_GREEN
					}
				});
			},
			showCone() {
				this.removeAll();
				this.viewer.entities.add({
					position: Cesium.Cartesian3.fromDegrees(this.positionArr[0], this.positionArr[1], this.positionArr[2]),
					name: 'Perple ellipse on surface with outline',
					cylinder: {
					    length: 4000000.0,
					    topRadius: 0.0,
					    bottomRadius: 2000000.0,
					    material: Cesium.Color.YELLOW,
						outline: true,
						outlineColor: Cesium.Color.DARK_GREEN
					}
				});
			},
		},
		mounted() {
			Cesium.Ion.defaultAccessToken = this.$root.cesiumToken;
			this.viewer = new Cesium.Viewer("vue-gis", {
				imageryProvider: new Cesium.SingleTileImageryProvider({
					url: 'Cesium/Assets/Images/555.jpg'
				}),
				vrButton: false,
				geocoder: false,
				homeButton: false,
				// selectionIndicator: false,
				animation: false,
				baseLayerPicker: false,
				timeline: false,
				sceneModePicker: false,
				navigationHelpButton: false,
				useDefaultRenderLoop: true,
				showRenderLoopErrors: true,
				fullscreenButton: false,
				// infoBox: false,
			});
			this.viewer._cesiumWidget._creditContainer.style.display = "none";
			// this.viewer.camera.setView( {
			//     destination: Cesium.Cartesian3.fromDegrees(this.positionArr[0], this.positionArr[1],this.positionArr[2])
			// } );

		}
	}
</script>
