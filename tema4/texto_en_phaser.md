---
title: Texto en Phaser
...


# Crear texto usando fuentes del sistema

---

Para crear texto simplemente podemos usar la clase `Phaser.GameObjects.Text`{.js} con la factoría de Phaser `add.text`{.js} de `Scene`{.js}

---

Pero podemos modificar los atributos de `text`{.js} para cambiar su aspecto como:

* `setAlign`{.js}: alineación del texto
* `setFont`{.js}: tipo de letra
* `setFontSize`{.js}: tamaño
* `setStroke`{.js}: color del borde y grosor
* `setFill`{.js}: color de relleno

---

```js
// this es una `Scene`
let text = this.add.text(this.cameras.main.centerX, this.cameras.main.centerY, '- phaser text stroke -');

// alineación del texto
text.setAlign('center');

// Font style
text.setFont('Arial Black');
text.setFontSize(50);

//Color del reborde de la letra y grosor.
text.setStroke('#000000', 6)
text.setFill('#43d637');
text.setShadow(5, 5, 'rgba(0,0,0,0.5)', 5);
```













# Problema de las fuentes del sistema


---

Una fuente de nuestra máquina puede no estar disponible en la máquina del usuario

¿Solución? Usar fuentes estándar, crear nuestras propias fuentes de mapa de bits (bitmaps) o usar fuentes Web (**webfonts**) como [Google Fonts](https://fonts.google.com/)

---


## Texto con fuentes de mapa de bits

Para cargar un fuente de mapa de bits hay que usar `scene.load.bitmapFont()`{.js} en el `preload`{.js}

Hay que pasarle el bitmap (en [PNG](https://es.wikipedia.org/wiki/Portable_Network_Graphics), por ejemplo) con las fuentes y el XML que las describe

---

Para generar el XML y el mapa de bits podemos usar:

- [Littera](http://kvazars.com/littera/)
- [Bmfont](http://www.angelcode.com/products/bmfont/) (Windows) 

---

```js
preload(){
    this.load.bitmapFont(
        'bitmapFont', 'assets/fonts/bitmapFonts/bitmapFont.png',
        'assets/fonts/bitmapFonts/bitmapFont.xml');
}
create(){
    this.greeting = this.add.bitmapText(200, 100, 'bitmapFont','Bitmap Fonts!', 64);
}
```













# Texto con fuentes Web

---

Podemos cargar fuentes desde la web, por ejemplo desde Google Fonts

Hay que cargar la fuente previamente antes de usarla

---

Cargamos el código para usar webfonts:

```js
preload() {
    this.load.script('webfont', 'https://ajax.googleapis.com/ajax/libs/webfont/1.6.26/webfont.js');
}
```

---

Después, llamamos a `WebFont.load()`{.js}:


```js
create() {
    WebFont.load({
        google: {
            families: [ 'Freckle Face', 'Finger Paint', 'Nosifer' ]
        },
        active: function () // se llama a esta función cuando está cargada
        {
            let nuevoTexto = 
                this.add.text(16, 0, 
                    'The face of the\nmoon was in\nshadow.', 
                    { fontFamily: 'Freckle Face', fontSize: 80, color: '#ffffff' })
            nuevoTexto.setShadow(2, 2, "#333333", 2, false, true);
        }
    });
}
```

---

## ¿Problemas de las Google Fonts u otras fuentes Web?

Que dependemos de ellas para que el juego funcione y no tenemos control sobre ellas

