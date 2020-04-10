![CutTicketView](https://www.superiorwallpapers.com/download/airplane-wing-in-the-sky-wonderful-landscape-1920x1200.jpg)

# CutTicketView

###### *in this blog we will demoenstrate some animations and create some custom views with clipping paths*

Ticket CustomView
------

you can use CustomView to modualrize any view interactions e.g make all views changes and UI interactions in on view class.
here we inflate a layout in our custom view using:
```
 init {
        LayoutInflater.from(context).inflate(R.layout.top_ticket_view_layout, this, true)
    }
```     
and then we draw custom shape to our view in ```canvas``` using ```path``` by knowing that top-left corner of view is where point (0,0)
for (x,y)
 
View Animation
------
now is the time for the intersting part.animating the view to look-like real tickt cut down.

we have to set first some animators with ```ValueAnimator``` so we create util function to return animated float value from ```0f``` to ```1f```
 
```
fun getValueAnimator(
        forward: Boolean = true,
        duration: Long,
        interpolator: TimeInterpolator,
        updateListener: (progress: Float) -> Unit
): ValueAnimator {
    val a =
            if (forward) ValueAnimator.ofFloat(0f, 1f)
            else ValueAnimator.ofFloat(1f, 0f)
    a.addUpdateListener { updateListener(it.animatedValue as Float) }
    a.duration = duration
    a.interpolator = interpolator
    return a
}
```

by skwing the view before translating it will result in effect of cutting view (may add roation also try it.😉)
then play and start these animators with ```AnimatorSet```

```
  val skewAnimation =
                                getValueAnimator(true, DURATION, AccelerateInterpolator()) { progress ->
                                    bottomTicketView.setSkew(0.0f, -progress / 10)
                                }

                        val translateCutter =
                                getValueAnimator(false, DURATION, AccelerateInterpolator()) { progress ->
                                    cutter.translationX = view.width - (progress * view.width)

                                }

                        set.play(translateCutter).with(skewAnimation).before(translateView)
```

Final Result
------
<img src="https://github.com/abualgait/CutTicketView/blob/master/device-2020-03-27-221226.png" height="390" >

[GitHub Repo.](https://github.com/abualgait/CutTicketView)


 
 
