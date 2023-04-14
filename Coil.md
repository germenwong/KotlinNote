### 介绍

**Coil** 是Android上的一个全新的图片加载框架（协程图片加载库）

与传统的图片加载库Glide，Picasso或Fresco等相比。该具有==轻量（只有大约1500个方法）、快、易于使用、更现代的API==等优势

它支持GIF和SVG，并且可以执行四个默认转换：模糊，圆形裁剪，灰度和圆角。并且是全用[Kotlin](https://so.csdn.net/so/search?q=Kotlin&spm=1001.2101.3001.7020)编写，如果你是纯Kotlin项目的话，那么这个库应该是你的首选。



### 使用

github地址为：[https://github.com/coil-kt/coil/](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fcoil-kt%2Fcoil%2F)

#### 添加依赖

```kotlin
implementation("io.coil-kt:coil:1.1.1")
```

#### 在 Compose 中使用

```kotlin
class MainActivity : ComponentActivity() {
	override fun onCreate(savedInstanceState: Bundle?) {
	    super.onCreate(savedInstanceState)
	    setContent {
	        CoilTheme {
	            val painter =
	                rememberImagePainter(
	                    data = "https://img2.baidu.com/it/u=3911260078,1816999265&fm=253&fmt=auto&app=138&f=PNG?w=1080&h=459",
                        builder = {
                            transformations(CircleCropTransformation())
                        }
                    )

                Image(
                    modifier = Modifier
                        .size(100.dp),
                    painter = painter,
                    contentDescription = null
                )
            }
        }
    }
}
```

#### 在传统代码中使用

```kotlin
imageView.load("https://www.example.com/image.jpg") {
    crossfade(true)
    placeholder(R.drawable.image)
    transformations(CircleCropTransformation())
}
```



### 基本变化

Coil默认提供了四种变换：

* 模糊变换（BlurTransformation）
* 圆形变换（CircleCropTransformation）
* 灰度变换（GrayscaleTransformation）
* 圆角变换（RoundedCornersTransformation）

<img src="https://img-blog.csdnimg.cn/20210907095839854.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5a6J5bGF6ICM5Y2T6LaK,size_20,color_FFFFFF,t_70,g_se,x_16"/>



### Gif加载

Coil基础包中是不支持Gif加载的，需要添加extend包：

```kotlin
implementation("io.coil-kt:coil-gif:0.9.5")
```

此时需要更改一下代码的方式，在imageLoader中注册Gif组件：

```kotlin
val gifImageLoader = ImageLoader(this) {
		componentRegistry {
		    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.P) {
		        add(ImageDecoderDecoder())
		    } else {
		        add(GifDecoder())
		    }
		}
}
```

使用本组件之后，ImageView可直接使用：

```kotlin
image_gif
	.load(GIF_IMAGE_URL, gifImageLoader)
```



### SVG加载

Coil也可以进行SVG加载的，同gif一样，也是需要添加extend包的：

```kotlin
implementation("io.coil-kt:coil-svg:0.9.5")
```

```kotlin
val svgImageLoader = ImageLoader(this){
	componentRegistry {
	    add(SvgDecoder(this@MainActivity))
	}
}
 
image_svg
.load(R.drawable.ic_directions_bus_black_24dp, svgImageLoader)
```

