
## agencement layout manager

```python

import sys
from PyQt5.QtWidgets import QApplication, QLabel, QMainWindow, QPushButton, QHBoxLayout, QVBoxLayout, QWidget

class MyWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        # Create a label and a button
        self.label = QLabel('Hello, world!', self)
        self.button = QPushButton('Click me!', self)

        # Create a horizontal layout for the button and label
        hlayout = QHBoxLayout()
        hlayout.addWidget(self.label)
        hlayout.addWidget(self.button)

        # Create a vertical layout for the window and add the horizontal layout
        vlayout = QVBoxLayout()
        vlayout.addLayout(hlayout)

        # Set the layout for the window
        widget = QWidget()
        widget.setLayout(vlayout)
        self.setCentralWidget(widget)

        # Connect the button to a function
        self.button.clicked.connect(self.on_button_click)

    def on_button_click(self):
        self.label.setText('Button clicked!')

if __name__ == '__main__':
    app = QApplication(sys.argv)
    window = MyWindow()
    window.setGeometry(100, 100, 300, 200)
    window.show()
    sys.exit(app.exec_())

```

### connexion d'un bouton et choice

```python

import sys
from PyQt5.QtWidgets import QApplication, QLabel, QMainWindow, QPushButton, QComboBox, QSpinBox

class MyWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        # Create a label, a button, a combobox, and a spinbox
        self.label = QLabel('Hello, world!', self)
        self.label.setGeometry(50, 50, 200, 30)
        self.button = QPushButton('Click me!', self)
        self.button.setGeometry(50, 100, 100, 30)
        self.combo_box = QComboBox(self)
        self.combo_box.addItem('Red')
        self.combo_box.addItem('Green')
        self.combo_box.addItem('Blue')
        self.combo_box.setGeometry(50, 150, 100, 30)
        self.spin_box = QSpinBox(self)
        self.spin_box.setMinimum(10)
        self.spin_box.setMaximum(30)
        self.spin_box.setGeometry(50, 200, 100, 30)

        # Connect the button to a function
        self.button.clicked.connect(self.on_button_click)

    def on_button_click(self):
        color = self.combo_box.currentText()
        font_size = self.spin_box.value()
        self.label.setStyleSheet('color: {}; font-size: {}pt'.format(color.lower(), font_size))
        self.label.setText('Button clicked!')

if __name__ == '__main__':
    app = QApplication(sys.argv)
    window = MyWindow()
    window.setGeometry(100, 100, 300, 300)
    window.show()
    sys.exit(app.exec_())

```


## updrage pyqt5 version on linux 


check version on linux 

```shell
pip3 show PyQt5
```

You can try some [third-party PPA](https://launchpad.net/%7Etrinitronx/+archive/ubuntu/focal-backport-buildeps) to get _5.15.2+dfsg-1~ubuntu20.04.1~ppa1_ on 20.04 LTS as follows:

```
sudo add-apt-repository ppa:trinitronx/focal-backport-buildeps
sudo apt-get update
sudo apt-get install python3-pyqt5
```

And if you find it bad, you can revert to previous version by running below commands:

```
sudo apt-get install ppa-purge
sudo ppa-purge ppa:trinitronx/focal-backport-buildeps
```


## add layout as child

```python

from PyQt5.QtWidgets import QApplication, QLabel, QVBoxLayout, QHBoxLayout, QWidget, QTabWidget
import sys

app = QApplication(sys.argv)
window = QWidget()

tab_widget = QTabWidget()

tab1 = QWidget()
label1 = QLabel('This is tab 1')
tab1_layout = QVBoxLayout()
tab1_layout.addWidget(label1)
tab1.setLayout(tab1_layout)

tab2 = QWidget()
label2 = QLabel('This is tab 2')
tab2_layout = QVBoxLayout()
tab2_layout.addWidget(label2)
tab2.setLayout(tab2_layout)

tab_widget.addTab(tab1, 'Tab 1')
tab_widget.addTab(tab2, 'Tab 2')

main_layout = QHBoxLayout()
main_layout.addWidget(tab_widget)

window.setLayout(main_layout)

window.show()
sys.exit(app.exec_())

```


`addLayout` and `setLayout` are both methods in PyQt that are used to set the layout of a widget. However, they work in slightly different ways.

`addLayout` is used to add a child layout to an existing layout. It takes a reference to another layout as an argument and adds it as a child layout within the parent layout. For example:

python

```python
parent_layout = QVBoxLayout()
child_layout = QHBoxLayout()
parent_layout.addLayout(child_layout)


```

In this example, we create a `QVBoxLayout` called `parent_layout` and a `QHBoxLayout` called `child_layout`. We then use `addLayout` to add `child_layout` as a child layout within `parent_layout`.

`setLayout`, on the other hand, is used to set the layout of a widget directly. It takes a reference to a layout as an argument and sets that layout as the top-level layout for the widget. For example:

```python
widget = QWidget()
layout = QVBoxLayout()
widget.setLayout(layout)
```

In this example, we create a `QWidget` called `widget` and a `QVBoxLayout` called `layout`. We then use `setLayout` to set `layout` as the top-level layout for `widget`.

So, the main difference between `addLayout` and `setLayout` is that `addLayout` is used to add a child layout to an existing layout, while `setLayout` is used to set the layout of a widget directly.


### addlayout vs setlayout in short 

In short, `setLayout` is used to set the layout for a widget, while `addLayout` is used to add a layout to another layout.