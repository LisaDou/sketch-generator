# Sketch Generator

**PLEASE NOTE: development on this project has been frozen, since I consider that the new export tools in Sketch 3, combined with [sketchtool](http://bohemiancoding.com/sketch/tool/) make this plugin unnecessary.** Feel free to fork & modify, but please don't file issues since they won't really be fixed. I considered deleting the project, but since the code may still have a use for learning purposes I'll just leave it in a suspended animation state.

This command is a recreation for Sketch of the Photoshop Generator functionality introduced by Adobe on Photoshop CC (see [this blog post on Adobe](http://blogs.adobe.com/photoshopdotcom/2013/09/introducing-adobe-generator-for-photoshop-cc.html) for more information).

It is a work in progress: most features in Photoshop Generator are implemented, but some are not there yet due to either lack of time or current technical limitations in Sketch (see the **Pending Features** section below).


## What is this?

If you've ever had to prepare a screen design for production use, you know how painful and time consuming it is: creating slices, naming them, making sure they're properly aligned, painstakingly exporting assets...

Well, it's 2013, and slicing images is *so* last century. Computers were invented to let us work less and spend more time watching kitten videos, so get ready to reclaim some of your precious time back.

Sketch Generator will let you export *all* your assets, no matter how complex your design, with a single keystroke. Forget about slicing, exporting, or moving files manually: welcome to the future, where everything that can be made automatically *is made automatically* :)

## Installation

- Just [download the latest release](https://github.com/bomberstudios/sketch-generator/releases/latest), and double click **Generate Assets.sketchplugin** to have Sketch install it for you :)

### If you're using both the beta and stable, and know your way around a command line

1. cd to ~/ (or wherever you prefer)
2. git clone https://github.com/bomberstudios/sketch-generator
3. ln -s ~/sketch-generator/Generate\ Assets.sketchplugin ~/Library/Containers/com.bohemiancoding.sketch/Data/Library/Application Support/sketch/Plugins/Generate\ Assets.sketchplugin
4. ln -s ~/sketch-generator/Generate\ Assets.sketchplugin ~/Library/Application\ Support/sketch/Plugins/Generate\ Assets.sketchplugin

## Usage

- Open your Sketch document
- Find an element you want to export as an asset (say, a button)
- Name the layer or layer group using the rules in the **Rules** section (i.e: 'button.png, button@2x.png 200%')
- Run Generator by either choosing it from the Plugins menu, or pressing the keyboard shortcut (Ctrl + Alt + Command + G)
- A new folder named "your-document-name-assets", containing all your assets grouped by Page and Artboard will be created in your document's current location.

## Features

So far, it supports the following Photoshop Generator features:

- Multiple assets per layer / layer group
- Export assets in JPG, PNG & GIF formats
- Arbitrary & unlimited asset scaling in output (extreme example: I've used a 10000% scale to export a 31800 × 9800 pixels JPG. Takes some time, but it works :)

In addition to that, the following are Sketch Generator-only features:

- Export assets in PDF, SVG, EPS & TIFF format
- **Export selection only**: if you have a selection when running the command, only the selected assets will be generated. This is useful for quick exports in complex documents, where you don't want to export the whole shebang.
- If you add a "@bounds" layer at the bottom of your layer group, it will be used for dimensions but won't get exported. This is usefull to use as a testing background for icons, where you want to keep the background transparent when exporting.

## Rules

Here are some examples of supported tags (beware: not all are supported, see **Pending Features** section):

- .png (Default value: png32 with semi-transparent alpha), .png8, .png24, .png32
- .jpg (Default value: 9), .jpg(1-10), .jpg(1-100%)
- .gif
- 1-n%, (Number) px x (Number) px for scaling
- can also so '200x? logo.jpg', apparently

Here are some examples of how tags can be used:

- “200% logo-retina.png, logo.png” produces both a 2x and a 1x asset
- “heroImage.jpg10” produces a 1x asset with max quality
- “400% tuningfork.png, 250×250 tuningfork.jpg40%” produces a 4x PNG asset and a custom-scaled JPEG asset

For a more complete list of layer names this should support, check the tests in <https://github.com/adobe-photoshop/generator-assets/blob/master/test/test-parse-layer-name.js>


## Pending Features

### Not yet implemented, but feasible

- Set asset size in pixels (using XXX px x YYY px or the shorthand XXXx? to scale proportionally)
- Use fractional units (yeah, this is a #WTF, but it's there in Photoshop Generator)
- Use '+' as filename separator
- Export on save (this can be faked via a keyboard shortcut trick)

### Not implemented due to lack of technical support in Sketch

- Export as WebP.
- Set JPG export quality. Reason: there’s no API in Sketch yet.
- Set PNG export format (PNG8, PNG24, PNG32). Reason: there’s no API in Sketch yet.
- Realtime export on layer modification. Reason: Sketch lacks a realtime backend (Photoshop is using a node.js backend for Generator)
- Export dimensions other than pixels. Reason: Sketch is a screen design tool. Why would you want to use inches?

### Upcoming features not included in Photoshop Generator

- Export for all Android pixel densities
- Add support for '@2x' and 'HDPI' style scales
- Export only layer groups, in PNG format, without requiring layer renames (this is how Sketch Framer works currently, and I think it makes more sense than Adobe's choice)

