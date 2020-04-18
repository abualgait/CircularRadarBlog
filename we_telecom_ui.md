![WEUI](https://www.telecomreview.com/images/stories/2019/f-telecom-egypt-1024x1024.jpg)

# WE UI Design with arc clipping and blur image

#### *in this blog i will show how to clip path of view like an arc for example and using coil lib for make image blured*

Arc CustomView
------

inflate the layout of the customview and use ```BlurTransformation(context)``` to blur the image.
```
  init {
        val view = LayoutInflater.from(context).inflate(R.layout.arc_view_layout, this, true)
        view.findViewById<ImageView>(R.id.imageView7).load(R.drawable.cairo) {
            this.transformations(BlurTransformation(context))
        }
    }
```     

and then we draw custom shape to our view in ```canvas``` using ```path``` by knowing that top-left corner of view is where point (0,0)
for (x,y)

 ```   
  private val path = Path()

    override fun dispatchDraw(canvas: Canvas?) {
        val count = canvas!!.save()
        //arc path
        path.moveTo(0f, 0f)
        path.lineTo(0f, canvas.height.toFloat() - 300f)
        path.quadTo(
            canvas.width.toFloat() / 2, canvas.height.toFloat(),
            canvas.width.toFloat(), canvas.height.toFloat() - 300f
        )
        path.lineTo(canvas.width.toFloat(), 0f)

        canvas.clipPath(path, Region.Op.INTERSECT)
        canvas.clipPath(path)
        super.dispatchDraw(canvas)
        canvas.restoreToCount(count)
    }
```   
Final Result
------
<img src="https://github.com/abualgait/WEUI/blob/master/we_ui_design.png" height="390" >

[GitHub Repo.](https://github.com/abualgait/WEUI)


 
 
