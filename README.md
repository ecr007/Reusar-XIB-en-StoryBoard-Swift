# Reusar-XIB-en-StoryBoard-Swift

1 - Se crea el xib a utilizar

2 - Al view principal se le coloca en Size: Freeform

3 - Luego se hace click en File's Owner y en Class; le asignamos la clase que manejara dicho view.
Ejemplo: Head.swift

```swift
import UIKit
@IBDesignable
class Head: UIView {
    let nibName = "Head"
    var contentView:UIView?
    
	/*Aqui van las acciones
	@IBOutlet weak var label: UILabel!
    @IBAction func buttonTap(_ sender: UIButton) {
        label.text = "Hi"
    }*/
	
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        commonInit()
    }
    override init(frame: CGRect) {
        super.init(frame: frame)
        commonInit()
    }
    func commonInit() {
        guard let view = loadViewFromNib() else { return }
        view.frame = self.bounds
        self.addSubview(view)
        contentView = view
    }
    func loadViewFromNib() -> UIView? {
        let bundle = Bundle(for: type(of: self))
        let nib = UINib(nibName: nibName, bundle: bundle)
        return nib.instantiate(withOwner: self, options: nil).first as? UIView
    }
	
	override func prepareForInterfaceBuilder() {
		super.prepareForInterfaceBuilder()
		commonInit()
		contentView?.prepareForInterfaceBuilder()
	}
}
```

4 - Ya luego en el storyboard principal arrastramos un view donde queremos que este el reutilizable y le asignamos la clase Head del . swift

Custom class > Class > "Head o nombre de mi .swift del xib"
