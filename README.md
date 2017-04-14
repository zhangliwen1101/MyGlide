# Glide

##背景
>在泰国举行的谷歌开发者论坛上，谷歌为我们介绍了一个名叫 Glide 的图片加载库，作者是bumptech。这个库被广泛的运用在google的开源项目中，包括2014年google I/O大会上发布的官方app。

##简介
>Glide是一个优秀的图片加载工具库.它可以支持多种图片数据源.在对图片加载并显示时,能较好的处理好缓存,保持较低的内存占用.目前已经被Google用于其官方应用中.

##Glide跟Picasso用哪个?
>Glide和Picasso有90%的相似度，准确的说，就是Picasso的克隆版本。但是在细节上还是有不少区别的。

>Glide可以加载GIF动态图，而Picasso不能。

##Gradle引入
dependencies {  
    compile 'com.github.bumptech.glide:glide:3.5.2'  
    compile 'com.android.support:support-v4:22.0.0'  
}  

##Jar
Download [the latest Glide JAR][1]

Maven:

###GitHub(官方)
https://github.com/bumptech/glide

>本文所有前后端联调数据都是由七牛云代理管理的


##Code
```
/**
         * 简单使用
         */
        //                Glide.with(this)
        //                        .load(url_gif)
        //                        .placeholder(R.mipmap.ic_launcher)//设置等待时的图片
        //                        .error(R.mipmap.ic_launcher)//加载失败后的图片显示
        //                        .skipMemoryCache(true)//跳过内存缓存
        //                        .diskCacheStrategy(DiskCacheStrategy.NONE)//跳过硬盘缓存
        //                        .priority(Priority.HIGH)//优先级
        //                        .centerCrop()
        // 使用centerCrop是利用图片图填充ImageView设置的大小，如果ImageView的Height是match_parent则图片就会被拉伸填充
        //                        .fitCenter()//使用fitCenter即缩放图像让图像都测量出来等于或小于 ImageView 的边界范围该图像将会完全显示，但可能不会填满整个
        // ImageView。
        //                        .into(imageView);

        /**
         * 获取Bitmap
         */
        //                Glide.with(this)
        //                        .load(url)
        //                        .placeholder(R.mipmap.ic_launcher)
        //                        .into(new SimpleTarget<GlideDrawable>() {
        //                            @Override
        //                            public void onResourceReady(GlideDrawable resource, GlideAnimation<? super
        // GlideDrawable>
        //                                    glideAnimation) {
        //                                Bitmap bitmap =Utils.drawableToBitmap(resource);
        //                                imageView.setImageBitmap(bitmap);
        //                            }
        //                        });
        /**
         * 先显示缩略图，再显示原图
         */
        //用原图的1/10作为缩略图
        //        Glide
        //                .with(this)
        //                .load(url)
        //                .thumbnail(0.1f)
        //                .into(imageView);
        //用其它图片作为缩略图
        //        DrawableRequestBuilder<Integer> thumbnailRequest = Glide
        //                .with(this)
        //                .load(R.mipmap.ic_launcher);
        //        Glide.with(this)
        //                .load(url)
        //                .thumbnail(thumbnailRequest)
        //                .into(imageView);
        /**
         * 圆角图片,两个参数第二个是圆角的弧度,自定义
         */
        //        Glide.with(this).load(url).transform(new GlideRoundTransform(this))
        //                .into(imageView);
        //        Glide.with(this).load(url).transform(new GlideRoundTransform(this,10))
        //                .into(imageView);
        /**
         * 圆形图片，自定义
         */
        //        Glide.with(this).load(url).transform(new GlideCircleTransform(this)).into
        //                (imageView);
```
##对图片进行裁剪、模糊、滤镜等处理，使用库
>grild引入

dependencies {  
compile 'jp.wasabeef:glide-transformations:2.0.2'
// If you want to use the GPU Filters
compile 'jp.co.cyberagent.android.gpuimage:gpuimage-library:1.4.1'  
} 

```
 //CropTransformation
        //        Glide.with(this)
        //                .load(url)
        //                .bitmapTransform(new CropTransformation(this))
        //                .into(imageView);

        //圆形裁剪
        //        Glide.with(this)
        //                .load(url)
        //                .bitmapTransform(new CropCircleTransformation(this))
        //                .into(imageView);

        //方形裁剪
        //                Glide.with(this)
        //                        .load(url)
        //                        .bitmapTransform(new CropSquareTransformation(this))
        //                        .into(imageView);

        //圆角裁剪
        //        Glide.with(this)
        //                .load(url)
        //                .bitmapTransform(new RoundedCornersTransformation(this,30,0, RoundedCornersTransformation
        // .CornerType.ALL))
        //                .into(imageView);

        //Color ：蒙层颜色值
        //        Glide.with(this)
        //                .load(url)
        //                .bitmapTransform(new ColorFilterTransformation(this, 0x7900CCCC))
        //                .into(imageView);

        //灰度处理
        //        Glide.with(this)
        //                .load(url)
        //                .bitmapTransform(new GrayscaleTransformation(this))
        //                .into(imageView);


        //毛玻璃
        //        Glide.with(this)
        //                .load(url)
        //                .bitmapTransform(new BlurTransformation(this))
        //                .into(imageView);


        //遮罩掩饰（视图叠加处理）
        Glide.with(this)
                .load(url)
                .bitmapTransform(new MaskTransformation(this, R.mipmap.ic_launcher))
                .into(imageView);
        /**
         * 卡通滤波器
         * 使用构造方法 ToonFilterTransformation(Context context, float threshold, float quantizationLevels)
         * threshold ：阀值（单参构造器 - 默认0.2F）影响色块边界的描边效果
         * quantizationLevels ：量化等级（单参构造器 - 默认10.0F）影响色块色彩
         */

        Glide.with(this)
                .load(url)
                .bitmapTransform(new ToonFilterTransformation(this, 0.2F, 10F))
                .into(imageView);

        /**
         * 乌墨色滤波器
         * 使用构造方法 SepiaFilterTransformation(Context context, float intensity)
         * intensity 渲染强度（单参构造器 - 默认1.0F）
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new SepiaFilterTransformation(this, 1.0F))
                .into(imageView);
        /**
         * 对比度滤波器
         * 使用构造方法 ContrastFilterTransformation(Context context, float contrast)
         * contrast 对比度 （单参构造器 - 默认1.0F）
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new ContrastFilterTransformation(this, 3F))
                .into(imageView);
        /**
         * 反转滤波器
         * 使用构造方法 InvertFilterTransformation(Context context)
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new InvertFilterTransformation(this))
                .into(imageView);
        /**
         * 像素化滤波器
         * 使用构造方法 PixelationFilterTransformation(Context context, float pixel)
         * pixel 像素值（单参构造器 - 默认10F）数值越大，绘制出的像素点越大，图像越失真
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new PixelationFilterTransformation(this, 20F))
                .into(imageView);
        /**
         * 素描滤波器
         * 使用构造方法 SketchFilterTransformation(Context context)
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new SketchFilterTransformation(this))
                .into(imageView);
        /**
         * 旋转滤波器
         * 使用构造方法 SwirlFilterTransformation(Context context, float radius, float angle, PointF center)
         * radius 旋转半径[0.0F，1.0F] （单参构造器 - 默认0.5F）
         * angle 角度[0.0F,无穷大）（单参构造器 - 默认1.0F）视图表现为旋转圈数
         * center 旋转中心点 （单参构造器 - 默认new PointF(0.5F,0.5F)）
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new SwirlFilterTransformation(this, 1.0F, 0.4F, new PointF(0.5F, 0.5F)))
                .into(imageView);
        /**
         * 亮度滤波器
         * 使用构造方法 BrightnessFilterTransformation(Context context, float brightness)
         * brightness 光亮强度[-1F,1F]（单参构造器 - 默认0.0F）小于-1F纯黑色,大于1F纯白色
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new BrightnessFilterTransformation(this, 0.5F))
                .into(imageView);
        /**
         * Kuwahara滤波器
         * 使用构造方法 KuwaharaFilterTransformation(Context context, int radius)
         * radius 半径 （单参构造器 - 默认25）
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new KuwaharaFilterTransformation(this, 10))
                .into(imageView);
        /**
         * 装饰图滤波器
         *使用构造方法 VignetteFilterTransformation(Context context, PointF center, float[] color, float start, float end)
         *center 装饰中心 （单参构造器 - 默认new PointF(0.5F, 0.5F)）
         *color 颜色组合 （单参构造器 - 默认new float[0.0F,0.0F,0.0F]） 3个颜色值分别对应RGB3种颜色，取值范围都为[0.0F,1.0F]
         *start 起始点 （单参构造器 - 默认0.0F）
         *end 终止点 （单参构造器 - 默认0.75F）
         */
        Glide.with(this)
                .load(url)
                .bitmapTransform(new VignetteFilterTransformation(this, new PointF(0.5F, 0.5F), new float[]{0.0F,
                        0.0F, 0.0F}, 0.0F, 0.5F))
                .into(imageView);
```







[1]:https://github.com/bumptech/glide/releases