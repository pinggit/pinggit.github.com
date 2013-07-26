---
layout: post
title: "complexity of xixibook"
published: false
created:  2013 May 20 07:56:14 PM
tags: [IM, photo]
categories: [tech]

---

<hr>

[TOC]

<hr>

# goals and example files

## the issue
I have scanned a lot of picutures/photos (totally around 800), the complexities
here are :

* when I scan them, I set different DPIs , sometime 200
* sometime I scan with input size A3 (for large pictures) , or A4
* I also have some other pictures that was taken by camrols.

## the goals

I want to re-format ALL of my pictures, and:

* make sure they can be printed to exactly (or at least roughly) the same physical size (A4),
* while at the same time, for bigger images only, don't lose resolutions
* for smaller image, I don't mind if they are expanded and thus lose some resolutions

so the whole purpose is,  later on I can merge them into a a pdf book with each
page has the same size, and thus to print hardcopies.  

it's easy for IM to convert between different format, resize, sample, and so
on...  but whenever I *resize* a large picture to smaller size, it looks not as
clear as the orignal ones, I guess I lost the resolutoin here.  

## example photos:

    2330996 May 20 20:35 a2-IMG_1626-1024x768-rotate90-density.pdf
     335121 May  9 16:27 a2-IMG_1626-1024x768-rotate90.pdf
     104206 May  9 18:22 a4-biru.pdf
      19542 May  9 17:40 b1-prefix_1.pdf
     165018 May  3 15:16 c-pg_0113.pdf
     235590 May  3 15:16 f-pg_0673.pdf

* [a2-IMG_1626-1024x768-rotate90.pdf](/images/xixibook-test/a2-IMG_1626-1024x768-rotate90.pdf)
* [a4-biru.pdf](/images/xixibook-test/a4-biru.pdf                      ) 
* [b1-prefix_1.pdf](/images/xixibook-test/b1-prefix_1.pdf                  ) 
* [c-pg_0113.pdf](/images/xixibook-test/c-pg_0113.pdf                    ) 
* [f-pg_0673.pdf](/images/xixibook-test/f-pg_0673.pdf                    ) 

# discussions/consulations

<http://www.imagemagick.org/discourse-server/viewtopic.php?f=1&t=23452>

# some basic knowledge
## A4 paper [pixel size][A4 pixel size] or [physical size]

## PDF "DPI" [don't have a DPI][PDF NO DPI]

## paper size/density/dimension/pixel/DPI/etc

from [fmw42][]:

>pixel dimensions don't equate to printed size. The latter depends upon the
>pixel dimensions and the density.
>
>So to keep the printed size the same you need to make sure that when you
>combine the pixel dimension with the density (resolution in inches or
>centimeters) so that it matches the physical printed size of the A4.
>
>According to http://www.imagemagick.org/script/comma ... s.php#page, A4 has a
>pixel dimension of 595x842 presumably at 72 dpi.
>
>Thus if you divide pixels dimensions x 72dpi you get 8.26 inches by 11.69
>inches. That seems to closely match https://en.wikipedia.org/wiki/Paper_size
>which say 8.27 × 11.69
>
>So what you want to do is find the image size (without resizing) and compute
>what density you need to achieve these printed sizes in inches. Then just set
>the density of the images.
>
>convert image -density XX -units pixelsperinch result
>
>To keep aspect ratio, you should not have -density XXxYY with different XX and
>YY. So you may need to either crop or pad your image appropriately.
>
>If you want smaller pixel dimensions than in your original image, you can
>resize and then do the same computations, but if you get too small pixel
>dimension, then you will lose quality and image will look blocky.
>
>Alternately, you can resize your images (cropping or padding) so that you can
>use a nominal density (say 150 or 300) for printing. So you have to work it the
>other way -- for the given density figure out what the pixel dimensions will
>need to be to achieve the given 8.26 inches by 11.69 inches


## [Avoid using ImageMagick for 'Vector Image' to 'Vector Image' conversions](http://www.imagemagick.org/Usage/formats/#vector)

>Their is more than one style of image storage in the world...
>
>* *Raster* 	
>    Images which are stored and processed using arrays of colored pixels.
>    Raster image formats include 
>
>    * GIF, 
>    * PNG, 
>    * JPEG, 
>    * TIFF, 
>    * and so on. 
>
>    Images can consist of multiple arrays (channels) representing different
>    colors, and can have multiple images, layers, or frames (depending on
>    usage) in the one image file format file.
>
>* *Vector* 	
>    Images are defined in terms of lines, thicknesses, tiles, gradients,
>    and larger compound objects. Formats include 
>
>    * SVG, 
>    * Postscript, 
>    * PDF,      <------
>    * FIG, 
>    * DXF, 
>    * WMF, and even 
>    * TTF fonts. 
>
>    It allows images to be resized, and even greatly enlarged without loss of
>    quality. Also while editing such formats, you can generally move whole
>    objects around without destroying what is underneath (object layering).
>
>* *Fractal* 	
>    Images are a special rare case, used to achieve extreme
>    compression of complex images, such as old paintings. However the only usage I
>    know about is in a very expensive commercial product. Outside that usage it is
>    also used for complex mathematical objects such as Mandelbrot and Julia sets,
>    and in generating randomized splashes of color in screen savers (IFS). It is
>    very rarely seen. 
>  ......
>    Avoid using ImageMagick for 'Vector Image' to 'Vector Image' conversions
>    EG: converting between formats like: PDF, PS, SVG 


## better scan in jpg/tif

--from [fmw42][]

>Scanning to a pdf is not advised if you want to do any post processing. You should be able to select other formats besides pdf. Typically there should be jpg and/or tif.
>
>The pdf will probably say 72 dpi, because that is the vector wrapper. You would need to use some other tool to extract the image from the vector wrapper. That is also why it is not advised to scan to pdf.
>
>If you must save a result as PDF, then it should be the last step.

## [pdfimage](http://www.cyberciti.biz/faq/easily-extract-images-from-pdf-file/)

# solutions

based on [this](http://www.imagemagick.org/Usage/formats/#vector) facts and
[consultations][], the solutions are:

1. extract images out of pdf , proceed based on it
   1. put them into OOO and resize manually, then print as pdf; or
   2. use IM to script

2. ignore the file size/internal algorithm hell, just force IM to handle the pdf
   the same way as other image formats.

# some tests

## density testing results

    convert a2-IMG_1626-1024x768-rotate90.pdf -density 93x88 a2-IMG_1626-1024x768-rotate90-density.pdf  

generates this [new pdf photo](/images/xixibook-test/a2-IMG_1626-1024x768-rotate90-density.pdf)

### the density is (wrongly) displayed as 72x72 forever

    $ identify -format "%x x %y" a2-IMG_1626-1024x768-rotate90-density.pdf 
    72 Undefined x 72 Undefined

    $ identify a2-IMG_1626-1024x768-rotate90-density.pdf 
    a2-IMG_1626-1024x768-rotate90-density.pdf PDF 595x838 595x838+0+0 16-bit Bilevel DirectClass 62.9KB 0.010u 0:00.010
    $ identify a2-IMG_1626-1024x768-rotate90.pdf 
    a2-IMG_1626-1024x768-rotate90.pdf PDF 768x1024 768x1024+0+0 16-bit Bilevel DirectClass 98.4KB 0.000u 0:00.000

So basically the result is:
* it's been shrunk (to an A4 paper size) as expected, good
* still looks clear
* file size grows much bigger (7 times!), this is not good

    2330996 May 20 20:35 a2-IMG_1626-1024x768-rotate90-density.pdf
     335121 May  9 16:27 a2-IMG_1626-1024x768-rotate90.pdf

## converting pdf to other format:`pdfimage` vs. `convert`

    $ pdfimages -j a2-IMG_1626-1024x768-rotate90.pdf test

    $ convert a2-IMG_1626-1024x768-rotate90.pdf test2.jpg

    $ identify test-000.jpg 
    test-000.jpg JPEG 768x1024 768x1024+0+0 8-bit DirectClass 327KB 0.000u 0:00.000

    $ identify test2.jpg 
    test2.jpg JPEG 768x1024 768x1024+0+0 8-bit DirectClass 227KB 0.000u 0:00.000

    $ identify -format "%x x %y" test-000.jpg 
    72 PixelsPerInch x 72 PixelsPerInch

    $ identify -format "%x x %y" test2.jpg 
    72 PixelsPerInch x 72 PixelsPerInch

generated files:

    327239 May 21 17:13 test-000.jpg
    226809 May 21 17:17 test2.jpg

* [a2-IMG_1626-1024x768-rotate90.pdf(original)](/images/xixibook-test/a2-IMG_1626-1024x768-rotate90.pdf)
* [test-000.jpg by pdfimage](/images/xixibook-test/test-000.jpg)
* [test2.jpg by convert](/images/xixibook-test/test2.jpg)
* visually, at least for me, there are no much difference

## another test of `pdfimage`

for this file [c-pg_0113.pdf(original)](/images/xixibook-test/c-pg_0113.pdf) 

    $ identify c-pg_0113.pdf 
       **** Warning: considering '0000000000 XXXXX n' as a free entry.

       **** This file had errors that were repaired or ignored.
       **** The file was produced by: 
       **** >>>> itext-paulo-155 (itextpdf.sf.net-lowagie.com) <<<<
       **** Please notify the author of the software that produced this
       **** file that it does not conform to Adobe's published PDF
       **** specification.

    c-pg_0113.pdf PDF 612x792 612x792+0+0 16-bit Bilevel DirectClass 61KB 0.000u 0:00.000

    $ pdfimages -j c-pg_0113.pdf c-pg_0113-pdfimage
    Error (425): Command token too long

    $ convert c-pg_0113.pdf -density 74x68 c-pg_0113-density74x68.jpg
       **** Warning: considering '0000000000 XXXXX n' as a free entry.

       **** This file had errors that were repaired or ignored.
       **** The file was produced by: 
       **** >>>> itext-paulo-155 (itextpdf.sf.net-lowagie.com) <<<<
       **** Please notify the author of the software that produced this
       **** file that it does not conform to Adobe's published PDF
       **** specification.

    $ identify c-pg_0113-density74x68.jpg 
    c-pg_0113.jpg JPEG 612x792 612x792+0+0 8-bit DirectClass 104KB 0.000u 0:00.000

    $ identify -format "%x x %y" c-pg_0113-density74x68.jpg 
    74 PixelsPerInch x 68 PixelsPerInch

generated files:

    $ ls -l
    total 12704
     131928 May 21 17:32 c-pg_0113-pdfimage-000.jpg
    6323873 May 21 17:20 c-pg_0113-pdfimage-000.ppm
    1053989 May 21 17:32 c-pg_0113-pdfimage-001.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-002.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-003.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-004.pbm
      37708 May 21 17:32 c-pg_0113-pdfimage-005.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-006.pbm
     159420 May 21 17:32 c-pg_0113-pdfimage-007.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-008.pbm
    103740 May 21 20:09 c-pg_0113-density74x68.jpg

* [c-pg_0113.pdf(original)](/images/xixibook-test/c-pg_0113.pdf                    ) 
* [c-pg_0113-density74x68.jpg(via IM)](/images/xixibook-test/c-pg_0113-density74x68.jpg)
* [c-pg_0113-pdfimage-000.jpg(via pdfimage](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-000.jpg)
* [c-pg_0113-pdfimage-000.ppm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-000.ppm)
* [c-pg_0113-pdfimage-001.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-001.pbm)
* [c-pg_0113-pdfimage-002.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-002.pbm)
* [c-pg_0113-pdfimage-003.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-003.pbm)
* [c-pg_0113-pdfimage-004.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-004.pbm)
* [c-pg_0113-pdfimage-005.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-005.pbm)
* [c-pg_0113-pdfimage-006.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-006.pbm)
* [c-pg_0113-pdfimage-007.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-007.pbm)
* [c-pg_0113-pdfimage-008.pbm](/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-008.pbm)

the interesting thing is, if you look at the jpg file that `pdfimage` extracted
from the original pdf, some parts of the drawing are missing... and they are put
in other `ppm` files.

My guess, based on the reading, is that the original drawing, when be scanned by
the printer, my printer happened to recognized some part of the drawing and
match them into some kinds of vector objects and hence stored in a different
format as a seperated objects, in the same PDF picture. that's why `pdfimage`
extract them into different files?

## other convert tools

to be tested (pstoedit,pstopnm,etc).

# final solution: [montage composition][] within a script

scripting image process

To simply the work, I wrote [this small shell script](/docs/xixibook/xixibook.sh) to do
the image processing work in batch mode. 

the lines that do the hardest work are :

       ...<snipped>...
       montage $picture1 $picture2 -geometry '612x792+1+1>' -frame 5 -set label '%f' -title "xixi's arts" $montage_dir/$montagefile_prefix-$pair.pdf
       ...<snipped>...
       pdftk $montage_dir/* cat output $montage_dir/$montage_dir-all-in-one.pdf
       ...<snipped>...

<hr>

[consultations]: http://www.imagemagick.org/discourse-server/viewtopic.php?f=1&t=23452
[PDF NO DPI]: http://forums.adobe.com/thread/285624
[A4 pixel size]: http://www.imagemagick.org/script/command-line-options.php#page
[A4 physical size]: https://en.wikipedia.org/wiki/Paper_size
[fmw42]: http://www.imagemagick.org/discourse-server/memberlist.php?mode=viewprofile&u=9098&sid=a1c3b9a348b0da9d0648d246dee84cc4
[montage composition]: http://www.imagemagick.org/Usage/montage/


<!--

# emails

## 1
experts:
I've been learning IM for a while, its amazingly powerful.
I'm reading a lot, but so far I couldn't find a good way to do what I wanted ...

the issue:

I have scanned a lot of picutures/photos (totally around 800), the complexities here are :

* when I scan them, I set different DPIs , sometime 200
* sometime I scan with input size A3 (for large pictures) , or A4
* I also have some other pictures that was taken by camrols.

my goals:
I want to re-format ALL of my pictures, and 
* make sure they can be printed to exactly (or at least roughly) the same physical size (A4), 
* while at the same time, for bigger images only,  don't lose resolutions
* for smaller image, I don't mind if they are expanded and lose some resolutions [/b]

so the whole purpose is, this way, later on I can merge them into a a pdf book with each page has the same size,  and to make hardcopies.

I know it's easy for IM to convert between different format, resize, sample, and so on...
but whenever I *resize* a large picture to smaller size, it looks not as clear as the orignal ones, I guess I lost the resolutoin here.
I'm wondering maybe I need to use some kind of *density* knobs, but no idea how to achieve this goal....


hope I can get some experts' advices...

thanks!

regards
ping

## 2
thanks a million guys for pointing these out!
 fmw42, I'll try what you say, see if I can put that calculation in a small cript...

based on these, I have a couple of more concerns:
1) [fmw42], first of all, when I scan these pictures, the scanner generate PDF format, I assume your method applys to PDF also ?right?

2) [GreenKoopa], I setup the scanner's DPI to 200 full color or sometime even 300DPI, 

but strangely, they all looks with a DPI 72 now regardless of what I set up in scanner...

    ping@640g-laptop:~/personal-materials/xinuosong/xixibook/xixibook-raw$ identify xixibook17.PDF 
    xixibook17.PDF[0] PDF 841x1189 841x1189+0+0 16-bit Bilevel DirectClass 126KB 0.030u 0:00.019
    xixibook17.PDF[1] PDF 841x1189 841x1189+0+0 16-bit Bilevel DirectClass 126KB 0.020u 0:00.019
    xixibook17.PDF[2] PDF 611x791 611x791+0+0 16-bit Bilevel DirectClass 126KB 0.020u 0:00.019
    ......
    xixibook17.PDF[19] PDF 611x791 611x791+0+0 16-bit Bilevel DirectClass 126KB 0.010u 0:00.000
    xixibook17.PDF[20] PDF 841x1189 841x1189+0+0 16-bit Bilevel DirectClass 126KB 0.010u 0:00.000
    ......
    xixibook17.PDF[22] PDF 841x1189 841x1189+0+0 16-bit Bilevel DirectClass 126KB 0.000u 0:00.000
    xixibook17.PDF[23] PDF 594x841 594x841+0+0 16-bit Bilevel DirectClass 126KB 0.000u 0:00.000
    xixibook17.PDF[24] PDF 594x841 594x841+0+0 16-bit Bilevel DirectClass 126KB 0.000u 0:00.000


    ping@640g-laptop:~/personal-materials/xinuosong/xixibook/xixibook-raw$ identify -format "%x x %y" xixibook17.PDF 
    72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 Undefined x 72 Undefined72 ......

    but according to this post: forums.adobe.com/thread/285624
    PDF "doesn't have a DPI", so I think the result of "identify" might be bogus?

if PDF is not supported, then what format shall I convert all my PDFs to , in order to proceed?

## 3
again thanks for the valueable infomations, I took a day to read/learn/test what you guys mentioned
so it all looks, my current issues are that my files are all in the PDF format, not easy for IM to process

so my issues are:

1. is it really that impossible (although hard) to achieve my goal based on PDF file, using IM?
2. shall I convert my PDF to what other format to proceed ? if yes, how about IM's convert command?

### for 1 , I did some testing:

according to [this link](http://www.imagemagick.org/Usage/formats/#vector) you pointed:

> Consequently if you are trying to convert a image from a vector format, to another vector format, IM will essentially rasterize this image at the currently defined resolution or density which will hopefully (but unlikely) be suitable for the output device you intend to use it on. 

so I did a test:

for [this file](http://pinggit.github.io/images/xixibook-test/a2-IMG_1626-1024x768-rotate90.pdf)

    $ identify a2-IMG_1626-1024x768-rotate90.pdf 
    a2-IMG_1626-1024x768-rotate90.pdf PDF 768x1024 768x1024+0+0 16-bit Bilevel DirectClass 98.4KB 0.000u 0:00.000

I use this command:

    convert a2-IMG_1626-1024x768-rotate90.pdf -density 93x88 a2-IMG_1626-1024x768-rotate90-density.pdf

and I got [this new pdf](http://pinggit.github.io/images/xixibook-test/a2-IMG_1626-1024x768-rotate90.pdf)

$ identify a2-IMG_1626-1024x768-rotate90-density.pdf 
a2-IMG_1626-1024x768-rotate90-density.pdf PDF 595x838 595x838+0+0 16-bit Bilevel DirectClass 62.9KB 0.010u 0:00.010

the `-density` value (93x88) are calculated based on the theory I learned from fmw42, so it's (1024/11.69 x 768/8.27)

I look at it, and print them to 2 A4 paper, for me basically, it looks the new file achieved what I hoped:
the size was shrunk to fit in an A4 paper for printing, but still looks as clear as the original one (not sure if it's more clearer)

these are good, but the only thing bad is, the new file is much *bigger (7 times in Bytes!)* than the original old one:

    2330996 May 20 20:35 a2-IMG_1626-1024x768-rotate90-density.pdf      <-new file
     335121 May  9 16:27 a2-IMG_1626-1024x768-rotate90.pdf
 
I'm guessing this was due to the internal tricks that IM is currently using , to convert between PDF (vector) images.

another thing I noticed, is that the DPI value we got from `identify` command seems to be 72DPI forever, even for the new file, which should be with DPI of 93x88, so it *IS* a bogus value, although my pdf image just contains one single picture in it.

but then even the pixel dimension it displayed (768x1024) is also bogus?

### for 2, I also did some test
I tested with 2 methods:

1. convert to *jpg* with IM's convert command
2. convert via [pdfimage tool](http://poppler.freedesktop.org/)

#### first test: real picture
I first tried to convert [the same pdf photo](http://pinggit.github.io/images/xixibook-test/a2-IMG_1626-1024x768-rotate90.pdf) as above

    $ pdfimages -j a2-IMG_1626-1024x768-rotate90.pdf test
    $ convert a2-IMG_1626-1024x768-rotate90.pdf test2.jpg

    $ identify test-000.jpg 
    test-000.jpg JPEG 768x1024 768x1024+0+0 8-bit DirectClass 327KB 0.000u 0:00.000

    $ identify test2.jpg 
    test2.jpg JPEG 768x1024 768x1024+0+0 8-bit DirectClass 227KB 0.000u 0:00.000

    $ identify -format "%x x %y" test-000.jpg 
    72 PixelsPerInch x 72 PixelsPerInch

    $ identify -format "%x x %y" test2.jpg 
    72 PixelsPerInch x 72 PixelsPerInch

the generated files are here:
[via pdfimage](http://pinggit.github.io/images/xixibook-test/test-000.jpg)
[via convert](http://pinggit.github.io/images/xixibook-test/test2.jpg)

as I can tell:

* there are no difference, in terms of pixel size and resolution
* both picture looks as clear as the origial one
* just the IM version is 1/3 smaller than pdfimage version

#### second test, drawings

I then did another test, this time the PDF under my test is not a real picture, but some drawings:
[oringal file](http://pinggit.github.io/images/xixibook-test/c-pg_0113.pdf)

again I convert them into jpg via both tools.

interestingly, this time pdfimage generate a lot of files, while IM's convert only generate one file.

    $ identify c-pg_0113.pdf 
       **** Warning: considering '0000000000 XXXXX n' as a free entry.

       **** This file had errors that were repaired or ignored.
       **** The file was produced by: 
       **** >>>> itext-paulo-155 (itextpdf.sf.net-lowagie.com) <<<<
       **** Please notify the author of the software that produced this
       **** file that it does not conform to Adobe's published PDF
       **** specification.

    c-pg_0113.pdf PDF 612x792 612x792+0+0 16-bit Bilevel DirectClass 61KB 0.000u 0:00.000

    $ pdfimages -j c-pg_0113.pdf c-pg_0113-pdfimage
    Error (425): Command token too long

    $ convert c-pg_0113.pdf -density 74x68 c-pg_0113-density74x68.jpg
       **** Warning: considering '0000000000 XXXXX n' as a free entry.

       **** This file had errors that were repaired or ignored.
       **** The file was produced by: 
       **** >>>> itext-paulo-155 (itextpdf.sf.net-lowagie.com) <<<<
       **** Please notify the author of the software that produced this
       **** file that it does not conform to Adobe's published PDF
       **** specification.

    $ identify c-pg_0113-density74x68.jpg 
    c-pg_0113.jpg JPEG 612x792 612x792+0+0 8-bit DirectClass 104KB 0.000u 0:00.000

    $ identify -format "%x x %y" c-pg_0113-density74x68.jpg 
    74 PixelsPerInch x 68 PixelsPerInch

generated files:

    $ ls -l
    total 12704
     131928 May 21 17:32 c-pg_0113-pdfimage-000.jpg
    6323873 May 21 17:20 c-pg_0113-pdfimage-000.ppm
    1053989 May 21 17:32 c-pg_0113-pdfimage-001.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-002.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-003.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-004.pbm
      37708 May 21 17:32 c-pg_0113-pdfimage-005.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-006.pbm
     159420 May 21 17:32 c-pg_0113-pdfimage-007.pbm
    1053989 May 21 17:32 c-pg_0113-pdfimage-008.pbm
    103740 May 21 20:09 c-pg_0113-density74x68.jpg

they can be accessed in here:

http://pinggit.github.io/images/xixibook-test/c-pg_0113.pdf
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-000.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-001.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-002.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-003.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-004.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-005.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-006.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-007.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-pdfimage/c-pg_0113-pdfimage-008.jpg
http://pinggit.github.io/images/xixibook-test/c-pg_0113-density74x68.jpg

the interesting thing is, if you look at the jpg file that `pdfimage` extracted
from the original pdf, some parts of the drawing are missing... and they are put
in other `ppm` files.

My guess, based on the reading, is that the original drawing, when be scanned by
the printer, my printer happened to recognized some part of the drawing and
match them into some kinds of vector objects and hence stored in a different
format as a seperated objects, in the same PDF picture. that's why `pdfimage`
extract them into different files?



## 4

hi  GreenKoopa:
thanks for the summarization, I think you hit the essential of my issues here.


1. You are starting with scanned-in PDFs. For images this possibly wasn't the
   best or easiest choice, but not necessarily catastrophic if you already have
   hundreds of scans. IM or otherwise, you probably need to extract the images
   before you can do anything with most any tool.

[ping]: I'm now learning what's the best tools to achieve that, some above links pointed to:

    >Solutions include

    >    "pstoedit" to convert to other vector formats such as SVG.
    >    "pdftoppm" from the "ghostscript" package.
    >    "pdfimage" from the "xpdf" package. 

    >Another posibility presented by Wolfgang Hugemann is to directly extract any
    >image contained by a PDF (especially from PDF's generated by scanners).
    >Basically by extracting any byte sequence between "stream" and "endstream",
    >and saving as a separate file. 

I'm testing them one by one and see how to use them well...

2. Is a PDF book the firm goal? Or are you just trying to resize (set DPI) and
   print?

[ping]: the PDF book is not the firm goal, but just a side product. I just want
to produce something (preferably PDF, but can be anything), that I can then
later send to the printing agent, so they can generate a decent-looking hardcopy
(with all images fit in A4 size nicely) for me.

3. You haven't mentioned any need for image processing or for scripting, so why
   IM? Why not extract the images from the scanned PDFs, import them into
   OpenOffice or whatever, resize the images and layout your pages, and save as
   a PDF?

[ping]: I'm not mean to script, but only goal is to have a consistent looking
hardcopy book as I mentioned about. the method you mentioned here is also a good
hint. initially I thought since I have around 800 drawings (including a few
photos), I was thinking get nice CLI tools (like IM) is good for scripting...

so it all looks I now need to quick/tested way to extract PDF to images, do you
know of any verified easy way to do that? Otherwise I'm still spending days to
study those CLI tools (IM,pstoedit,...), while my deadline of the book delivery
are approaching :( ...

thanks as always!


-->
