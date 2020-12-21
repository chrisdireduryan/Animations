# Animations

## Creating implicit animations

```swift
struct ContentView: View {
    @State private var animationAmount: CGFloat = 1

    var body: some View {
        Button("Tap me") {
            self.animationAmount += 1
        }
        .padding(50)
        .background(Color.red)
        .foregroundColor(.white)
        .clipShape(Circle())
        .scaleEffect(animationAmount)
        .blur(radius: (animationAmount - 1) * 3)
        .animation(.default)
    }
}
```

## Customizing animations in SwiftUI
```swift
struct ContentView: View {
    @State private var animationAmount: CGFloat = 1

    var body: some View {
        Button("Tap me") {
            // self.animationAmount += 1
        }
        .padding(40)
        .background(Color.red)
        .foregroundColor(.white)
        .clipShape(Circle())
        .overlay(
            Circle()
                .stroke(Color.red)
                .scaleEffect(animationAmount)
                .opacity(Double(2 - animationAmount))
                .animation(
                    Animation.easeOut(duration: 1)
                            .repeatForever(autoreverses: false)
                )
        )
        .onAppear {
            self.animationAmount = 2
        }
    }
}
```

## Animating bindings
```swift
struct AnimatingBindings: View {
    @State private var animationAmount: CGFloat = 1
    var body: some View {
        print(animationAmount)
        return VStack {
            Stepper("Scale amount", value: $animationAmount.animation(
                Animation.easeInOut(duration: 1)
                    .repeatCount(3, autoreverses: true)
            ), in: 1...10)
            Spacer()
            Button("Tap Me") {
                self.animationAmount += 1
            }
            .padding(40)
            .background(Color.red)
            .foregroundColor(.white)
            .clipShape(/*@START_MENU_TOKEN@*/Circle()/*@END_MENU_TOKEN@*/)
            .scaleEffect(animationAmount)
        }
    }
}
```