# Image **Processor**

[Edit on GitHub <svg width="14" height="14" xmlns="http://www.w3.org/2000/svg"><g fill="none" stroke="#F3652B"><path d="M4.81.71H.672v11.43H12.1V8.001" stroke-width=".8"/><path d="M6.87.786h5.155V5.94M6.31 6.5L12.026.786"/></g></svg>](https://github.com/aziontech/docs_en/edit/master/image-processor/index.md)

The Azion Image Processor automates your workflow for processing images.

Optimizing your images reduces their size, but without any perceivable loss of visual quality. This reduces their transfer time and improves the user’s experience. This makes your pages load better and speeds up navigation, without you needing to do practically anything.

You automate your workflow for processing images, using the functions to resize or edit your images or apply filters, without needing to manage dozens of versions and edits of each image in your library.

> 1. [Instructions](#instructions)
> 2. [Resize the image with auto-crop](#resize-with-auto-crop)
> 3. [Resize the image with fit-in](#resize-with-fit-in)
> 4. [Crop the image](#crop)
> 5. [Change image quality](#change-image-quality)
> 6. [Add a watermark to the image](#add-watermark)
> 7. [Convert image to another format](#convert-image-format)
> 8. [Fill image](#fill-image)
> 9. [Combine Filters](#combine-filters)

---

## 1. Instructions {#instructions}

We developed this product for people to be able to optimize, resize, crop and apply filters to their images, with the aim of making the user experience faster and more dynamic.

It supports the following formats: JPEG, GIF, PNG, BMP, ICO and WEBP (for [compatible browsers](https://caniuse.com/%23search=webp))

**How to configure Azion Image Processor**

To configure Azion Image Processor, take the following steps and, when necessary, check the technical manuals:

**Step 1: Set up or edit an Edge Application setting for sending your images.**

1.  Open up [Real-Time Manager](https://manager.azion.com/) and go into the Edge Services > Edge Application menu.
2.  If you have already set up an Edge Application setting for sending your images, jump straight to step 2.
3.  If not, set up an Edge Application setting for sending your images, following the [First Steps]({% tl documentation_first_steps %}#crie-uma-nova-configuracao) guide.

**Step 2: Set up Advanced Cache Key for your images**

> To make use of the resize and crop functions and apply filters to your images, you need to configure some of the various content for Query String

1.  Open the Edge Application setting that is responsible for sending your images, created in Step 1.
2.  In the Cache Settings tab, add or edit a cache policy customized for your images.
3.  Give your policy a suitable name, you will need to be able to identify it in Step 3.
4.  In the Expiration Settings section, configure the cache expiry policy for your images, follow the instructions you learned from the First Steps guidance; for images, Azion recommends that you choose times that are longer than the maximum TTL for the CDN Cache, for example, 7,776,000 seconds (3 months).
5.  In the Advanced Cache Key section, choose one of the following options:
    *   *Content varies by some Query String fields (Whitelist):* if you want to list all the fields in the Query String that will identify your images. Image Processor uses the *ims* field, so this has to be included in the list as one of the required fields for your image manager application. For this you need the **Application Acceleration** product.
    *   *Content varies by Query String, except for some fields (Blacklist):* if you only want to list those fields in the Query String that should be ignored to identify the objects in your cache. In this case, it guarantees that the *ims* field will be removed from the list. For this you need the **Application Acceleration** product.
    *   *Content varies by all Query String fields:* if you don’t know or aren’t sure about which fields to list in the Query String because you aren’t responsible for all the content in the cache or do not have the Application Acceleration product.
6.  In the other sections, edit the settings as required and save your cache setting.

**Step 3: Set up Image Processor**

1.  In the Rules Engine tab, add or edit a customized rule for one or more image paths.
2.  In the Path field, enter the path for your images or use the regex recommended by Azion *`\.(jpg|jpeg|gif|png|bmp)$`*
3.  Choose the logical operator **Matches**, if you used the regular expression in the Path field.
4.  In the Behavior field **Set Cache Settings**, select the preset used in Stage 2.
5.  Also select **Image Processor** in the Behavior field.
6.  In the other sections, use whatever settings are best for you and save the rule.

From this point on, images in the configured *path* will automatically be optimized. As well as this, Image Processor will detect whether the browser is compatible with the WEBP format and, where possible, it will try to automatically convert the format of the image, giving you yet another benefit. BMP images will also be automatically converted to JPEG or WEBP, depending on the browser’s compatibility.

**Real-Time Metrics** gives you a graph showing the *Bandwidth Saving* achieved, enabling you to monitor the savings you make from the optimization.

See below the other features of the product, configured as arguments in the Query String of the image’s URL.

---

## 2. **Resize the image with auto-crop** {#resize-with-auto-crop}

You can use Azion’s Image Processor to resize your images, without needing to manage multiple files in your image library.

Once an image is in your library, Image Processor can create images derived from it, as required, in the size that best suits your page.

You specify the required size as arguments in the Query String, in the format:

~~~
ims=WidthxHeight
~~~

*   Width: in pixels for the derived image
*   Height: in pixels for the derived image


To preserve the *aspect ratio* when you resize an image, just leave out one of the two dimensions, and it will be calculated automatically. Use *Widthx* to only specify the width and the height will be calculated proportionately, or *xHeight*, to specify just the height and the width will be automatically calculated.


You can also specify both dimensions, *Width* and *Height* and crop (*auto-crop*) the image to the required size. The image is cropped centrally and both horizontal and vertical sections may be adjusted, depending on the best fit with the specified dimensions.

Use the value *orig* for any of the image dimensions, if you wish to keep them at the original size.

**Sample results**

_http://yourdomain.com/image.jpg?ims=880x_ (880 pixels in width, automatic height)

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=880x)]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=880x)


_http://yourdomain.com/image.jpg?ims=880xorig_ (880 pixels in width, original height)

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=880xorig)]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=880xorig)


_http://yourdomain.com/image.jpg?ims=400x_ (400 pixels in width, automatic height)

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=400x)]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=400x)

_http://yourdomain.com/image.jpg?ims=400x400_ (400 pixels in width, 400 pixels in height)

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=400x400)]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=400x400)

_http://yourdomain.com/image.jpg?ims=x100_ (automatic width, 100 pixels in height)

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=x100)]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=x100)

---

## 3. Resize the image with fit-in {#resize-with-fit-in}

Another way to resize an image is to use fit-in:

~~~
ims=fit-in/WidthxHeight
~~~

*   Width: maximum width, in pixels for the derived image
*   Height: maximum height, in pixels for the derived image

The derived image will be resized to fit the specified area (Width x Height). The aspect ratio of the original image is kept and, if you like, you can hide one of the values.

Should the specified area be greater than the image’s size, the image will be blown up. The specified dimensions are parameters for *fit-in*. They represent the maximum area that the image may occupy. One or both of the images dimensions will be less than the area limit.

**Sample result**

_https://yourdomain.com/image.jpg?ims=fit-in/400x400_ (maximum width of 400 pixels and maximum height of 400 pixels)

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400)]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400)

---

## 4. Crop the image {#crop}

Cropping the image may be done by entering a starting point (AxB) and an end point (CxD), as an argument in the Query String of the image’s URL:


~~~
ims=AxB:CxD
~~~


*   AxB: the starting point for the crop indicates the coordinates in pixels form the top left corner of the area to be cropped.
*   CxD: the end point for the crop indicates the coordinates in pixels form the lower right corner of the area to be cropped.

**Sample result**

_http://yourdomain.com/image.jpg?ims=430x20:910x730_

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=430x20:910x730)]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=430x20:910x730)

---

## 5. Change image quality {#change-quality}

The Image Processor optimizes your images, reducing the file size and, therefore, its transfer time. The default value for the quality level to be used is 85%, which allows for them to be optimized, without any perceptible loss of visual quality.

If necessary, however, you can customize this for your images, using the filter:

~~~
filters:quality(Number)
~~~

Where Number must be a whole number between 0 and 100, that equals the level of quality you wish.

**Sample result**

__http://yourdomain.com/image.jpg?ims=filters:quality(100)__

[![bulldog]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:quality(100))]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:quality(100))

__http://yourdomain.com/image.jpg?ims=filters:quality(85)__

[![bulldog]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:quality(85))]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:quality(85))

__http://yourdomain.com/image.jpg?ims=filters:quality(15)__

[![bulldog]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:quality(15))]({{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:quality(15))

---

## 6. Add a watermark to the image {#add-waterark}

To add a watermark to images, using Image Processor, use the following filter:

~~~
filters:watermark(ImageURL,X,Y,Alpha)
~~~

*   ImageURL: this is the URL of the image that you wish to insert as a watermark. Should the URL include parentheses, they must be coded as %28 for “(“ and %29 for “)”.
*   X: The horizontal position for the watermark to be inserted at. Positive numbers represent the degree of offset, in pixels, from the left edge to the right, while negative numbers represent the offset from the right edge to the left. You can use the value, center, to have the watermark set centrally along the horizontal, or the value, repeat, to horizontally fill the image with repeated watermarks.
*   Y: The vertical position for the watermark to be inserted at. Positive numbers represent the degree of offset, in pixels, from the top to the bottom, while negative numbers represent the offset from the bottom to the top. You can use the value, center, to have the watermark set centrally along the vertical, or the value, repeat, to vertically fill the image with repeated watermarks.
*   Alpha: The watermark’s degree of transparency. It must be a number between 0 (totally opaque) and 100 (totally transparent).

**Sample result**

__http://yourdomain.com/image.jpg?ims=filters:watermark(http://yourdomain.com/watermark-image.png,-25,-10,50)__

---

## 7. Convert image to another format {#convert-image-format}

You can convert the image to another format using the filter:

~~~
filters:format(ImageFormat)
~~~

Where ImageFormat can be replaced by the values webp, jpeg, gif or png.

**Sample result**

To convert a jpeg image to a gif:

__http://yourdomain.com/image.jpg?ims=filters:format(gif)__

[![bulldog]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:format(gif))]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=filters:format(gif))

---

## 8. Fill Image {#fill-image}

Image Processor can also be used to create a derived image that is a larger size than the original, but instead of resizing it to the required size, you can fill the area with a custom color. Use the same parameters as [fit-in](https://www.azion.com/pt-br/docs/produtos/image-optimization/%23redimensionar-a-imagem-com-fit-in) to the dimensions you want, together with the filter *fill*:

~~~
filters:fill(Color)
~~~

Where *Color* is the color to be used for the fill, using the nomenclature and codes specified for [standard HTML](https://en.wikipedia.org/wiki/Web_colors).

**Sample results**

__http://yourdomain.com/image.jpg?ims=fit-in/400x400/filters:fill(gray)__

[![bulldog]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400/filters:fill(gray))]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400/filters:fill(gray))

__http://yourdomain.com/image.jpg?ims=fit-in/400x400/filters:fill(008080)__

[![bulldog]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400/filters:fill(008080))]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400/filters:fill(008080))

__http://yourdomain.com/image.jpg?ims=fit-in/400x400/filters:fill(00ffff)__

[![bulldog]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400/filters:fill(00ffff))]({{ {{ site.url }}/images/docs/image-optimization/bulldog-1280px.jpg?ims=fit-in/400x400/filters:fill(00ffff))

---

## 9. Combine filters {#combine-filters}

Image Processor allows you to combine the filters you want, separating each of them with “:”.

~~~
filters:filter1(arg1):filter2(arg2)
~~~

Where filter1(arg1) and filter2(arg2) are the filters you want to apply.

**Sample result**

__http://yourdomain.com/image.jpg?ims=fit-in/400x400/filters:fill(gray):quality(100)__

---

Didn't find what you were looking for? [Open a support ticket.](https://tickets.azion.com/)
