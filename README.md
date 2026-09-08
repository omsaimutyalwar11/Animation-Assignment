# Task 4 Documentation

# Assignment 1 – Square View Animation
## Problem Statement
 Create a square view and an Animate button. When the button is tapped, use UIView.animate to
 move the square to a new position and increase its size. When the button is tapped again,
 animate the square back to its original position and size. Use parameters such as duration, delay
 and animation curve to configure the animation.

## Implementation

- Used `isExpanded` property to track the current state of the square view whether it is expanded or collapsed. Each button tap toggles its value to switch between the two states.
`private var isExpanded = false`
- Two constraints are stored and modified during animation. 
    - `private var topConstraint: NSLayoutConstraint!` controls the square's vertical position.
    - `private var widthConstraint: NSLayoutConstraint!` controls its width.
    - Height is constrained equal to width, keeping it square.

- Initial state:
```text
Position: 400 pt from top
Size: 50 × 50 pt
```
- Expanded state:

```text
Position: 20 pt from top
Size: 200 × 200 pt
```

### 3. Button Action

`performAction()` toggles the state and updates the constraint constants:

```swift
isExpanded.toggle()

topConstraint.constant = isExpanded ? 20 : 400
widthConstraint.constant = isExpanded ? 200 : 50
```

### 4. Animation

The constraint changes are animated using:

```swift
UIView.animate(
    withDuration: 1,
    delay: 0.5,
    options: [.curveEaseInOut]
) {
    self.view.layoutIfNeeded()
}
```

* **Duration:** 1 second
* **Delay:** 0.5 seconds
* **Curve:** `curveEaseInOut`
* `layoutIfNeeded()` applies the updated constraints within the animation.


## Result

The first tap moves and enlarges the square, while the second tap moves and shrinks it back to its original state. The animation is smooth and respects the user's Reduce Motion accessibility preference.

