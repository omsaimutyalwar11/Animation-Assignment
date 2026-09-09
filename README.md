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

```swift
UIView.animate(
    withDuration: 0.5,
    delay: 0.5,
    options: [.curveEaseInOut]
) { [weak self] in
    self?.view.layoutIfNeeded()
}
