## 获取用户地理位置--百度api方式

```html
<!-- 引入百度api -->
// ak码是api的密钥，可以去百度地图api官网申请，此处ak码不是正常可用码，需要的自己去申请
<script type="text/javascript" src="//api.map.baidu.com/api?ak=TxxxhIELjL39ujuPdLvQmGPrym&v=2.0&services=false"></script>
```html


```javascript
<!-- 定位对象 -->
var geoc = new BMap.Geocoder();

<!-- 经纬度获取方式1: geolocation方式获取经纬度 -->
if(navigator.geolocation) {
	navigator.geolocation.getCurrentPosition(function(pos) {
		<!-- pos 的出参 -->
		<!-- {speed: "-1.000000", longitude: "121.451945", latitude: "31.184739", accuracy: "65.000000", timestamp: "2018-06-27 07:12:33 +0000", …} -->
		var point = new BMap.Point(pos.coords.longitude,  pos.coords.latitude);
		setLocation(point);
	}, function(err) {
		console.log(err,'err----')
	})
}
<!-- 经纬度获取方式2: 百度地图方式获取经纬度 -->
// 注释内容是绘制地图相关功能，如果只是为了获取经纬度是不需要的
// var map = new BMap.Map("allmap");      
// var point = new BMap.Point(116.501573, 39.900877);
// map.centerAndZoom(point, 16)
// 定位对象
var geoc = new BMap.Geocoder();
var geolocation = new BMap.Geolocation();
geolocation.getCurrentPosition(function(r){
	if(this.getStatus() == BMAP_STATUS_SUCCESS){
		// var mk = new BMap.Marker(r.point);
		// map.addOverlay(mk);
		// map.panTo(r.point);
		// console.log("当前位置经度为:"+r.point.lng+"纬度为:"+r.point.lat);
		setLocation(r.point);
	} else {
		console.log('无法定位到您的当前位置，导航失败，请手动输入您的当前位置！'+this.getStatus());
	}
},{ enableHighAccuracy: true });


<!-- 获取地理位置的函数 -->
function setLocation(point){
	geoc.getLocation(point, function(rs){
		var addComp = rs.addressComponents;
		<!--  addComp的出参 -->
		<!-- {streetNumber: "111", street: “凯滨路”, district: "徐汇区", city: "上海市", province: "上海市"} -->
	});
}

```javascript