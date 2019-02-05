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

### Installing
Download compiled library from the last release;
Include jar lib on your project.


### Compiling
I used the following development tools. But it might work with other versions or even another tools.
Apache Ant(TM) version 1.10.5
Netbeans 8.2
java version "1.8.0_172"

The lib and samples can be compiled with above commands:
```
cd src/escpos_coffee
ant clean
ant  jar
```

## Samples
You can find samples code on src/samples directory.
how to run samples:
```
java -jar samplename.jar "printer name"
```

### getstart
Simply send info of the library to the printer.

### textstyle
Shows how to construnct one simple receipt.
Also this sample show how simple is to create diferent text styles, like title, subtitle, bold, etc.
```
  Style title = new Style()
          .setFontSize(Style.FontSize._3, Style.FontSize._3)
          .setJustification(EscPosConst.Justification.Center);
```

### graphicsimage, bitimage and rasterimage
Shows how to work with ImageWrapper.
Then you will see things like how to print on center-justified one image, like this: 
```
    escpos.writeLF("print on Center");
    imageWrapper.setJustification(EscPosConst.Justification.Center);
    escpos.write(imageWrapper, escposImage);
```

### dithering
Shows how to work with BitonalThreshold and BitonalOrderedDither. 
Bellow, we can see how to use ordered dither class.
```
  algorithm = new BitonalOrderedDither();
  escposImage = new EscPosImage(imageBufferedImage, algorithm);     
  escpos.write(imageWrapper, escposImage);

```
### barcode
Samples of barcode, PDF417 and qrcode.
Bellow, code to send barcode to the printer

```
  BarCode barcode = new BarCode();
  escpos.write(barcode, "hello barcode");
```

### codetable
Shows how to send texts from different languages.
```
  escpos.setCharacterCodeTable(CharacterCodeTable.CP863_Canadian_French);
  escpos.writeLF("Liberté et Fraternité.");
```

## Versioning
Using [SemVer](https://semver.org) for versioning.



