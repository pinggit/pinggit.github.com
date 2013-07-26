---
layout: post
title: "ascii art:shaape"
published: true
created:  2013 Apr 29 08:17:46 PM
tags: [asciiart, shaape]
categories: [tech]
---

## production work use
[`shaape`](https://github.com/christiangoltz/shaape) is a nice tool to render
asciiart into the real graph.

[***this***](/docs/asciiart-network-topology.txt) funny looking `asciiart` texts
can be rendered into :


![asciiart shaape](/images/asciiart-network-topology.png)


[***this***](/docs/flow-chart.txt) asciiart flow chart can be rendered into: 


![asciiart shaape](/images/flow-chart.png)

## (2013-05-11) more on this tool:
here is the command of `shaape` to render the asciiart:

    shaape -o /home/ping/pinggitblog/images/asciiart-network-topology.png -s 0.5 myasciiart.txt

if you are a VIMer, natually it's going to be, under the asciiart file, and type:

    :w !shaape -o /home/ping/pinggitblog/images/asciiart-network-topology.png -s 0.5 -&

the short usage:

    ping@640g-laptop:~$ shaape --help
    usage: shaape [-h] [-o OUTFILE] [--hash] [-t {png,svg,pdf,eps}] [-s SCALE]
                  [--width WIDTH] [--height HEIGHT]
                  infile

    - Asciiart to image processing

    positional arguments:
      infile                input file, use - for stdin

    optional arguments:
      -h, --help            show this help message and exit
      -o OUTFILE, --outfile OUTFILE
                            output file, will be infile.png if not specified
      --hash                only update the image if the hash sum of t: png svg
                            pdf epshe input changed
      -t {png,svg,pdf,eps}, --type {png,svg,pdf,eps}
                            image type to generate
      -s SCALE, --scale SCALE
                            scale factor of the resulting image
      --width WIDTH         width of the resulting image in pixels
      --height HEIGHT       height of the resulting image in pixels

here we only use `-o` (output file) and `-s 0.5` (scale half size to make it fit
in the blog page better).

[the README source file](https://github.com/christiangoltz/shaape) (and the [the
README HTML file](/docs/shaape-README.html)) provide more usage
tips/rules/examples,
e.g
[***this file***](https://github.com/christiangoltz/shaape/blob/master/shaape/tests/input/feature_multiple_boxes_same_name.shaape)

    +-----------------------------+
    |        +--------+           |
    |        |        |           |
    |+------------------+         |
    ||       |        | |         |
    ||    +-------------|-----+   |
    ||    |  |  +---+ | |     |   |
    ||    |  |  |box| | |     |   |
    ||    |  |  +---+ | |     |   |
    ||    |  +--------+ |     |   |
    |+------------------+     |   |
    |     |                   |   |
    |     |                   |   |
    |     +-------------------+   |
    +-----------------------------+

renders into:

![this](/images/feature_multiple_boxes_same_name.shaape.png)

see more examples here: 
[**asciiart**](https://github.com/christiangoltz/shaape/tree/master/shaape/tests/input)
source, and the rendered 
[**images**](https://github.com/christiangoltz/shaape/tree/master/shaape/tests/input)

if you think it's complicated to draw the asciiart in your current editor, there 
are a couple of great helper tools available. e.g.
[asciio](http://search.cpan.org/dist/App-Asciio/lib/App/Asciio.pm) or
[drawit](http://www.vim.org/scripts/script.php?script_id=40)

too complex? too simple? try it in your word/visio ...

