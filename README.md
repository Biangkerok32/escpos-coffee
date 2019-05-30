# escpos-coffee

Java library for ESC/POS printer commands. Can send text, images and barcodes to the printer.
All commands are send to one OutputStream, than you can redirect to printer, file or network.

## Getting Start
The EscPos works with OutputStream to send its commands. Here we have two examples that show different output streams.

Creating printer output stream:
```
  PrintService printService = PrinterOutputStream.getPrintServiceByName("printerName");
  PrinterOutputStream printerOutputStream = new PrinterOutputStream(printService);
  EscPos escpos = new EscPos(printerOutputStream);
  escpos.writeLF("Hello Wold");
  escpos.feed(5);
  escpos.cut(EscPos.CutMode.FULL);
  escpos.close();

```

Sending hello world to system out:
```
  EscPos escpos = new EscPos(System.out);
  escpos.writeLF("Hello Wold");
  escpos.feed(5);
  escpos.cut(EscPos.CutMode.FULL);
  escpos.close();
```
See on samples directory to view more codes.



### Downloading
Download code and binaries from the [last release of escpos-coffee](https://github.com/anastaciocintra/escpos-coffee/releases/latest).




### Compiling
I used the following development tools. But it might work with other versions or even another tools.

Apache Ant(TM) version 1.10.5

Netbeans 8.2

java version "1.8.0_172"

The project can be compiled with below commands:
```
./mvnw clean package
```

## Samples
You can find samples code on src/samples/ directory.
Download the binaries [here](https://github.com/anastaciocintra/escpos-coffee/releases/latest).
how to run samples:
```
java -jar samples/[samplename]/target/[samplename].jar "printer name"
```

### getstart.jar
Send info of the library to the printer.

![output](sample_images/info.png?raw=true "output")


### textstyle.jar

Shows how to construnct one simple receipt.

![output](sample_images/style.png?raw=true "output")


Also this sample show how simple is to create diferent text styles, like title, subtitle, bold, etc.

```
  Style title = new Style()
          .setFontSize(Style.FontSize._3, Style.FontSize._3)
          .setJustification(EscPosConst.Justification.Center);
```



### graphicsimage.jar, bitimage.jar and rasterimage.jar

Shows how to work with ImageWrapper.

Then you will see things like how to print on center-justified one image, like this: 
```
    escpos.writeLF("print on Center");
    imageWrapper.setJustification(EscPosConst.Justification.Center);
    escpos.write(imageWrapper, escposImage);
```

### dithering.jar

Shows how to work with BitonalThreshold and BitonalOrderedDither. 

![output](sample_images/threshould.png?raw=true "output")

![output](sample_images/ordered_dither.png?raw=true "output")


Bellow, we can see how to use ordered dither class.
```
  algorithm = new BitonalOrderedDither();
  escposImage = new EscPosImage(imageBufferedImage, algorithm);     
  escpos.write(imageWrapper, escposImage);

```
### barcode.jar

Samples of barcode, PDF417 and qrcode.

![output](sample_images/barcode.png?raw=true "output")

![output](sample_images/qrcode.png?raw=true "output")

![output](sample_images/pdf417.png?raw=true "output")


Bellow, code to send barcode to the printer

```
  BarCode barcode = new BarCode();
  escpos.write(barcode, "hello barcode");
```

### codetable.jar
Shows how to send texts from different languages.
```
  escpos.setCharacterCodeTable(CharacterCodeTable.CP863_Canadian_French);
  escpos.writeLF("Liberté et Fraternité.");
```

## Versioning

Using [SemVer](https://semver.org) for versioning.

Last release [here](https://github.com/anastaciocintra/escpos-coffee/releases/latest).


## Contributting 
Contributors are wellcome, 
but before you do it its important to read and agree with [CODE_OF_CONDUCT.md](https://github.com/anastaciocintra/escpos-coffee/blob/master/CODE_OF_CONDUCT.md) and [CONTRIBUTING.md](https://github.com/anastaciocintra/escpos-coffee/blob/master/CONTRIBUTING.md).

## Acknowledgments
I would like to thanks [Michael Billington](https://github.com/mike42) and contributors for the great work on the [mike42/escpos-php](https://github.com/mike42/escpos-php) project that inspired me to start this project.
