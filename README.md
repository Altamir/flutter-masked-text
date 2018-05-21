# flutter_masked_text

Masked text input for flutter.

![logo](doc/flutter_logo.png)

## Install

On your dependencies, add:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_masked_text: ^0.3.0 #here
```

In terminal, run:
```
flutter packages get
```

## Usage
Import the library
```dart
import 'package:flutter_masked_text/flutter_masked_text.dart';
```

Create your mask controller:
```dart
var controller = new MaskedTextController(mask: '000.000.000-00');
```

Set controller to your text field:
```dart
return new MaterialApp(
    title: 'Flutter Demo',
    theme: new ThemeData(
        primarySwatch: Colors.blue,
    ),
    home: new SafeArea(
        child: new Scaffold(
            body: new Column(
                children: <Widget>[
                    new TextField(controller: controller,) // <--- here
                ],
            ),
        ),
    ),
);
```

This is the result:

![sample](doc/mask.mov.gif)

## Mask Options

In mask, you can use the following characters:
* `0`: accept numbers
* `A`: accept letters
* `@`: accept numbers and letters
* `*`: accept any character

## Initial Value
To start a mask with initial value, just use `text` property on constructor:
```dart
var controller = new MaskedTextController(mask: '000-000', text: '123456');
```

## Update text programaticaly
If you want to set new text after controller initiatialization, use the `updateText` method:
```dart
var controller = new MaskedTextController(text: '', mask: '000-000');
controller.updateText('123456');

print(controller.text); //123-456
```

## Using custom translators
If you want to use your custom regex to allow values, you can pass a custom translation dictionary:
```dart
const translator = {
    '#': new RegExp(r'my regex here')
};

var controller = new MaskedTextController(mask: '####', translator: translator);
```

If you want to use default translator but override some of then, just get base from `getDefaultTranslator` and override what you want (here is a sample for obfuscated credit card):
```dart
var translator = MaskedTextController.getDefaultTranslator(); // get new instance of default translator.
translator.remove('*'); // removing wildcard translator.

var controller = new MaskedTextController(mask: '0000 **** **** 0000', translator: translator);
controller.updateText('12345678');

print(controller.text); //1234 **** **** 5678
```

## Using default TextEditingController
The MaskedTextController extends TextEditingController. You can use all default native methods from this class.

## TODO
- [x] Custom translations
- [ ] Raw Text Widget
- [ ] Money Mask
- [ ] Default Pre-Sets like CPF, CNPJ, Date, Credit Card