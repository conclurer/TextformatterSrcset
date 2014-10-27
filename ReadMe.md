# TextformatterImageSRCSET
 
This is a Textformatter for the [ProcessWire CMS](http://www.processwire.com). It will add the [srcset](http://responsiveimages.org) and sizes attributes to every `img` tag inside a field. This enables your site to make better use of responsive/adaptive images even when they were created by a regular editor inside e.g. a Textarea. 
 
The formatter requires ProcessWire 2.5+. It will generate lots of different image variations that might fill up your storage. _Use it on your own risk._

 
## Features
- Create srcset and sizes attributes
- Generate the right image resolutions on the fly
- Simple HiDPI/Retina images
- Use a low-quality placeholder as the src
- Easy Usage with the respimg.js and lazyload.js scripts from XXX
- Configurable to fit your needs
- Respects all settings from the CKEditor or other ProcessWire modules
 
![Screenshot Configuration](https://www.conclurer.com/site/assets/files/1133/textformattersrcset-screen.jpg)
## Setup
Please note, that this module only affects fields where the Textformatter ist active. For images outside of the fields, you have to create the markup for srcset images yourself. 

Install it like any other Textformatter for ProcessWire:

1. Install the module
2. Configure the module
3. Go e.g. to your `body` field, go to the `Details` page and add TextformatterSrcset

## Settings
You can find those settings on the module configuration page. 
 
### Resolutions
Enter the different sizes you want to have in your srcset-attribute. Those will be used as the *w values and images will be created accordingly. For example, if you have a 960px large grid with breakpoints at 720px and 320px, you enter  `320,720,960 ` into this field. Note, that the HiDPI option might add another value to this.
 
Example with those three values and sizes set to “auto”:
```html
<img alt="" src="/site/assets/files/1013/desert.993x0-is.jpg" sizes="auto" srcset="/site/assets/files/1013/desert.320x0.jpg 320w,/site/assets/files/1013/desert.720x0.jpg 720w,/site/assets/files/1013/desert.960x0.jpg 960w"/>
```
 
 
This does depend on the orientation of the image. The longer side of the image will be resized to fit to the value.
 
### Sizes-Attribute
This field will directly populate the sizes attribute of the image tag.  You might want to leave the default value “auto” or set it to the maximum width in pixel that images will be displayed.
 
### Generate HiDPI images
This will create an image for high density displays (“retina”). As long as the original image is larger than the target image, it will create an image with the twice the resolution of the source. This will be added as an additional size to the  `srcset `, so you don’t need to specify this image in the Resolutions tab. When no resolutions are set, it will use the  `1x,2x `notation for the srcset.
 
Example without Resolutions:
```html
<img  alt="" src="/site/assets/files/1013/desert.993x0-is.jpg" sizes="" srcset="/site/assets/files/1013/desert.993x0-is.jpg 1x, /site/assets/files/1013/desert.1986x0.jpg 2x"/>
```
 
It is recommended to activate this feature.
 
### Low-quality Placeholder
When active, the Formatter will create a really low quality image (small resolutions, low JPG setting) and use it as the default  `src `.  This can speed up the page. This is recommended if you have a Javascript-Fallback active that will exchange the LQP with the right image in browsers that don’t support  `srcset ` yet. Remember that the  `src ` is always a fallback for older browser/no JS browser and will always be loaded by every browser.
 
Example, with only LQP activated:
```html
<img alt="" src="/site/assets/files/1013/desert.204x0.jpg" sizes="" srcset="/site/assets/files/1013/desert.993x0-is.jpg 1x"/>
```
### Use smallest size as LQP
Instead of using a low-quality JPG as the LQP, use the smallest size from the Resolution setting as the  `src `. This file might be larger because it uses your default ProcessWire Image quality configuration but provides a better fallback for older browsers.
 
### Width/Height Attributes
If activated, it will add a width and height attribute to the  `img `. The width is the one set by the Textarea Editor. When used with the HiDPI option, it will prevent images from becoming too large.
 
### Data* Attributes
Use this to prefix the sizes and the  `srcset ` attribute with data-*. This means, that  `srcset ` will become  `data-srcset `. Might be required by some fallbacks or lazyloading scripts.
 
### CSS Class
Values entered here will be added as a CSS-class to the `img`. Note, that any classes set by the Textarea/Editor will be kept.

## Example usage scenarios
These examples can be quickly implemented.
#### Make Apple Retina users happy (also HiDPI visitors)
1. Activate the "HiDPI" and the "width/height Attribute" options. Leave the "Resolutions" field blank.
2. Place the polyfill [respimage.js](https://github.com/aFarkas/respimage) on your page. 

#### Integrate lazy-loading images 
1. Activate the Low-quality placeholder and the data-* attributes. Leave the "Resolutions" blank.
2. Enter `lazyload` into the "CSS Class" field.
3. Make sure that the [lazysizes](https://github.com/aFarkas/lazysizes) script is included in your sites markup

#### 

 
## Further information
### Other PageImage fields
This Textformatter is compatible with every other type of PageImage. This means, that the great (new) [ImageFocusArea module](https://processwire.com/talk/topic/8079-imagefocusarea/) will work with this and even use the correct sizing options.
 
### Useful JS libraries
Best used together with
- [Arkas Lazysizes](https://github.com/aFarkas/lazysizes), a superfast, flexible and easy-to-use Image lazyloader
- [Arkas respimage](https://github.com/aFarkas/respimage), the easist way to get all browser to use the new srcset images.
 
### Thanks
We would like to thank 
- Martijn Geerts for some parts of the image search code
- Horst Nogajski for helping finding the right image field
 
### Improve more
You can try this module on our [one-click ProcessWire Hosting Service lightning.pw](https://lightning.pw) or make the images even smaller with the [image compression service minimize.pw](https://minimize.pw).

