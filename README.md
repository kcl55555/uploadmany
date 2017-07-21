# uploadmany
微信小程序上传多张图片插件

因为微信自带的uploadFile接口只能每次上传一张图片，这就造成上传多张图片你的场景受到限制，所以就对uploadfile接口做了扩展。

使用方法：

1，  
 
 ```javascript 
     var util = require('../../../utils/upLoad.js') 
```
2， 
 ```javascript  
     chooseImg: function() {
    	var that = this;
		wx.chooseImage({
			count: 9 - that.data.chooseImgs.length,
			sizeType: ['original', 'compressed'], // 可以指定是原图还是压缩图，默认二者都有
			success: function(res) {
				wx.showLoading({
					title: '上传中'
				})
				var tempFilePaths = res.tempFilePaths
				util.uploadMany(tempFilePaths, function(obj) {

					that.data.chooseImgs.push(obj.path)
					that.setData({
						chooseImgs: that.data.chooseImgs
					})
					wx.hideLoading()
				})

			}
		})
	}

```

3，
upload.js 里面的域名和上传的接口对应改一下
