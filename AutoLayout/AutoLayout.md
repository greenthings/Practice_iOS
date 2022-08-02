# Practice_iOS

# Autolayout 

```
        let blueView = UIView()
        blueView.backgroundColor = .blue
        
        view.addSubview(blueView)
        
        //enables auto layout
        blueView.translatesAutoresizingMaskIntoConstraints = false
        
        blueView.topAnchor.constraint(equalTo: view.topAnchor).isActive = true
        blueView.bottomAnchor.constraint(equalTo: view.bottomAnchor).isActive = true
        blueView.leadingAnchor.constraint(equalTo: view.leadingAnchor).isActive = true
        blueView.tarilingAnchor.constraint(equalTo: view.trailingAnchor).isActive = true
```

Using Extension

```
       blueView.anchor(top: view.safeAreaLayoutGuide.topAnchor, leading: view.safeAreaLayoutGuide.leadingAnchor, bottom: view.safeAreaLayoutGuide.bottomAnchor, trailing: view.safeAreaLayoutGuide.trailingAnchor)
       
       extension UIView{
         func anchor(top: NSLayoutYAxisAnchor, leading: NSLayoutXAxisAnchor, bottom: NSLayoutYAxisAnchor, trailing: NSLayoutXAxisAnchor){
           translatesAutoresizingMaskIntoConstraints = false
        
          self.topAnchor.constraint(equalTo: top).isActive = true
          self.bottomAnchor.constraint(equalTo: bottom).isActive = true
          self.leadingAnchor.constraint(equalTo: leading).isActive = true
          self.trailingAnchor.constraint(equalTo: trailing).isActive = true
        
      }
```

```
Something...confused
    // leftAnchor: A layout anchor representing the left edge of the view’s frame.
    // leadingAnchor: A layout anchor representing the leading edge of the view’s frame
```

Padding

```

    blueView.anchor(top: view.safeAreaLayoutGuide.topAnchor, leading: view.safeAreaLayoutGuide.leadingAnchor, bottom: view.safeAreaLayoutGuide.bottomAnchor, trailing: view.safeAreaLayoutGuide.trailingAnchor, padding: .init(top:0,left:12,bottom:0,right:12))
    
    
extension UIView{
    func anchor(top: NSLayoutYAxisAnchor, leading: NSLayoutXAxisAnchor, bottom: NSLayoutYAxisAnchor, trailing: NSLayoutXAxisAnchor, padding: UIEdgeInsets = .zero){
        translatesAutoresizingMaskIntoConstraints = false
        
        topAnchor.constraint(equalTo: top, constant: padding.top).isActive = true
        leadingAnchor.constraint(equalTo: leading, constant: padding.left).isActive = true
        bottomAnchor.constraint(equalTo: bottom, constant: -padding.bottom).isActive = true
        trailingAnchor.constraint(equalTo: trailing, constant: -padding.right).isActive = true
        
    }
}

```


Confliction between anchor and width or height
```
 blueView.anchor(top: view.safeAreaLayoutGuide.topAnchor, leading: nil, bottom: nil, trailing: view.safeAreaLayoutGuide.trailingAnchor, padding: .init(top:0,left:0,bottom:0,right:16),size: .init(width: 100, height: 100))
 
 
 extension UIView{
    func anchor(top: NSLayoutYAxisAnchor?, leading: NSLayoutXAxisAnchor?, bottom: NSLayoutYAxisAnchor?, trailing: NSLayoutXAxisAnchor?, padding: UIEdgeInsets = .zero, size: CGSize = .zero){
        translatesAutoresizingMaskIntoConstraints = false
        
        if let top = top{
            topAnchor.constraint(equalTo: top, constant: padding.top).isActive = true
        }
        if let leading = leading {
            leadingAnchor.constraint(equalTo: leading, constant: padding.left).isActive = true
        }
        if let bottom = bottom {
            bottomAnchor.constraint(equalTo: bottom, constant: -padding.bottom).isActive = true
        }
        if let trailing = trailing {
            trailingAnchor.constraint(equalTo: trailing, constant: -padding.right).isActive = true
        }
        
        if size.width != 0{
            widthAnchor.constraint(equalToConstant: size.width).isActive = true
        }
        
        if size.height != 0{
            heightAnchor.constraint(equalToConstant: size.height).isActive = true
        }
        
    }
}

```

<img width="351" alt="image" src="https://user-images.githubusercontent.com/69499549/182347635-b1dc1e5e-0262-4be6-8d1e-30fe5b2124a2.png">

Multiple Boxes

```
        blueView.anchor(top: view.safeAreaLayoutGuide.topAnchor, leading: nil, bottom: nil, trailing: view.safeAreaLayoutGuide.trailingAnchor, padding: .init(top:0,left:0,bottom:0,right:16),size: .init(width: 100, height: 100))
        
        yellowView.anchor(top: blueView.bottomAnchor, leading: nil, bottom: nil, trailing: blueView.trailingAnchor, padding: .init(top: 16, left: 0, bottom: 0, right: 0), size: .init(width: 100, height: 100))
        
        redView.anchor(top: blueView.topAnchor, leading: view.safeAreaLayoutGuide.leadingAnchor, bottom: yellowView.bottomAnchor, trailing: blueView.leadingAnchor, padding: .init(top: 0, left: 16, bottom: 0, right: 16))

```

![image](https://user-images.githubusercontent.com/69499549/182367766-89ee1b02-7d9d-4def-ac5b-1dff925f22b0.png)


Full Superview
```
     let purpleView = UIView()
        purpleView.backgroundColor = .purple
        view.addSubview(purpleView)
        purpleView.fillSuperview()
        
    func fillSuperview(){
        anchor(top: superview?.topAnchor, leading: superview?.leadingAnchor, bottom: superview?.bottomAnchor, trailing: superview?.trailingAnchor)
    }
```

![image](https://user-images.githubusercontent.com/69499549/182372090-6ab7dddc-6363-4117-9e9a-a5839317ae99.png)
