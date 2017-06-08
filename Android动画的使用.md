---
title: Android动画的使用
tags: 属性动画,补间动画
grammar_cjkRuby: true
---

补间动画
直接可以根据控件大小进行动画的设置,无需计算.
``` stylus
//补间动画
        TranslateAnimation translateAnimation = new TranslateAnimation(
                TranslateAnimation.RELATIVE_TO_SELF, 0,
                TranslateAnimation.RELATIVE_TO_SELF, 0,
                TranslateAnimation.RELATIVE_TO_SELF, start,
                TranslateAnimation.RELATIVE_TO_SELF, end);
        translateAnimation.setDuration(500);
        mSelectChannelFl.startAnimation(translateAnimation);
```

属性动画

``` stylus
//属性动画
        final ObjectAnimator alphaAnim = ObjectAnimator.ofFloat(mChangeChannelTv, "alpha", start, end);
        alphaAnim.setDuration(300);
        alphaAnim.start();
```
