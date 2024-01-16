utilisation de prototype dans backbone  : [[prototype vs attributes]]
```js
Model.prototype[options.panelName] = this;
```

```chatgpt
you're not actually causing the model to inherit something from the view instance (`this`). Instead, you're adding a property to the prototype of the model class (`Model`) and assigning the view instance (`this`) to that property.
```
