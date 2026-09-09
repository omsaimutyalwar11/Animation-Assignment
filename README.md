# Task 4 Documentation

# Assignment 1 – Square View Animation

## Problem Statement

Create a square view and an **Animate** button. When the button is tapped, use `UIView.animate` to move the square to a new position and increase its size. When tapped again, animate it back to its original position and size. Configure the animation using parameters such as duration, delay, and animation curve.

## Implementation

- Created a `squareView` and an `animateButton` and added them to the view hierarchy with the required Auto Layout constraints.
- Added an `isExpanded` property to keep track of the square's expanded and collapsed states.
- Stored the `topConstraint` and `widthConstraint` as properties because their constants need to be modified during the animation.
- Added a height constraint equal to the square's width to maintain its square shape.
- Created the `performAction` method, which is called when the **Animate** button is tapped.
- Inside `performAction`, the `isExpanded` state is toggled:
  - When `isExpanded` is `true`, the top constraint is changed to `20` and the width constraint to `200`. This moves the square towards the top and increases its size.
  - When `isExpanded` is `false`, the top constraint is changed back to `400` and the width constraint to `50`. This returns the square to its original position and size.
- Used `UIView.animate` to animate the constraint changes with:
  - **Duration:** `0.5` seconds
  - **Delay:** `0.5` seconds
  - **Animation Curve:** `.curveEaseInOut`
- Called `layoutIfNeeded()` inside the animation block to animate the Auto Layout constraint changes smoothly.

```
UIView.animate(
    withDuration: 0.5,
    delay: 0.5,
    options: [.curveEaseInOut]
) { [weak self] in
    self?.view.layoutIfNeeded()
}
```

# Assignment 2 – Bouncing ball animation using CAKeyframeAnimation

## Problem Statement
Create a bouncing ball animation using CAKeyframeAnimation, where the ball follows a curved path and gradually settles back to its original position.

## Implementation

- Created a `ballLayer` using `CALayer` and an `animateButton` using `UIButton`. Added them to the view hierarchy with the required frame and Auto Layout constraints.
- Stored the ball's initial position in the `originalPosition` property so that the animation can return the ball to its starting point.
- Created the `animateButtonTapped` action method, which is called when the **Animate** button is tapped.
- Before starting a new animation, checked whether an animation with the key `"bounce"` is already running. This prevents multiple animations from being added while the current animation is still in progress.
  ```
  guard ballLayer.animation(forKey: "bounce") == nil else {
      return
  }
  ```
- Created a `pathForBounceAnimation()` method that returns the `CAKeyframeAnimation` used for the bouncing effect.
- Inside `pathForBounceAnimation()`:
    - Created a `CAKeyframeAnimation` with "position" as the key path to animate the ball's position.
    - Created a `UIBezierPath` to define the ball's movement.
    - Added multiple Bezier curves with different control points to create a smooth bouncing path.
    - Added three main bounces with gradually decreasing heights.
    - Added a final curve that makes the ball come back to its originalPosition, creating the settling effect.
    - Set the animation duration to `4.0 seconds`.
    - Applied the `.easeInEaseOut` timing function to make the animation start and end smoothly.
    - Added the generated animation to `ballLayer` using the "bounce" key:
```
let animation = pathForBounceAnimation()
ballLayer.add(animation, forKey: "bounce")
```
## Result
- When the Animate button is tapped, the ball follows the predefined curved path, performs multiple bounces with gradually decreasing heights, and finally returns to its original position with a smooth settling effect.



