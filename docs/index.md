<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Vue & Js</title>
	</head>

	<body>

		<br>
		<table id='app' border="1">
			<tr>
				<th>縣市</th>
				<th>地名</th>
				<th>經度</th>
				<th>緯度</th>
				<th>溫度</th>
				<th>更新時間</th>
				<th>小提示</th>
			</tr>
			<tr v-for="data in JsonData">
				<td>{{data.parameter[0].parameterValue}}</td>
				<td>{{data.locationName}}</td>
				<td>{{data.lat}}</td>
				<td>{{data.lon}}</td>
				<td>{{data.weatherElement[3].elementValue}}</td>
				<td>{{data.time.obsTime}}</td>
				<td>
					<span v-if="data.weatherElement[3].elementValue >= 28">注意</span>
				</td>
			</tr>
		</table>
		<script src="https://cdn.jsdelivr.net/vue/latest/vue.js"></script>
		<script src="http://lib.sinaapp.com/js/jquery/1.9.1/jquery-1.9.1.min.js"></script>
		<script>
			var openUrl =
				"https://opendata.cwb.gov.tw/api/v1/rest/datastore/O-A0001-001?Authorization=rdec-key-123-45678-011121314";
			$(function() {
				$.ajax({
					type: 'get',
					url: openUrl,
					success: function(data) {

						pushDom(data.records.location);
						// console.log(JSON.stringify(data.records.location));

					},
					error: function(data) {
						// alert(JSON.stringify(data));
					}
				});

				function pushDom(jsonData) {
					var vm = new Vue({
						el: '#app',
						data: {
							JsonData: jsonData
						}
					});
				}
			})
		</script>
	</body>
</html>
