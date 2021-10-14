# UI Components - programmatically

**EN:**

Building UI Components programmatically is quite easy. It might be thought for the beginner, however if you follow this steps it would be nice, clear and easy. 

Steps

1. In class create variable/constant with desired name and add a type of component (in our case it will be UIImageView)
2. Initiate your component
3. Set some attributes
4. Return component

IMPORTANT: Remember to add () at the end of closure to make it work :)

**PL:**

Z początku tworzenie komponentów programistycznie może wydawać się trudne. Jeśli prześledzisz poniższe kroki, z pewnością wyda Ci się to szybkie, łatwe i przyjemne.

Kroki

1. W klasie stwórz zmienną/stałą oraz dodaj do niej wybrany typ (jaki komponent chcesz zbudować)
2. Zainicjuj swój nowy komponent. 
3. Wystylizuj w wybrany przez siebie sposób
4. Zwróć komponent

WAŻNE: Na końcu domknięcia (closure) dodaj ().


```swift
 private let iconImage: UIImageView = { // Step 1
        let iconView = UIImageView() // Step 2
        iconView.image = UIImage(systemName: "bubble.right") // Step 3
        iconView.tintColor = .white // Step 3
        return iconView // Step 4
    }() // IMPORTANT

```

## How to add component to a view? 

**EN:**

This part is tricky. You can do it in few ways for ex. standard way or by creating an extension. Below you will find both mentioned ways to bring your component to life. 

**PL:**

Tutaj mogą zacząć się schody, ale nie muszą. 'Powołać do życia' nasz komponent możemy na różne sposoby np. standardowo lub tworząc rozszerzenie (extnension)
Poniżej znajdziesz przykłady obu podejść.

Standard:

```swift
 override func viewDidLoad() {
        super.viewDidLoad()
        
        view.addSubview(iconImage)
        iconImage.translatesAutoresizingMaskIntoConstraints = false // This line is most important. It let's know that we are adding our custom created component. In other case it won't show up
        iconImage.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true // center according to Y anchor
        iconImage.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true // center according to X anchor
        iconImage.heightAnchor.constraint(equalToConstant: 120).isActive = true // set the height of component
        iconImage.widthAnchor.constraint(equalToConstant: 120).isActive = true // set the width of component
    }

```

However you can imagine that having a few components will multiply this code. So better solution is to build an example extension (Utils -> Extensions.swift):

Extension:

```swift

extension UIView {
    func anchor(top: NSLayoutYAxisAnchor? = nil,
                left: NSLayoutXAxisAnchor? = nil,
                bottom: NSLayoutYAxisAnchor? = nil,
                right: NSLayoutXAxisAnchor? = nil,
                paddingTop: CGFloat = 0,
                paddingLeft: CGFloat = 0,
                paddingBottom: CGFloat = 0,
                paddingRight: CGFloat = 0,
                width: CGFloat? = nil,
                height: CGFloat? = nil) {
        
        translatesAutoresizingMaskIntoConstraints = false
        
        if let top = top {
            topAnchor.constraint(equalTo: top, constant: paddingTop).isActive = true
        }
        
        if let left = left {
            leftAnchor.constraint(equalTo: left, constant: paddingLeft).isActive = true
        }
        
        if let bottom = bottom {
            bottomAnchor.constraint(equalTo: bottom, constant: -paddingBottom).isActive = true
        }
        
        if let right = right {
            rightAnchor.constraint(equalTo: right, constant: -paddingRight).isActive = true
        }
        
        if let width = width {
            widthAnchor.constraint(equalToConstant: width).isActive = true
        }
        
        if let height = height {
            heightAnchor.constraint(equalToConstant: height).isActive = true
        }
    }
    
    func centerX(inView view: UIView) {
        translatesAutoresizingMaskIntoConstraints = false
        centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true
    }
    
    func centerY(inView view: UIView, leftAnchor: NSLayoutXAxisAnchor? = nil,
                 paddingLeft: CGFloat = 0, constant: CGFloat = 0) {
        
        translatesAutoresizingMaskIntoConstraints = false
        centerYAnchor.constraint(equalTo: view.centerYAnchor, constant: constant).isActive = true
        
        if let left = leftAnchor {
            anchor(left: left, paddingLeft: paddingLeft)
        }
    }
    
    func setDimensions(height: CGFloat, width: CGFloat) {
        translatesAutoresizingMaskIntoConstraints = false
        heightAnchor.constraint(equalToConstant: height).isActive = true
        widthAnchor.constraint(equalToConstant: width).isActive = true
    }
    
    func setHeight(height: CGFloat) {
        translatesAutoresizingMaskIntoConstraints = false
        heightAnchor.constraint(equalToConstant: height).isActive = true
    }
    
    func setWidth(width: CGFloat) {
        translatesAutoresizingMaskIntoConstraints = false
        widthAnchor.constraint(equalToConstant: width).isActive = true
    }
}

```
