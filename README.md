![circularradar](https://github.com/abualgait/CircularRadarBlog/blob/master/the-london-eye-landscape-night.jpg) 

# circularradar

###### *tutorial about how to center statically in xml or programmatically around certain view.* 

*I got attracted by an interesting UI at [slack online community](https://mindorks-community.slack.com/archives/CK0TXAAQ2/p1585893166005300) @MindOrks and tried to create it.
firstly i thought about inflating customviews, but i figured an easy clean way to create this view staticky or dynamically via constraint-layout.
you can use the following attributes to center views to certain view and also by using ConstraintSet you can set these attrs dynamically.
hope it helps.*

Statically in XML
------
in ```ConstrainLayout``` you can add views and define the following attrs to make circle constraint to the center view  
```
app:layout_constraintCircle="@id/center_image"
app:layout_constraintCircleAngle="45"
app:layout_constraintCircleRadius="150dp"
```     
Programmaticlly in code
------
you should create the view programmaticlly and set it's dimens (width and hieght) 

 ```
 val childView = CircleImageView(this).apply {
  setImageResource(img)
  val lp = LinearLayout.LayoutParams(size, size)
  layoutParams = lp
  id = View.generateViewId()
  container.addView(this)
  }
```

and then clone ```ConstrainLyout``` constrains and set it in ```ConstraintSet``` and add/edit any constraints then applay these constraints to the parent ```ConstrainLyout```
```
ConstraintSet().apply {
            clone(container)
            connect(childView.id, ConstraintSet.TOP, center_image.id, ConstraintSet.TOP)
            connect(childView.id, ConstraintSet.START, center_image.id, ConstraintSet.START)
            // you can control the angle and radius to prevent repetitive over same place
            constrainCircle(childView.id, center_image.id, raduis, angle)
            applyTo(container)
}
```

Final Result
------
<img src="https://github.com/abualgait/CircularRadar/blob/master/circular_radar.png" height="390" >

[GitHub Repo.](https://github.com/abualgait/CircularRadar)


 
 
