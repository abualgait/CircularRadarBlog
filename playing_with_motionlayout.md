![MotionLayout](https://image.slidesharecdn.com/motionlayout-190901150733/95/android-motion-layout-1-638.jpg?cb=1572724767)

# Playing with MotionLayout

#### *in this blog i will try to demonsetrate some motionlayout and View Property animation*

View Property animation
------

add listener to view layout to launch animation after view positioning
   ```   
   dishView.viewTreeObserver.addOnGlobalLayoutListener(
            object : OnGlobalLayoutListener {
                override fun onGlobalLayout() { // Layout has happened here.

                    fillVegteablesDish()
                    dishView.viewTreeObserver.removeOnGlobalLayoutListener(this)
                }
            })
```

i have to define my data as array of drawable or strings to animate seperatly.
```
   val vegetables = arrayOf(
        R.drawable.picture1,
        R.drawable.picture2,
        ...
    )

    val stophunger = arrayOf(
        "S",
        "t",
        "o",
        "p",
        ...
    )

```   



* ### *animate vegetables*
position the view at a random place between the left and right edges of the container
and get current view posiotion (x,y) and target view (x1,y1) and animate with ```ObjectAnimator()``` and then play together
```
newVegetable.translationX = Math.random().toFloat() * containerW
val vegPostition = newVegetable.getPositionOnScreen()


            xAnimator = newVegetable.objectAnimator(
                propertyName = "translationX",
                durationToAnimate = ANIMATION_DURATION,
                startValue = vegPostition[0].toFloat(),
                endValue = dishPosition[0].toFloat() + Math.random().toFloat() * 1.5f + .1f
            )
            yAnimator = newVegetable.objectAnimator(
                propertyName = "translationY",
                durationToAnimate = ANIMATION_DURATION,
                startValue = vegPostition[1].toFloat() - dishView.measuredHeight,
                endValue = dishPosition[1].toFloat() - dishView.measuredHeight
            )
```
* ### *animate letters*
create programmatically ```TextView``` to set colors and add to view
```
   val newLetter = TextView(this)
            newLetter.text = element
            newLetter.textSize = 25f
            newLetter.typeface = Typeface.DEFAULT_BOLD
            val color =
                if ("stop".contains(
                        element,
                        ignoreCase = true
                    )
                ) resources.getColor(R.color.colorAccent) else resources.getColor(
                    R.color.colorPrimary
                )
            newLetter.setTextColor(color)
            newLetter.layoutParams = FrameLayout.LayoutParams(
                FrameLayout.LayoutParams.WRAP_CONTENT,
                FrameLayout.LayoutParams.WRAP_CONTENT
            )
            lettersContainer.addView(newLetter)
```
then animate this ```TextView ```

```
            val yAnimator: ObjectAnimator


            yAnimator = newLetter.objectAnimator(
                propertyName = "translationY",
                durationToAnimate = ANIMATION_DURATION,
                startValue = if (index % 2 == 0) 50f else -50f,
                endValue = 0f
            )
```
Gmail Profile Animation [MotionLayout#1]
------
i want you to check the code for view animation with keyframes and custome attributes along side the start and end of transition

but what is intersting here is that you can include MotionLayout with AppBar 
by set on appbar offsetchangelistner and the set motionlayout progress accordingly 
```
 private fun coordinateMotion() {
        val appBarLayout: AppBarLayout = findViewById(R.id.appbar_layout)
        val motionLayout: MotionLayout = findViewById(R.id.motion_layout)


        val listener = AppBarLayout.OnOffsetChangedListener { unused, verticalOffset ->
            val seekPosition = -verticalOffset / appBarLayout.totalScrollRange.toFloat()
            motionLayout.progress = seekPosition
        }

        appBarLayout.addOnOffsetChangedListener(listener)
    }
```

DayNight [MotionLayout#2]
------
i prefer here also to check out the code and play with keyframes to get the value out of ```Motionlayout``` and ```KeyFrames```

Final Result
------
[LinkedIn Post.](https://www.linkedin.com/posts/abualgait_last-but-not-least-animation-view-property-activity-6623159182545821696-5iao)

[GitHub Repo.](https://github.com/abualgait/WEUI)


 
 
