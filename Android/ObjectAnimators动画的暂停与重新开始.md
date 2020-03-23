## ObjectAnimators动画的暂停与重新开始

```java
private void stopAnimation() {
    mCurrentPlayTime = mAnimator.getCurrentPlayTime();
    mAnimator.cancel();
}

private void startAnimation() {
    mAnimator.start();
    mAnimator.setCurrentPlayTime(mCurrentPlayTime);
}
```

