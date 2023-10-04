![Octocat]![ctocat-1696334902400](https://github.com/mm2027/mason/assets/146838324/daca09b4-2211-4bb9-a245-eb9157946caf)


# mason

This is for programming

The school is Walpole high School'

Student

### Coede.org Gamelab
[Robot Face] [Uploading code.jvar p5Inst = new p5(null, 'sketch');

    * anything with it, place the loadImage() call in preload().
 * You may also supply a callback function to handle the image when it's ready.
 * <br><br>
 * The path to the image should be relative to the HTML file
 * that links in your sketch. Loading an from a URL or other
 * remote location may be blocked due to your browser's built-in
 * security.
 *
 * @method loadImage
 * @param  {String} path Path of the image to be loaded
 * @param  {Function(p5.Image)} [successCallback] Function to be called once
 *                                the image is loaded. Will be passed the
 *                                p5.Image.
 * @param  {Function(Event)}    [failureCallback] called with event error if
 *                                the image fails to load.
 * @return {p5.Image}             the p5.Image object
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/laDefense.jpg");
 * }
 * function setup() {
 *   image(img, 0, 0);
 * }
 * </code>
 * </div>
 * <div>
 * <code>
 * function setup() {
 *   // here we use a callback to display the image after loading
 *   loadImage("assets/laDefense.jpg", function(img) {
 *     image(img, 0, 0);
 *   });
 * }
 * </code>
 * </div>
 *
 * @alt
 * image of the underside of a white umbrella and grided ceililng above
 * image of the underside of a white umbrella and grided ceililng above
 *
 */
p5.prototype.loadImage = function(path, successCallback, failureCallback) {
  var img = new Image();
  var pImg = new p5.Image(1, 1, this);
  var decrementPreload = p5._getDecrementPreload.apply(this, arguments);

  img.onload = function() {
    pImg.width = pImg.canvas.width = img.width;
    pImg.height = pImg.canvas.height = img.height;

    // Draw the image into the backing canvas of the p5.Image
    pImg.drawingContext.drawImage(img, 0, 0);

    if (typeof successCallback === 'function') {
      successCallback(pImg);
    }
    if (decrementPreload && (successCallback !== decrementPreload)) {
      decrementPreload();
    }
  };
  img.onerror = function(e) {
    p5._friendlyFileLoadError(0,img.src);
    // don't get failure callback mixed up with decrementPreload
    if ((typeof failureCallback === 'function') &&
      (failureCallback !== decrementPreload)) {
      failureCallback(e);
    }
  };

  //set crossOrigin in case image is served which CORS headers
  //this will let us draw to canvas without tainting it.
  //see https://developer.mozilla.org/en-US/docs/HTML/CORS_Enabled_Image
  // When using data-uris the file will be loaded locally
  // so we don't need to worry about crossOrigin with base64 file types
  if(path.indexOf('data:image/') !== 0) {
    img.crossOrigin = 'Anonymous';
  }

  //start loading the image
  img.src = path;

  return pImg;
};

/**
 * Validates clipping params. Per drawImage spec sWidth and sHight cannot be
 * negative or greater than image intrinsic width and height
 * @private
 * @param {Number} sVal
 * @param {Number} iVal
 * @returns {Number}
 * @private
 */
function _sAssign(sVal, iVal) {
  if (sVal > 0 && sVal < iVal) {
    return sVal;
  }
  else {
    return iVal;
  }
}

/**
 * Draw an image to the main canvas of the p5js sketch
 *
 * @method image
 * @param  {p5.Image} img    the image to display
 * @param  {Number}   [sx=0]   The X coordinate of the top left corner of the
 *                             sub-rectangle of the source image to draw into
 *                             the destination canvas.
 * @param  {Number}   [sy=0]   The Y coordinate of the top left corner of the
 *                             sub-rectangle of the source image to draw into
 *                             the destination canvas.
 * @param {Number} [sWidth=img.width] The width of the sub-rectangle of the
 *                                    source image to draw into the destination
 *                                    canvas.
 * @param {Number} [sHeight=img.height] The height of the sub-rectangle of the
 *                                      source image to draw into the
 *                                      destination context.
 * @param  {Number}   [dx=0]    The X coordinate in the destination canvas at
 *                              which to place the top-left corner of the
 *                              source image.
 * @param  {Number}   [dy=0]    The Y coordinate in the destination canvas at
 *                              which to place the top-left corner of the
 *                              source image.
 * @param  {Number}   [dWidth]  The width to draw the image in the destination
 *                              canvas. This allows scaling of the drawn image.
 * @param  {Number}   [dHeight] The height to draw the image in the destination
 *                              canvas. This allows scaling of the drawn image.
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/laDefense.jpg");
 * }
 * function setup() {
 *   image(img, 0, 0);
 *   image(img, 0, 0, 100, 100);
 *   image(img, 0, 0, 100, 100, 0, 0, 100, 100);
 * }
 * </code>
 * </div>
 * <div>
 * <code>
 * function setup() {
 *   // here we use a callback to display the image after loading
 *   loadImage("assets/laDefense.jpg", function(img) {
 *     image(img, 0, 0);
 *   });
 * }
 * </code>
 * </div>
 *
 * @alt
 * image of the underside of a white umbrella and grided ceiling above
 * image of the underside of a white umbrella and grided ceiling above
 *
 */
p5.prototype.image =
  function(img, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight) {
  // Temporarily disabling until options for p5.Graphics are added.
  // var args = new Array(arguments.length);
  // for (var i = 0; i < args.length; ++i) {
  //   args[i] = arguments[i];
  // }
  // this._validateParameters(
  //   'image',
  //   args,
  //   [
  //     ['p5.Image', 'Number', 'Number'],
  //     ['p5.Image', 'Number', 'Number', 'Number', 'Number']
  //   ]
  // );

  // set defaults per spec: https://goo.gl/3ykfOq
  if (arguments.length <= 5) {
    dx = sx || 0;
    dy = sy || 0;
    sx = 0;
    sy = 0;
    if (img.elt && img.elt.videoWidth && !img.canvas) { // video no canvas
      var actualW = img.elt.videoWidth;
      var actualH = img.elt.videoHeight;
      dWidth = sWidth || img.elt.width;
      dHeight = sHeight || img.elt.width*actualH/actualW;
      sWidth = actualW;
      sHeight = actualH;
    } else {
      dWidth = sWidth || img.width;
      dHeight = sHeight || img.height;
      sWidth = img.width;
      sHeight = img.height;
    }
  } else if (arguments.length === 9) {
    sx = sx || 0;
    sy = sy || 0;
    sWidth = _sAssign(sWidth, img.width);
    sHeight = _sAssign(sHeight, img.height);

    dx = dx || 0;
    dy = dy || 0;
    dWidth = dWidth || img.width;
    dHeight = dHeight || img.height;
  } else {
    throw 'Wrong number of arguments to image()';
  }

  var vals = canvas.modeAdjust(dx, dy, dWidth, dHeight,
    this._renderer._imageMode);

  // tint the image if there is a tint
  this._renderer.image(img, sx, sy, sWidth, sHeight, vals.x, vals.y, vals.w,
    vals.h);
};

/**
 * Sets the fill value for displaying images. Images can be tinted to
 * specified colors or made transparent by including an alpha value.
 * <br><br>
 * To apply transparency to an image without affecting its color, use
 * white as the tint color and specify an alpha value. For instance,
 * tint(255, 128) will make an image 50% transparent (assuming the default
 * alpha range of 0-255, which can be changed with colorMode()).
 * <br><br>
 * The value for the gray parameter must be less than or equal to the current
 * maximum value as specified by colorMode(). The default maximum value is
 * 255.
 *
 * @method tint
 * @param {Number|Array} v1   gray value, red or hue value (depending on the
 *                            current color mode), or color Array
 * @param {Number|Array} [v2] green or saturation value (depending on the
 *                            current color mode)
 * @param {Number|Array} [v3] blue or brightness value (depending on the
 *                            current color mode)
 * @param {Number|Array} [a]  opacity of the background
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/laDefense.jpg");
 * }
 * function setup() {
 *   image(img, 0, 0);
 *   tint(0, 153, 204);  // Tint blue
 *   image(img, 50, 0);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/laDefense.jpg");
 * }
 * function setup() {
 *   image(img, 0, 0);
 *   tint(0, 153, 204, 126);  // Tint blue and set transparency
 *   image(img, 50, 0);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/laDefense.jpg");
 * }
 * function setup() {
 *   image(img, 0, 0);
 *   tint(255, 126);  // Apply transparency without changing color
 *   image(img, 50, 0);
 * }
 * </code>
 * </div>
 *
 * @alt
 * 2 side by side images of umbrella and ceiling, one image with blue tint
 * Images of umbrella and ceiling, one half of image with blue tint
 * 2 side by side images of umbrella and ceiling, one image translucent
 *
 */
p5.prototype.tint = function () {
  var c = this.color.apply(this, arguments);
  this._renderer._tint = c.levels;
};

/**
 * Sets the alpha value on the renderer which can be used in a tint special
 * case to change the opacity of the sprite
 * @method alphaTint
 * @param {Number} alpha  opacity of the sprite
 */
p5.prototype.alphaTint = function () {
  // alpha should be between 0 and 1
  var alpha = arguments[0];
  if (typeof alpha === 'string') {
    alpha = Number(alpha);
  }
  alpha = Math.max(alpha, 0);
  alpha = Math.min(alpha, 1);
  this._renderer._alpha = alpha;
};

/**
 * Removes the current fill value for displaying images and reverts to
 * displaying images with their original hues.
 *
 * @method noTint
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *   tint(0, 153, 204);  // Tint blue
 *   image(img, 0, 0);
 *   noTint();  // Disable tint
 *   image(img, 50, 0);
 * }
 * </code>
 * </div>
 *
 * @alt
 * 2 side by side images of bricks, left image with blue tint
 *
 */
p5.prototype.noTint = function() {
  this._renderer._tint = null;
};

/**
 * Apply the current tint color to the input image, return the resulting
 * canvas.
 *
 * @param {p5.Image} The image to be tinted
 * @return {canvas} The resulting tinted canvas
 *
 */
p5.prototype._getTintedImageCanvas = function(img) {
  if (!img.canvas) {
    return img;
  }
  var pixels = Filters._toPixels(img.canvas);
  var tmpCanvas = document.createElement('canvas');
  tmpCanvas.width = img.canvas.width;
  tmpCanvas.height = img.canvas.height;
  var tmpCtx = tmpCanvas.getContext('2d');
  var id = tmpCtx.createImageData(img.canvas.width, img.canvas.height);
  var newPixels = id.data;

  for(var i = 0; i < pixels.length; i += 4) {
    var r = pixels[i];
    var g = pixels[i+1];
    var b = pixels[i+2];
    var a = pixels[i+3];

    newPixels[i] = r*this._renderer._tint[0]/255;
    newPixels[i+1] = g*this._renderer._tint[1]/255;
    newPixels[i+2] = b*this._renderer._tint[2]/255;
    newPixels[i+3] = a*this._renderer._tint[3]/255;
  }

  tmpCtx.putImageData(id, 0, 0);
  return tmpCanvas;
};

/**
 * Set image mode. Modifies the location from which images are drawn by
 * changing the way in which parameters given to image() are interpreted.
 * The default mode is imageMode(CORNER), which interprets the second and
 * third parameters of image() as the upper-left corner of the image. If
 * two additional parameters are specified, they are used to set the image's
 * width and height.
 * <br><br>
 * imageMode(CORNERS) interprets the second and third parameters of image()
 * as the location of one corner, and the fourth and fifth parameters as the
 * opposite corner.
 * <br><br>
 * imageMode(CENTER) interprets the second and third parameters of image()
 * as the image's center point. If two additional parameters are specified,
 * they are used to set the image's width and height.
 *
 * @method imageMode
 * @param {Constant} mode either CORNER, CORNERS, or CENTER
 * @example
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *   imageMode(CORNER);
 *   image(img, 10, 10, 50, 50);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *   imageMode(CORNERS);
 *   image(img, 10, 10, 90, 40);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *   imageMode(CENTER);
 *   image(img, 50, 50, 80, 80);
 * }
 * </code>
 * </div>
 *
 * @alt
 * small square image of bricks
 * horizontal rectangle image of bricks
 * large square image of bricks
 *
 */
p5.prototype.imageMode = function(m) {
  if (m === constants.CORNER ||
    m === constants.CORNERS ||
    m === constants.CENTER) {
    this._renderer._imageMode = m;
  }
};


module.exports = p5;

},{"../core/canvas":37,"../core/constants":38,"../core/core":39,"../core/error_helpers":42,"./filters":56}],59:[function(_dereq_,module,exports){
/**
 * @module Image
 * @submodule Image
 * @requires core
 * @requires constants
 * @requires filters
 */

/**
 * This module defines the p5.Image class and P5 methods for
 * drawing images to the main display canvas.
 */

'use strict';

var p5 = _dereq_('../core/core');
var Filters = _dereq_('./filters');

/*
 * Class methods
 */

/**
 * Creates a new p5.Image. A p5.Image is a canvas backed representation of an
 * image.
 * <br><br>
 * p5 can display .gif, .jpg and .png images. Images may be displayed
 * in 2D and 3D space. Before an image is used, it must be loaded with the
 * loadImage() function. The p5.Image class contains fields for the width and
 * height of the image, as well as an array called pixels[] that contains the
 * values for every pixel in the image.
 * <br><br>
 * The methods described below allow easy access to the image's pixels and
 * alpha channel and simplify the process of compositing.
 * <br><br>
 * Before using the pixels[] array, be sure to use the loadPixels() method on
 * the image to make sure that the pixel data is properly loaded.
 *
 * @class p5.Image
 * @constructor
 * @param {Number} width
 * @param {Number} height
 * @param {Object} pInst An instance of a p5 sketch.
 */
p5.Image = function(width, height){
  /**
   * Image width.
   * @property width
   * @example
   * <div><code>
   * var img;
   * function preload() {
   *   img = loadImage("assets/rockies.jpg");
   * }
   *
   * function setup() {
   *   createCanvas(100, 100);
   *   image(img, 0, 0);
   *   for (var i=0; i < img.width; i++) {
   *     var c = img.get(i, img.height/2);
   *     stroke(c);
   *     line(i, height/2, i, height);
   *   }
   * }
   * </code></div>
   *
   * @alt
   * rocky mountains in top and horizontal lines in corresponding colors in bottom.
   *
   */
  this.width = width;
  /**
   * Image height.
   * @property height
   * @example
   * <div><code>
   * var img;
   * function preload() {
   *   img = loadImage("assets/rockies.jpg");
   * }
   *
   * function setup() {
   *   createCanvas(100, 100);
   *   image(img, 0, 0);
   *   for (var i=0; i < img.height; i++) {
   *     var c = img.get(img.width/2, i);
   *     stroke(c);
   *     line(0, i, width/2, i);
   *   }
   * }
   * </code></div>
   *
   * @alt
   * rocky mountains on right and vertical lines in corresponding colors on left.
   *
   */
  this.height = height;
  this.canvas = document.createElement('canvas');
  this.canvas.width = this.width;
  this.canvas.height = this.height;
  this.drawingContext = this.canvas.getContext('2d');
  this._pixelDensity = 1;
  //used for webgl texturing only
  this.isTexture = false;
  /**
   * Array containing the values for all the pixels in the display window.
   * These values are numbers. This array is the size (include an appropriate
   * factor for pixelDensity) of the display window x4,
   * representing the R, G, B, A values in order for each pixel, moving from
   * left to right across each row, then down each column. Retina and other
   * high denisty displays may have more pixels[] (by a factor of
   * pixelDensity^2).
   * For example, if the image is 100x100 pixels, there will be 40,000. With
   * pixelDensity = 2, there will be 160,000. The first four values
   * (indices 0-3) in the array will be the R, G, B, A values of the pixel at
   * (0, 0). The second four values (indices 4-7) will contain the R, G, B, A
   * values of the pixel at (1, 0). More generally, to set values for a pixel
   * at (x, y):
   * <code><pre>var d = pixelDensity;
   * for (var i = 0; i < d; i++) {
   *   for (var j = 0; j < d; j++) {
   *     // loop over
   *     idx = 4*((y * d + j) * width * d + (x * d + i));
   *     pixels[idx] = r;
   *     pixels[idx+1] = g;
   *     pixels[idx+2] = b;
   *     pixels[idx+3] = a;
   *   }
   * }
   * </pre></code>
   * <br><br>
   * Before accessing this array, the data must loaded with the loadPixels()
   * function. After the array data has been modified, the updatePixels()
   * function must be run to update the changes.
   * @property pixels[]
   * @example
   * <div>
   * <code>
   * img = createImage(66, 66);
   * img.loadPixels();
   * for (i = 0; i < img.width; i++) {
   *   for (j = 0; j < img.height; j++) {
   *     img.set(i, j, color(0, 90, 102));
   *   }
   * }
   * img.updatePixels();
   * image(img, 17, 17);
   * </code>
   * </div>
   * <div>
   * <code>
   * var pink = color(255, 102, 204);
   * img = createImage(66, 66);
   * img.loadPixels();
   * for (var i = 0; i < 4*(width*height/2); i+=4) {
   *   img.pixels[i] = red(pink);
   *   img.pixels[i+1] = green(pink);
   *   img.pixels[i+2] = blue(pink);
   *   img.pixels[i+3] = alpha(pink);
   * }
   * img.updatePixels();
   * image(img, 17, 17);
   * </code>
   * </div>
   *
   * @alt
   * 66x66 turquoise rect in center of canvas
   * 66x66 pink rect in center of canvas
   *
   */
  this.pixels = [];
};

/**
 * Helper fxn for sharing pixel methods
 *
 */
p5.Image.prototype._setProperty = function (prop, value) {
  this[prop] = value;
};

/**
 * Loads the pixels data for this image into the [pixels] attribute.
 *
 * @method loadPixels
 * @example
 * <div><code>
 * var myImage;
 * var halfImage;
 *
 * function preload() {
 *   myImage = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   myImage.loadPixels();
 *   halfImage = 4 * width * height/2;
 *   for(var i = 0; i < halfImage; i++){
 *     myImage.pixels[i+halfImage] = myImage.pixels[i];
 *   }
 *   myImage.updatePixels();
 * }
 *
 * function draw() {
 *   image(myImage, 0, 0);
 * }
 * </code></div>
 *
   * @alt
   * 2 images of rocky mountains vertically stacked
   *
 */
p5.Image.prototype.loadPixels = function(){
  p5.Renderer2D.prototype.loadPixels.call(this);
};

/**
 * Updates the backing canvas for this image with the contents of
 * the [pixels] array.
 *
 * @method updatePixels
 * @param {Integer|undefined} x x-offset of the target update area for the
 *                              underlying canvas
 * @param {Integer|undefined} y y-offset of the target update area for the
 *                              underlying canvas
 * @param {Integer|undefined} w height of the target update area for the
 *                              underlying canvas
 * @param {Integer|undefined} h height of the target update area for the
 *                              underlying canvas
 * @example
 * <div><code>
 * var myImage;
 * var halfImage;
 *
 * function preload() {
 *   myImage = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   myImage.loadPixels();
 *   halfImage = 4 * width * height/2;
 *   for(var i = 0; i < halfImage; i++){
 *     myImage.pixels[i+halfImage] = myImage.pixels[i];
 *   }
 *   myImage.updatePixels();
 * }
 *
 * function draw() {
 *   image(myImage, 0, 0);
 * }
 * </code></div>
 *
 * @alt
 * 2 images of rocky mountains vertically stacked
 *
 */
p5.Image.prototype.updatePixels = function(x, y, w, h){
  p5.Renderer2D.prototype.updatePixels.call(this, x, y, w, h);
};

/**
 * Get a region of pixels from an image.
 *
 * If no params are passed, those whole image is returned,
 * if x and y are the only params passed a single pixel is extracted
 * if all params are passed a rectangle region is extracted and a p5.Image
 * is returned.
 *
 * Returns undefined if the region is outside the bounds of the image
 *
 * @method get
 * @param  {Number}               [x] x-coordinate of the pixel
 * @param  {Number}               [y] y-coordinate of the pixel
 * @param  {Number}               [w] width
 * @param  {Number}               [h] height
 * @return {Array/Color | p5.Image}     color of pixel at x,y in array format
 *                                    [R, G, B, A] or p5.Image
 * @example
 * <div><code>
 * var myImage;
 * var c;
 *
 * function preload() {
 *   myImage = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   background(myImage);
 *   noStroke();
 *   c = myImage.get(60, 90);
 *   fill(c);
 *   rect(25, 25, 50, 50);
 * }
 *
 * //get() returns color here
 * </code></div>
 *
 * @alt
 * image of rocky mountains with 50x50 green rect in front
 *
 */
p5.Image.prototype.get = function(x, y, w, h){
  return p5.Renderer2D.prototype.get.call(this, x, y, w, h);
};

/**
 * Set the color of a single pixel or write an image into
 * this p5.Image.
 *
 * Note that for a large number of pixels this will
 * be slower than directly manipulating the pixels array
 * and then calling updatePixels().
 *
 * @method set
 * @param {Number}              x x-coordinate of the pixel
 * @param {Number}              y y-coordinate of the pixel
 * @param {Number|Array|Object}   a grayscale value | pixel array |
 *                                a p5.Color | image to copy
 * @example
 * <div>
 * <code>
 * img = createImage(66, 66);
 * img.loadPixels();
 * for (i = 0; i < img.width; i++) {
 *   for (j = 0; j < img.height; j++) {
 *     img.set(i, j, color(0, 90, 102, i % img.width * 2));
 *   }
 * }
 * img.updatePixels();
 * image(img, 17, 17);
 * image(img, 34, 34);
 * </code>
 * </div>
 *
 * @alt
 * 2 gradated dark turquoise rects fade left. 1 center 1 bottom right of canvas
 *
 */
p5.Image.prototype.set = function(x, y, imgOrCol){
  p5.Renderer2D.prototype.set.call(this, x, y, imgOrCol);
};

/**
 * Resize the image to a new width and height. To make the image scale
 * proportionally, use 0 as the value for the wide or high parameter.
 * For instance, to make the width of an image 150 pixels, and change
 * the height using the same proportion, use resize(150, 0).
 *
 * @method resize
 * @param {Number} width the resized image width
 * @param {Number} height the resized image height
 * @example
 * <div><code>
 * var img;
 *
 * function setup() {
 *   img = loadImage("assets/rockies.jpg");
 * }

 * function draw() {
 *   image(img, 0, 0);
 * }
 *
 * function mousePressed() {
 *   img.resize(50, 100);
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains. zoomed in
 *
 */
p5.Image.prototype.resize = function(width, height){

  // Copy contents to a temporary canvas, resize the original
  // and then copy back.
  //
  // There is a faster approach that involves just one copy and swapping the
  // this.canvas reference. We could switch to that approach if (as i think
  // is the case) there an expectation that the user would not hold a
  // reference to the backing canvas of a p5.Image. But since we do not
  // enforce that at the moment, I am leaving in the slower, but safer
  // implementation.

  // auto-resize
  if (width === 0 && height === 0) {
    width = this.canvas.width;
    height = this.canvas.height;
  } else if (width === 0) {
    width = this.canvas.width * height / this.canvas.height;
  } else if (height === 0) {
    height = this.canvas.height * width / this.canvas.width;
  }

  width = Math.floor(width);
  height = Math.floor(height);

  var tempCanvas = document.createElement('canvas');
  tempCanvas.width = width;
  tempCanvas.height = height;
  tempCanvas.getContext('2d').drawImage(this.canvas,
    0, 0, this.canvas.width, this.canvas.height,
    0, 0, tempCanvas.width, tempCanvas.height
  );


  // Resize the original canvas, which will clear its contents
  this.canvas.width = this.width = width;
  this.canvas.height = this.height = height;

  //Copy the image back

  this.drawingContext.drawImage(tempCanvas,
    0, 0, width, height,
    0, 0, width, height
  );

  if(this.pixels.length > 0){
    this.loadPixels();
  }
};

/**
 * Copies a region of pixels from one image to another. If no
 * srcImage is specified this is used as the source. If the source
 * and destination regions aren't the same size, it will
 * automatically resize source pixels to fit the specified
 * target region.
 *
 * @method copy
 * @param  {p5.Image|undefined} srcImage source image
 * @param  {Integer} sx X coordinate of the source's upper left corner
 * @param  {Integer} sy Y coordinate of the source's upper left corner
 * @param  {Integer} sw source image width
 * @param  {Integer} sh source image height
 * @param  {Integer} dx X coordinate of the destination's upper left corner
 * @param  {Integer} dy Y coordinate of the destination's upper left corner
 * @param  {Integer} dw destination image width
 * @param  {Integer} dh destination image height
 * @example
 * <div><code>
 * var photo;
 * var bricks;
 * var x;
 * var y;
 *
 * function preload() {
 *   photo = loadImage("assets/rockies.jpg");
 *   bricks = loadImage("assets/bricks.jpg");
 * }
 *
 * function setup() {
 *   x = bricks.width/2;
 *   y = bricks.height/2;
 *   photo.copy(bricks, 0, 0, x, y, 0, 0, x, y);
 *   image(photo, 0, 0);
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains and smaller image on top of bricks at top left
 *
 */
p5.Image.prototype.copy = function () {
  p5.prototype.copy.apply(this, arguments);
};

/**
 * Masks part of an image from displaying by loading another
 * image and using it's blue channel as an alpha channel for
 * this image.
 *
 * @method mask
 * @param {p5.Image} srcImage source image
 * @example
 * <div><code>
 * var photo, maskImage;
 * function preload() {
 *   photo = loadImage("assets/rockies.jpg");
 *   maskImage = loadImage("assets/mask2.png");
 * }
 *
 * function setup() {
 *   createCanvas(100, 100);
 *   photo.mask(maskImage);
 *   image(photo, 0, 0);
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains with white at right
 *
 *
 * http://blogs.adobe.com/webplatform/2013/01/28/blending-features-in-canvas/
 *
 */
// TODO: - Accept an array of alpha values.
//       - Use other channels of an image. p5 uses the
//       blue channel (which feels kind of arbitrary). Note: at the
//       moment this method does not match native processings original
//       functionality exactly.
p5.Image.prototype.mask = function(p5Image) {
  if(p5Image === undefined){
    p5Image = this;
  }
  var currBlend = this.drawingContext.globalCompositeOperation;

  var scaleFactor = 1;
  if (p5Image instanceof p5.Renderer) {
    scaleFactor = p5Image._pInst._pixelDensity;
  }

  var copyArgs = [
    p5Image,
    0,
    0,
    scaleFactor*p5Image.width,
    scaleFactor*p5Image.height,
    0,
    0,
    this.width,
    this.height
  ];

  this.drawingContext.globalCompositeOperation = 'destination-in';
  p5.Image.prototype.copy.apply(this, copyArgs);
  this.drawingContext.globalCompositeOperation = currBlend;
};

/**
 * Applies an image filter to a p5.Image
 *
 * @method filter
 * @param {String} operation one of threshold, gray, invert, posterize and
 *                           opaque see Filters.js for docs on each available
 *                           filter
 * @param {Number|undefined} value
 * @example
 * <div><code>
 * var photo1;
 * var photo2;
 *
 * function preload() {
 *   photo1 = loadImage("assets/rockies.jpg");
 *   photo2 = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   photo2.filter("gray");
 *   image(photo1, 0, 0);
 *   image(photo2, width/2, 0);
 * }
 * </code></div>
 *
 * @alt
 * 2 images of rocky mountains left one in color, right in black and white
 *
 */
p5.Image.prototype.filter = function(operation, value) {
  Filters.apply(this.canvas, Filters[operation.toLowerCase()], value);
};

/**
 * Copies a region of pixels from one image to another, using a specified
 * blend mode to do the operation.
 *
 * @method blend
 * @param  {p5.Image|undefined} srcImage source image
 * @param  {Integer} sx X coordinate of the source's upper left corner
 * @param  {Integer} sy Y coordinate of the source's upper left corner
 * @param  {Integer} sw source image width
 * @param  {Integer} sh source image height
 * @param  {Integer} dx X coordinate of the destination's upper left corner
 * @param  {Integer} dy Y coordinate of the destination's upper left corner
 * @param  {Integer} dw destination image width
 * @param  {Integer} dh destination image height
 * @param  {Integer} blendMode the blend mode
 *
 * Available blend modes are: normal | multiply | screen | overlay |
 *            darken | lighten | color-dodge | color-burn | hard-light |
 *            soft-light | difference | exclusion | hue | saturation |
 *            color | luminosity
 *
 *
 * http://blogs.adobe.com/webplatform/2013/01/28/blending-features-in-canvas/
 * @example
 * <div><code>
 * var mountains;
 * var bricks;
 *
 * function preload() {
 *   mountains = loadImage("assets/rockies.jpg");
 *   bricks = loadImage("assets/bricks_third.jpg");
 * }
 *
 * function setup() {
 *   mountains.blend(bricks, 0, 0, 33, 100, 67, 0, 33, 100, ADD);
 *   image(mountains, 0, 0);
 *   image(bricks, 0, 0);
 * }
 * </code></div>
 * <div><code>
 * var mountains;
 * var bricks;
 *
 * function preload() {
 *   mountains = loadImage("assets/rockies.jpg");
 *   bricks = loadImage("assets/bricks_third.jpg");
 * }
 *
 * function setup() {
 *   mountains.blend(bricks, 0, 0, 33, 100, 67, 0, 33, 100, DARKEST);
 *   image(mountains, 0, 0);
 *   image(bricks, 0, 0);
 * }
 * </code></div>
 * <div><code>
 * var mountains;
 * var bricks;
 *
 * function preload() {
 *   mountains = loadImage("assets/rockies.jpg");
 *   bricks = loadImage("assets/bricks_third.jpg");
 * }
 *
 * function setup() {
 *   mountains.blend(bricks, 0, 0, 33, 100, 67, 0, 33, 100, LIGHTEST);
 *   image(mountains, 0, 0);
 *   image(bricks, 0, 0);
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains. Brick images on left and right. Right overexposed
 * image of rockies. Brickwall images on left and right. Right mortar transparent
 * image of rockies. Brickwall images on left and right. Right translucent
 *
 */
p5.Image.prototype.blend = function() {
  p5.prototype.blend.apply(this, arguments);
};

/**
 * Saves the image to a file and force the browser to download it.
 * Accepts two strings for filename and file extension
 * Supports png (default) and jpg.
 *
 * @method save
 * @param {String} filename give your file a name
 * @param  {String} extension 'png' or 'jpg'
 * @example
 * <div><code>
 * var photo;
 *
 * function preload() {
 *   photo = loadImage("assets/rockies.jpg");
 * }
 *
 * function draw() {
 *   image(photo, 0, 0);
 * }
 *
 * function keyTyped() {
 *   if (key == 's') {
 *     photo.save("photo", "png");
 *   }
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains.
 *
 */
p5.Image.prototype.save = function(filename, extension) {
  var mimeType;
  if (!extension) {
    extension = 'png';
    mimeType = 'image/png';
  }
  else {
    // en.wikipedia.org/wiki/Comparison_of_web_browsers#Image_format_support
    switch(extension.toLowerCase()){
      case 'png':
        mimeType = 'image/png';
        break;
      case 'jpeg':
        mimeType = 'image/jpeg';
        break;
      case 'jpg':
        mimeType = 'image/jpeg';
        break;
      default:
        mimeType = 'image/png';
        break;
    }
  }
  var downloadMime = 'image/octet-stream';
  var imageData = this.canvas.toDataURL(mimeType);
  imageData = imageData.replace(mimeType, downloadMime);

  //Make the browser download the file
  p5.prototype.downloadFile(imageData, filename, extension);
};

module.exports = p5.Image;
},{"../core/core":39,"./filters":56}],60:[function(_dereq_,module,exports){
/**
 * @module Image
 * @submodule Pixels
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');
var Filters = _dereq_('./filters');
_dereq_('../color/p5.Color');

/**
 * <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference
 * /Global_Objects/Uint8ClampedArray' target='_blank'>Uint8ClampedArray</a>
 * containing the values for all the pixels in the display window.
 * These values are numbers. This array is the size (include an appropriate
 * factor for pixelDensity) of the display window x4,
 * representing the R, G, B, A values in order for each pixel, moving from
 * left to right across each row, then down each column. Retina and other
 * high denisty displays will have more pixels[] (by a factor of
 * pixelDensity^2).
 * For example, if the image is 100x100 pixels, there will be 40,000. On a
 * retina display, there will be 160,000.
 * <br><br>
 * The first four values (indices 0-3) in the array will be the R, G, B, A
 * values of the pixel at (0, 0). The second four values (indices 4-7) will
 * contain the R, G, B, A values of the pixel at (1, 0). More generally, to
 * set values for a pixel at (x, y):
 * <code><pre>
 * var d = pixelDensity;
 * for (var i = 0; i < d; i++) {
 *   for (var j = 0; j < d; j++) {
 *     // loop over
 *     idx = 4 * ((y * d + j) * width * d + (x * d + i));
 *     pixels[idx] = r;
 *     pixels[idx+1] = g;
 *     pixels[idx+2] = b;
 *     pixels[idx+3] = a;
 *   }
 * }
 * </pre></code>
 *
 * <p>While the above method is complex, it is flexible enough to work with
 * any pixelDensity. Note that set() will automatically take care of
 * setting all the appropriate values in pixels[] for a given (x, y) at
 * any pixelDensity, but the performance may not be as fast when lots of
 * modifications are made to the pixel array.
 * <br><br>
 * Before accessing this array, the data must loaded with the loadPixels()
 * function. After the array data has been modified, the updatePixels()
 * function must be run to update the changes.
 * <br><br>
 * Note that this is not a standard javascript array.  This means that
 * standard javascript functions such as <code>slice()</code> or
 * <code>arrayCopy()</code> do not
 * work.</p>
 *
 * @property pixels[]
 * @example
 * <div>
 * <code>
 * var pink = color(255, 102, 204);
 * loadPixels();
 * var d = pixelDensity();
 * var halfImage = 4 * (width * d) * (height/2 * d);
 * for (var i = 0; i < halfImage; i+=4) {
 *   pixels[i] = red(pink);
 *   pixels[i+1] = green(pink);
 *   pixels[i+2] = blue(pink);
 *   pixels[i+3] = alpha(pink);
 * }
 * updatePixels();
 * </code>
 * </div>
 *
 * @alt
 * top half of canvas pink, bottom grey
 *
 */
p5.prototype.pixels = [];

/**
 * Copies a region of pixels from one image to another, using a specified
 * blend mode to do the operation.<br><br>
 * Available blend modes are: BLEND | DARKEST | LIGHTEST | DIFFERENCE |
 * MULTIPLY| EXCLUSION | SCREEN | REPLACE | OVERLAY | HARD_LIGHT |
 * SOFT_LIGHT | DODGE | BURN | ADD | NORMAL
 *
 *
 * @method blend
 * @param  {p5.Image|undefined} srcImage source image
 * @param  {Integer} sx X coordinate of the source's upper left corner
 * @param  {Integer} sy Y coordinate of the source's upper left corner
 * @param  {Integer} sw source image width
 * @param  {Integer} sh source image height
 * @param  {Integer} dx X coordinate of the destination's upper left corner
 * @param  {Integer} dy Y coordinate of the destination's upper left corner
 * @param  {Integer} dw destination image width
 * @param  {Integer} dh destination image height
 * @param  {Integer} blendMode the blend mode
 *
 * @example
 * <div><code>
 * var img0;
 * var img1;
 *
 * function preload() {
 *   img0 = loadImage("assets/rockies.jpg");
 *   img1 = loadImage("assets/bricks_third.jpg");
 * }
 *
 * function setup() {
 *   background(img0);
 *   image(img1, 0, 0);
 *   blend(img1, 0, 0, 33, 100, 67, 0, 33, 100, LIGHTEST);
 * }
 * </code></div>
 * <div><code>
 * var img0;
 * var img1;
 *
 * function preload() {
 *   img0 = loadImage("assets/rockies.jpg");
 *   img1 = loadImage("assets/bricks_third.jpg");
 * }
 *
 * function setup() {
 *   background(img0);
 *   image(img1, 0, 0);
 *   blend(img1, 0, 0, 33, 100, 67, 0, 33, 100, DARKEST);
 * }
 * </code></div>
 * <div><code>
 * var img0;
 * var img1;
 *
 * function preload() {
 *   img0 = loadImage("assets/rockies.jpg");
 *   img1 = loadImage("assets/bricks_third.jpg");
 * }
 *
 * function setup() {
 *   background(img0);
 *   image(img1, 0, 0);
 *   blend(img1, 0, 0, 33, 100, 67, 0, 33, 100, ADD);
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains. Brick images on left and right. Right overexposed
 * image of rockies. Brickwall images on left and right. Right mortar transparent
 * image of rockies. Brickwall images on left and right. Right translucent
 *
 *
 */
p5.prototype.blend = function() {
  if (this._renderer) {
    this._renderer.blend.apply(this._renderer, arguments);
  } else {
    p5.Renderer2D.prototype.blend.apply(this, arguments);
  }
};

/**
 * Copies a region of the canvas to another region of the canvas
 * and copies a region of pixels from an image used as the srcImg parameter
 * into the canvas srcImage is specified this is used as the source. If
 * the source and destination regions aren't the same size, it will
 * automatically resize source pixels to fit the specified
 * target region.
 *
 * @method copy
 * @param  {p5.Image|undefined} srcImage source image
 * @param  {Integer} sx X coordinate of the source's upper left corner
 * @param  {Integer} sy Y coordinate of the source's upper left corner
 * @param  {Integer} sw source image width
 * @param  {Integer} sh source image height
 * @param  {Integer} dx X coordinate of the destination's upper left corner
 * @param  {Integer} dy Y coordinate of the destination's upper left corner
 * @param  {Integer} dw destination image width
 * @param  {Integer} dh destination image height
 *
 * @example
 * <div><code>
 * var img;
 *
 * function preload() {
 *   img = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   background(img);
 *   copy(img, 7, 22, 10, 10, 35, 25, 50, 50);
 *   stroke(255);
 *   noFill();
 *   // Rectangle shows area being copied
 *   rect(7, 22, 10, 10);
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains. Brick images on left and right. Right overexposed
 * image of rockies. Brickwall images on left and right. Right mortar transparent
 * image of rockies. Brickwall images on left and right. Right translucent
 *
 */
p5.prototype.copy = function () {
  p5.Renderer2D._copyHelper.apply(this, arguments);
};
* @method copy
 * @param  {p5.Image|undefined} srcImage source image
 * @param  {Integer} sx X coordinate of the source's upper left corner
 * @param  {Integer} sy Y coordinate of the source's upper left corner
 * @param  {Integer} sw source image width
 * @param  {Integer} sh source image height
 * @param  {Integer} dx X coordinate of the destination's upper left corner
 * @param  {Integer} dy Y coordinate of the destination's upper left corner
 * @param  {Integer} dw destination image width
 * @param  {Integer} dh destination image height
 *
 * @example
 * <div><code>
 * var img;
 *
 * function preload() {
 *   img = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   background(img);
 *   copy(img, 7, 22, 10, 10, 35, 25, 50, 50);
 *   stroke(255);
 *   noFill();
 *   // Rectangle shows area being copied
 *   rect(7, 22, 10, 10);
 * }
 * </code></div>
 *
 * @alt
 * image of rocky mountains. Brick images on left and right. Right overexposed
 * image of rockies. Brickwall images on left and right. Right mortar transparent
 * image of rockies. Brickwall images on left and right. Right translucent
 *
 */
p5.prototype.copy = function () {
  p5.Renderer2D._copyHelper.apply(this, arguments);
};

/**
 * Applies a filter to the canvas.
 * <br><br>
 *
 * The presets options are:
 * <br><br>
 *
 * THRESHOLD
 * Converts the image to black and white pixels depending if they are above or
 * below the threshold defined by the level parameter. The parameter must be
 * between 0.0 (black) and 1.0 (white). If no level is specified, 0.5 is used.
 * <br><br>
 *
 * GRAY
 * Converts any colors in the image to grayscale equivalents. No parameter
 * is used.
 * <br><br>
 *
 * OPAQUE
 * Sets the alpha channel to entirely opaque. No parameter is used.
 * <br><br>
 *
 * INVERT
 * Sets each pixel to its inverse value. No parameter is used.
 * <br><br>
 *
 * POSTERIZE
 * Limits each channel of the image to the number of colors specified as the
 * parameter. The parameter can be set to values between 2 and 255, but
 * results are most noticeable in the lower ranges.
 * <br><br>
 *
 * BLUR
 * Executes a Guassian blur with the level parameter specifying the extent
 * of the blurring. If no parameter is used, the blur is equivalent to
 * Guassian blur of radius 1. Larger values increase the blur.
 * <br><br>
 *
 * ERODE
 * Reduces the light areas. No parameter is used.
 * <br><br>
 *
 * DILATE
 * Increases the light areas. No parameter is used.
 *
 * @method filter
 * @param  {Constant} filterType
 * @param  {Number} filterParam an optional parameter unique
 *  to each filter, see above
 *
 *
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(THRESHOLD);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(GRAY);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(OPAQUE);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(INVERT);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(POSTERIZE,3);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(DILATE);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(BLUR,3);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/bricks.jpg");
 * }
 * function setup() {
 *  image(img, 0, 0);
 *  filter(ERODE);
 * }
 * </code>
 * </div>
 *
 * @alt
 * black and white image of a brick wall.
 * greyscale image of a brickwall
 * image of a brickwall
 * jade colored image of a brickwall
 * red and pink image of a brickwall
 * image of a brickwall
 * blurry image of a brickwall
 * image of a brickwall
 * image of a brickwall with less detail
 *
 */
p5.prototype.filter = function(operation, value) {
  Filters.apply(this.canvas, Filters[operation.toLowerCase()], value);
};

/**
 * Returns an array of [R,G,B,A] values for any pixel or grabs a section of
 * an image. If no parameters are specified, the entire image is returned.
 * Use the x and y parameters to get the value of one pixel. Get a section of
 * the display window by specifying additional w and h parameters. When
 * getting an image, the x and y parameters define the coordinates for the
 * upper-left corner of the image, regardless of the current imageMode().
 * <br><br>
 * If the pixel requested is outside of the image window, [0,0,0,255] is
 * returned. To get the numbers scaled according to the current color ranges
 * and taking into account colorMode, use getColor instead of get.
 * <br><br>
 * Getting the color of a single pixel with get(x, y) is easy, but not as fast
 * as grabbing the data directly from pixels[]. The equivalent statement to
 * get(x, y) using pixels[] with pixel density d is
 * <code>
 * var off = (y * width + x) * d * 4;
 * [pixels[off],
 * pixels[off+1],
 * pixels[off+2],
 * pixels[off+3]]</code>
 * <br><br>
 * See the reference for pixels[] for more information.
 *
 * @method get
 * @param  {Number}         [x] x-coordinate of the pixel
 * @param  {Number}         [y] y-coordinate of the pixel
 * @param  {Number}         [w] width
 * @param  {Number}         [h] height
 * @return {Array|p5.Image}     values of pixel at x,y in array format
 *                              [R, G, B, A] or p5.Image
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/rockies.jpg");
 * }
 * function setup() {
 *   image(img, 0, 0);
 *   var c = get();
 *   image(c, width/2, 0);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/rockies.jpg");
 * }
 * function setup() {
 *   image(img, 0, 0);
 *   var c = get(50, 90);
 *   fill(c);
 *   noStroke();
 *   rect(25, 25, 50, 50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * 2 images of the rocky mountains, side-by-side
 * Image of the rocky mountains with 50x50 green rect in center of canvas
 *
 */
p5.prototype.get = function(x, y, w, h){
  return this._renderer.get(x, y, w, h);
};

/**
 * Loads the pixel data for the display window into the pixels[] array. This
 * function must always be called before reading from or writing to pixels[].
 *
 * @method loadPixels
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   image(img, 0, 0);
 *   var d = pixelDensity();
 *   var halfImage = 4 * (img.width * d) *
       (img.height/2 * d);
 *   loadPixels();
 *   for (var i = 0; i < halfImage; i++) {
 *     pixels[i+halfImage] = pixels[i];
 *   }
 *   updatePixels();
 * }
 * </code>
 * </div>
 *
 * @alt
 * two images of the rocky mountains. one on top, one on bottom of canvas.
 *
 */
p5.prototype.loadPixels = function() {
  this._renderer.loadPixels();
};

/**
 * <p>Changes the color of any pixel, or writes an image directly to the
 * display window.</p>
 * <p>The x and y parameters specify the pixel to change and the c parameter
 * specifies the color value. This can be a p5.Color object, or [R, G, B, A]
 * pixel array. It can also be a single grayscale value.
 * When setting an image, the x and y parameters define the coordinates for
 * the upper-left corner of the image, regardless of the current imageMode().
 * </p>
 * <p>
 * After using set(), you must call updatePixels() for your changes to
 * appear.  This should be called once all pixels have been set.
 * </p>
 * <p>Setting the color of a single pixel with set(x, y) is easy, but not as
 * fast as putting the data directly into pixels[]. Setting the pixels[]
 * values directly may be complicated when working with a retina display,
 * but will perform better when lots of pixels need to be set directly on
 * every loop.</p>
 * <p>See the reference for pixels[] for more information.</p>
 *
 * @method set
 * @param {Number}              x x-coordinate of the pixel
 * @param {Number}              y y-coordinate of the pixel
 * @param {Number|Array|Object} c insert a grayscale value | a pixel array |
 *                                a p5.Color object | a p5.Image to copy
 * @example
 * <div>
 * <code>
 * var black = color(0);
 * set(30, 20, black);
 * set(85, 20, black);
 * set(85, 75, black);
 * set(30, 75, black);
 * updatePixels();
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * for (var i = 30; i < width-15; i++) {
 *   for (var j = 20; j < height-25; j++) {
 *     var c = color(204-j, 153-i, 0);
 *     set(i, j, c);
 *   }
 * }
 * updatePixels();
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   set(0, 0, img);
 *   updatePixels();
 *   line(0, 0, width, height);
 *   line(0, height, width, 0);
 * }
 * </code>
 * </div>
 *
 * @alt
 * 4 black points in the shape of a square middle-right of canvas.
 * square with orangey-brown gradient lightening at bottom right.
 * image of the rocky mountains. with lines like an 'x' through the center.
 */
p5.prototype.set = function (x, y, imgOrCol) {
  this._renderer.set(x, y, imgOrCol);
};
/**
 * Updates the display window with the data in the pixels[] array.
 * Use in conjunction with loadPixels(). If you're only reading pixels from
 * the array, there's no need to call updatePixels() — updating is only
 * necessary to apply changes. updatePixels() should be called anytime the
 * pixels array is manipulated or set() is called.
 *
 * @method updatePixels
 * @param  {Number} [x]    x-coordinate of the upper-left corner of region
 *                         to update
 * @param  {Number} [y]    y-coordinate of the upper-left corner of region
 *                         to update
 * @param  {Number} [w]    width of region to update
 * @param  {Number} [w]    height of region to update
 * @example
 * <div>
 * <code>
 * var img;
 * function preload() {
 *   img = loadImage("assets/rockies.jpg");
 * }
 *
 * function setup() {
 *   image(img, 0, 0);
 *   var halfImage = 4 * (img.width * pixelDensity()) *
 *     (img.height * pixelDensity()/2);
 *   loadPixels();
 *   for (var i = 0; i < halfImage; i++) {
 *     pixels[i+halfImage] = pixels[i];
 *   }
 *   updatePixels();
 * }
 * </code>
 * </div>
 * @alt
 * two images of the rocky mountains. one on top, one on bottom of canvas.
 */
p5.prototype.updatePixels = function (x, y, w, h) {
  // graceful fail - if loadPixels() or set() has not been called, pixel
  // array will be empty, ignore call to updatePixels()
  if (this.pixels.length === 0) {
    return;
  }
  this._renderer.updatePixels(x, y, w, h);
};

module.exports = p5;

},{"../color/p5.Color":33,"../core/core":39,"./filters":56}],61:[function(_dereq_,module,exports){
/**
 * @module IO
 * @submodule Input
 * @for p5
 * @requires core
 * @requires reqwest
 */

'use strict';

var p5 = _dereq_('../core/core');
var reqwest = _dereq_('reqwest');
var opentype = _dereq_('opentype.js');
_dereq_('../core/error_helpers');

/**
 * Checks if we are in preload and returns the last arg which will be the
 * _decrementPreload function if called from a loadX() function.  Should
 * only be used in loadX() functions.
 * @private
 */
p5._getDecrementPreload = function () {
  var decrementPreload = arguments[arguments.length - 1];

  // when in preload decrementPreload will always be the last arg as it is set
  // with args.push() before invocation in _wrapPreload
  if ((window.preload || (this && this.preload)) &&
    typeof decrementPreload === 'function') {
    return decrementPreload;
  } else {
    return null;
  }
};

/**
 * Loads an opentype font file (.otf, .ttf) from a file or a URL,
 * and returns a PFont Object. This method is asynchronous,
 * meaning it may not finish before the next line in your sketch
 * is executed.
 * <br><br>
 * The path to the font should be relative to the HTML file
 * that links in your sketch. Loading an from a URL or other
 * remote location may be blocked due to your browser's built-in
 * security.
 *
 * @method loadFont
 * @param  {String}        path       name of the file or url to load
 * @param  {Function}      [callback] function to be executed after
 *                                    loadFont()
 *                                    completes
 * @return {Object}                   p5.Font object
 * @example
 *
 * <p>Calling loadFont() inside preload() guarantees that the load
 * operation will have completed before setup() and draw() are called.</p>
 *
 * <div><code>
 * var myFont;
 * function preload() {
 *   myFont = loadFont('assets/AvenirNextLTPro-Demi.otf');
 * }
 *
 * function setup() {
 *   fill('#ED225D');
 *   textFont(myFont);
 *   textSize(36);
 *   text('p5*js', 10, 50);
 * }
 * </code></div>
 *
 * Outside of preload(), you may supply a callback function to handle the
 * object:
 *
 * <div><code>
 * function setup() {
 *   loadFont('assets/AvenirNextLTPro-Demi.otf', drawText);
 * }
 *
 * function drawText(font) {
 *   fill('#ED225D');
 *   textFont(font, 36);
 *   text('p5*js', 10, 50);
 * }
 *
 * </code></div>
 *
 * <p>You can also use the string name of the font to style other HTML
 * elements.</p>
 *
 * <div><code>
 * var myFont;
 *
 * function preload() {
 *   myFont = loadFont('assets/Avenir.otf');
 * }
 *
 * function setup() {
 *   var myDiv = createDiv('hello there');
 *   myDiv.style('font-family', 'Avenir');
 * }
 * </code></div>
 *
 * @alt
 * p5*js in p5's theme dark pink
 * p5*js in p5's theme dark pink
 *
 */
p5.prototype.loadFont = function (path, onSuccess, onError) {

  var p5Font = new p5.Font(this);
  var decrementPreload = p5._getDecrementPreload.apply(this, arguments);

  opentype.load(path, function (err, font) {

    if (err) {

      if ((typeof onError !== 'undefined') && (onError !== decrementPreload)) {
        return onError(err);
      }
      p5._friendlyFileLoadError(4, path);
      console.error(err, path);
      return;
    }

    p5Font.font = font;

    if (typeof onSuccess !== 'undefined') {
      onSuccess(p5Font);
    }

    if (decrementPreload && (onSuccess !== decrementPreload)) {
      decrementPreload();
    }

    // check that we have an acceptable font type
    var validFontTypes = [ 'ttf', 'otf', 'woff', 'woff2' ],
      fileNoPath = path.split('\\').pop().split('/').pop(),
      lastDotIdx = fileNoPath.lastIndexOf('.'), fontFamily, newStyle,
      fileExt = lastDotIdx < 1 ? null : fileNoPath.substr(lastDotIdx + 1);

    // if so, add it to the DOM (name-only) for use with p5.dom
    if (validFontTypes.indexOf(fileExt) > -1) {

      fontFamily = fileNoPath.substr(0, lastDotIdx);
      newStyle = document.createElement('style');
      newStyle.appendChild(document.createTextNode('\n@font-face {' +
        '\nfont-family: ' + fontFamily + ';\nsrc: url(' + path + ');\n}\n'));
      document.head.appendChild(newStyle);
    }

  });

  return p5Font;
};

//BufferedReader
p5.prototype.createInput = function () {
  // TODO
  throw 'not yet implemented';
};

p5.prototype.createReader = function () {
  // TODO
  throw 'not yet implemented';
};

p5.prototype.loadBytes = function () {
  // TODO
  throw 'not yet implemented';
};

/**
 * Loads a JSON file from a file or a URL, and returns an Object or Array.
 * This method is asynchronous, meaning it may not finish before the next
 * line in your sketch is executed.
 *
 * @method loadJSON
 * @param  {String}        path       name of the file or url to load
 * @param  {Function}      [callback] function to be executed after
 *                                    loadJSON() completes, data is passed
 *                                    in as first argument
 * @param  {Function}      [errorCallback] function to be executed if
 *                                    there is an error, response is passed
 *                                    in as first argument
 * @param  {String}        [datatype] "json" or "jsonp"
 * @return {Object|Array}             JSON data
 * @example
 *
 * <p>Calling loadJSON() inside preload() guarantees to complete the
 * operation before setup() and draw() are called.</p>
 *
 * <div><code>
 * var weather;
 * function preload() {
 *   var url = 'http://api.openweathermap.org/data/2.5/weather?q=London,UK'+
 *    '&APPID=7bbbb47522848e8b9c26ba35c226c734';
 *   weather = loadJSON(url);
 * }
 *
 * function setup() {
 *   noLoop();
 * }
 *
 * function draw() {
 *   background(200);
 *   // get the humidity value out of the loaded JSON
 *   var humidity = weather.main.humidity;
 *   fill(0, humidity); // use the humidity value to set the alpha
 *   ellipse(width/2, height/2, 50, 50);
 * }
 * </code></div>
 *
 *
 * <p>Outside of preload(), you may supply a callback function to handle the
 * object:</p>
 * <div><code>
 * function setup() {
 *   noLoop();
 *   var url = 'http://api.openweathermap.org/data/2.5/weather?q=NewYork'+
 *    '&APPID=7bbbb47522848e8b9c26ba35c226c734';
 *   loadJSON(url, drawWeather);
 * }
 *
 * function draw() {
 *   background(200);
 * }
 *
 * function drawWeather(weather) {
 *   // get the humidity value out of the loaded JSON
 *   var humidity = weather.main.humidity;
 *   fill(0, humidity); // use the humidity value to set the alpha
 *   ellipse(width/2, height/2, 50, 50);
 * }
 * </code></div>
 *
 * @alt
 * 50x50 ellipse that changes from black to white depending on the current humidity
 * 50x50 ellipse that changes from black to white depending on the current humidity
 *
 */
p5.prototype.loadJSON = function () {
  var path = arguments[0];
  var callback = arguments[1];
  var errorCallback;
  var decrementPreload = p5._getDecrementPreload.apply(this, arguments);

  var ret = {}; // object needed for preload
  // assume jsonp for URLs
  var t = 'json'; //= path.indexOf('http') === -1 ? 'json' : 'jsonp';

  // check for explicit data type argument
  for (var i = 2; i < arguments.length; i++) {
    var arg = arguments[i];
    if (typeof arg === 'string') {
      if (arg === 'jsonp' || arg === 'json') {
        t = arg;
      }
    } else if (typeof arg === 'function') {
      errorCallback = arg;
    }
  }

  reqwest({
    url: path,
    type: t,
    crossOrigin: true,
    error: function (resp) {
      // pass to error callback if defined
      if (errorCallback) {
        errorCallback(resp);
      } else { // otherwise log error msg
        console.log(resp.statusText);
      }
    },
    success: function (resp) {
      for (var k in resp) {
        ret[k] = resp[k];
      }
      if (typeof callback !== 'undefined') {
        callback(resp);
      }
      if (decrementPreload && (callback !== decrementPreload)) {
        decrementPreload();
      }
    }
  });

  return ret;
};

/**
 * Reads the contents of a file and creates a String array of its individual
 * lines. If the name of the file is used as the parameter, as in the above
 * example, the file must be located in the sketch directory/folder.
 * <br><br>
 * Alternatively, the file maybe be loaded from anywhere on the local
 * computer using an absolute path (something that starts with / on Unix and
 * Linux, or a drive letter on Windows), or the filename parameter can be a
 * URL for a file found on a network.
 * <br><br>
 * This method is asynchronous, meaning it may not finish before the next
 * line in your sketch is executed.
 *
 * @method loadStrings
 * @param  {String}   filename   name of the file or url to load
 * @param  {Function} [callback] function to be executed after loadStrings()
 *                               completes, Array is passed in as first
 *                               argument
 * @param  {Function} [errorCallback] function to be executed if
 *                               there is an error, response is passed
 *                               in as first argument
 * @return {Array}               Array of Strings
 * @example
 *
 * <p>Calling loadStrings() inside preload() guarantees to complete the
 * operation before setup() and draw() are called.</p>
 *
 * <div><code>
 * var result;
 * function preload() {
 *   result = loadStrings('assets/test.txt');
 * }

 * function setup() {
 *   background(200);
 *   var ind = floor(random(result.length));
 *   text(result[ind], 10, 10, 80, 80);
 * }
 * </code></div>
 *
 * <p>Outside of preload(), you may supply a callback function to handle the
 * object:</p>
 *
 * <div><code>
 * function setup() {
 *   loadStrings('assets/test.txt', pickString);
 * }
 *
 * function pickString(result) {
 *   background(200);
 *   var ind = floor(random(result.length));
 *   text(result[ind], 10, 10, 80, 80);
 * }
 * </code></div>
 *
 * @alt
 * randomly generated text from a file, for example "i smell like butter"
 * randomly generated text from a file, for example "i have three feet"
 *
 */
p5.prototype.loadStrings = function (path, callback, errorCallback) {
  var ret = [];
  var req = new XMLHttpRequest();
  var decrementPreload = p5._getDecrementPreload.apply(this, arguments);

  req.addEventListener('error', function (resp) {
    if (errorCallback) {
      errorCallback(resp);
    } else {
      console.log(resp.responseText);
    }
  });

  req.open('GET', path, true);
  req.onreadystatechange = function () {
    if (req.readyState === 4) {
      if (req.status === 200) {
        var arr = req.responseText.match(/[^\r\n]+/g);
        for (var k in arr) {
          ret[k] = arr[k];
        }
        if (typeof callback !== 'undefined') {
          callback(ret);
        }
        if (decrementPreload && (callback !== decrementPreload)) {
          decrementPreload();
        }
      } else {
        if (errorCallback) {
          errorCallback(req);
        } else {
          console.log(req.statusText);
        }
        //p5._friendlyFileLoadError(3, path);
      }
    }
  };
  req.send(null);
  return ret;
};

/**
 * <p>Reads the contents of a file or URL and creates a p5.Table object with
 * its values. If a file is specified, it must be located in the sketch's
 * "data" folder. The filename parameter can also be a URL to a file found
 * online. By default, the file is assumed to be comma-separated (in CSV
 * format). Table only looks for a header row if the 'header' option is
 * included.</p>
 *
 * <p>Possible options include:
 * <ul>
 * <li>csv - parse the table as comma-separated values</li>
 * <li>tsv - parse the table as tab-separated values</li>
 * <li>header - this table has a header (title) row</li>
 * </ul>
 * </p>
 *
 * <p>When passing in multiple options, pass them in as separate parameters,
 * seperated by commas. For example:
 * <br><br>
 * <code>
 *   loadTable("my_csv_file.csv", "csv", "header")
 * </code>
 * </p>
 *
 * <p> All files loaded and saved use UTF-8 encoding.</p>
 *
 * <p>This method is asynchronous, meaning it may not finish before the next
 * line in your sketch is executed. Calling loadTable() inside preload()
 * guarantees to complete the operation before setup() and draw() are called.
 * <p>Outside of preload(), you may supply a callback function to handle the
 * object:</p>
 * </p>
 *
 * @method loadTable
 * @param  {String}         filename   name of the file or URL to load
 * @param  {String|Strings} [options]  "header" "csv" "tsv"
 * @param  {Function}       [callback] function to be executed after
 *                                     loadTable() completes. On success, the
 *                                     Table object is passed in as the
 *                                     first argument; otherwise, false
 *                                     is passed in.
 * @return {Object}                    Table object containing data
 *
 * @example
 * <div class="norender">
 * <code>
 * // Given the following CSV file called "mammals.csv"
 * // located in the project's "assets" folder:
 * //
 * // id,species,name
 * // 0,Capra hircus,Goat
 * // 1,Panthera pardus,Leopard
 * // 2,Equus zebra,Zebra
 *
 * var table;
 *
 * function preload() {
 *   //my table is comma separated value "csv"
 *   //and has a header specifying the columns labels
 *   table = loadTable("assets/mammals.csv", "csv", "header");
 *   //the file can be remote
 *   //table = loadTable("http://p5js.org/reference/assets/mammals.csv",
 *   //                  "csv", "header");
 * }
 *
 * function setup() {
 *   //count the columns
 *   print(table.getRowCount() + " total rows in table");
 *   print(table.getColumnCount() + " total columns in table");
 *
 *   print(table.getColumn("name"));
 *   //["Goat", "Leopard", "Zebra"]
 *
 *   //cycle through the table
 *   for (var r = 0; r < table.getRowCount(); r++)
 *     for (var c = 0; c < table.getColumnCount(); c++) {
 *       print(table.getString(r, c));
 *     }
 * }
 * </code>
 * </div>
 *
 * @alt
 * randomly generated text from a file, for example "i smell like butter"
 * randomly generated text from a file, for example "i have three feet"
 *
 */
p5.prototype.loadTable = function (path) {
  var callback = null;
  var options = [];
  var header = false;
  var sep = ',';
  var separatorSet = false;
  var decrementPreload = p5._getDecrementPreload.apply(this, arguments);

  for (var i = 1; i < arguments.length; i++) {
    if ((typeof (arguments[i]) === 'function') &&
      (arguments[i] !== decrementPreload)) {
      callback = arguments[i];
    } else if (typeof (arguments[i]) === 'string') {
      options.push(arguments[i]);
      if (arguments[i] === 'header') {
        header = true;
      }
      if (arguments[i] === 'csv') {
        if (separatorSet) {
          throw new Error('Cannot set multiple separator types.');
        } else {
          sep = ',';
          separatorSet = true;
        }
      } else if (arguments[i] === 'tsv') {
        if (separatorSet) {
          throw new Error('Cannot set multiple separator types.');
        } else {
          sep = '\t';
          separatorSet = true;
        }
      }
    }
  }

  var t = new p5.Table();
  reqwest({
      url: path,
      crossOrigin: true,
      type: 'csv'
    })
    .then(function (resp) {
      resp = resp.responseText;

      var state = {};

      // define constants
      var PRE_TOKEN = 0,
        MID_TOKEN = 1,
        POST_TOKEN = 2,
        POST_RECORD = 4;

      var QUOTE = '\"',
        CR = '\r',
        LF = '\n';

      var records = [];
      var offset = 0;
      var currentRecord = null;
      var currentChar;

      var recordBegin = function () {
        state.escaped = false;
        currentRecord = [];
        tokenBegin();
      };

      var recordEnd = function () {
        state.currentState = POST_RECORD;
        records.push(currentRecord);
        currentRecord = null;
      };

      var tokenBegin = function () {
        state.currentState = PRE_TOKEN;
        state.token = '';
      };

      var tokenEnd = function () {
        currentRecord.push(state.token);
        tokenBegin();
      };

      while (true) {
        currentChar = resp[offset++];

        // EOF
        if (currentChar == null) {
          if (state.escaped) {
            throw new Error('Unclosed quote in file.');
          }
          if (currentRecord) {
            tokenEnd();
            recordEnd();
            break;
          }
        }
        if (currentRecord === null) {
          recordBegin();
        }

        // Handle opening quote
        if (state.currentState === PRE_TOKEN) {
          if (currentChar === QUOTE) {
            state.escaped = true;
            state.currentState = MID_TOKEN;
            continue;
          }
          state.currentState = MID_TOKEN;
        }

        // mid-token and escaped, look for sequences and end quote
        if (state.currentState === MID_TOKEN && state.escaped) {
          if (currentChar === QUOTE) {
            if (resp[offset] === QUOTE) {
              state.token += QUOTE;
              offset++;
            } else {
              state.escaped = false;
              state.currentState = POST_TOKEN;
            }
          } else {
            state.token += currentChar;
          }
          continue;
        }

        // fall-through: mid-token or post-token, not escaped
        if (currentChar === CR) {
          if (resp[offset] === LF) {
            offset++;
          }
          tokenEnd();
          recordEnd();
        } else if (currentChar === LF) {
          tokenEnd();
          recordEnd();
        } else if (currentChar === sep) {
          tokenEnd();
        } else if (state.currentState === MID_TOKEN) {
          state.token += currentChar;
        }
      }

      // set up column names
      if (header) {
        t.columns = records.shift();
      } else {
        for (i = 0; i < records[0].length; i++) {
          t.columns[i] = 'null';
        }
      }
      var row;
      for (i = 0; i < records.length; i++) {
        //Handles row of 'undefined' at end of some CSVs
        if (i === records.length - 1 && records[i].length === 1) {
          if (records[i][0] === 'undefined') {
            break;
          }
        }
        row = new p5.TableRow();
        row.arr = records[i];
        row.obj = makeObject(records[i], t.columns);
        t.addRow(row);
      }
      if (callback !== null) {
        callback(t);
      }
      if (decrementPreload && (callback !== decrementPreload)) {
        decrementPreload();
      }
    })
    .fail(function (err, msg) {
      p5._friendlyFileLoadError(2, path);
      // don't get error callback mixed up with decrementPreload
      if ((typeof callback === 'function') &&
        (callback !== decrementPreload)) {
        callback(false);
      }
    });

  return t;
};

// helper function to turn a row into a JSON object
function makeObject(row, headers) {
  var ret = {};
  headers = headers || [];
  if (typeof (headers) === 'undefined') {
    for (var j = 0; j < row.length; j++) {
      headers[j.toString()] = j;
    }
  }
  for (var i = 0; i < headers.length; i++) {
    var key = headers[i];
    var val = row[i];
    ret[key] = val;
  }
  return ret;
}

/*global parseXML */
p5.prototype.parseXML = function (two) {
  var one = new p5.XML();
  var i;
  if (two.children.length) {
    for ( i = 0; i < two.children.length; i++ ) {
      var node = parseXML(two.children[i]);
      one.addChild(node);
    }
    one.setName(two.nodeName);
    one._setCont(two.textContent);
    one._setAttributes(two);
    for (var j = 0; j < one.children.length; j++) {
      one.children[j].parent = one;
    }
    return one;
  }
  else {
    one.setName(two.nodeName);
    one._setCont(two.textContent);
    one._setAttributes(two);
    return one;
  }
};

/**
 * Reads the contents of a file and creates an XML object with its values.
 * If the name of the file is used as the parameter, as in the above example,
 * the file must be located in the sketch directory/folder.
 *
 * Alternatively, the file maybe be loaded from anywhere on the local
 * computer using an absolute path (something that starts with / on Unix and
 * Linux, or a drive letter on Windows), or the filename parameter can be a
 * URL for a file found on a network.
 *
 * This method is asynchronous, meaning it may not finish before the next
 * line in your sketch is executed. Calling loadXML() inside preload()
 * guarantees to complete the operation before setup() and draw() are called.
 *
 * <p>Outside of preload(), you may supply a callback function to handle the
 * object:</p>
 *
 * @method loadXML
 * @param  {String}   filename   name of the file or URL to load
 * @param  {Function} [callback] function to be executed after loadXML()
 *                               completes, XML object is passed in as
 *                               first argument
 * @param  {Function} [errorCallback] function to be executed if
 *                               there is an error, response is passed
 *                               in as first argument
 * @return {Object}              XML object containing data
 */
p5.prototype.loadXML = function (path, callback, errorCallback) {
  var ret = {};
  var decrementPreload = p5._getDecrementPreload.apply(this, arguments);
  reqwest({
      url: path,
      type: 'xml',
      crossOrigin: true,
      error: function (resp) {
        // pass to error callback if defined
        if (errorCallback) {
          errorCallback(resp);
        } else { // otherwise log error msg
          console.log(resp.statusText);
        }
        //p5._friendlyFileLoadError(1,path);
      }
    })
    .then(function (resp) {
      var xml = parseXML(resp.documentElement);
      for(var key in xml) {
        ret[key] = xml[key];
      }
      if (typeof callback !== 'undefined') {
        callback(ret);
      }
      if (decrementPreload && (callback !== decrementPreload)) {
        decrementPreload();
      }
    });
  return ret;
};

// name clash with window.open
// p5.prototype.open = function() {
//   // TODO

// };

p5.prototype.selectFolder = function () {
  // TODO
  throw 'not yet implemented';

};

p5.prototype.selectInput = function () {
  // TODO
  throw 'not yet implemented';

};

/**
 * Method for executing an HTTP GET request. If data type is not specified,
 * p5 will try to guess based on the URL, defaulting to text.
 *
 * @method httpGet
 * @param  {String}        path       name of the file or url to load
 * @param  {Object}        [data]     param data passed sent with request
 * @param  {String}        [datatype] "json", "jsonp", "xml", or "text"
 * @param  {Function}      [callback] function to be executed after
 *                                    httpGet() completes, data is passed in
 *                                    as first argument
 * @param  {Function}      [errorCallback] function to be executed if
 *                                    there is an error, response is passed
 *                                    in as first argument
 */
p5.prototype.httpGet = function () {
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  args.push('GET');
  p5.prototype.httpDo.apply(this, args);
};

/**
 * Method for executing an HTTP POST request. If data type is not specified,
 * p5 will try to guess based on the URL, defaulting to text.
 *
 * @method httpPost
 * @param  {String}        path       name of the file or url to load
 * @param  {Object}        [data]     param data passed sent with request
 * @param  {String}        [datatype] "json", "jsonp", "xml", or "text"
 * @param  {Function}      [callback] function to be executed after
 *                                    httpGet() completes, data is passed in
 *                                    as first argument
 * @param  {Function}      [errorCallback] function to be executed if
 *                                    there is an error, response is passed
 *                                    in as first argument
 */
p5.prototype.httpPost = function () {
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  args.push('POST');
  p5.prototype.httpDo.apply(this, args);
};

/**
 * Method for executing an HTTP request. If data type is not specified,
 * p5 will try to guess based on the URL, defaulting to text.<br><br>
 * You may also pass a single object specifying all parameters for the
 * request following the examples inside the reqwest() calls here:
 * <a href='https://github.com/ded/reqwest#api'>
 * https://github.com/ded/reqwest#api</a>
 *
 * @method httpDo
 * @param  {String}        path       name of the file or url to load
 * @param  {String}        [method]   either "GET", "POST", or "PUT",
 *                                    defaults to "GET"
 * @param  {Object}        [data]     param data passed sent with request
 * @param  {String}        [datatype] "json", "jsonp", "xml", or "text"
 * @param  {Function}      [callback] function to be executed after
 *                                    httpGet() completes, data is passed in
 *                                    as first argument
 * @param  {Function}      [errorCallback] function to be executed if
 *                                    there is an error, response is passed
 *                                    in as first argument
 */
p5.prototype.httpDo = function () {
  if (typeof arguments[0] === 'object') {
    reqwest(arguments[0]);
  } else {
    var method = 'GET';
    var path = arguments[0];
    var data = {};
    var type = '';
    var callback;
    var errorCallback;

    for (var i = 1; i < arguments.length; i++) {
      var a = arguments[i];
      if (typeof a === 'string') {
        if (a === 'GET' || a === 'POST' || a === 'PUT') {
          method = a;
        } else {
          type = a;
        }
      } else if (typeof a === 'object') {
        data = a;
      } else if (typeof a === 'function') {
        if (!callback) {
          callback = a;
        } else {
          errorCallback = a;
        }
      }
    }

    // do some sort of smart type checking
    if (type === '') {
      if (path.indexOf('json') !== -1) {
        type = 'json';
      } else if (path.indexOf('xml') !== -1) {
        type = 'xml';
      } else {
        type = 'text';
      }
    }

    reqwest({
      url: path,
      method: method,
      data: data,
      type: type,
      crossOrigin: true,
      success: function (resp) {
        if (typeof callback !== 'undefined') {
          if (type === 'text') {
            callback(resp.response);
          } else {
            callback(resp);
          }
        }
      },
      error: function (resp) {
        if (errorCallback) {
          errorCallback(resp);
        } else {
          console.log(resp.statusText);
        }
      }
    });
  }
};

/**
 * @module IO
 * @submodule Output
 * @for p5
 */

window.URL = window.URL || window.webkitURL;

// private array of p5.PrintWriter objects
p5.prototype._pWriters = [];

p5.prototype.beginRaw = function () {
  // TODO
  throw 'not yet implemented';

};

p5.prototype.beginRecord = function () {
  // TODO
  throw 'not yet implemented';

};

p5.prototype.createOutput = function () {
  // TODO

  throw 'not yet implemented';
};

p5.prototype.createWriter = function (name, extension) {
  var newPW;
  // check that it doesn't already exist
  for (var i in p5.prototype._pWriters) {
    if (p5.prototype._pWriters[i].name === name) {
      // if a p5.PrintWriter w/ this name already exists...
      // return p5.prototype._pWriters[i]; // return it w/ contents intact.
      // or, could return a new, empty one with a unique name:
      newPW = new p5.PrintWriter(name + window.millis(), extension);
      p5.prototype._pWriters.push(newPW);
      return newPW;
    }
  }
  newPW = new p5.PrintWriter(name, extension);
  p5.prototype._pWriters.push(newPW);
  return newPW;
};

p5.prototype.endRaw = function () {
  // TODO

  throw 'not yet implemented';
};

p5.prototype.endRecord = function () {
  // TODO
  throw 'not yet implemented';

};

p5.PrintWriter = function (filename, extension) {
  var self = this;
  this.name = filename;
  this.content = '';
  this.print = function (data) {
    this.content += data;
  };
  this.print = function (data) {
    this.content += data + '\n';
  };
  this.flush = function () {
    this.content = '';
  };
  this.close = function () {
    // convert String to Array for the writeFile Blob
    var arr = [];
    arr.push(this.content);
    p5.prototype.writeFile(arr, filename, extension);
    // remove from _pWriters array and delete self
    for (var i in p5.prototype._pWriters) {
      if (p5.prototype._pWriters[i].name === this.name) {
        // remove from _pWriters array
        p5.prototype._pWriters.splice(i, 1);
      }
    }
    self.flush();
    self = {};
  };
};

p5.prototype.saveBytes = function () {
  // TODO
  throw 'not yet implemented';

};

// object, filename, options --> saveJSON, saveStrings, saveTable
// filename, [extension] [canvas] --> saveImage

/**
 *  <p>Save an image, text, json, csv, wav, or html. Prompts download to
 *  the client's computer. <b>Note that it is not recommended to call save()
 *  within draw if it's looping, as the save() function will open a new save
 *  dialog every frame.</b></p>
 *  <p>The default behavior is to save the canvas as an image. You can
 *  optionally specify a filename.
 *  For example:</p>
 *  <pre class='language-javascript'><code>
 *  save();
 *  save('myCanvas.jpg'); // save a specific canvas with a filename
 *  </code></pre>
 *
 *  <p>Alternately, the first parameter can be a pointer to a canvas
 *  p5.Element, an Array of Strings,
 *  an Array of JSON, a JSON object, a p5.Table, a p5.Image, or a
 *  p5.SoundFile (requires p5.sound). The second parameter is a filename
 *  (including extension). The third parameter is for options specific
 *  to this type of object. This method will save a file that fits the
 *  given paramaters. For example:</p>
 *
 *  <pre class='language-javascript'><code>
 *
 *  save('myCanvas.jpg');           // Saves canvas as an image
 *
 *  var cnv = createCanvas(100, 100);
 *  save(cnv, 'myCanvas.jpg');      // Saves canvas as an image
 *
 *  var gb = createGraphics(100, 100);
 *  save(gb, 'myGraphics.jpg');      // Saves p5.Renderer object as an image
 *
 *  save(myTable, 'myTable.html');  // Saves table as html file
 *  save(myTable, 'myTable.csv',);  // Comma Separated Values
 *  save(myTable, 'myTable.tsv');   // Tab Separated Values
 *
 *  save(myJSON, 'my.json');        // Saves pretty JSON
 *  save(myJSON, 'my.json', true);  // Optimizes JSON filesize
 *
 *  save(img, 'my.png');            // Saves pImage as a png image
 *
 *  save(arrayOfStrings, 'my.txt'); // Saves strings to a text file with line
 *                                  // breaks after each item in the array
 *  </code></pre>
 *
 *  @method save
 *  @param  {[Object|String]} objectOrFilename  If filename is provided, will
 *                                             save canvas as an image with
 *                                             either png or jpg extension
 *                                             depending on the filename.
 *                                             If object is provided, will
 *                                             save depending on the object
 *                                             and filename (see examples
 *                                             above).
 *  @param  {[String]} filename If an object is provided as the first
 *                               parameter, then the second parameter
 *                               indicates the filename,
 *                               and should include an appropriate
 *                               file extension (see examples above).
 *  @param  {[Boolean/String]} options  Additional options depend on
 *                            filetype. For example, when saving JSON,
 *                            <code>true</code> indicates that the
 *                            output will be optimized for filesize,
 *                            rather than readability.
 */
p5.prototype.save = function (object, _filename, _options) {
  // parse the arguments and figure out which things we are saving
  var args = arguments;
  // =================================================
  // OPTION 1: saveCanvas...

  // if no arguments are provided, save canvas
  var cnv = this._curElement.elt;
  if (args.length === 0) {
    p5.prototype.saveCanvas(cnv);
    return;
  }
  // otherwise, parse the arguments

  // if first param is a p5Graphics, then saveCanvas
  else if (args[0] instanceof p5.Renderer ||
    args[0] instanceof p5.Graphics) {
    p5.prototype.saveCanvas(args[0].elt, args[1], args[2]);
    return;
  }

  // if 1st param is String and only one arg, assume it is canvas filename
  else if (args.length === 1 && typeof (args[0]) === 'string') {
    p5.prototype.saveCanvas(cnv, args[0]);
  }

  // =================================================
  // OPTION 2: extension clarifies saveStrings vs. saveJSON
  else {
    var extension = _checkFileExtension(args[1], args[2])[1];
    switch (extension) {
      case 'json':
        p5.prototype.saveJSON(args[0], args[1], args[2]);
        return;
      case 'txt':
        p5.prototype.saveStrings(args[0], args[1], args[2]);
        return;
        // =================================================
        // OPTION 3: decide based on object...
      default:
        if (args[0] instanceof Array) {
          p5.prototype.saveStrings(args[0], args[1], args[2]);
        } else if (args[0] instanceof p5.Table) {
          p5.prototype.saveTable(args[0], args[1], args[2], args[3]);
        } else if (args[0] instanceof p5.Image) {
          p5.prototype.saveCanvas(args[0].canvas, args[1]);
        } else if (args[0] instanceof p5.SoundFile) {
          p5.prototype.saveSound(args[0], args[1], args[2], args[3]);
        }
    }
  }
};

/**
 *  Writes the contents of an Array or a JSON object to a .json file.
 *  The file saving process and location of the saved file will
 *  vary between web browsers.
 *
 *  @method saveJSON
 *  @param  {Array|Object} json
 *  @param  {String} filename
 *  @param  {Boolean} [optimize]   If true, removes line breaks
 *                                 and spaces from the output
 *                                 file to optimize filesize
 *                                 (but not readability).
 *  @example
 *  <div><code>
 *  var json;
 *
 *  function setup() {
 *
 *    json = {}; // new JSON Object
 *
 *    json.id = 0;
 *    json.species = 'Panthera leo';
 *    json.name = 'Lion';
 *
 *  // To save, un-comment the line below, then click 'run'
 *  // saveJSON(json, 'lion.json');
 *  }
 *
 *  // Saves the following to a file called "lion.json":
 *  // {
 *  //   "id": 0,
 *  //   "species": "Panthera leo",
 *  //   "name": "Lion"
 *  // }
 *  </div></code>
 *
 * @alt
 * no image displayed
 *
 */
p5.prototype.saveJSON = function (json, filename, opt) {
  var stringify;
  if (opt) {
    stringify = JSON.stringify(json);
  } else {
    stringify = JSON.stringify(json, undefined, 2);
  }
  console.log(stringify);
  this.saveStrings(stringify.split('\n'), filename, 'json');
};

p5.prototype.saveJSONObject = p5.prototype.saveJSON;
p5.prototype.saveJSONArray = p5.prototype.saveJSON;

p5.prototype.saveStream = function () {
  // TODO
  throw 'not yet implemented';

};

/**
 *  Writes an array of Strings to a text file, one line per String.
 *  The file saving process and location of the saved file will
 *  vary between web browsers.
 *
 *  @method saveStrings
 *  @param  {Array} list      string array to be written
 *  @param  {String} filename filename for output
 *  @example
 *  <div><code>
 *  var words = 'apple bear cat dog';
 *
 *  // .split() outputs an Array
 *  var list = split(words, ' ');
 *
 *  // To save the file, un-comment next line and click 'run'
 *  // saveStrings(list, 'nouns.txt');
 *
 *  // Saves the following to a file called 'nouns.txt':
 *  //
 *  // apple
 *  // bear
 *  // cat
 *  // dog
 *  </code></div>
 *
 * @alt
 * no image displayed
 *
 */
p5.prototype.saveStrings = function (list, filename, extension) {
  var ext = extension || 'txt';
  var pWriter = this.createWriter(filename, ext);
  for (var i = 0; i < list.length; i++) {
    if (i < list.length - 1) {
      pWriter.print(list[i]);
    } else {
      pWriter.print(list[i]);
    }
  }
  pWriter.close();
  pWriter.flush();
};

p5.prototype.saveXML = function () {
  // TODO
  throw 'not yet implemented';

};

p5.prototype.selectOutput = function () {
  // TODO
  throw 'not yet implemented';

};

// =======
// HELPERS
// =======

function escapeHelper(content) {
  return content
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#039;');
}

/**
 *  Writes the contents of a Table object to a file. Defaults to a
 *  text file with comma-separated-values ('csv') but can also
 *  use tab separation ('tsv'), or generate an HTML table ('html').
 *  The file saving process and location of the saved file will
 *  vary between web browsers.
 *
 *  @method saveTable
 *  @param  {p5.Table} Table  the Table object to save to a file
 *  @param  {String} filename the filename to which the Table should be saved
 *  @param  {String} [options]  can be one of "tsv", "csv", or "html"
 *  @example
 *  <div><code>
 *  var table;
 *
 *  function setup() {
 *    table = new p5.Table();
 *
 *    table.addColumn('id');
 *    table.addColumn('species');
 *    table.addColumn('name');
 *
 *    var newRow = table.addRow();
 *    newRow.setNum('id', table.getRowCount() - 1);
 *    newRow.setString('species', 'Panthera leo');
 *    newRow.setString('name', 'Lion');
 *
 *    // To save, un-comment next line then click 'run'
 *    // saveTable(table, 'new.csv');
 *    }
 *
 *    // Saves the following to a file called 'new.csv':
 *    // id,species,name
 *    // 0,Panthera leo,Lion
 *  </code></div>
 *
 * @alt
 * no image displayed
 *
 */
p5.prototype.saveTable = function (table, filename, options) {
  var pWriter = this.createWriter(filename, options);

  var header = table.columns;

  var sep = ','; // default to CSV
  if (options === 'tsv') {
    sep = '\t';
  }
  if (options !== 'html') {
    // make header if it has values
    if (header[0] !== '0') {
      for (var h = 0; h < header.length; h++) {
        if (h < header.length - 1) {
          pWriter.print(header[h] + sep);
        } else {
          pWriter.print(header[h]);
        }
      }
    }

    // make rows
    for (var i = 0; i < table.rows.length; i++) {
      var j;
      for (j = 0; j < table.rows[i].arr.length; j++) {
        if (j < table.rows[i].arr.length - 1) {
          pWriter.print(table.rows[i].arr[j] + sep);
        } else if (i < table.rows.length - 1) {
          pWriter.print(table.rows[i].arr[j]);
        } else {
          pWriter.print(table.rows[i].arr[j]); // no line break
        }
      }
    }
  }

  // otherwise, make HTML
  else {
    pWriter.print('<html>');
    pWriter.print('<head>');
    var str = '  <meta http-equiv=\"content-type\" content';
    str += '=\"text/html;charset=utf-8\" />';
    pWriter.print(str);
    pWriter.print('</head>');

    pWriter.print('<body>');
    pWriter.print('  <table>');

    // make header if it has values
    if (header[0] !== '0') {
      pWriter.print('    <tr>');
      for (var k = 0; k < header.length; k++) {
        var e = escapeHelper(header[k]);
        pWriter.print('      <td>' + e);
        pWriter.print('      </td>');
      }
      pWriter.print('    </tr>');
    }

    // make rows
    for (var row = 0; row < table.rows.length; row++) {
      pWriter.print('    <tr>');
      for (var col = 0; col < table.columns.length; col++) {
        var entry = table.rows[row].getString(col);
        var htmlEntry = escapeHelper(entry);
        pWriter.print('      <td>' + htmlEntry);
        pWriter.print('      </td>');
      }
      pWriter.print('    </tr>');
    }
    pWriter.print('  </table>');
    pWriter.print('</body>');
    pWriter.print('</html>');
  }
  // close and flush the pWriter
  pWriter.close();
  pWriter.flush();
}; // end saveTable()

/**
 *  Generate a blob of file data as a url to prepare for download.
 *  Accepts an array of data, a filename, and an extension (optional).
 *  This is a private function because it does not do any formatting,
 *  but it is used by saveStrings, saveJSON, saveTable etc.
 *
 *  @param  {Array} dataToDownload
 *  @param  {String} filename
 *  @param  {[String]} extension
 *  @private
 */
p5.prototype.writeFile = function (dataToDownload, filename, extension) {
  var type = 'application\/octet-stream';
  if (p5.prototype._isSafari()) {
    type = 'text\/plain';
  }
  var blob = new Blob(dataToDownload, {
    'type': type
  });
  var href = window.URL.createObjectURL(blob);
  p5.prototype.downloadFile(href, filename, extension);
};

/**
 *  Forces download. Accepts a url to filedata/blob, a filename,
 *  and an extension (optional).
 *  This is a private function because it does not do any formatting,
 *  but it is used by saveStrings, saveJSON, saveTable etc.
 *
 *  @param  {String} href      i.e. an href generated by createObjectURL
 *  @param  {[String]} filename
 *  @param  {[String]} extension
 */
p5.prototype.downloadFile = function (href, fName, extension) {
  var fx = _checkFileExtension(fName, extension);
  var filename = fx[0];
  var ext = fx[1];

  var a = document.createElement('a');
  a.href = href;
  a.download = filename;

  // Firefox requires the link to be added to the DOM before click()
  a.onclick = destroyClickedElement;
  a.style.display = 'none';
  document.body.appendChild(a);

  // Safari will open this file in the same page as a confusing Blob.
  if (p5.prototype._isSafari()) {
    var aText = 'Hello, Safari user! To download this file...\n';
    aText += '1. Go to File --> Save As.\n';
    aText += '2. Choose "Page Source" as the Format.\n';
    aText += '3. Name it with this extension: .\"' + ext + '\"';
    alert(aText);
  }
  a.click();
  href = null;
};

/**
 *  Returns a file extension, or another string
 *  if the provided parameter has no extension.
 *
 *  @param   {String} filename
 *  @return  {Array} [fileName, fileExtension]
 *
 *  @private
 */
function _checkFileExtension(filename, extension) {
  if (!extension || extension === true || extension === 'true') {
    extension = '';
  }
  if (!filename) {
    filename = 'untitled';
  }
  var ext = '';
  // make sure the file will have a name, see if filename needs extension
  if (filename && filename.indexOf('.') > -1) {
    ext = filename.split('.').pop();
  }
  // append extension if it doesn't exist
  if (extension) {
    if (ext !== extension) {
      ext = extension;
      filename = filename + '.' + ext;
    }
  }
  return [filename, ext];
}
p5.prototype._checkFileExtension = _checkFileExtension;

/**
 *  Returns true if the browser is Safari, false if not.
 *  Safari makes trouble for downloading files.
 *
 *  @return  {Boolean} [description]
 *  @private
 */
p5.prototype._isSafari = function () {
  var x = Object.prototype.toString.call(window.HTMLElement);
  return x.indexOf('Constructor') > 0;
};

/**
 *  Helper function, a callback for download that deletes
 *  an invisible anchor element from the DOM once the file
 *  has been automatically downloaded.
 *
 *  @private
 */
function destroyClickedElement(event) {
  document.body.removeChild(event.target);
}

module.exports = p5;

},{"../core/core":39,"../core/error_helpers":42,"opentype.js":8,"reqwest":29}],62:[function(_dereq_,module,exports){
/**
 * @module IO
 * @submodule Table
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');


/**
 *  Table Options
 *  <p>Generic class for handling tabular data, typically from a
 *  CSV, TSV, or other sort of spreadsheet file.</p>
 *  <p>CSV files are
 *  <a href="http://en.wikipedia.org/wiki/Comma-separated_values">
 *  comma separated values</a>, often with the data in quotes. TSV
 *  files use tabs as separators, and usually don't bother with the
 *  quotes.</p>
 *  <p>File names should end with .csv if they're comma separated.</p>
 *  <p>A rough "spec" for CSV can be found
 *  <a href="http://tools.ietf.org/html/rfc4180">here</a>.</p>
 *  <p>To load files, use the loadTable method.</p>
 *  <p>To save tables to your computer, use the save method
 *   or the saveTable method.</p>
 *
 *  Possible options include:
 *  <ul>
 *  <li>csv - parse the table as comma-separated values
 *  <li>tsv - parse the table as tab-separated values
 *  <li>header - this table has a header (title) row
 *  </ul>
 */

/**
 *  Table objects store data with multiple rows and columns, much
 *  like in a traditional spreadsheet. Tables can be generated from
 *  scratch, dynamically, or using data from an existing file.
 *
 *  @class p5.Table
 *  @constructor
 *  @param  {Array}     [rows] An array of p5.TableRow objects
 *  @return {p5.Table}         p5.Table generated
 */
p5.Table = function (rows) {
  /**
   *  @property columns
   *  @type {Array}
   */
  this.columns = [];

  /**
   *  @property rows
   *  @type {Array}
   */
  this.rows = [];
};

/**
 *  Use addRow() to add a new row of data to a p5.Table object. By default,
 *  an empty row is created. Typically, you would store a reference to
 *  the new row in a TableRow object (see newRow in the example above),
 *  and then set individual values using set().
 *
 *  If a p5.TableRow object is included as a parameter, then that row is
 *  duplicated and added to the table.
 *
 *  @method  addRow
 *  @param   {p5.TableRow} [row] row to be added to the table
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   //add a row
	*   var newRow = table.addRow();
	*   newRow.setString("id", table.getRowCount() - 1);
	*   newRow.setString("species", "Canis Lupus");
	*   newRow.setString("name", "Wolf");
	*
	*   //print the results
	*   for (var r = 0; r < table.getRowCount(); r++)
	*     for (var c = 0; c < table.getColumnCount(); c++)
	*       print(table.getString(r, c));
	* }
	* </code>
	* </div>
	*
 * @alt
 * no image displayed
 *
 */
p5.Table.prototype.addRow = function(row) {
  // make sure it is a valid TableRow
  var r = row || new p5.TableRow();

  if (typeof(r.arr) === 'undefined' || typeof(r.obj) === 'undefined') {
    //r = new p5.prototype.TableRow(r);
    throw 'invalid TableRow: ' + r;
  }
  r.table = this;
  this.rows.push(r);
  return r;
};

/**
 * Removes a row from the table object.
 *
 * @method  removeRow
 * @param   {Number} id ID number of the row to remove
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   //remove the first row
	*   var r = table.removeRow(0);
	*
	*   //print the results
	*   for (var r = 0; r < table.getRowCount(); r++)
	*     for (var c = 0; c < table.getColumnCount(); c++)
	*       print(table.getString(r, c));
	* }
	* </code>
	* </div>
	*
    * @alt
 	* no image displayed
 	*
 */
p5.Table.prototype.removeRow = function(id) {
  this.rows[id].table = null; // remove reference to table
  var chunk = this.rows.splice(id+1, this.rows.length);
  this.rows.pop();
  this.rows = this.rows.concat(chunk);
};


/**
 * Returns a reference to the specified p5.TableRow. The reference
 * can then be used to get and set values of the selected row.
 *
 * @method  getRow
 * @param  {Number}   rowID ID number of the row to get
 * @return {TableRow} p5.TableRow object
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   var row = table.getRow(1);
	*   //print it column by column
	*   //note: a row is an object, not an array
	*   for (var c = 0; c < table.getColumnCount(); c++)
	*     print(row.getString(c));
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.getRow = function(r) {
  return this.rows[r];
};

/**
 *  Gets all rows from the table. Returns an array of p5.TableRows.
 *
 *  @method  getRows
 *  @return {Array}   Array of p5.TableRows
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   var rows = table.getRows();
	*
	*   //warning: rows is an array of objects
	*   for (var r = 0; r < rows.length; r++)
	*     rows[r].set("name", "Unicorn");
	*
	*   //print the results
	*   for (var r = 0; r < table.getRowCount(); r++)
	*     for (var c = 0; c < table.getColumnCount(); c++)
	*       print(table.getString(r, c));
	* }
	* </code>
	* </div>
	*
    * @alt
    * no image displayed
    *
 */
p5.Table.prototype.getRows = function() {
  return this.rows;
};

/**
 *  Finds the first row in the Table that contains the value
 *  provided, and returns a reference to that row. Even if
 *  multiple rows are possible matches, only the first matching
 *  row is returned. The column to search may be specified by
 *  either its ID or title.
 *
 *  @method  findRow
 *  @param  {String} value  The value to match
 *  @param  {Number|String} column ID number or title of the
 *                                 column to search
 *  @return {TableRow}
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   //find the animal named zebra
	*   var row = table.findRow("Zebra", "name");
	*   //find the corresponding species
	*   print(row.getString("species"));
	* }
	* </code>
	* </div>
	*
 * @alt
 * no image displayed
 *
 */
p5.Table.prototype.findRow = function(value, column) {
  // try the Object
  if (typeof(column) === 'string') {
    for (var i = 0; i < this.rows.length; i++){
      if (this.rows[i].obj[column] === value) {
        return this.rows[i];
      }
    }
  }
  // try the Array
  else {
    for (var j = 0; j < this.rows.length; j++){
      if (this.rows[j].arr[column] === value) {
        return this.rows[j];
      }
    }
  }
  // otherwise...
  return null;
};

/**
 *  Finds the rows in the Table that contain the value
 *  provided, and returns references to those rows. Returns an
 *  Array, so for must be used to iterate through all the rows,
 *  as shown in the example above. The column to search may be
 *  specified by either its ID or title.
 *
 *  @method  findRows
 *  @param  {String} value  The value to match
 *  @param  {Number|String} column ID number or title of the
 *                                 column to search
 *  @return {Array}        An Array of TableRow objects
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   //add another goat
	*   var newRow = table.addRow();
	*   newRow.setString("id", table.getRowCount() - 1);
	*   newRow.setString("species", "Scape Goat");
	*   newRow.setString("name", "Goat");
	*
	*   //find the rows containing animals named Goat
	*   var rows = table.findRows("Goat", "name");
	*   print(rows.length + " Goats found");
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.findRows = function(value, column) {
  var ret = [];
  if (typeof(column) === 'string') {
    for (var i = 0; i < this.rows.length; i++){
      if (this.rows[i].obj[column] === value) {
        ret.push( this.rows[i] );
      }
    }
  }
  // try the Array
  else {
    for (var j = 0; j < this.rows.length; j++){
      if (this.rows[j].arr[column] === value) {
        ret.push( this.rows[j] );
      }
    }
  }
  return ret;
};

/**
 *  Finds the first row in the Table that matches the regular
 *  expression provided, and returns a reference to that row.
 *  Even if multiple rows are possible matches, only the first
 *  matching row is returned. The column to search may be
 *  specified by either its ID or title.
 *
 *  @method  matchRow
 *  @param  {String} regexp The regular expression to match
 *  @param  {String|Number} column The column ID (number) or
 *                                   title (string)
 *  @return {TableRow}        TableRow object
 */
p5.Table.prototype.matchRow = function(regexp, column) {
  if (typeof(column) === 'number') {
    for (var j = 0; j < this.rows.length; j++) {
      if ( this.rows[j].arr[column].match(regexp) ) {
        return this.rows[j];
      }
    }
  }

  else {
    for (var i = 0; i < this.rows.length; i++) {
      if ( this.rows[i].obj[column].match(regexp) ) {
        return this.rows[i];
      }
    }
  }
  return null;
};

/**
 *  Finds the rows in the Table that match the regular expression provided,
 *  and returns references to those rows. Returns an array, so for must be
 *  used to iterate through all the rows, as shown in the example. The
 *  column to search may be specified by either its ID or title.
 *
 *  @method  matchRows
 *  @param  {String} regexp The regular expression to match
 *  @param  {String|Number} [column] The column ID (number) or
 *                                   title (string)
 *  @return {Array}        An Array of TableRow objects
 *  @example
 *  var table;
 *
 *  function setup() {
 *
 *    table = new p5.Table();
 *
 *    table.addColumn('name');
 *    table.addColumn('type');
 *
 *    var newRow = table.addRow();
 *    newRow.setString('name', 'Lion');
 *    newRow.setString('type', 'Mammal');
 *
 *    newRow = table.addRow();
 *    newRow.setString('name', 'Snake');
 *    newRow.setString('type', 'Reptile');
 *
 *    newRow = table.addRow();
 *    newRow.setString('name', 'Mosquito');
 *    newRow.setString('type', 'Insect');
 *
 *    newRow = table.addRow();
 *    newRow.setString('name', 'Lizard');
 *    newRow.setString('type', 'Reptile');
 *
 *    var rows = table.matchRows('R.*', 'type');
 *    for (var i = 0; i < rows.length; i++) {
 *      print(rows[i].getString('name') + ': ' + rows[i].getString('type'));
 *    }
 *  }
 *  // Sketch prints:
 *  // Snake: Reptile
 *  // Lizard: Reptile
 */
p5.Table.prototype.matchRows = function(regexp, column) {
  var ret = [];
  if (typeof(column) === 'number') {
    for (var j = 0; j < this.rows.length; j++) {
      if ( this.rows[j].arr[column].match(regexp) ) {
        ret.push( this.rows[j] );
      }
    }
  }

  else {
    for (var i = 0; i < this.rows.length; i++) {
      if ( this.rows[i].obj[column].match(regexp) ) {
        ret.push( this.rows[i] );
      }
    }
  }
  return ret;
};


/**
 *  Retrieves all values in the specified column, and returns them
 *  as an array. The column may be specified by either its ID or title.
 *
 *  @method  getColumn
 *  @param  {String|Number} column String or Number of the column to return
 *  @return {Array}       Array of column values
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   //getColumn returns an array that can be printed directly
	*   print(table.getColumn("species"));
	*   //outputs ["Capra hircus", "Panthera pardus", "Equus zebra"]
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.getColumn = function(value) {
  var ret = [];
  if (typeof(value) === 'string'){
    for (var i = 0; i < this.rows.length; i++){
      ret.push (this.rows[i].obj[value]);
    }
  } else {
    for (var j = 0; j < this.rows.length; j++){
      ret.push (this.rows[j].arr[value]);
    }
  }
  return ret;
};

/**
 *  Removes all rows from a Table. While all rows are removed,
 *  columns and column titles are maintained.
 *
 *  @method  clearRows
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   table.clearRows();
	*   print(table.getRowCount() + " total rows in table");
	*   print(table.getColumnCount() + " total columns in table");
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.clearRows = function() {
  delete this.rows;
  this.rows = [];
};

/**
 *  Use addColumn() to add a new column to a Table object.
 *  Typically, you will want to specify a title, so the column
 *  may be easily referenced later by name. (If no title is
 *  specified, the new column's title will be null.)
 *
 *  @method  addColumn
 *  @param {String} [title] title of the given column
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   table.addColumn("carnivore");
	*   table.set(0, "carnivore", "no");
	*   table.set(1, "carnivore", "yes");
	*   table.set(2, "carnivore", "no");
	*
	*   //print the results
	*   for (var r = 0; r < table.getRowCount(); r++)
	*     for (var c = 0; c < table.getColumnCount(); c++)
	*       print(table.getString(r, c));
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.addColumn = function(title) {
  var t = title || null;
  this.columns.push(t);
};

/**
 *  Returns the total number of columns in a Table.
 *
 *  @return {Number} Number of columns in this table
 */
p5.Table.prototype.getColumnCount = function() {
  return this.columns.length;
};

/**
 *  Returns the total number of rows in a Table.
 *
 *  @method  getRowCount
 *  @return {Number} Number of rows in this table

 */
p5.Table.prototype.getRowCount = function() {
  return this.rows.length;
};

/**
 *  <p>Removes any of the specified characters (or "tokens").</p>
 *
 *  <p>If no column is specified, then the values in all columns and
 *  rows are processed. A specific column may be referenced by
 *  either its ID or title.</p>
 *
 *  @method  removeTokens
 *  @param  {String} chars  String listing characters to be removed
 *  @param  {String|Number} [column] Column ID (number)
 *                                   or name (string)
 */
p5.Table.prototype.removeTokens = function(chars, column) {
  var escape= function(s) {
    return s.replace(/[-\/\\^$*+?.()|[\]{}]/g, '\\$&');
  };
  var charArray = [];
  for (var i = 0; i < chars.length; i++) {
    charArray.push( escape( chars.charAt(i) ) );
  }
  var regex = new RegExp(charArray.join('|'), 'g');

  if (typeof(column) === 'undefined'){
    for (var c = 0; c < this.columns.length; c++) {
      for (var d = 0; d < this.rows.length; d++) {
        var s = this.rows[d].arr[c];
        s = s.replace(regex, '');
        this.rows[d].arr[c] = s;
        this.rows[d].obj[this.columns[c]] = s;
      }
    }
  }
  else if (typeof(column) === 'string'){
    for (var j = 0; j < this.rows.length; j++) {
      var val = this.rows[j].obj[column];
      val = val.replace(regex, '');
      this.rows[j].obj[column] = val;
      var pos = this.columns.indexOf(column);
      this.rows[j].arr[pos] = val;
    }
  }
  else {
    for (var k = 0; k < this.rows.length; k++) {
      var str = this.rows[k].arr[column];
      str = str.replace(regex, '');
      this.rows[k].arr[column] = str;
      this.rows[k].obj[this.columns[column]] = str;
    }
  }
};

/**
 *  Trims leading and trailing whitespace, such as spaces and tabs,
 *  from String table values. If no column is specified, then the
 *  values in all columns and rows are trimmed. A specific column
 *  may be referenced by either its ID or title.
 *
 *  @method  trim
 *  @param  {String|Number} column Column ID (number)
 *                                   or name (string)
 */
p5.Table.prototype.trim = function(column) {
  var regex = new RegExp( (' '), 'g');

  if (typeof(column) === 'undefined'){
    for (var c = 0; c < this.columns.length; c++) {
      for (var d = 0; d < this.rows.length; d++) {
        var s = this.rows[d].arr[c];
        s = s.replace(regex, '');
        this.rows[d].arr[c] = s;
        this.rows[d].obj[this.columns[c]] = s;
      }
    }
  }
  else if (typeof(column) === 'string'){
    for (var j = 0; j < this.rows.length; j++) {
      var val = this.rows[j].obj[column];
      val = val.replace(regex, '');
      this.rows[j].obj[column] = val;
      var pos = this.columns.indexOf(column);
      this.rows[j].arr[pos] = val;
    }
  }
  else {
    for (var k = 0; k < this.rows.length; k++) {
      var str = this.rows[k].arr[column];
      str = str.replace(regex, '');
      this.rows[k].arr[column] = str;
      this.rows[k].obj[this.columns[column]] = str;
    }
  }
};

/**
 *  Use removeColumn() to remove an existing column from a Table
 *  object. The column to be removed may be identified by either
 *  its title (a String) or its index value (an int).
 *  removeColumn(0) would remove the first column, removeColumn(1)
 *  would remove the second column, and so on.
 *
 *  @method  removeColumn
 *  @param  {String|Number} column columnName (string) or ID (number)
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   table.removeColumn("id");
	*   print(table.getColumnCount());
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.removeColumn = function(c) {
  var cString;
  var cNumber;
  if (typeof(c) === 'string') {
    // find the position of c in the columns
    cString = c;
    cNumber = this.columns.indexOf(c);
    console.log('string');
  }
  else{
    cNumber = c;
    cString = this.columns[c];
  }

  var chunk = this.columns.splice(cNumber+1, this.columns.length);
  this.columns.pop();
  this.columns = this.columns.concat(chunk);

  for (var i = 0; i < this.rows.length; i++){
    var tempR = this.rows[i].arr;
    var chip = tempR.splice(cNumber+1, tempR.length);
    tempR.pop();
    this.rows[i].arr = tempR.concat(chip);
    delete this.rows[i].obj[cString];
  }

};


/**
 * Stores a value in the Table's specified row and column.
 * The row is specified by its ID, while the column may be specified
 * by either its ID or title.
 *
 * @method  set
 * @param {String|Number} column column ID (Number)
 *                               or title (String)
 * @param {String|Number} value  value to assign
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   table.set(0, "species", "Canis Lupus");
	*   table.set(0, "name", "Wolf");
	*
	*   //print the results
	*   for (var r = 0; r < table.getRowCount(); r++)
	*     for (var c = 0; c < table.getColumnCount(); c++)
	*       print(table.getString(r, c));
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.set = function(row, column, value) {
  this.rows[row].set(column, value);
};

/**
 * Stores a Float value in the Table's specified row and column.
 * The row is specified by its ID, while the column may be specified
 * by either its ID or title.
 *
 * @method setNum
 * @param {Number} row row ID
 * @param {String|Number} column column ID (Number)
 *                               or title (String)
 * @param {Number} value  value to assign
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   table.setNum(1, "id", 1);
	*
	*   print(table.getColumn(0));
	*   //["0", 1, "2"]
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 */
p5.Table.prototype.setNum = function(row, column, value){
  this.rows[row].setNum(column, value);
};


/**
 * Stores a String value in the Table's specified row and column.
 * The row is specified by its ID, while the column may be specified
 * by either its ID or title.
 *
 * @method  setString
 * @param {Number} row row ID
 * @param {String|Number} column column ID (Number)
 *                               or title (String)
 * @param {String} value  value to assign
 */
p5.Table.prototype.setString = function(row, column, value){
  this.rows[row].setString(column, value);
};

/**
 * Retrieves a value from the Table's specified row and column.
 * The row is specified by its ID, while the column may be specified by
 * either its ID or title.
 *
 * @method  get
 * @param {Number} row row ID
 * @param  {String|Number} column columnName (string) or
 *                                   ID (number)
 * @return {String|Number}
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   print(table.get(0, 1));
	*   //Capra hircus
	*   print(table.get(0, "species"));
	*   //Capra hircus
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.get = function(row, column) {
  return this.rows[row].get(column);
};

/**
 * Retrieves a Float value from the Table's specified row and column.
 * The row is specified by its ID, while the column may be specified by
 * either its ID or title.
 *
 * @method  getNum
 * @param {Number} row row ID
 * @param  {String|Number} column columnName (string) or
 *                                   ID (number)
 * @return {Number}
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   print(table.getNum(1, 0) + 100);
	*   //id 1 + 100 = 101
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.getNum = function(row, column) {
  return this.rows[row].getNum(column);
};

/**
 * Retrieves a String value from the Table's specified row and column.
 * The row is specified by its ID, while the column may be specified by
 * either its ID or title.
 *
 * @method  getString
 * @param {Number} row row ID
 * @param  {String|Number} column columnName (string) or
 *                                   ID (number)
 * @return {String}
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   var tableArray = table.getArray();
	*
	*   //output each row as array
	*   for (var i = 0; i < tableArray.length; i++)
	*     print(tableArray[i]);
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.getString = function(row, column) {
  return this.rows[row].getString(column);
};

/**
 * Retrieves all table data and returns as an object. If a column name is
 * passed in, each row object will be stored with that attribute as its
 * title.
 *
 * @method  getObject
 * @param {String} headerColumn Name of the column which should be used to
 *                              title each row object (optional)
 * @return {Object}
 *
 * @example
	* <div class="norender">
	* <code>
	* // Given the CSV file "mammals.csv"
	* // in the project's "assets" folder:
	* //
	* // id,species,name
	* // 0,Capra hircus,Goat
	* // 1,Panthera pardus,Leopard
	* // 2,Equus zebra,Zebra
	*
	* var table;
	*
	* function preload() {
	*   //my table is comma separated value "csv"
	*   //and has a header specifying the columns labels
	*   table = loadTable("assets/mammals.csv", "csv", "header");
	* }
	*
	* function setup() {
	*   var tableObject = table.getObject();
	*
	*   print(tableObject);
	*   //outputs an object
	* }
	* </code>
	* </div>
	*
 	*@alt
 	* no image displayed
 	*
 */
p5.Table.prototype.getObject = function (headerColumn) {
  var tableObject = {};
  var obj, cPos, index;

  for(var i = 0; i < this.rows.length; i++) {
    obj = this.rows[i].obj;

    if (typeof(headerColumn) === 'string'){
      cPos = this.columns.indexOf(headerColumn); // index of columnID
      if (cPos >= 0) {
        index = obj[headerColumn];
        tableObject[index] = obj;
      } else {
        throw 'This table has no column named "' + headerColumn +'"';
      }
    } else {
      tableObject[i] = this.rows[i].obj;
    }
  }
  return tableObject;
};

/**
 * Retrieves all table data and returns it as a multidimensional array.
 *
 * @method  getArray
 * @return {Array}
 */
p5.Table.prototype.getArray = function () {
  var tableArray = [];
  for(var i = 0; i < this.rows.length; i++) {
    tableArray.push(this.rows[i].arr);
  }
  return tableArray;
};

module.exports = p5.Table;

},{"../core/core":39}],63:[function(_dereq_,module,exports){
/**
 * @module IO
 * @submodule Table
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 *  A TableRow object represents a single row of data values,
 *  stored in columns, from a table.
 *
 *  A Table Row contains both an ordered array, and an unordered
 *  JSON object.
 *
 *  @class p5.TableRow
 *  @constructor
 *  @param {String} [str]       optional: populate the row with a
 *                              string of values, separated by the
 *                              separator
 *  @param {String} [separator] comma separated values (csv) by default
 */
p5.TableRow = function (str, separator) {
  var arr = [];
  var obj = {};
  if (str){
    separator = separator || ',';
    arr = str.split(separator);
  }
  for (var i = 0; i < arr.length; i++){
    var key = i;
    var val = arr[i];
    obj[key] = val;
  }
  this.arr = arr;
  this.obj = obj;
  this.table = null;
};

/**
 *  Stores a value in the TableRow's specified column.
 *  The column may be specified by either its ID or title.
 *
 *  @method  set
 *  @param {String|Number} column Column ID (Number)
 *                                or Title (String)
 *  @param {String|Number} value  The value to be stored
 */
p5.TableRow.prototype.set = function(column, value) {
  // if typeof column is string, use .obj
  if (typeof(column) === 'string'){
    var cPos = this.table.columns.indexOf(column); // index of columnID
    if (cPos >= 0) {
      this.obj[column] = value;
      this.arr[cPos] = value;
    }
    else {
      throw 'This table has no column named "' + column +'"';
    }
  }

  // if typeof column is number, use .arr
  else {
    if (column < this.table.columns.length) {
      this.arr[column] = value;
      var cTitle = this.table.columns[column];
      this.obj[cTitle] = value;
    }
    else {
      throw 'Column #' + column + ' is out of the range of this table';
    }
  }
};


/**
 *  Stores a Float value in the TableRow's specified column.
 *  The column may be specified by either its ID or title.
 *
 *  @method  setNum
 *  @param {String|Number} column Column ID (Number)
 *                                or Title (String)
 *  @param {Number} value  The value to be stored
 *                                as a Float
 */
p5.TableRow.prototype.setNum = function(column, value){
  var floatVal = parseFloat(value, 10);
  this.set(column, floatVal);
};


/**
 *  Stores a String value in the TableRow's specified column.
 *  The column may be specified by either its ID or title.
 *
 *  @method  setString
 *  @param {String|Number} column Column ID (Number)
 *                                or Title (String)
 *  @param {String} value  The value to be stored
 *                                as a String
 */
p5.TableRow.prototype.setString = function(column, value){
  var stringVal = value.toString();
  this.set(column, stringVal);
};

/**
 *  Retrieves a value from the TableRow's specified column.
 *  The column may be specified by either its ID or title.
 *
 *  @method  get
 *  @param  {String|Number} column columnName (string) or
 *                                   ID (number)
 *  @return {String|Number}
 */
p5.TableRow.prototype.get = function(column) {
  if (typeof(column) === 'string'){
    return this.obj[column];
  } else {
    return this.arr[column];
  }
};

/**
 *  Retrieves a Float value from the TableRow's specified
 *  column. The column may be specified by either its ID or
 *  title.
 *
 *  @method  getNum
 *  @param  {String|Number} column columnName (string) or
 *                                   ID (number)
 *  @return {Number}  Float Floating point number
 */
p5.TableRow.prototype.getNum = function(column) {
  var ret;
  if (typeof(column) === 'string'){
    ret = parseFloat(this.obj[column], 10);
  } else {
    ret = parseFloat(this.arr[column], 10);
  }

  if (ret.toString() === 'NaN') {
    throw 'Error: ' + this.obj[column]+ ' is NaN (Not a Number)';
  }
  return ret;
};

/**
 *  Retrieves an String value from the TableRow's specified
 *  column. The column may be specified by either its ID or
 *  title.
 *
 *  @method  getString
 *  @param  {String|Number} column columnName (string) or
 *                                   ID (number)
 *  @return {String}  String
 */
p5.TableRow.prototype.getString = function(column) {
  if (typeof(column) === 'string'){
    return this.obj[column].toString();
  } else {
    return this.arr[column].toString();
  }
};

module.exports = p5.TableRow;

},{"../core/core":39}],64:[function(_dereq_,module,exports){
/**
 * @module IO
 * @submodule XML
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * XML is a representation of an XML object, able to parse XML code. Use
 * loadXML() to load external XML files and create XML objects.
 *
 * @class p5.XML
 * @constructor
 * @return {p5.XML}    p5.XML object generated
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var children = xml.getChildren("animal");
 *
 *   for (var i = 0; i < children.length; i++) {
 *     var id = children[i].getNumber("id");
 *     var coloring = children[i].getString("species");
 *     var name = children[i].getContent();
 *     print(id + ", " + coloring + ", " + name);
 *   }
 * }
 *
 * // Sketch prints:
 * // 0, Capra hircus, Goat
 * // 1, Panthera pardus, Leopard
 * // 2, Equus zebra, Zebra
 * </code></div>
  *
  * @alt
  * no image displayed
  *
 */
p5.XML = function () {
  this.name = null; //done
  this.attributes = {}; //done
  this.children = [];
  this.parent = null;
  this.content = null; //done
};


/**
 * Gets a copy of the element's parent. Returns the parent as another
 * p5.XML object.
 *
 * @method getParent
 * @return {Object}   element parent
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var children = xml.getChildren("animal");
 *   var parent = children[1].getParent();
 *   print(parent.getName());
 * }
 *
 * // Sketch prints:
 * // mammals
 * </code></div>
 */
p5.XML.prototype.getParent = function() {
  return this.parent;
};

/**
 *  Gets the element's full name, which is returned as a String.
 *
 * @method getName
 * @return {String} the name of the node
 * @example&lt;animal
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   print(xml.getName());
 * }
 *
 * // Sketch prints:
 * // mammals
 * </code></div>
 */
p5.XML.prototype.getName = function() {
  return this.name;
};

/**
 * Sets the element's name, which is specified as a String.
 *
 * @method setName
 * @param {String} the new name of the node
 * @example&lt;animal
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   print(xml.getName());
 *   xml.setName("fish");
 *   print(xml.getName());
 * }
 *
 * // Sketch prints:
 * // mammals
 * // fish
 * </code></div>
 */
p5.XML.prototype.setName = function(name) {
  this.name = name;
};

/**
 * Checks whether or not the element has any children, and returns the result
 * as a boolean.
 *
 * @method hasChildren
 * @return {boolean}
 * @example&lt;animal
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   print(xml.hasChildren());
 * }
 *
 * // Sketch prints:
 * // true
 * </code></div>
 */
p5.XML.prototype.hasChildren = function() {
  return this.children.length > 0;
};

/**
 * Get the names of all of the element's children, and returns the names as an
 * array of Strings. This is the same as looping through and calling getName()
 * on each child element individually.
 *
 * @method listChildren
 * @return {Array} names of the children of the element
 * @example&lt;animal
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   print(xml.listChildren());
 * }
 *
 * // Sketch prints:
 * // ["animal", "animal", "animal"]
 * </code></div>
 */
p5.XML.prototype.listChildren = function() {
  return this.children.map(function(c) { return c.name; });
};

/**
 * Returns all of the element's children as an array of p5.XML objects. When
 * the name parameter is specified, then it will return all children that match
 * that name.
 *
 * @method getChildren
 * @param {String} [name] element name
 * @return {Array} children of the element
 * @example&lt;animal
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var animals = xml.getChildren("animal");
 *
 *   for (var i = 0; i < animals.length; i++) {
 *     print(animals[i].getContent());
 *   }
 * }
 *
 * // Sketch prints:
 * // "Goat"
 * // "Leopard"
 * // "Zebra"
 * </code></div>
 */
p5.XML.prototype.getChildren = function(param) {
  if (param) {
    return this.children.filter(function(c) { return c.name === param; });
  }
  else {
    return this.children;
  }
};

/**
 * Returns the first of the element's children that matches the name parameter
 * or the child of the given index.It returns undefined if no matching
 * child is found.
 *
 * @method getChild
 * @param {String|Number} name element name or index
 * @return {p5.XML}
 * @example&lt;animal
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.getContent());
 * }
 *
 * // Sketch prints:
 * // "Goat"
 * </code></div>
 * <div class='norender'><code>
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var secondChild = xml.getChild(1);
 *   print(secondChild.getContent());
 * }
 *
 * // Sketch prints:
 * // "Leopard"
 * </code></div>
 */
p5.XML.prototype.getChild = function(param) {
  if(typeof param === 'string') {
    return this.children.find(function(c) {
      return c.name === param;
    });
  }
  else {
    return this.children[param];
  }
};

/**
 * Appends a new child to the element. The child can be specified with
 * either a String, which will be used as the new tag's name, or as a
 * reference to an existing p5.XML object.
 * A reference to the newly created child is returned as an p5.XML object.
 *
 * @method addChild
 * @param {Object} a p5.XML Object which will be the child to be added
 */
p5.XML.prototype.addChild = function(node) {
  if (node instanceof p5.XML) {
    this.children.push(node);
  } else {
    // PEND
  }
};

/**
 * Removes the element specified by name or index.
 *
 * @method removeChild
 * @param {String|Number} name element name or index
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   xml.removeChild("animal");
 *   var children = xml.getChildren();
 *   for (var i=0; i<children.length; i++) {
 *     print(children[i].getContent());
 *   }
 * }
 *
 * // Sketch prints:
 * // "Leopard"
 * // "Zebra"
 * </code></div>
 * <div class='norender'><code>
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   xml.removeChild(1);
 *   var children = xml.getChildren();
 *   for (var i=0; i<children.length; i++) {
 *     print(children[i].getContent());
 *   }
 * }
 *
 * // Sketch prints:
 * // "Goat"
 * // "Zebra"
 * </code></div>
 */
p5.XML.prototype.removeChild = function(param) {
  var ind = -1;
  if(typeof param === 'string') {
    for (var i=0; i<this.children.length; i++) {
      if (this.children[i].name === param) {
        ind = i;
        break;
      }
    }
  } else {
    ind = param;
  }
  if (ind !== -1) {
    this.children.splice(ind, 1);
  }
};


/**
 * Counts the specified element's number of attributes, returned as an Number.
 *
 * @method getAttributeCount
 * @return {Number}
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.getAttributeCount());
 * }
 *
 * // Sketch prints:
 * // 2
 * </code></div>
 */
p5.XML.prototype.getAttributeCount = function() {
  return Object.keys(this.attributes).length;
};

/**
 * Gets all of the specified element's attributes, and returns them as an
 * array of Strings.
 *
 * @method listAttributes
 * @return {Array} an array of strings containing the names of attributes
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.listAttributes());
 * }
 *
 * // Sketch prints:
 * // ["id", "species"]
 * </code></div>
 */
p5.XML.prototype.listAttributes = function() {
  return Object.keys(this.attributes);
};

/**
 *  Checks whether or not an element has the specified attribute.
 *
 * @method hasAttribute
 * @param {String} the attribute to be checked
 * @return {boolean} true if attribute found else false
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.hasAttribute("species"));
 *   print(firstChild.hasAttribute("color"));
 * }
 *
 * // Sketch prints:
 * // true
 * // false
 * </code></div>
 */
p5.XML.prototype.hasAttribute = function(name) {
  return this.attributes[name] ? true : false;
};

/**
 * Returns an attribute value of the element as an Number. If the defaultValue
 * parameter is specified and the attribute doesn't exist, then defaultValue
 * is returned. If no defaultValue is specified and the attribute doesn't
 * exist, the value 0 is returned.
 *
 * @method getNumber
 * @param {String} name            the non-null full name of the attribute
 * @param {Number} [defaultValue]  the default value of the attribute
 * @return {Number}
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.getNumber("id"));
 * }
 *
 * // Sketch prints:
 * // 0
 * </code></div>
 */
p5.XML.prototype.getNumber = function(name, defaultValue) {
  return Number(this.attributes[name]) || defaultValue || 0;
};

/**
 * Returns an attribute value of the element as an String. If the defaultValue
 * parameter is specified and the attribute doesn't exist, then defaultValue
 * is returned. If no defaultValue is specified and the attribute doesn't
 * exist, null is returned.
 *
 * @method getString
 * @param {String} name            the non-null full name of the attribute
 * @param {Number} [defaultValue]  the default value of the attribute
 * @return {Number}
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.getString("species"));
 * }
 *
 * // Sketch prints:
 * // "Capra hircus"
 * </code></div>
 */
p5.XML.prototype.getString = function(name, defaultValue) {
  return String(this.attributes[name]) || defaultValue || null;
};

/**
 * Sets the content of an element's attribute. The first parameter specifies
 * the attribute name, while the second specifies the new content.
 *
 * @method setAttribute
 * @param {String} name            the full name of the attribute
 * @param {Number} value           the value of the attribute
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.getString("species"));
 *   firstChild.setAttribute("species", "Jamides zebra");
 *   print(firstChild.getString("species"));
 * }
 *
 * // Sketch prints:
 * // "Capra hircus"
 * // "Jamides zebra"
 * </code></div>
 */
p5.XML.prototype.setAttribute = function(name, value) {
  if (this.attributes[name]) {
    this.attributes[name] = value;
  }
};

/**
 * Returns the content of an element. If there is no such content,
 * defaultValue is returned if specified, otherwise null is returned.
 *
 * @method getContent
 * @param {String} [defaultValue] value returned if no content is found
 * @return {String}
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.getContent());
 * }
 *
 * // Sketch prints:
 * // "Goat"
 * </code></div>
 */
p5.XML.prototype.getContent = function(defaultValue) {
  return this.content || defaultValue || null;
};

/**
 * Sets the element's content.
 *
 * @method setContent
 * @param {String} text the new content
 * @example
 * <div class='norender'><code>
 * // The following short XML file called "mammals.xml" is parsed
 * // in the code below.
 * //
 * // <?xml version="1.0"?>
 * // &lt;mammals&gt;
 * //   &lt;animal id="0" species="Capra hircus">Goat&lt;/animal&gt;
 * //   &lt;animal id="1" species="Panthera pardus">Leopard&lt;/animal&gt;
 * //   &lt;animal id="2" species="Equus zebra">Zebra&lt;/animal&gt;
 * // &lt;/mammals&gt;
 *
 * var xml;
 *
 * function preload() {
 *   xml = loadXML("assets/mammals.xml");
 * }
 *
 * function setup() {
 *   var firstChild = xml.getChild("animal");
 *   print(firstChild.getContent());
 *   firstChild.setContent("Mountain Goat");
 *   print(firstChild.getContent());
 * }
 *
 * // Sketch prints:
 * // "Goat"
 * // "Mountain Goat"
 * </code></div>
 */
p5.XML.prototype.setContent = function( content ) {
  if(!this.children.length) {
    this.content = content;
  }
};

/* HELPERS */
/**
 * This method is called while the parsing of XML (when loadXML() is
 * called). The difference between this method and the setContent()
 * method defined later is that this one is used to set the content
 * when the node in question has more nodes under it and so on and
 * not directly text content. While in the other one is used when
 * the node in question directly has text inside it.
 *
 */
p5.XML.prototype._setCont = function(content) {
  var str;
  str = content;
  str = str.replace(/\s\s+/g, ',');
  //str = str.split(',');
  this.content = str;
};

/**
 * This method is called while the parsing of XML (when loadXML() is
 * called). The XML node is passed and its attributes are stored in the
 * p5.XML's attribute Object.
 *
 */
p5.XML.prototype._setAttributes = function(node) {
  var  i, att = {};
  for( i = 0; i < node.attributes.length; i++) {
    att[node.attributes[i].nodeName] = node.attributes[i].nodeValue;
  }
  this.attributes = att;
};

module.exports = p5.XML;
},{"../core/core":39}],65:[function(_dereq_,module,exports){
/**
 * @module Math
 * @submodule Calculation
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * Calculates the absolute value (magnitude) of a number. Maps to Math.abs().
 * The absolute value of a number is always positive.
 *
 * @method abs
 * @param  {Number} n number to compute
 * @return {Number}   absolute value of given number
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var x = -3;
 *   var y = abs(x);
 *
 *   print(x); // -3
 *   print(y); // 3
 * }
 * </code></div>
 *
 * @alt
 * no image displayed
 *
 */
p5.prototype.abs = Math.abs;

/**
 * Calculates the closest int value that is greater than or equal to the
 * value of the parameter. Maps to Math.ceil(). For example, ceil(9.03)
 * returns the value 10.
 *
 * @method ceil
 * @param  {Number} n number to round up
 * @return {Number}   rounded up number
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *   // map, mouseX between 0 and 5.
 *   var ax = map(mouseX, 0, 100, 0, 5);
 *   var ay = 66;
 *
 *   //Get the ceiling of the mapped number.
 *   var bx = ceil(map(mouseX, 0, 100, 0,5));
 *   var by = 33;
 *
 *   // Multiply the mapped numbers by 20 to more easily
 *   // see the changes.
 *   stroke(0);
 *   fill(0);
 *   line(0, ay, ax * 20, ay);
 *   line(0, by, bx * 20, by);
 *
 *   // Reformat the float returned by map and draw it.
 *   noStroke();
 *   text(nfc(ax, 2,2), ax, ay - 5);
 *   text(nfc(bx,1,1), bx, by - 5);
 * }
 * </code></div>
  *
 * @alt
 * 2 horizontal lines & number sets. increase with mouse x. bottom to 2 decimals
 *
 */
p5.prototype.ceil = Math.ceil;

/**
 * Constrains a value between a minimum and maximum value.
 *
 * @method constrain
 * @param  {Number} n    number to constrain
 * @param  {Number} low  minimum limit
 * @param  {Number} high maximum limit
 * @return {Number}      constrained number
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *
 *   var leftWall = 25;
 *   var rightWall = 75;
 *
 *   // xm is just the mouseX, while
 *   // xc is the mouseX, but constrained
 *   // between the leftWall and rightWall!
 *   var xm = mouseX;
 *   var xc = constrain(mouseX, leftWall, rightWall);
 *
 *   // Draw the walls.
 *   stroke(150);
 *   line(leftWall, 0, leftWall, height);
 *   line(rightWall, 0, rightWall, height);
 *
 *   // Draw xm and xc as circles.
 *   noStroke();
 *   fill(150);
 *   ellipse(xm, 33, 9,9); // Not Constrained
 *   fill(0);
 *   ellipse(xc, 66, 9,9); // Constrained
 * }
 * </code></div>
 *
 * @alt
 * 2 vertical lines. 2 ellipses move with mouse X 1 does not move passed lines
 *
 */
p5.prototype.constrain = function(n, low, high) {
  return Math.max(Math.min(n, high), low);
};

/**
 * Calculates the distance between two points.
 *
 * @method dist
 * @param  {Number} x1 x-coordinate of the first point
 * @param  {Number} y1 y-coordinate of the first point
 * @param  {Number} [z1] z-coordinate of the first point
 * @param  {Number} x2 x-coordinate of the second point
 * @param  {Number} y2 y-coordinate of the second point
 * @param  {Number} [z2] z-coordinate of the second point
 * @return {Number}    distance between the two points
 * @example
 * <div><code>
 * // Move your mouse inside the canvas to see the
 * // change in distance between two points!
 * function draw() {
 *   background(200);
 *   fill(0);
 *
 *   var x1 = 10;
 *   var y1 = 90;
 *   var x2 = mouseX;
 *   var y2 = mouseY;
 *
 *   line(x1, y1, x2, y2);
 *   ellipse(x1, y1, 7, 7);
 *   ellipse(x2, y2, 7, 7);
 *
 *   // d is the length of the line
 *   // the distance from point 1 to point 2.
 *   var d = int(dist(x1, y1, x2, y2));
 *
 *   // Let's write d along the line we are drawing!
 *   push();
 *   translate( (x1+x2)/2, (y1+y2)/2 );
 *   rotate( atan2(y2-y1,x2-x1) );
 *   text(nfc(d,1,1), 0, -5);
 *   pop();
 *   // Fancy!
 * }
 * </code></div>
 *
 * @alt
 * 2 ellipses joined by line. 1 ellipse moves with mouse X&Y. Distance displayed.
 *
 */
p5.prototype.dist = function(x1, y1, z1, x2, y2, z2) {
  if (arguments.length === 4) {
    // In the case of 2d: z1 means x2 and x2 means y2
    return Math.sqrt( (z1-x1)*(z1-x1) + (x2-y1)*(x2-y1) );
  } else if (arguments.length === 6) {
    return Math.sqrt( (x2-x1)*(x2-x1) + (y2-y1)*(y2-y1) + (z2-z1)*(z2-z1) );
  }
};

/**
 * Returns Euler's number e (2.71828...) raised to the power of the n
 * parameter. Maps to Math.exp().
 *
 * @method exp
 * @param  {Number} n exponent to raise
 * @return {Number}   e^n
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *
 *   // Compute the exp() function with a value between 0 and 2
 *   var xValue = map(mouseX, 0, width, 0, 2);
 *   var yValue = exp(xValue);
 *
 *   var y = map(yValue, 0, 8, height, 0);
 *
 *   var legend = "exp (" + nfc(xValue, 3) +")\n= " + nf(yValue, 1, 4);
 *   stroke(150);
 *   line(mouseX, y, mouseX, height);
 *   fill(0);
 *   text(legend, 5, 15);
 *   noStroke();
 *   ellipse (mouseX,y, 7, 7);
 *
 *   // Draw the exp(x) curve,
 *   // over the domain of x from 0 to 2
 *   noFill();
 *   stroke(0);
 *   beginShape();
 *   for (var x = 0; x < width; x++) {
 *     xValue = map(x, 0, width, 0, 2);
 *     yValue = exp(xValue);
 *     y = map(yValue, 0, 8, height, 0);
 *     vertex(x, y);
 *   }
 *
 *   endShape();
 *   line(0, 0, 0, height);
 *   line(0, height-1, width, height-1);
 * }
 * </code></div>
 *
 * @alt
 * ellipse moves along a curve with mouse x. e^n displayed.
 *
 */
p5.prototype.exp = Math.exp;

/**
 * Calculates the closest int value that is less than or equal to the
 * value of the parameter. Maps to Math.floor().
 *
 * @method floor
 * @param  {Number} n number to round down
 * @return {Number}   rounded down number
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *   //map, mouseX between 0 and 5.
 *   var ax = map(mouseX, 0, 100, 0, 5);
 *   var ay = 66;
 *
 *   //Get the floor of the mapped number.
 *   var bx = floor(map(mouseX, 0, 100, 0,5));
 *   var by = 33;
 *
 *   // Multiply the mapped numbers by 20 to more easily
 *   // see the changes.
 *   stroke(0);
 *   fill(0);
 *   line(0, ay, ax * 20, ay);
 *   line(0, by, bx * 20, by);
 *
 *   // Reformat the float returned by map and draw it.
 *   noStroke();
 *   text(nfc(ax, 2,2), ax, ay - 5);
 *   text(nfc(bx,1,1), bx, by - 5);
 * }
 * </code></div>
 *
 * @alt
 * 2 horizontal lines & number sets. increase with mouse x. bottom to 2 decimals
 *
 */
p5.prototype.floor = Math.floor;

/**
 * Calculates a number between two numbers at a specific increment. The amt
 * parameter is the amount to interpolate between the two values where 0.0
 * equal to the first point, 0.1 is very near the first point, 0.5 is
 * half-way in between, etc. The lerp function is convenient for creating
 * motion along a straight path and for drawing dotted lines.
 *
 * @method lerp
 * @param  {Number} start first value
 * @param  {Number} stop  second value
 * @param  {Number} amt   number between 0.0 and 1.0
 * @return {Number}       lerped value
 * @example
 * <div><code>
 * function setup() {
 *   background(200);
 *   var a = 20;
 *   var b = 80;
 *   var c = lerp(a,b, .2);
 *   var d = lerp(a,b, .5);
 *   var e = lerp(a,b, .8);
 *
 *   var y = 50
 *
 *   strokeWeight(5);
 *   stroke(0); // Draw the original points in black
 *   point(a, y);
 *   point(b, y);
 *
 *   stroke(100); // Draw the lerp points in gray
 *   point(c, y);
 *   point(d, y);
 *   point(e, y);
 * }
 * </code></div>
 *
 * @alt
 * 5 points horizontally staggered mid-canvas. mid 3 are grey, outer black
 *
 */
p5.prototype.lerp = function(start, stop, amt) {
  return amt*(stop-start)+start;
};

/**
 * Calculates the natural logarithm (the base-e logarithm) of a number. This
 * function expects the n parameter to be a value greater than 0.0. Maps to
 * Math.log().
 *
 * @method log
 * @param  {Number} n number greater than 0
 * @return {Number}   natural logarithm of n
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *   var maxX = 2.8;
 *   var maxY = 1.5;
 *
 *   // Compute the natural log of a value between 0 and maxX
 *   var xValue = map(mouseX, 0, width, 0, maxX);
 *   if (xValue > 0) { // Cannot take the log of a negative number.
 *     var yValue = log(xValue);
 *     var y = map(yValue, -maxY, maxY, height, 0);
 *
 *     // Display the calculation occurring.
 *     var legend = "log(" + nf(xValue, 1, 2) + ")\n= " + nf(yValue, 1, 3);
 *     stroke(150);
 *     line(mouseX, y, mouseX, height);
 *     fill(0);
 *     text (legend, 5, 15);
 *     noStroke();
 *     ellipse (mouseX, y, 7, 7);
 *   }
 *
 *   // Draw the log(x) curve,
 *   // over the domain of x from 0 to maxX
 *   noFill();
 *   stroke(0);
 *   beginShape();
 *   for(var x=0; x < width; x++) {
 *     xValue = map(x, 0, width, 0, maxX);
 *     yValue = log(xValue);
 *     y = map(yValue, -maxY, maxY, height, 0);
 *     vertex(x, y);
 *   }
 *   endShape();
 *   line(0,0,0,height);
 *   line(0,height/2,width, height/2);
 * }
 * </code></div>
 *
 * @alt
 * ellipse moves along a curve with mouse x. natural logarithm of n displayed.
 *
 */
p5.prototype.log = Math.log;

/**
 * Calculates the magnitude (or length) of a vector. A vector is a direction
 * in space commonly used in computer graphics and linear algebra. Because it
 * has no "start" position, the magnitude of a vector can be thought of as
 * the distance from the coordinate 0,0 to its x,y value. Therefore, mag() is
 * a shortcut for writing dist(0, 0, x, y).
 *
 * @method mag
 * @param  {Number} a first value
 * @param  {Number} b second value
 * @return {Number}   magnitude of vector from (0,0) to (a,b)
 * @example
 * <div><code>
 * function setup() {
 *   var x1 = 20;
 *   var x2 = 80;
 *   var y1 = 30;
 *   var y2 = 70;
 *
 *   line(0, 0, x1, y1);
 *   print(mag(x1, y1));  // Prints "36.05551"
 *   line(0, 0, x2, y1);
 *   print(mag(x2, y1));  // Prints "85.44004"
 *   line(0, 0, x1, y2);
 *   print(mag(x1, y2));  // Prints "72.8011"
 *   line(0, 0, x2, y2);
 *   print(mag(x2, y2));  // Prints "106.30146"
 * }
 * </code></div>
 *
 * @alt
 * 4 lines of different length radiate from top left of canvas.
 *
 */
p5.prototype.mag = function(x, y) {
  return Math.sqrt(x*x+y*y);
};

/**
 * Re-maps a number from one range to another.
 * <br><br>
 * In the first example above, the number 25 is converted from a value in the
 * range of 0 to 100 into a value that ranges from the left edge of the
 * window (0) to the right edge (width).
 *
 * @method map
 * @param  {Number} value  the incoming value to be converted
 * @param  {Number} start1 lower bound of the value's current range
 * @param  {Number} stop1  upper bound of the value's current range
 * @param  {Number} start2 lower bound of the value's target range
 * @param  {Number} stop2  upper bound of the value's target range
 * @return {Number}        remapped number
 * @example
 *   <div><code>
 *     var value = 25;
 *     var m = map(value, 0, 100, 0, width);
 *     ellipse(m, 50, 10, 10);
 *   </code></div>
 *
 *   <div><code>
 *     function setup() {
 *       noStroke();
 *     }
 *
 *     function draw() {
 *       background(204);
 *       var x1 = map(mouseX, 0, width, 25, 75);
 *       ellipse(x1, 25, 25, 25);
 *       var x2 = map(mouseX, 0, width, 0, 100);
 *       ellipse(x2, 75, 25, 25);
 *     }
 *   </code></div>
 *
 * @alt
 * 10 by 10 white ellipse with in mid left canvas
 * 2 25 by 25 white ellipses move with mouse x. Bottom has more range from X
 *
 */
p5.prototype.map = function(n, start1, stop1, start2, stop2) {
  return ((n-start1)/(stop1-start1))*(stop2-start2)+start2;
};

/**
 * Determines the largest value in a sequence of numbers, and then returns
 * that value. max() accepts any number of Number parameters, or an Array
 * of any length.
 *
 * @method max
 * @param  {Number|Array} n0 Numbers to compare
 * @return {Number}          maximum Number
 * @example
 * <div><code>
 * function setup() {
 *   // Change the elements in the array and run the sketch
 *   // to show how max() works!
 *   numArray = new Array(2,1,5,4,8,9);
 *   fill(0);
 *   noStroke();
 *   text("Array Elements", 0, 10);
 *   // Draw all numbers in the array
 *   var spacing = 15;
 *   var elemsY = 25;
 *   for(var i = 0; i < numArray.length; i++) {
 *     text(numArray[i], i * spacing, elemsY);
 *   }
 *   maxX = 33;
 *   maxY = 80;
 *   // Draw the Maximum value in the array.
 *   textSize(32);
 *   text(max(numArray), maxX, maxY);
 * }
 * </code></div>
 *
 * @alt
 * Small text at top reads: Array Elements 2 1 5 4 8 9. Large text at center: 9
 *
 */
p5.prototype.max = function() {
  if (arguments[0] instanceof Array) {
    return Math.max.apply(null,arguments[0]);
  } else {
    return Math.max.apply(null,arguments);
  }
};

/**
 * Determines the smallest value in a sequence of numbers, and then returns
 * that value. min() accepts any number of Number parameters, or an Array
 * of any length.
 *
 * @method min
 * @param  {Number|Array} n0 Numbers to compare
 * @return {Number}          minimum Number
 * @example
 * <div><code>
 * function setup() {
 *   // Change the elements in the array and run the sketch
 *   // to show how min() works!
 *   numArray = new Array(2,1,5,4,8,9);
 *   fill(0);
 *   noStroke();
 *   text("Array Elements", 0, 10);
 *   // Draw all numbers in the array
 *   var spacing = 15;
 *   var elemsY = 25;
 *   for(var i = 0; i < numArray.length; i++) {
 *     text(numArray[i], i * spacing, elemsY);
 *   }
 *   maxX = 33;
 *   maxY = 80;
 *   // Draw the Minimum value in the array.
 *   textSize(32);
 *   text(min(numArray), maxX, maxY);
 * }
 * </code></div>
 *
 * @alt
 * Small text at top reads: Array Elements 2 1 5 4 8 9. Large text at center: 1
 *
 */
p5.prototype.min = function() {
  if (arguments[0] instanceof Array) {
    return Math.min.apply(null,arguments[0]);
  } else {
    return Math.min.apply(null,arguments);
  }
};

/**
 * Normalizes a number from another range into a value between 0 and 1.
 * Identical to map(value, low, high, 0, 1).
 * Numbers outside of the range are not clamped to 0 and 1, because
 * out-of-range values are often intentional and useful. (See the second
 * example above.)
 *
 * @method norm
 * @param  {Number} value incoming value to be normalized
 * @param  {Number} start lower bound of the value's current range
 * @param  {Number} stop  upper bound of the value's current range
 * @return {Number}       normalized number
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *   currentNum = mouseX;
 *   lowerBound = 0;
 *   upperBound = width; //100;
 *   normalized = norm(currentNum, lowerBound, upperBound);
 *   lineY = 70
 *   line(0, lineY, width, lineY);
 *   //Draw an ellipse mapped to the non-normalized value.
 *   noStroke();
 *   fill(50)
 *   var s = 7; // ellipse size
 *   ellipse(currentNum, lineY, s, s);
 *
 *   // Draw the guide
 *   guideY = lineY + 15;
 *   text("0", 0, guideY);
 *   textAlign(RIGHT);
 *   text("100", width, guideY);
 *
 *   // Draw the normalized value
 *   textAlign(LEFT);
 *   fill(0);
 *   textSize(32);
 *   normalY = 40;
 *   normalX = 20;
 *   text(normalized, normalX, normalY);
 * }
 * </code></div>
 *
 * @alt
 * ellipse moves with mouse. 0 shown left & 100 right and updating values center
 *
 */
p5.prototype.norm = function(n, start, stop) {
  return this.map(n, start, stop, 0, 1);
};

/**
 * Facilitates exponential expressions. The pow() function is an efficient
 * way of multiplying numbers by themselves (or their reciprocals) in large
 * quantities. For example, pow(3, 5) is equivalent to the expression
 * 3*3*3*3*3 and pow(3, -5) is equivalent to 1 / 3*3*3*3*3. Maps to
 * Math.pow().
 *
 * @method pow
 * @param  {Number} n base of the exponential expression
 * @param  {Number} e power by which to raise the base
 * @return {Number}   n^e
 * @example
 * <div><code>
 * function setup() {
 *   //Exponentially increase the size of an ellipse.
 *   eSize = 3; // Original Size
 *   eLoc = 10; // Original Location
 *
 *   ellipse(eLoc, eLoc, eSize, eSize);
 *
 *   ellipse(eLoc*2, eLoc*2, pow(eSize, 2), pow(eSize, 2));
 *
 *   ellipse(eLoc*4, eLoc*4, pow(eSize, 3), pow(eSize, 3));
 *
 *   ellipse(eLoc*8, eLoc*8, pow(eSize, 4), pow(eSize, 4));
 * }
 * </code></div>
 *
 * @alt
 * small to large ellipses radiating from top left of canvas
 *
 */
p5.prototype.pow = Math.pow;

/**
 * Calculates the integer closest to the n parameter. For example,
 * round(133.8) returns the value 134. Maps to Math.round().
 *
 * @method round
 * @param  {Number} n number to round
 * @return {Number}   rounded number
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *   //map, mouseX between 0 and 5.
 *   var ax = map(mouseX, 0, 100, 0, 5);
 *   var ay = 66;
 *
 *   // Round the mapped number.
 *   var bx = round(map(mouseX, 0, 100, 0,5));
 *   var by = 33;
 *
 *   // Multiply the mapped numbers by 20 to more easily
 *   // see the changes.
 *   stroke(0);
 *   fill(0);
 *   line(0, ay, ax * 20, ay);
 *   line(0, by, bx * 20, by);
 *
 *   // Reformat the float returned by map and draw it.
 *   noStroke();
 *   text(nfc(ax, 2,2), ax, ay - 5);
 *   text(nfc(bx,1,1), bx, by - 5);
 * }
 * </code></div>
 *
 * @alt
 * horizontal center line squared values displayed on top and regular on bottom.
 *
 */
p5.prototype.round = Math.round;

/**
 * Squares a number (multiplies a number by itself). The result is always a
 * positive number, as multiplying two negative numbers always yields a
 * positive result. For example, -1 * -1 = 1.
 *
 * @method sq
 * @param  {Number} n number to square
 * @return {Number}   squared number
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *   eSize = 7;
 *   x1 = map(mouseX, 0, width, 0, 10);
 *   y1 = 80;
 *   x2 = sq(x1);
 *   y2 = 20;
 *
 *   // Draw the non-squared.
 *   line(0, y1, width, y1);
 *   ellipse(x1, y1, eSize, eSize);
 *
 *   // Draw the squared.
 *   line(0, y2, width, y2);
 *   ellipse(x2, y2, eSize, eSize);
 *
 *   // Draw dividing line.
 *   stroke(100)
 *   line(0, height/2, width, height/2);
 *
 *   // Draw text.
 *   var spacing = 15;
 *   noStroke();
 *   fill(0);
 *   text("x = " + x1, 0, y1 + spacing);
 *   text("sq(x) = " + x2, 0, y2 + spacing);
 * }
 * </code></div>
 *
 * @alt
 * horizontal center line squared values displayed on top and regular on bottom.
 *
 */
p5.prototype.sq = function(n) { return n*n; };

/**
 * Calculates the square root of a number. The square root of a number is
 * always positive, even though there may be a valid negative root. The
 * square root s of number a is such that s*s = a. It is the opposite of
 * squaring. Maps to Math.sqrt().
 *
 * @method sqrt
 * @param  {Number} n non-negative number to square root
 * @return {Number}   square root of number
 * @example
 * <div><code>
 * function draw() {
 *   background(200);
 *   eSize = 7;
 *   x1 = mouseX;
 *   y1 = 80;
 *   x2 = sqrt(x1);
 *   y2 = 20;
 *
 *   // Draw the non-squared.
 *   line(0, y1, width, y1);
 *   ellipse(x1, y1, eSize, eSize);
 *
 *   // Draw the squared.
 *   line(0, y2, width, y2);
 *   ellipse(x2, y2, eSize, eSize);
 *
 *   // Draw dividing line.
 *   stroke(100)
 *   line(0, height/2, width, height/2);
 *
 *   // Draw text.
 *   noStroke();
 *   fill(0);
 *   var spacing = 15;
 *   text("x = " + x1, 0, y1 + spacing);
 *   text("sqrt(x) = " + x2, 0, y2 + spacing);
 * }
 * </code></div>
 *
 * @alt
 * horizontal center line squareroot values displayed on top and regular on bottom.
 *
 */
p5.prototype.sqrt = Math.sqrt;

module.exports = p5;

},{"../core/core":39}],66:[function(_dereq_,module,exports){
/**
 * @module Math
 * @submodule Math
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');


/**
 * Creates a new p5.Vector (the datatype for storing vectors). This provides a
 * two or three dimensional vector, specifically a Euclidean (also known as
 * geometric) vector. A vector is an entity that has both magnitude and
 * direction.
 *
 * @method createVector
 * @param {Number} [x] x component of the vector
 * @param {Number} [y] y component of the vector
 * @param {Number} [z] z component of the vector
 */
p5.prototype.createVector = function (x, y, z) {
  if (this instanceof p5) {
    return new p5.Vector(this, arguments);
  } else {
    return new p5.Vector(x, y, z);
  }
};

module.exports = p5;

},{"../core/core":39}],67:[function(_dereq_,module,exports){
//////////////////////////////////////////////////////////////

// http://mrl.nyu.edu/~perlin/noise/
// Adapting from PApplet.java
// which was adapted from toxi
// which was adapted from the german demo group farbrausch
// as used in their demo "art": http://www.farb-rausch.de/fr010src.zip

// someday we might consider using "improved noise"
// http://mrl.nyu.edu/~perlin/paper445.pdf
// See: https://github.com/shiffman/The-Nature-of-Code-Examples-p5.js/
//      blob/master/introduction/Noise1D/noise.js

/**
 * @module Math
 * @submodule Noise
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

var PERLIN_YWRAPB = 4;
var PERLIN_YWRAP = 1<<PERLIN_YWRAPB;
var PERLIN_ZWRAPB = 8;
var PERLIN_ZWRAP = 1<<PERLIN_ZWRAPB;
var PERLIN_SIZE = 4095;

var perlin_octaves = 4; // default to medium smooth
var perlin_amp_falloff = 0.5; // 50% reduction/octave

var scaled_cosine = function(i) {
  return 0.5*(1.0-Math.cos(i*Math.PI));
};

var perlin; // will be initialized lazily by noise() or noiseSeed()


/**
 * Returns the Perlin noise value at specified coordinates. Perlin noise is
 * a random sequence generator producing a more natural ordered, harmonic
 * succession of numbers compared to the standard <b>random()</b> function.
 * It was invented by Ken Perlin in the 1980s and been used since in
 * graphical applications to produce procedural textures, natural motion,
 * shapes, terrains etc.<br /><br /> The main difference to the
 * <b>random()</b> function is that Perlin noise is defined in an infinite
 * n-dimensional space where each pair of coordinates corresponds to a
 * fixed semi-random value (fixed only for the lifespan of the program; see
 * the noiseSeed() function). p5.js can compute 1D, 2D and 3D noise,
 * depending on the number of coordinates given. The resulting value will
 * always be between 0.0 and 1.0. The noise value can be animated by moving
 * through the noise space as demonstrated in the example above. The 2nd
 * and 3rd dimension can also be interpreted as time.<br /><br />The actual
 * noise is structured similar to an audio signal, in respect to the
 * function's use of frequencies. Similar to the concept of harmonics in
 * physics, perlin noise is computed over several octaves which are added
 * together for the final result. <br /><br />Another way to adjust the
 * character of the resulting sequence is the scale of the input
 * coordinates. As the function works within an infinite space the value of
 * the coordinates doesn't matter as such, only the distance between
 * successive coordinates does (eg. when using <b>noise()</b> within a
 * loop). As a general rule the smaller the difference between coordinates,
 * the smoother the resulting noise sequence will be. Steps of 0.005-0.03
 * work best for most applications, but this will differ depending on use.
 *
 *
 * @method noise
 * @param  {Number} x   x-coordinate in noise space
 * @param  {Number} y   y-coordinate in noise space
 * @param  {Number} z   z-coordinate in noise space
 * @return {Number}     Perlin noise value (between 0 and 1) at specified
 *                      coordinates
 * @example
 * <div>
 * <code>var xoff = 0.0;
 *
 * function draw() {
 *   background(204);
 *   xoff = xoff + .01;
 *   var n = noise(xoff) * width;
 *   line(n, 0, n, height);
 * }
 * </code>
 * </div>
 * <div>
 * <code>var noiseScale=0.02;
 *
 * function draw() {
 *   background(0);
 *   for (var x=0; x < width; x++) {
 *     var noiseVal = noise((mouseX+x)*noiseScale, mouseY*noiseScale);
 *     stroke(noiseVal*255);
 *     line(x, mouseY+noiseVal*80, x, height);
 *   }
 * }
 * </code>
 * </div>
 *
 * @alt
 * vertical line moves left to right with updating noise values.
 * horizontal wave pattern effected by mouse x-position & updating noise values.
 *
 */

p5.prototype.noise = function(x,y,z) {
  y = y || 0;
  z = z || 0;

  if (perlin == null) {
    perlin = new Array(PERLIN_SIZE + 1);
    for (var i = 0; i < PERLIN_SIZE + 1; i++) {
      perlin[i] = Math.random();
    }
  }

  if (x<0) { x=-x; }
  if (y<0) { y=-y; }
  if (z<0) { z=-z; }

  var xi=Math.floor(x), yi=Math.floor(y), zi=Math.floor(z);
  var xf = x - xi;
  var yf = y - yi;
  var zf = z - zi;
  var rxf, ryf;

  var r=0;
  var ampl=0.5;

  var n1,n2,n3;

  for (var o=0; o<perlin_octaves; o++) {
    var of=xi+(yi<<PERLIN_YWRAPB)+(zi<<PERLIN_ZWRAPB);

    rxf = scaled_cosine(xf);
    ryf = scaled_cosine(yf);

    n1  = perlin[of&PERLIN_SIZE];
    n1 += rxf*(perlin[(of+1)&PERLIN_SIZE]-n1);
    n2  = perlin[(of+PERLIN_YWRAP)&PERLIN_SIZE];
    n2 += rxf*(perlin[(of+PERLIN_YWRAP+1)&PERLIN_SIZE]-n2);
    n1 += ryf*(n2-n1);

    of += PERLIN_ZWRAP;
    n2  = perlin[of&PERLIN_SIZE];
    n2 += rxf*(perlin[(of+1)&PERLIN_SIZE]-n2);
    n3  = perlin[(of+PERLIN_YWRAP)&PERLIN_SIZE];
    n3 += rxf*(perlin[(of+PERLIN_YWRAP+1)&PERLIN_SIZE]-n3);
    n2 += ryf*(n3-n2);

    n1 += scaled_cosine(zf)*(n2-n1);

    r += n1*ampl;
    ampl *= perlin_amp_falloff;
    xi<<=1;
    xf*=2;
    yi<<=1;
    yf*=2;
    zi<<=1;
    zf*=2;

    if (xf>=1.0) { xi++; xf--; }
    if (yf>=1.0) { yi++; yf--; }
    if (zf>=1.0) { zi++; zf--; }
  }
  return r;
};


/**
 *
 * Adjusts the character and level of detail produced by the Perlin noise
 * function. Similar to harmonics in physics, noise is computed over
 * several octaves. Lower octaves contribute more to the output signal and
 * as such define the overall intensity of the noise, whereas higher octaves
 * create finer grained details in the noise sequence.
 * <br><br>
 * By default, noise is computed over 4 octaves with each octave contributing
 * exactly half than its predecessor, starting at 50% strength for the 1st
 * octave. This falloff amount can be changed by adding an additional function
 * parameter. Eg. a falloff factor of 0.75 means each octave will now have
 * 75% impact (25% less) of the previous lower octave. Any value between
 * 0.0 and 1.0 is valid, however note that values greater than 0.5 might
 * result in greater than 1.0 values returned by <b>noise()</b>.
 * <br><br>
 * By changing these parameters, the signal created by the <b>noise()</b>
 * function can be adapted to fit very specific needs and characteristics.
 *
 * @method noiseDetail
 * @param {Number} lod number of octaves to be used by the noise
 * @param {Number} falloff falloff factor for each octave
 * @example
 * <div>
 * <code>
 *
 * var noiseVal;
 * var noiseScale=0.02;
 *
 * function setup() {
 *   createCanvas(100,100);
 * }
 *
 * function draw() {
 *   background(0);
 *   for (var y = 0; y < height; y++) {
 *     for (var x = 0; x < width/2; x++) {
 *       noiseDetail(2,0.2);
 *       noiseVal = noise((mouseX+x) * noiseScale,
 *                        (mouseY+y) * noiseScale);
 *       stroke(noiseVal*255);
 *       point(x,y);
 *       noiseDetail(8,0.65);
 *       noiseVal = noise((mouseX + x + width/2) * noiseScale,
 *                        (mouseY + y) * noiseScale);
 *       stroke(noiseVal*255);
 *       point(x + width/2, y);
 *     }
 *   }
 * }
 * </code>
 * </div>
 *
 * @alt
 * 2 vertical grey smokey patterns affected my mouse x-position and noise.
 *
 */
p5.prototype.noiseDetail = function(lod, falloff) {
  if (lod>0)     { perlin_octaves=lod; }
  if (falloff>0) { perlin_amp_falloff=falloff; }
};

/**
 * Sets the seed value for <b>noise()</b>. By default, <b>noise()</b>
 * produces different results each time the program is run. Set the
 * <b>value</b> parameter to a constant to return the same pseudo-random
 * numbers each time the software is run.
 *
 * @method noiseSeed
 * @param {Number} seed   the seed value
 * @example
 * <div>
 * <code>var xoff = 0.0;
 *
 * function setup() {
 *   noiseSeed(99);
 *   stroke(0, 10);
 * }
 *
 * function draw() {
 *   xoff = xoff + .01;
 *   var n = noise(xoff) * width;
 *   line(n, 0, n, height);
 * }
 * </code>
 * </div>
 *
 * @alt
 * vertical grey lines drawing in pattern affected by noise.
 *
 */
p5.prototype.noiseSeed = function(seed) {
  // Linear Congruential Generator
  // Variant of a Lehman Generator
  var lcg = (function() {
    // Set to values from http://en.wikipedia.org/wiki/Numerical_Recipes
    // m is basically chosen to be large (as it is the max period)
    // and for its relationships to a and c
    var m = 4294967296,
    // a - 1 should be divisible by m's prime factors
    a = 1664525,
     // c and m should be co-prime
    c = 1013904223,
    seed, z;
    return {
      setSeed : function(val) {
        // pick a random seed if val is undefined or null
        // the >>> 0 casts the seed to an unsigned 32-bit integer
        z = seed = (val == null ? Math.random() * m : val) >>> 0;
      },
      getSeed : function() {
        return seed;
      },
      rand : function() {
        // define the recurrence relationship
        z = (a * z + c) % m;
        // return a float in [0, 1)
        // if z = m then z / m = 0 therefore (z % m) / m < 1 always
        return z / m;
      }
    };
  }());

  lcg.setSeed(seed);
  perlin = new Array(PERLIN_SIZE + 1);
  for (var i = 0; i < PERLIN_SIZE + 1; i++) {
    perlin[i] = lcg.rand();
  }
};

module.exports = p5;

},{"../core/core":39}],68:[function(_dereq_,module,exports){
/**
 * @module Math
 * @submodule Math
 * @requires constants
 */

'use strict';

var p5 = _dereq_('../core/core');
var polarGeometry = _dereq_('./polargeometry');
var constants = _dereq_('../core/constants');

/**
 * A class to describe a two or three dimensional vector, specifically
 * a Euclidean (also known as geometric) vector. A vector is an entity
 * that has both magnitude and direction. The datatype, however, stores
 * the components of the vector (x, y for 2D, and x, y, z for 3D). The magnitude
 * and direction can be accessed via the methods mag() and heading().
 * <br><br>
 * In many of the p5.js examples, you will see p5.Vector used to describe a
 * position, velocity, or acceleration. For example, if you consider a rectangle
 * moving across the screen, at any given instant it has a position (a vector
 * that points from the origin to its location), a velocity (the rate at which
 * the object's position changes per time unit, expressed as a vector), and
 * acceleration (the rate at which the object's velocity changes per time
 * unit, expressed as a vector).
 * <br><br>
 * Since vectors represent groupings of values, we cannot simply use
 * traditional addition/multiplication/etc. Instead, we'll need to do some
 * "vector" math, which is made easy by the methods inside the p5.Vector class.
 *
 * @class p5.Vector
 * @constructor
 * @param {Number} [x] x component of the vector
 * @param {Number} [y] y component of the vector
 * @param {Number} [z] z component of the vector
 * @example
 * <div>
 * <code>
 * var v1 = createVector(40, 50);
 * var v2 = createVector(40, 50);
 *
 * ellipse(v1.x, v1.y, 50, 50);
 * ellipse(v2.x, v2.y, 50, 50);
 * v1.add(v2);
 * ellipse(v1.x, v1.y, 50, 50);
 * </code>
 * </div>
 *
 * @alt
 * 2 white ellipses. One center-left the other bottom right and off canvas
 *
 */
p5.Vector = function() {
  var x,y,z;
  // This is how it comes in with createVector()
  if(arguments[0] instanceof p5) {
    // save reference to p5 if passed in
    this.p5 = arguments[0];
    x  = arguments[1][0] || 0;
    y  = arguments[1][1] || 0;
    z  = arguments[1][2] || 0;
  // This is what we'll get with new p5.Vector()
  } else {
    x = arguments[0] || 0;
    y = arguments[1] || 0;
    z = arguments[2] || 0;
  }
  /**
   * The x component of the vector
   * @property x
   * @type {Number}
   */
  this.x = x;
  /**
   * The y component of the vector
   * @property y
   * @type {Number}
   */
  this.y = y;
  /**
   * The z component of the vector
   * @property z
   * @type {Number}
   */
  this.z = z;
};

/**
 * Returns a string representation of a vector v by calling String(v)
 * or v.toString(). This method is useful for logging vectors in the
 * console.
 * @method  toString
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var v = createVector(20,30);
 *   print(String(v)); // prints "p5.Vector Object : [20, 30, 0]"
 * }
 * </div></code>
 *
 */
p5.Vector.prototype.toString = function p5VectorToString() {
  return 'p5.Vector Object : ['+ this.x +', '+ this.y +', '+ this.z + ']';
};

/**
 * Sets the x, y, and z component of the vector using two or three separate
 * variables, the data from a p5.Vector, or the values from a float array.
 * @method set
 *
 * @param {Number|p5.Vector|Array} [x] the x component of the vector or a
 *                                     p5.Vector or an Array
 * @param {Number}                 [y] the y component of the vector
 * @param {Number}                 [z] the z component of the vector
 * @example
 * <div class="norender">
 * <code>
 * function setup() {
 *    var v = createVector(1, 2, 3);
 *    v.set(4,5,6); // Sets vector to [4, 5, 6]
 *
 *    var v1 = createVector(0, 0, 0);
 *    var arr = [1, 2, 3];
 *    v1.set(arr); // Sets vector to [1, 2, 3]
 * }
 * </code>
 * </div>
 */
p5.Vector.prototype.set = function (x, y, z) {
  if (x instanceof p5.Vector) {
    this.x = x.x || 0;
    this.y = x.y || 0;
    this.z = x.z || 0;
    return this;
  }
  if (x instanceof Array) {
    this.x = x[0] || 0;
    this.y = x[1] || 0;
    this.z = x[2] || 0;
    return this;
  }
  this.x = x || 0;
  this.y = y || 0;
  this.z = z || 0;
  return this;
};

/**
 * Gets a copy of the vector, returns a p5.Vector object.
 *
 * @method copy
 * @return {p5.Vector} the copy of the p5.Vector object
 * @example
 * <div class="norender">
 * <code>
 * var v1 = createVector(1, 2, 3);
 * var v2 = v1.copy();
 * print(v1.x == v2.x && v1.y == v2.y && v1.z == v2.z);
 * // Prints "true"
 * </code>
 * </div>
 */
p5.Vector.prototype.copy = function () {
  if (this.p5) {
    return new p5.Vector(this.p5,[this.x, this.y, this.z]);
  } else {
    return new p5.Vector(this.x,this.y,this.z);
  }
};

/**
 * Adds x, y, and z components to a vector, adds one vector to another, or
 * adds two independent vectors together. The version of the method that adds
 * two vectors together is a static method and returns a p5.Vector, the others
 * acts directly on the vector. See the examples for more context.
 *
 * @method add
 * @chainable
 * @param  {Number|p5.Vector|Array} x   the x component of the vector to be
 *                                      added or a p5.Vector or an Array
 * @param  {Number}                 [y] the y component of the vector to be
 *                                      added
 * @param  {Number}                 [z] the z component of the vector to be
 *                                      added
 * @return {p5.Vector}                  the p5.Vector object.
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(1, 2, 3);
 * v.add(4,5,6);
 * // v's compnents are set to [5, 7, 9]
 * </code>
 * </div>
 * <div class="norender">
 * <code>
 * // Static method
 * var v1 = createVector(1, 2, 3);
 * var v2 = createVector(2, 3, 4);
 *
 * var v3 = p5.Vector.add(v1, v2);
 * // v3 has components [3, 5, 7]
 * </code>
 * </div>
 */
p5.Vector.prototype.add = function (x, y, z) {
  if (x instanceof p5.Vector) {
    this.x += x.x || 0;
    this.y += x.y || 0;
    this.z += x.z || 0;
    return this;
  }
  if (x instanceof Array) {
    this.x += x[0] || 0;
    this.y += x[1] || 0;
    this.z += x[2] || 0;
    return this;
  }
  this.x += x || 0;
  this.y += y || 0;
  this.z += z || 0;
  return this;
};

/**
 * Subtracts x, y, and z components from a vector, subtracts one vector from
 * another, or subtracts two independent vectors. The version of the method
 * that subtracts two vectors is a static method and returns a p5.Vector, the
 * other acts directly on the vector. See the examples for more context.
 *
 * @method sub
 * @chainable
 * @param  {Number|p5.Vector|Array} x   the x component of the vector or a
 *                                      p5.Vector or an Array
 * @param  {Number}                 [y] the y component of the vector
 * @param  {Number}                 [z] the z component of the vector
 * @return {p5.Vector}                  p5.Vector object.
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(4, 5, 6);
 * v.sub(1, 1, 1);
 * // v's compnents are set to [3, 4, 5]
 * </code>
 * </div>
 *
 * <div class="norender">
 * <code>
 * // Static method
 * var v1 = createVector(2, 3, 4);
 * var v2 = createVector(1, 2, 3);
 *
 * var v3 = p5.Vector.sub(v1, v2);
 * // v3 has compnents [1, 1, 1]
 * </code>
 * </div>
 */
p5.Vector.prototype.sub = function (x, y, z) {
  if (x instanceof p5.Vector) {
    this.x -= x.x || 0;
    this.y -= x.y || 0;
    this.z -= x.z || 0;
    return this;
  }
  if (x instanceof Array) {
    this.x -= x[0] || 0;
    this.y -= x[1] || 0;
    this.z -= x[2] || 0;
    return this;
  }
  this.x -= x || 0;
  this.y -= y || 0;
  this.z -= z || 0;
  return this;
};

/**
 * Multiply the vector by a scalar. The static version of this method
 * creates a new p5.Vector while the non static version acts on the vector
 * directly. See the examples for more context.
 *
 * @method mult
 * @chainable
 * @param  {Number}    n the number to multiply with the vector
 * @return {p5.Vector} a reference to the p5.Vector object (allow chaining)
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(1, 2, 3);
 * v.mult(2);
 * // v's compnents are set to [2, 4, 6]
 * </code>
 * </div>
 *
 * <div class="norender">
 * <code>
 * // Static method
 * var v1 = createVector(1, 2, 3);
 * var v2 = p5.Vector.mult(v1, 2);
 * // v2 has compnents [2, 4, 6]
 * </code>
 * </div>
 */
p5.Vector.prototype.mult = function (n) {
  this.x *= n || 0;
  this.y *= n || 0;
  this.z *= n || 0;
  return this;
};

/**
 * Divide the vector by a scalar. The static version of this method creates a
 * new p5.Vector while the non static version acts on the vector directly.
 * See the examples for more context.
 *
 * @method div
 * @chainable
 * @param  {number}    n the number to divide the vector by
 * @return {p5.Vector} a reference to the p5.Vector object (allow chaining)
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(6, 4, 2);
 * v.div(2); //v's compnents are set to [3, 2, 1]
 * </code>
 * </div>
 *
 * <div class="norender">
 * <code>
 * // Static method
 * var v1  = createVector(6, 4, 2);
 * var v2 = p5.Vector.div(v, 2);
 * // v2 has compnents [3, 2, 1]
 * </code>
 * </div>
 */
p5.Vector.prototype.div = function (n) {
  this.x /= n;
  this.y /= n;
  this.z /= n;
  return this;
};

/**
 * Calculates the magnitude (length) of the vector and returns the result as
 * a float (this is simply the equation sqrt(x*x + y*y + z*z).)
 *
 * @method mag
 * @return {Number} magnitude of the vector
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(20.0, 30.0, 40.0);
 * var m = v.mag();
 * print(m); // Prints "53.85164807134504"
 * </code>
 * </div>
 */
p5.Vector.prototype.mag = function () {
  return Math.sqrt(this.magSq());
};

/**
 * Calculates the squared magnitude of the vector and returns the result
 * as a float (this is simply the equation <em>(x*x + y*y + z*z)</em>.)
 * Faster if the real length is not required in the
 * case of comparing vectors, etc.
 *
 * @method magSq
 * @return {number} squared magnitude of the vector
 * @example
 * <div class="norender">
 * <code>
 * // Static method
 * var v1 = createVector(6, 4, 2);
 * print(v1.magSq()); // Prints "56"
 * </code>
 * </div>
 */
p5.Vector.prototype.magSq = function () {
  var x = this.x, y = this.y, z = this.z;
  return (x * x + y * y + z * z);
};

/**
 * Calculates the dot product of two vectors. The version of the method
 * that computes the dot product of two independent vectors is a static
 * method. See the examples for more context.
 *
 *
 * @method dot
 * @param  {Number|p5.Vector} x   x component of the vector or a p5.Vector
 * @param  {Number}           [y] y component of the vector
 * @param  {Number}           [z] z component of the vector
 * @return {Number}                 the dot product
 *
 * @example
 * <div class="norender">
 * <code>
 * var v1 = createVector(1, 2, 3);
 * var v2 = createVector(2, 3, 4);
 *
 * print(v1.dot(v2)); // Prints "20"
 * </code>
 * </div>
 *
 * <div class="norender">
 * <code>
 * //Static method
 * var v1 = createVector(1, 2, 3);
 * var v2 = createVector(3, 2, 1);
 * print (p5.Vector.dot(v1, v2)); // Prints "10"
 * </code>
 * </div>
 */
p5.Vector.prototype.dot = function (x, y, z) {
  if (x instanceof p5.Vector) {
    return this.dot(x.x, x.y, x.z);
  }
  return this.x * (x || 0) +
         this.y * (y || 0) +
         this.z * (z || 0);
};

/**
 * Calculates and returns a vector composed of the cross product between
 * two vectors. Both the static and non static methods return a new p5.Vector.
 * See the examples for more context.
 *
 * @method cross
 * @param  {p5.Vector} v p5.Vector to be crossed
 * @return {p5.Vector}   p5.Vector composed of cross product
 * @example
 * <div class="norender">
 * <code>
 * var v1 = createVector(1, 2, 3);
 * var v2 = createVector(1, 2, 3);
 *
 * v1.cross(v2); // v's components are [0, 0, 0]
 * </code>
 * </div>
 *
 * <div class="norender">
 * <code>
 * // Static method
 * var v1 = createVector(1, 0, 0);
 * var v2 = createVector(0, 1, 0);
 *
 * var crossProduct = p5.Vector.cross(v1, v2);
 * // crossProduct has components [0, 0, 1]
 * </code>
 * </div>
 */
p5.Vector.prototype.cross = function (v) {
  var x = this.y * v.z - this.z * v.y;
  var y = this.z * v.x - this.x * v.z;
  var z = this.x * v.y - this.y * v.x;
  if (this.p5) {
    return new p5.Vector(this.p5,[x,y,z]);
  } else {
    return new p5.Vector(x,y,z);
  }
};

/**
 * Calculates the Euclidean distance between two points (considering a
 * point as a vector object).
 *
 * @method dist
 * @param  {p5.Vector} v the x, y, and z coordinates of a p5.Vector
 * @return {Number}      the distance
 * @example
 * <div class="norender">
 * <code>
 * var v1 = createVector(1, 0, 0);
 * var v2 = createVector(0, 1, 0);
 *
 * var distance = v1.dist(v2); // distance is 1.4142...
 * </code>
 * </div>
 * <div class="norender">
 * <code>
 * // Static method
 * var v1 = createVector(1, 0, 0);
 * var v2 = createVector(0, 1, 0);
 *
 * var distance = p5.Vector.dist(v1,v2);
 * // distance is 1.4142...
 * </code>
 * </div>
 */
p5.Vector.prototype.dist = function (v) {
  var d = v.copy().sub(this);
  return d.mag();
};

/**
 * Normalize the vector to length 1 (make it a unit vector).
 *
 * @method normalize
 * @return {p5.Vector} normalized p5.Vector
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(10, 20, 2);
 * // v has compnents [10.0, 20.0, 2.0]
 * v.normalize();
 * // v's compnents are set to
 * // [0.4454354, 0.8908708, 0.089087084]
 * </code>
 * </div>
 *
 */
p5.Vector.prototype.normalize = function () {
  return this.mag() === 0 ? this : this.div(this.mag());
};

/**
 * Limit the magnitude of this vector to the value used for the <b>max</b>
 * parameter.
 *
 * @method limit
 * @param  {Number}    max the maximum magnitude for the vector
 * @return {p5.Vector}     the modified p5.Vector
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(10, 20, 2);
 * // v has compnents [10.0, 20.0, 2.0]
 * v.limit(5);
 * // v's compnents are set to
 * // [2.2271771, 4.4543543, 0.4454354]
 * </code>
 * </div>
 */
p5.Vector.prototype.limit = function (max) {
  var mSq = this.magSq();
  if(mSq > max*max) {
    this.div(Math.sqrt(mSq)); //normalize it
    this.mult(max);
  }
  return this;
};

/**
 * Set the magnitude of this vector to the value used for the <b>len</b>
 * parameter.
 *
 * @method setMag
 * @param  {number}    len the new length for this vector
 * @return {p5.Vector}     the modified p5.Vector
 * @example
 * <div class="norender">
 * <code>
 * var v1 = createVector(10, 20, 2);
 * // v has compnents [10.0, 20.0, 2.0]
 * v1.setMag(10);
 * // v's compnents are set to [6.0, 8.0, 0.0]
 * </code>
 * </div>
 */
p5.Vector.prototype.setMag = function (n) {
  return this.normalize().mult(n);
};

/**
 * Calculate the angle of rotation for this vector (only 2D vectors)
 *
 * @method heading
 * @return {Number} the angle of rotation
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var v1 = createVector(30,50);
 *   print(v1.heading()); // 1.0303768265243125
 *
 *   var v1 = createVector(40,50);
 *   print(v1.heading()); // 0.8960553845713439
 *
 *   var v1 = createVector(30,70);
 *   print(v1.heading()); // 1.1659045405098132
 * }
 * </div></code>
 */
p5.Vector.prototype.heading = function () {
  var h = Math.atan2(this.y, this.x);
  if (this.p5) {
    if (this.p5._angleMode === constants.RADIANS) {
      return h;
    } else {
      return polarGeometry.radiansToDegrees(h);
    }
  } else {
    return h;
  }
};

/**
 * Rotate the vector by an angle (only 2D vectors), magnitude remains the
 * same
 *
 * @method rotate
 * @param  {number}    angle the angle of rotation
 * @return {p5.Vector} the modified p5.Vector
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(10.0, 20.0);
 * // v has compnents [10.0, 20.0, 0.0]
 * v.rotate(HALF_PI);
 * // v's compnents are set to [-20.0, 9.999999, 0.0]
 * </code>
 * </div>
 */
p5.Vector.prototype.rotate = function (a) {
  if (this.p5) {
    if (this.p5._angleMode === constants.DEGREES) {
      a = polarGeometry.degreesToRadians(a);
    }
  }
  var newHeading = this.heading() + a;
  var mag = this.mag();
  this.x = Math.cos(newHeading) * mag;
  this.y = Math.sin(newHeading) * mag;
  return this;
};

/**
 * Linear interpolate the vector to another vector
 *
 * @method lerp
 * @param  {p5.Vector} x   the x component or the p5.Vector to lerp to
 * @param  {p5.Vector} [y] y the y component
 * @param  {p5.Vector} [z] z the z component
 * @param  {Number}    amt the amount of interpolation; some value between 0.0
 *                         (old vector) and 1.0 (new vector). 0.1 is very near
 *                         the new vector. 0.5 is halfway in between.
 * @return {p5.Vector}     the modified p5.Vector
 * @example
 * <div class="norender">
 * <code>
 * var v = createVector(1, 1, 0);
 *
 * v.lerp(3, 3, 0, 0.5); // v now has components [2,2,0]
 * </code>
 * </div>
 *
 * <div class="norender">
 * <code>
 * var v1 = createVector(0, 0, 0);
 * var v2 = createVector(100, 100, 0);
 *
 * var v3 = p5.Vector.lerp(v1, v2, 0.5);
 * // v3 has components [50,50,0]
 * </code>
 * </div>
 */
p5.Vector.prototype.lerp = function (x, y, z, amt) {
  if (x instanceof p5.Vector) {
    return this.lerp(x.x, x.y, x.z, y);
  }
  this.x += (x - this.x) * amt || 0;
  this.y += (y - this.y) * amt || 0;
  this.z += (z - this.z) * amt || 0;
  return this;
};

/**
 * Return a representation of this vector as a float array. This is only
 * for temporary use. If used in any other fashion, the contents should be
 * copied by using the <b>p5.Vector.copy()</b> method to copy into your own
 * array.
 *
 * @method array
 * @return {Array} an Array with the 3 values
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var v = createVector(20,30);
 *   print(v.array()); // Prints : Array [20, 30, 0]
 * }
 * </div></code>
 * <div class="norender">
 * <code>
 * var v = createVector(10.0, 20.0, 30.0);
 * var f = v.array();
 * print(f[0]); // Prints "10.0"
 * print(f[1]); // Prints "20.0"
 * print(f[2]); // Prints "30.0"
 * </code>
 * </div>
 */
p5.Vector.prototype.array = function () {
  return [this.x || 0, this.y || 0, this.z || 0];
};

/**
 * Equality check against a p5.Vector
 *
 * @method equals
 * @param {Number|p5.Vector|Array} [x] the x component of the vector or a
 *                                     p5.Vector or an Array
 * @param {Number}                 [y] the y component of the vector
 * @param {Number}                 [z] the z component of the vector
 * @return {Boolean} whether the vectors are equals
 * @example
 * <div class = "norender"><code>
 * v1 = createVector(5,10,20);
 * v2 = createVector(5,10,20);
 * v3 = createVector(13,10,19);
 *
 * print(v1.equals(v2.x,v2.y,v2.z)); // true
 * print(v1.equals(v3.x,v3.y,v3.z)); // false
 * </div></code>
 * <div class="norender">
 * <code>
 * var v1 = createVector(10.0, 20.0, 30.0);
 * var v2 = createVector(10.0, 20.0, 30.0);
 * var v3 = createVector(0.0, 0.0, 0.0);
 * print (v1.equals(v2)) // true
 * print (v1.equals(v3)) // false
 * </code>
 * </div>
 */
p5.Vector.prototype.equals = function (x, y, z) {
  var a, b, c;
  if (x instanceof p5.Vector) {
    a = x.x || 0;
    b = x.y || 0;
    c = x.z || 0;
  } else if (x instanceof Array) {
    a = x[0] || 0;
    b = x[1] || 0;
    c = x[2] || 0;
  } else {
    a = x || 0;
    b = y || 0;
    c = z || 0;
  }
  return this.x === a && this.y === b && this.z === c;
};


// Static Methods


/**
 * Make a new 2D unit vector from an angle
 *
 * @method fromAngle
 * @static
 * @param {Number}     angle the desired angle
 * @return {p5.Vector}       the new p5.Vector object
 * @example
 * <div>
 * <code>
 * function draw() {
 *   background (200);
 *
 *   // Create a variable, proportional to the mouseX,
 *   // varying from 0-360, to represent an angle in degrees.
 *   angleMode(DEGREES);
 *   var myDegrees = map(mouseX, 0,width, 0,360);
 *
 *   // Display that variable in an onscreen text.
 *   // (Note the nfc() function to truncate additional decimal places,
 *   // and the "\xB0" character for the degree symbol.)
 *   var readout = "angle = " + nfc(myDegrees,1,1) + "\xB0"
 *   noStroke();
 *   fill (0);
 *   text (readout, 5, 15);
 *
 *   // Create a p5.Vector using the fromAngle function,
 *   // and extract its x and y components.
 *   var v = p5.Vector.fromAngle(radians(myDegrees));
 *   var vx = v.x;
 *   var vy = v.y;
 *
 *   push();
 *   translate (width/2, height/2);
 *   noFill();
 *   stroke (150);
 *   line (0,0, 30,0);
 *   stroke (0);
 *   line (0,0, 30*vx, 30*vy);
 *   pop()
 * }
 * </code>
 * </div>
 */
p5.Vector.fromAngle = function(angle) {
  if (this.p5) {
    if (this.p5._angleMode === constants.DEGREES) {
      angle = polarGeometry.degreesToRadians(angle);
    }
  }
  if (this.p5) {
    return new p5.Vector(this.p5,[Math.cos(angle),Math.sin(angle),0]);
  } else {
    return new p5.Vector(Math.cos(angle),Math.sin(angle),0);
  }
};

/**
 * Make a new 2D unit vector from a random angle
 *
 * @method random2D
 * @static
 * @return {p5.Vector} the new p5.Vector object
 * @example
 * <div class="norender">
 * <code>
 * var v = p5.Vector.random2D();
 * // May make v's attributes something like:
 * // [0.61554617, -0.51195765, 0.0] or
 * // [-0.4695841, -0.14366731, 0.0] or
 * // [0.6091097, -0.22805278, 0.0]
 * </code>
 * </div>
 */
p5.Vector.random2D = function () {
  var angle;
  // A lot of nonsense to determine if we know about a
  // p5 sketch and whether we should make a random angle in degrees or radians
  if (this.p5) {
    if (this.p5._angleMode === constants.DEGREES) {
      angle = this.p5.random(360);
    } else {
      angle = this.p5.random(constants.TWO_PI);
    }
  } else {
    angle = Math.random()*Math.PI*2;
  }
  return this.fromAngle(angle);
};

/**
 * Make a new random 3D unit vector.
 *
 * @method random3D
 * @static
 * @return {p5.Vector} the new p5.Vector object
 * @example
 * <div class="norender">
 * <code>
 * var v = p5.Vector.random3D();
 * // May make v's attributes something like:
 * // [0.61554617, -0.51195765, 0.599168] or
 * // [-0.4695841, -0.14366731, -0.8711202] or
 * // [0.6091097, -0.22805278, -0.7595902]
 * </code>
 * </div>
 */
p5.Vector.random3D = function () {
  var angle,vz;
  // If we know about p5
  if (this.p5) {
    angle = this.p5.random(0,constants.TWO_PI);
    vz = this.p5.random(-1,1);
  } else {
    angle = Math.random()*Math.PI*2;
    vz = Math.random()*2-1;
  }
  var vx = Math.sqrt(1-vz*vz)*Math.cos(angle);
  var vy = Math.sqrt(1-vz*vz)*Math.sin(angle);
  if (this.p5) {
    return new p5.Vector(this.p5,[vx,vy,vz]);
  } else {
    return new p5.Vector(vx,vy,vz);
  }
};


/**
 * Adds two vectors together and returns a new one.
 *
 * @static
 * @param  {p5.Vector} v1 a p5.Vector to add
 * @param  {p5.Vector} v2 a p5.Vector to add
 * @param  {p5.Vector} target if undefined a new vector will be created
 * @return {p5.Vector} the resulting p5.Vector
 *
 */

p5.Vector.add = function (v1, v2, target) {
  if (!target) {
    target = v1.copy();
  } else {
    target.set(v1);
  }
  target.add(v2);
  return target;
};

/**
 * Subtracts one p5.Vector from another and returns a new one.  The second
 * vector (v2) is subtracted from the first (v1), resulting in v1-v2.
 *
 * @static
 * @param  {p5.Vector} v1 a p5.Vector to subtract from
 * @param  {p5.Vector} v2 a p5.Vector to subtract
 * @param  {p5.Vector} target if undefined a new vector will be created
 * @return {p5.Vector} the resulting p5.Vector
 */

p5.Vector.sub = function (v1, v2, target) {
  if (!target) {
    target = v1.copy();
  } else {
    target.set(v1);
  }
  target.sub(v2);
  return target;
};


/**
 * Multiplies a vector by a scalar and returns a new vector.
 *
 * @static
 * @param  {p5.Vector} v the p5.Vector to multiply
 * @param  {Number}  n the scalar
 * @param  {p5.Vector} target if undefined a new vector will be created
 * @return {p5.Vector}  the resulting new p5.Vector
 */
p5.Vector.mult = function (v, n, target) {
  if (!target) {
    target = v.copy();
  } else {
    target.set(v);
  }
  target.mult(n);
  return target;
};

/**
 * Divides a vector by a scalar and returns a new vector.
 *
 * @static
 * @param  {p5.Vector} v the p5.Vector to divide
 * @param  {Number}  n the scalar
 * @param  {p5.Vector} target if undefined a new vector will be created
 * @return {p5.Vector} the resulting new p5.Vector
 */
p5.Vector.div = function (v, n, target) {
  if (!target) {
    target = v.copy();
  } else {
    target.set(v);
  }
  target.div(n);
  return target;
};


/**
 * Calculates the dot product of two vectors.
 *
 * @static
 * @param  {p5.Vector} v1 the first p5.Vector
 * @param  {p5.Vector} v2 the second p5.Vector
 * @return {Number}     the dot product
 */
p5.Vector.dot = function (v1, v2) {
  return v1.dot(v2);
};

/**
 * Calculates the cross product of two vectors.
 *
 * @static
 * @param  {p5.Vector} v1 the first p5.Vector
 * @param  {p5.Vector} v2 the second p5.Vector
 * @return {Number}     the cross product
 */
p5.Vector.cross = function (v1, v2) {
  return v1.cross(v2);
};

/**
 * Calculates the Euclidean distance between two points (considering a
 * point as a vector object).
 *
 * @static
 * @param  {p5.Vector} v1 the first p5.Vector
 * @param  {p5.Vector} v2 the second p5.Vector
 * @return {Number}     the distance
 */
p5.Vector.dist = function (v1,v2) {
  return v1.dist(v2);
};

/**
 * Linear interpolate a vector to another vector and return the result as a
 * new vector.
 *
 * @static
 * @param {p5.Vector} v1 a starting p5.Vector
 * @param {p5.Vector} v2 the p5.Vector to lerp to
 * @param {Number}       the amount of interpolation; some value between 0.0
 *                       (old vector) and 1.0 (new vector). 0.1 is very near
 *                       the new vector. 0.5 is halfway in between.
 */
p5.Vector.lerp = function (v1, v2, amt, target) {
  if (!target) {
    target = v1.copy();
  } else {
    target.set(v1);
  }
  target.lerp(v2, amt);
  return target;
};

/**
 * Calculates and returns the angle (in radians) between two vectors.
 * @method angleBetween
 * @static
 * @param  {p5.Vector} v1 the x, y, and z components of a p5.Vector
 * @param  {p5.Vector} v2 the x, y, and z components of a p5.Vector
 * @return {Number}       the angle between (in radians)
 * @example
 * <div class="norender">
 * <code>
 * var v1 = createVector(1, 0, 0);
 * var v2 = createVector(0, 1, 0);
 *
 * var angle = p5.Vector.angleBetween(v1, v2);
 * // angle is PI/2
 * </code>
 * </div>
 */
p5.Vector.angleBetween = function (v1, v2) {
  var angle = Math.acos(v1.dot(v2) / (v1.mag() * v2.mag()));
  if (this.p5) {
    if (this.p5._angleMode === constants.DEGREES) {
      angle = polarGeometry.radiansToDegrees(angle);
    }
  }
  return angle;
};

/**
 * @static
 */
p5.Vector.mag = function (vecT){
  var x = vecT.x,
    y = vecT.y,
    z = vecT.z;
  var magSq = x * x + y * y + z * z;
  return Math.sqrt(magSq);
};

module.exports = p5.Vector;

},{"../core/constants":38,"../core/core":39,"./polargeometry":69}],69:[function(_dereq_,module,exports){

module.exports = {

  degreesToRadians: function(x) {
    return 2 * Math.PI * x / 360;
  },

  radiansToDegrees: function(x) {
    return 360 * x / (2 * Math.PI);
  }

};

},{}],70:[function(_dereq_,module,exports){
/**
 * @module Math
 * @submodule Random
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

var seeded = false;

// Linear Congruential Generator
// Variant of a Lehman Generator
var lcg = (function() {
  // Set to values from http://en.wikipedia.org/wiki/Numerical_Recipes
  // m is basically chosen to be large (as it is the max period)
  // and for its relationships to a and c
  var m = 4294967296,
    // a - 1 should be divisible by m's prime factors
    a = 1664525,
    // c and m should be co-prime
    c = 1013904223,
    seed, z;
  return {
    setSeed : function(val) {
      // pick a random seed if val is undefined or null
      // the >>> 0 casts the seed to an unsigned 32-bit integer
      z = seed = (val == null ? Math.random() * m : val) >>> 0;
    },
    getSeed : function() {
      return seed;
    },
    rand : function() {
      // define the recurrence relationship
      z = (a * z + c) % m;
      // return a float in [0, 1)
      // if z = m then z / m = 0 therefore (z % m) / m < 1 always
      return z / m;
    }
  };
}());

/**
 * Sets the seed value for random().
 *
 * By default, random() produces different results each time the program
 * is run. Set the seed parameter to a constant to return the same
 * pseudo-random numbers each time the software is run.
 *
 * @method randomSeed
 * @param {Number} seed   the seed value
 * @example
 * <div>
 * <code>
 * randomSeed(99);
 * for (var i=0; i < 100; i++) {
 *   var r = random(0, 255);
 *   stroke(r);
 *   line(i, 0, i, 100);
 * }
 * </code>
 * </div>
 *
 * @alt
 * many vertical lines drawn in white, black or grey.
 *
 */
p5.prototype.randomSeed = function(seed) {
  lcg.setSeed(seed);
  seeded = true;
};

/**
 * Return a random floating-point number.
 *
 * Takes either 0, 1 or 2 arguments.
 *
 * If no argument is given, returns a random number from 0
 * up to (but not including) 1.
 *
 * If one argument is given and it is a number, returns a random number from 0
 * up to (but not including) the number.
 *
 * If one argument is given and it is an array, returns a random element from
 * that array.
 *
 * If two arguments are given, returns a random number from the
 * first argument up to (but not including) the second argument.
 *
 * @method random
 * @param  {Number} [min]   the lower bound (inclusive)
 * @param  {Number} [max]   the upper bound (exclusive)
 * @return {Number|mixed} the random number or a random element in choices
 * @example
 * <div>
 * <code>
 * for (var i = 0; i < 100; i++) {
 *   var r = random(50);
 *   stroke(r*5);
 *   line(50, i, 50+r, i);
 * }
 * </code>
 * </div>
 * <div>
 * <code>
 * for (var i = 0; i < 100; i++) {
 *   var r = random(-50, 50);
 *   line(50,i,50+r,i);
 * }
 * </code>
 * </div>
 * <div>
 * <code>
 * // Get a random element from an array using the random(Array) syntax
 * var words = [ "apple", "bear", "cat", "dog" ];
 * var word = random(words);  // select random word
 * text(word,10,50);  // draw the word
 * </code>
 * </div>
 *
 * @alt
 * 100 horizontal lines from center canvas to right. size+fill change each time
 * 100 horizontal lines from center of canvas. height & side change each render
 * word displayed at random. Either apple, bear, cat, or dog
 *
 */
/**
 * @method random
 * @param  {Array} choices   the array to choose from
 * @return {mixed} the random element from the array
 * @example
 */
p5.prototype.random = function (min, max) {

  var rand;

  if (seeded) {
    rand  = lcg.rand();
  } else {
    rand = Math.random();
  }
  if (typeof min === 'undefined') {
    return rand;
  } else
  if (typeof max === 'undefined') {
    if (min instanceof Array) {
      return min[Math.floor(rand * min.length)];
    } else {
      return rand * min;
    }
  } else {
    if (min > max) {
      var tmp = min;
      min = max;
      max = tmp;
    }

    return rand * (max-min) + min;
  }
};


/**
 *
 * Returns a random number fitting a Gaussian, or
 * normal, distribution. There is theoretically no minimum or maximum
 * value that randomGaussian() might return. Rather, there is
 * just a very low probability that values far from the mean will be
 * returned; and a higher probability that numbers near the mean will
 * be returned.
 * <br><br>
 * Takes either 0, 1 or 2 arguments.<br>
 * If no args, returns a mean of 0 and standard deviation of 1.<br>
 * If one arg, that arg is the mean (standard deviation is 1).<br>
 * If two args, first is mean, second is standard deviation.
 *
 * @method randomGaussian
 * @param  {Number} mean  the mean
 * @param  {Number} sd    the standard deviation
 * @return {Number} the random number
 * @example
 * <div>
 * <code>for (var y = 0; y < 100; y++) {
 *  var x = randomGaussian(50,15);
 *  line(50, y, x, y);
 *}
 * </code>
 * </div>
 * <div>
 * <code>
 *var distribution = new Array(360);
 *
 *function setup() {
 *  createCanvas(100, 100);
 *  for (var i = 0; i < distribution.length; i++) {
 *    distribution[i] = floor(randomGaussian(0,15));
 *  }
 *}
 *
 *function draw() {
 *  background(204);
 *
 *  translate(width/2, width/2);
 *
 *  for (var i = 0; i < distribution.length; i++) {
 *    rotate(TWO_PI/distribution.length);
 *    stroke(0);
 *    var dist = abs(distribution[i]);
 *    line(0, 0, dist, 0);
 *  }
 *}
 * </code>
 * </div>
 * @alt
 * 100 horizontal lines from center of canvas. height & side change each render
 * black lines radiate from center of canvas. size determined each render
 */
var y2;
var previous = false;
p5.prototype.randomGaussian = function(mean, sd)  {
  var y1,x1,x2,w;
  if (previous) {
    y1 = y2;
    previous = false;
  } else {
    do {
      x1 = this.random(2) - 1;
      x2 = this.random(2) - 1;
      w = x1 * x1 + x2 * x2;
    } while (w >= 1);
    w = Math.sqrt((-2 * Math.log(w))/w);
    y1 = x1 * w;
    y2 = x2 * w;
    previous = true;
  }

  var m = mean || 0;
  var s = sd || 1;
  return y1*s + m;
};

module.exports = p5;

},{"../core/core":39}],71:[function(_dereq_,module,exports){
/**
 * @module Math
 * @submodule Trigonometry
 * @for p5
 * @requires core
 * @requires polargeometry
 * @requires constants
 */

'use strict';

var p5 = _dereq_('../core/core');
var polarGeometry = _dereq_('./polargeometry');
var constants = _dereq_('../core/constants');

p5.prototype._angleMode = constants.RADIANS;

/**
 * The inverse of cos(), returns the arc cosine of a value. This function
 * expects the values in the range of -1 to 1 and values are returned in
 * the range 0 to PI (3.1415927).
 *
 * @method acos
 * @param  {Number} value the value whose arc cosine is to be returned
 * @return {Number}       the arc cosine of the given value
 *
 * @example
 * <div class= “norender">
 * <code>
 * var a = PI;
 * var c = cos(a);
 * var ac = acos(c);
 * // Prints: "3.1415927 : -1.0 : 3.1415927"
 * print(a + " : " + c + " : " +  ac);
 * </code>
 * </div>
 *
 * <div class= “norender">
 * <code>
 * var a = PI + PI/4.0;
 * var c = cos(a);
 * var ac = acos(c);
 * // Prints: "3.926991 : -0.70710665 : 2.3561943"
 * print(a + " : " + c + " : " +  ac);
 * </code>
 * </div>
 */
p5.prototype.acos = function(ratio) {
  if (this._angleMode === constants.RADIANS) {
    return Math.acos(ratio);
  } else {
    return polarGeometry.radiansToDegrees(Math.acos(ratio));
  }
};

/**
 * The inverse of sin(), returns the arc sine of a value. This function
 * expects the values in the range of -1 to 1 and values are returned
 * in the range -PI/2 to PI/2.
 *
 * @method asin
 * @param  {Number} value the value whose arc sine is to be returned
 * @return {Number}       the arc sine of the given value
 *
 * @example
 * <div class= “norender">
 * <code>
 * var a = PI + PI/3;
 * var s = sin(a);
 * var as = asin(s);
 * // Prints: "1.0471976 : 0.86602545 : 1.0471976"
 * print(a + " : " + s + " : " +  as);
 * </code>
 * </div>
 *
 * <div class= “norender">
 * <code>
 * var a = PI + PI/3.0;
 * var s = sin(a);
 * var as = asin(s);
 * // Prints: "4.1887903 : -0.86602545 : -1.0471976"
 * print(a + " : " + s + " : " +  as);
 * </code>
 * </div>
 *
 */
p5.prototype.asin = function(ratio) {
  if (this._angleMode === constants.RADIANS) {
    return Math.asin(ratio);
  } else {
    return polarGeometry.radiansToDegrees(Math.asin(ratio));
  }
};

/**
 * The inverse of tan(), returns the arc tangent of a value. This function
 * expects the values in the range of -Infinity to Infinity (exclusive) and
 * values are returned in the range -PI/2 to PI/2.
 *
 * @method atan
 * @param  {Number} value the value whose arc tangent is to be returned
 * @return {Number}       the arc tangent of the given value
 *
 * @example
 * <div class= “norender">
 * <code>
 * var a = PI + PI/3;
 * var t = tan(a);
 * var at = atan(t);
 * // Prints: "1.0471976 : 1.7320509 : 1.0471976"
 * print(a + " : " + t + " : " +  at);
 * </code>
 * </div>
 *
 * <div class= “norender">
 * <code>
 * var a = PI + PI/3.0;
 * var t = tan(a);
 * var at = atan(t);
 * // Prints: "4.1887903 : 1.7320513 : 1.0471977"
 * print(a + " : " + t + " : " +  at);
 * </code>
 * </div>
 *
 */
p5.prototype.atan = function(ratio) {
  if (this._angleMode === constants.RADIANS) {
    return Math.atan(ratio);
  } else {
    return polarGeometry.radiansToDegrees(Math.atan(ratio));
  }
};

/**
 * Calculates the angle (in radians) from a specified point to the coordinate
 * origin as measured from the positive x-axis. Values are returned as a
 * float in the range from PI to -PI. The atan2() function is most often used
 * for orienting geometry to the position of the cursor.
 * <br><br>
 * Note: The y-coordinate of the point is the first parameter, and the
 * x-coordinate is the second parameter, due the the structure of calculating
 * the tangent.
 *
 * @method atan2
 * @param  {Number} y y-coordinate of the point
 * @param  {Number} x x-coordinate of the point
 * @return {Number}   the arc tangent of the given point
 *
 * @example
 * <div>
 * <code>
 * function draw() {
 *   background(204);
 *   translate(width/2, height/2);
 *   var a = atan2(mouseY-height/2, mouseX-width/2);
 *   rotate(a);
 *   rect(-30, -5, 60, 10);
 * }
 * </code>
 * </div>
 *
 * @alt
 * 60 by 10 rect at center of canvas rotates with mouse movements
 *
 */
p5.prototype.atan2 = function (y, x) {
  if (this._angleMode === constants.RADIANS) {
    return Math.atan2(y, x);
  } else {
    return polarGeometry.radiansToDegrees(Math.atan2(y, x));
  }
};

/**
 * Calculates the cosine of an angle. This function takes into account the
 * current angleMode. Values are returned in the range -1 to 1.
 *
 * @method cos
 * @param  {Number} angle the angle
 * @return {Number}       the cosine of the angle
 *
 * @example
 * <div>
 * <code>
 * var a = 0.0;
 * var inc = TWO_PI/25.0;
 * for (var i = 0; i < 25; i++) {
 *   line(i*4, 50, i*4, 50+cos(a)*40.0);
 *   a = a + inc;
 * }
 * </code>
 * </div>
 *
 * @alt
 * vertical black lines form wave patterns, extend-down on left and right side
 *
 */
p5.prototype.cos = function(angle) {
  if (this._angleMode === constants.RADIANS) {
    return Math.cos(angle);
  } else {
    return Math.cos(this.radians(angle));
  }
};

/**
 * Calculates the sine of an angle. This function takes into account the
 * current angleMode. Values are returned in the range -1 to 1.
 *
 * @method sin
 * @param  {Number} angle the angle
 * @return {Number}       the sine of the angle
 *
 * @example
 * <div>
 * <code>
 * var a = 0.0;
 * var inc = TWO_PI/25.0;
 * for (var i = 0; i < 25; i++) {
 *   line(i*4, 50, i*4, 50+sin(a)*40.0);
 *   a = a + inc;
 * }
 * </code>
 * </div>
 *
 * @alt
 * vertical black lines extend down and up from center to form wave pattern
 *
 */
p5.prototype.sin = function(angle) {
  if (this._angleMode === constants.RADIANS) {
    return Math.sin(angle);
  } else {
    return Math.sin(this.radians(angle));
  }
};

/**
 * Calculates the tangent of an angle. This function takes into account
 * the current angleMode. Values are returned in the range -1 to 1.
 *
 * @method tan
 * @param  {Number} angle the angle
 * @return {Number}       the tangent of the angle
 *
 * @example
 * <div>
 * <code>
 *   var a = 0.0;
 *   var inc = TWO_PI/50.0;
 *   for (var i = 0; i < 100; i = i+2) {
 *     line(i, 50, i, 50+tan(a)*2.0);
 *     a = a + inc;
 *   }
 * </code>
 *
 *
 * @alt
 * vertical black lines end down and up from center to form spike pattern
 *
 */
p5.prototype.tan = function(angle) {
  if (this._angleMode === constants.RADIANS) {
    return Math.tan(angle);
  } else {
    return Math.tan(this.radians(angle));
  }
};

/**
 * Converts a radian measurement to its corresponding value in degrees.
 * Radians and degrees are two ways of measuring the same thing. There are
 * 360 degrees in a circle and 2*PI radians in a circle. For example,
 * 90° = PI/2 = 1.5707964.
 *
 * @method degrees
 * @param  {Number} radians the radians value to convert to degrees
 * @return {Number}         the converted angle
 *
 *
 * @example
 * <div class= “norender">
 * <code>
 * var rad = PI/4;
 * var deg = degrees(rad);
 * print(rad + " radians is " + deg + " degrees");
 * // Prints: 0.7853981633974483 radians is 45 degrees
 * </code>
 * </div>
 *
 */
p5.prototype.degrees = function(angle) {
  return polarGeometry.radiansToDegrees(angle);
};

/**
 * Converts a degree measurement to its corresponding value in radians.
 * Radians and degrees are two ways of measuring the same thing. There are
 * 360 degrees in a circle and 2*PI radians in a circle. For example,
 * 90° = PI/2 = 1.5707964.
 *
 * @method radians
 * @param  {Number} degrees the degree value to convert to radians
 * @return {Number}         the converted angle
 *
 * @example
 * <div class= “norender">
 * <code>
 * var deg = 45.0;
 * var rad = radians(deg);
 * print(deg + " degrees is " + rad + " radians");
 * // Prints: 45 degrees is 0.7853981633974483 radians
 * </code>
 * </div>
 */
p5.prototype.radians = function(angle) {
  return polarGeometry.degreesToRadians(angle);
};

/**
 * Sets the current mode of p5 to given mode. Default mode is RADIANS.
 *
 * @method angleMode
 * @param {Constant} mode either RADIANS or DEGREES
 *
 * @example
 * <div>
 * <code>
 * function draw(){
 *   background(204);
 *   angleMode(DEGREES); // Change the mode to DEGREES
 *   var a = atan2(mouseY-height/2, mouseX-width/2);
 *   translate(width/2, height/2);
 *   push();
 *   rotate(a);
 *   rect(-20, -5, 40, 10); // Larger rectangle is rotating in degrees
 *   pop();
 *   angleMode(RADIANS); // Change the mode to RADIANS
 *   rotate(a); // var a stays the same
 *   rect(-40, -5, 20, 10); // Smaller rectangle is rotating in radians
 * }
 * </code>
 * </div>
 *
 * @alt
 * 40 by 10 rect in center rotates with mouse moves. 20 by 10 rect moves faster.
 *
 *
 */
p5.prototype.angleMode = function(mode) {
  if (mode === constants.DEGREES || mode === constants.RADIANS) {
    this._angleMode = mode;
  }
};

module.exports = p5;

},{"../core/constants":38,"../core/core":39,"./polargeometry":69}],72:[function(_dereq_,module,exports){
/**
 * @module Typography
 * @submodule Attributes
 * @for p5
 * @requires core
 * @requires constants
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * Sets the current alignment for drawing text. Accepts two
 * arguments: horizAlign (LEFT, CENTER, or RIGHT) and
 * vertAlign (TOP, BOTTOM, CENTER, or BASELINE).
 *
 * The horizAlign parameter is in reference to the x value
 * of the text() function, while the vertAlign parameter is
 * in reference to the y value.
 *
 * So if you write textAlign(LEFT), you are aligning the left
 * edge of your text to the x value you give in text(). If you
 * write textAlign(RIGHT, TOP), you are aligning the right edge
 * of your text to the x value and the top of edge of the text
 * to the y value.
 *
 * @method textAlign
 * @param {Constant} horizAlign horizontal alignment, either LEFT,
 *                            CENTER, or RIGHT
 * @param {Constant} vertAlign vertical alignment, either TOP,
 *                            BOTTOM, CENTER, or BASELINE
 * @return {Number}
 * @example
 * <div>
 * <code>
 * textSize(16);
 * textAlign(RIGHT);
 * text("ABCD", 50, 30);
 * textAlign(CENTER);
 * text("EFGH", 50, 50);
 * textAlign(LEFT);
 * text("IJKL", 50, 70);
 * </code>
 * </div>
 *
 * @alt
 *Letters ABCD displayed at top right, EFGH at center and IJKL at bottom left.
 *
 */
p5.prototype.textAlign = function(horizAlign, vertAlign) {
  return this._renderer.textAlign.apply(this._renderer, arguments);
};

/**
 * Sets/gets the spacing, in pixels, between lines of text. This
 * setting will be used in all subsequent calls to the text() function.
 *
 * @method textLeading
 * @param {Number} leading the size in pixels for spacing between lines
 * @return {Object|Number}
 * @example
 * <div>
 * <code>
 * // Text to display. The "\n" is a "new line" character
 * lines = "L1\nL2\nL3";
 * textSize(12);
 *
 * textLeading(10);  // Set leading to 10
 * text(lines, 10, 25);
 *
 * textLeading(20);  // Set leading to 20
 * text(lines, 40, 25);
 *
 * textLeading(30);  // Set leading to 30
 * text(lines, 70, 25);
 * </code>
 * </div>
 *
 * @alt
 *set L1 L2 & L3 displayed vertically 3 times. spacing increases for each set
 *
 */
p5.prototype.textLeading = function(theLeading) {
  return this._renderer.textLeading.apply(this._renderer, arguments);
};

/**
 * Sets/gets the current font size. This size will be used in all subsequent
 * calls to the text() function. Font size is measured in pixels.
 *
 * @method textSize
 * @param {Number} theSize the size of the letters in units of pixels
 * @return {Object|Number}
 * @example
 * <div>
 * <code>
 * textSize(12);
 * text("Font Size 12", 10, 30);
 * textSize(14);
 * text("Font Size 14", 10, 60);
 * textSize(16);
 * text("Font Size 16", 10, 90);
 * </code>
 * </div>
 *
 * @alt
 *Font Size 12 displayed small, Font Size 14 medium & Font Size 16 large
 *
 */
p5.prototype.textSize = function(theSize) {
  return this._renderer.textSize.apply(this._renderer, arguments);
};

/**
 * Sets/gets the style of the text for system fonts to NORMAL, ITALIC, or BOLD.
 * Note: this may be is overridden by CSS styling. For non-system fonts
 * (opentype, truetype, etc.) please load styled fonts instead.
 *
 * @method textStyle
 * @param {Number/Constant} theStyle styling for text, either NORMAL,
 *                            ITALIC, or BOLD
 * @return {Object|String}
 * @example
 * <div>
 * <code>
 * strokeWeight(0);
 * textSize(12);
 * textStyle(NORMAL);
 * text("Font Style Normal", 10, 30);
 * textStyle(ITALIC);
 * text("Font Style Italic", 10, 60);
 * textStyle(BOLD);
 * text("Font Style Bold", 10, 90);
 * </code>
 * </div>
 *
 * @alt
 *words Font Style Normal displayed normally, Italic in italic and bold in bold
 *
 */
p5.prototype.textStyle = function(theStyle) {
  return this._renderer.textStyle.apply(this._renderer, arguments);
};

/**
 * Calculates and returns the width of any character or text string.
 *
 * @method textWidth
 * @param {String} theText the String of characters to measure
 * @return {Number}
 * @example
 * <div>
 * <code>
 * textSize(28);
 *
 * var aChar = 'P';
 * var cWidth = textWidth(aChar);
 * text(aChar, 0, 40);
 * line(cWidth, 0, cWidth, 50);
 *
 * var aString = "p5.js";
 * var sWidth = textWidth(aString);
 * text(aString, 0, 85);
 * line(sWidth, 50, sWidth, 100);
 * </code>
 * </div>
 *
 * @alt
 *Letter P and p5.js are displayed with vertical lines at end. P is wide
 *
 */
p5.prototype.textWidth = function(theText) {
  if (theText.length === 0) {
    return 0;
  }
  return this._renderer.textWidth.apply(this._renderer, arguments);
};

/**
 * Returns the ascent of the current font at its current size. The ascent
 * represents the distance, in pixels, of the tallest character above
 * the baseline.
 *
 * @return {Number}
 * @example
 * <div>
 * <code>
 * var base = height * 0.75;
 * var scalar = 0.8; // Different for each font
 *
 * textSize(32);  // Set initial text size
 * var asc = textAscent() * scalar;  // Calc ascent
 * line(0, base - asc, width, base - asc);
 * text("dp", 0, base);  // Draw text on baseline
 *
 * textSize(64);  // Increase text size
 * asc = textAscent() * scalar;  // Recalc ascent
 * line(40, base - asc, width, base - asc);
 * text("dp", 40, base);  // Draw text on baseline
 * </code>
 * </div>
 */
p5.prototype.textAscent = function() {
  return this._renderer.textAscent();
};

/**
 * Returns the descent of the current font at its current size. The descent
 * represents the distance, in pixels, of the character with the longest
 * descender below the baseline.
 *
 * @return {Number}
 * @example
 * <div>
 * <code>
 * var base = height * 0.75;
 * var scalar = 0.8; // Different for each font
 *
 * textSize(32);  // Set initial text size
 * var desc = textDescent() * scalar;  // Calc ascent
 * line(0, base+desc, width, base+desc);
 * text("dp", 0, base);  // Draw text on baseline
 *
 * textSize(64);  // Increase text size
 * desc = textDescent() * scalar;  // Recalc ascent
 * line(40, base + desc, width, base + desc);
 * text("dp", 40, base);  // Draw text on baseline
 * </code>
 * </div>
 */
p5.prototype.textDescent = function() {
  return this._renderer.textDescent();
};

/**
 * Helper function to measure ascent and descent.
 */
p5.prototype._updateTextMetrics = function() {
  return this._renderer._updateTextMetrics();
};

module.exports = p5;

},{"../core/core":39}],73:[function(_dereq_,module,exports){
/**
 * @module Typography
 * @submodule Loading & Displaying
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');
var constants = _dereq_('../core/constants');

_dereq_('../core/error_helpers');


/**
 * Draws text to the screen. Displays the information specified in the first
 * parameter on the screen in the position specified by the additional
 * parameters. A default font will be used unless a font is set with the
 * textFont() function and a default size will be used unless a font is set
 * with textSize(). Change the color of the text with the fill() function.
 * Change the outline of the text with the stroke() and strokeWeight()
 * functions.
 * <br><br>
 * The text displays in relation to the textAlign() function, which gives the
 * option to draw to the left, right, and center of the coordinates.
 * <br><br>
 * The x2 and y2 parameters define a rectangular area to display within and
 * may only be used with string data. When these parameters are specified,
 * they are interpreted based on the current rectMode() setting. Text that
 * does not fit completely within the rectangle specified will not be drawn
 * to the screen.
 *
 * @method text
 * @param {String} str the alphanumeric symbols to be displayed
 * @param {Number} x   x-coordinate of text
 * @param {Number} y   y-coordinate of text
 * @param {Number} x2  by default, the width of the text box,
 *                     see rectMode() for more info
 * @param {Number} y2  by default, the height of the text box,
 *                     see rectMode() for more info
 * @return {Object} this
 * @example
 * <div>
 * <code>
 * textSize(32);
 * text("word", 10, 30);
 * fill(0, 102, 153);
 * text("word", 10, 60);
 * fill(0, 102, 153, 51);
 * text("word", 10, 90);
 * </code>
 * </div>
 * <div>
 * <code>
 * s = "The quick brown fox jumped over the lazy dog.";
 * fill(50);
 * text(s, 10, 10, 70, 80); // Text wraps within text box
 * </code>
 * </div>
 *
 * @alt
 *'word' displayed 3 times going from black, blue to translucent blue
 * The quick brown fox jumped over the lazy dog.
 *
 */
p5.prototype.text = function(str, x, y, maxWidth, maxHeight) {
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  this._validateParameters(
    'text',
    args,
    [
      ['*', 'Number', 'Number'],
      ['*', 'Number', 'Number', 'Number', 'Number']
    ]
  );

  return (!(this._renderer._doFill || this._renderer._doStroke)) ? this :
    this._renderer.text.apply(this._renderer, arguments);
};

/**
 * Sets the current font that will be drawn with the text() function.
 *
 * @method textFont
 * @param {Object|String} f a font loaded via loadFont(), or a String
 * representing a <a href="https://mzl.la/2dOw8WD">web safe font</a> (a font
 * that is generally available across all systems).
 * @return {Object} this
 * @example
 * <div>
 * <code>
 * fill(0);
 * textSize(12);
 * textFont("Georgia");
 * text("Georgia", 12, 30);
 * textFont("Helvetica");
 * text("Helvetica", 12, 60);
 * </code>
 * </div>
 * <div>
 * <code>
 * var fontRegular, fontItalic, fontBold;
 * function preload() {
 *    fontRegular = loadFont("assets/Regular.otf");
 *    fontItalic = loadFont("assets/Italic.ttf");
 *    fontBold = loadFont("assets/Bold.ttf");
 * }
 * function setup() {
 *    background(210);
 *    fill(0).strokeWeight(0).textSize(10);
 *    textFont(fontRegular);
 *    text("Font Style Normal", 10, 30);
 *    textFont(fontItalic);
 *    text("Font Style Italic", 10, 50);
 *    textFont(fontBold);
 *    text("Font Style Bold", 10, 70);
 * }
 * </code>
 * </div>
 *
 * @alt
 *words Font Style Normal displayed normally, Italic in italic and bold in bold
 *
 */
p5.prototype.textFont = function(theFont, theSize) {

  if (arguments.length) {

    if (!theFont) {

      throw Error('null font passed to textFont');
    }

    this._renderer._setProperty('_textFont', theFont);

    if (theSize) {

      this._renderer._setProperty('_textSize', theSize);
      this._renderer._setProperty('_textLeading',
        theSize * constants._DEFAULT_LEADMULT);
    }

    return this._renderer._applyTextProperties();
  }

  return this;
};

module.exports = p5;

},{"../core/constants":38,"../core/core":39,"../core/error_helpers":42}],74:[function(_dereq_,module,exports){
/**
 * This module defines the p5.Font class and functions for
 * drawing text to the display canvas.
 * @module Typography
 * @submodule Font
 * @requires core
 * @requires constants
 */

'use strict';

var p5 = _dereq_('../core/core');
var constants = _dereq_('../core/constants');

/*
 * TODO:
 *
 * API:
 * -- textBounds()
 * -- getPath()
 * -- getPoints()
 *
 * ===========================================
 * -- PFont functions:
 *    PFont.list()
 *
 * -- kerning
 * -- alignment: justified?
 * -- integrate p5.dom? (later)
 */

/**
 * Base class for font handling
 * @class p5.Font
 * @constructor
 * @param {Object} [pInst] pointer to p5 instance
 */
p5.Font = function(p) {

  this.parent = p;

  this.cache = {};

  /**
   * Underlying opentype font implementation
   * @property font
   */
  this.font = undefined;
};

p5.Font.prototype.list = function() {

  // TODO
  throw 'not yet implemented';
};

/**
 * Returns a tight bounding box for the given text string using this
 * font (currently only supports single lines)
 *
 * @method textBounds
 * @param  {String} line     a line of text
 * @param  {Number} x        x-position
 * @param  {Number} y        y-position
 * @param  {Number} fontSize font size to use (optional)
 * @param  {Object} options opentype options (optional)
 *
 * @return {Object}          a rectangle object with properties: x, y, w, h
 *
 * @example
 * <div>
 * <code>
 * var font;
 * var textString = 'Lorem ipsum dolor sit amet.';
 * function preload() {
 *    font = loadFont('./assets/Regular.otf');
 * };
 * function setup() {
 *    background(210);
 *
 *    var bbox = font.textBounds(textString, 10, 30, 12);
 *    fill(255);
 *    stroke(0);
 *    rect(bbox.x, bbox.y, bbox.w, bbox.h);
 *    fill(0);
 *    noStroke();
 *
 *    textFont(font);
 *    textSize(12);
 *    text(textString, 10, 30);
 * };
 * </code>
 * </div>
 *
 * @alt
 *words Lorem ipsum dol go off canvas and contained by white bounding box
 *
 */
p5.Font.prototype.textBounds = function(str, x, y, fontSize, options) {

  x = x !== undefined ? x : 0;
  y = y !== undefined ? y : 0;
  fontSize = fontSize || this.parent._renderer._textSize;

  // Check cache for existing bounds. Take into consideration the text alignment
  // settings. Default alignment should match opentype's origin: left-aligned &
  // alphabetic baseline.
  var p = (options && options.renderer && options.renderer._pInst) ||
    this.parent,
    ctx = p._renderer.drawingContext,
    alignment = ctx.textAlign || constants.LEFT,
    baseline = ctx.textBaseline || constants.BASELINE;
  var result = this.cache[cacheKey('textBounds', str, x, y, fontSize, alignment,
    baseline)];

  if (!result) {

    var xCoords = [], yCoords = [], self = this,
      scale = this._scale(fontSize), minX, minY, maxX, maxY;

    this.font.forEachGlyph(str, x, y, fontSize, options,
      function(glyph, gX, gY, gFontSize) {

        xCoords.push(gX);
        yCoords.push(gY);

        var gm = glyph.getMetrics();

        if (glyph.name !== 'space') {

          xCoords.push(gX + (gm.xMax * scale));
          yCoords.push(gY + (-gm.yMin * scale));
          yCoords.push(gY + (-gm.yMax * scale));

        } else { // NOTE: deals with broken metrics for spaces in opentype.js

          xCoords.push(gX + self.font.charToGlyph(' ').advanceWidth *
            self._scale(fontSize));
        }
      });

    // fix to #1409 (not sure why these max() functions were here)
    /*minX = Math.max(0, Math.min.apply(null, xCoords));
    minY = Math.max(0, Math.min.apply(null, yCoords));
    maxX = Math.max(0, Math.max.apply(null, xCoords));
    maxY = Math.max(0, Math.max.apply(null, yCoords));*/
    minX = Math.min.apply(null, xCoords);
    minY = Math.min.apply(null, yCoords);
    maxX = Math.max.apply(null, xCoords);
    maxY = Math.max.apply(null, yCoords);

    result = {
      x: minX,
      y: minY,
      h: maxY - minY,
      w: maxX - minX,
      advance: minX - x
    };

    // Bounds are now calculated, so shift the x & y to match alignment settings
    var textWidth = result.w + result.advance;
    var pos = this._handleAlignment(p, ctx, str, result.x, result.y, textWidth);
    result.x = pos.x;
    result.y = pos.y;

    this.cache[cacheKey('textBounds', str, x, y, fontSize, alignment,
      baseline)] = result;
  }
  //else console.log('cache-hit');

  return result;
};


/**
 * Computes an array of points following the path for specified text
 *
 * @param  {String} txt     a line of text
 * @param  {Number} x        x-position
 * @param  {Number} y        y-position
 * @param  {Number} fontSize font size to use (optional)
 * @param  {Object} options  an (optional) object that can contain:
 *
 * <br>sampleFactor - the ratio of path-length to number of samples
 * (default=.25); higher values yield more points and are therefore
 * more precise
 *
 * <br>simplifyThreshold - if set to a non-zero value, collinear points will be
 * be removed from the polygon; the value represents the threshold angle to use
 * when determining whether two edges are collinear
 *
 * @return {Array}  an array of points, each with x, y, alpha (the path angle)
 */
p5.Font.prototype.textToPoints = function(txt, x, y, fontSize, options) {

  var xoff = 0, result = [], glyphs = this._getGlyphs(txt);

  fontSize = fontSize || this.parent._renderer._textSize;

  for (var i = 0; i < glyphs.length; i++) {

    var gpath = glyphs[i].getPath(x, y, fontSize),
      paths = splitPaths(gpath.commands);

    for (var j = 0; j < paths.length; j++) {

      var pts = pathToPoints(paths[j], options);

      for (var k = 0; k < pts.length; k++) {
        pts[k].x += xoff;
        result.push(pts[k]);
      }
    }

    xoff += glyphs[i].advanceWidth * this._scale(fontSize);
  }

  return result;
};

// ----------------------------- End API ------------------------------

/**
 * Returns the set of opentype glyphs for the supplied string.
 *
 * Note that there is not a strict one-to-one mapping between characters
 * and glyphs, so the list of returned glyphs can be larger or smaller
 *  than the length of the given string.
 *
 * @param  {String} str the string to be converted
 * @return {array}     the opentype glyphs
 */
p5.Font.prototype._getGlyphs = function(str) {

  return this.font.stringToGlyphs(str);
};

/**
 * Returns an opentype path for the supplied string and position.
 *
 * @param  {String} line     a line of text
 * @param  {Number} x        x-position
 * @param  {Number} y        y-position
 * @param  {Object} options opentype options (optional)
 * @return {Object}     the opentype path
 */
p5.Font.prototype._getPath = function(line, x, y, options) {

  var p = (options && options.renderer && options.renderer._pInst) ||
    this.parent,
    ctx = p._renderer.drawingContext,
    pos = this._handleAlignment(p, ctx, line, x, y);

  return this.font.getPath(line, pos.x, pos.y, p._renderer._textSize, options);
};

/*
 * Creates an SVG-formatted path-data string
 * (See http://www.w3.org/TR/SVG/paths.html#PathData)
 * from the given opentype path or string/position
 *
 * @param  {Object} path    an opentype path, OR the following:
 *
 * @param  {String} line     a line of text
 * @param  {Number} x        x-position
 * @param  {Number} y        y-position
 * @param  {Object} options opentype options (optional), set options.decimals
 * to set the decimal precision of the path-data
 *
 * @return {Object}     this p5.Font object
 */
p5.Font.prototype._getPathData = function(line, x, y, options) {

  var decimals = 3;

  // create path from string/position
  if (typeof line === 'string' && arguments.length > 2) {

    line = this._getPath(line, x, y, options);
  }
  // handle options specified in 2nd arg
  else if (typeof x === 'object') {

    options = x;
  }

  // handle svg arguments
  if (options && typeof options.decimals === 'number') {

    decimals = options.decimals;
  }

  return line.toPathData(decimals);
};

/*
 * Creates an SVG <path> element, as a string,
 * from the given opentype path or string/position
 *
 * @param  {Object} path    an opentype path, OR the following:
 *
 * @param  {String} line     a line of text
 * @param  {Number} x        x-position
 * @param  {Number} y        y-position
 * @param  {Object} options opentype options (optional), set options.decimals
 * to set the decimal precision of the path-data in the <path> element,
 *  options.fill to set the fill color for the <path> element,
 *  options.stroke to set the stroke color for the <path> element,
 *  options.strokeWidth to set the strokeWidth for the <path> element.
 *
 * @return {Object}     this p5.Font object
 */
p5.Font.prototype._getSVG = function(line, x, y, options) {

  var decimals = 3;

  // create path from string/position
  if (typeof line === 'string' && arguments.length > 2) {

    line = this._getPath(line, x, y, options);
  }
  // handle options specified in 2nd arg
  else if (typeof x === 'object') {

    options = x;
  }

  // handle svg arguments
  if (options) {
    if (typeof options.decimals === 'number') {
      decimals = options.decimals;
    }
    if (typeof options.strokeWidth === 'number') {
      line.strokeWidth = options.strokeWidth;
    }
    if (typeof options.fill !== 'undefined') {
      line.fill = options.fill;
    }
    if (typeof options.stroke !== 'undefined') {
      line.stroke = options.stroke;
    }
  }

  return line.toSVG(decimals);
};

/*
 * Renders an opentype path or string/position
 * to the current graphics context
 *
 * @param  {Object} path    an opentype path, OR the following:
 *
 * @param  {String} line     a line of text
 * @param  {Number} x        x-position
 * @param  {Number} y        y-position
 * @param  {Object} options opentype options (optional)
 *
 * @return {Object}     this p5.Font object
 */
p5.Font.prototype._renderPath = function(line, x, y, options) {

  var pdata, pg = (options && options.renderer) || this.parent._renderer,
    ctx = pg.drawingContext;

  if (typeof line === 'object' && line.commands) {

    pdata = line.commands;
  } else {

    //pos = handleAlignment(p, ctx, line, x, y);
    pdata = this._getPath(line, x, y, options).commands;
  }

  ctx.beginPath();
  for (var i = 0; i < pdata.length; i += 1) {

    var cmd = pdata[i];
    if (cmd.type === 'M') {
      ctx.moveTo(cmd.x, cmd.y);
    } else if (cmd.type === 'L') {
      ctx.lineTo(cmd.x, cmd.y);
    } else if (cmd.type === 'C') {
      ctx.bezierCurveTo(cmd.x1, cmd.y1, cmd.x2, cmd.y2, cmd.x, cmd.y);
    } else if (cmd.type === 'Q') {
      ctx.quadraticCurveTo(cmd.x1, cmd.y1, cmd.x, cmd.y);
    } else if (cmd.type === 'Z') {
      ctx.closePath();
    }
  }

  // only draw stroke if manually set by user
  if (pg._doStroke && pg._strokeSet) {

    ctx.stroke();
  }

  if (pg._doFill) {

    // if fill hasn't been set by user, use default-text-fill
    ctx.fillStyle = pg._fillSet ? ctx.fillStyle : constants._DEFAULT_TEXT_FILL;
    ctx.fill();
  }

  return this;
};

p5.Font.prototype._textWidth = function(str, fontSize) {

  if (str === ' ') { // special case for now

    return this.font.charToGlyph(' ').advanceWidth * this._scale(fontSize);
  }

  var bounds = this.textBounds(str, 0, 0, fontSize);
  return bounds.w + bounds.advance;
};

p5.Font.prototype._textAscent = function(fontSize) {

  return this.font.ascender * this._scale(fontSize);
};

p5.Font.prototype._textDescent = function(fontSize) {

  return -this.font.descender * this._scale(fontSize);
};

p5.Font.prototype._scale = function(fontSize) {

  return (1 / this.font.unitsPerEm) * (fontSize ||
    this.parent._renderer._textSize);
};

p5.Font.prototype._handleAlignment = function(p, ctx, line, x, y, textWidth) {
  var fontSize = p._renderer._textSize,
    textAscent = this._textAscent(fontSize),
    textDescent = this._textDescent(fontSize);

  textWidth = textWidth !== undefined ? textWidth :
    this._textWidth(line, fontSize);

  if (ctx.textAlign === constants.CENTER) {
    x -= textWidth / 2;
  } else if (ctx.textAlign === constants.RIGHT) {
    x -= textWidth;
  }

  if (ctx.textBaseline === constants.TOP) {
    y += textAscent;
  } else if (ctx.textBaseline === constants._CTX_MIDDLE) {
    y += textAscent / 2;
  } else if (ctx.textBaseline === constants.BOTTOM) {
    y -= textDescent;
  }

  return { x: x, y: y };
};

// path-utils

function pathToPoints(cmds, options) {

  var opts = parseOpts(options, {
    sampleFactor: 0.1,
    simplifyThreshold: 0,
  });

  var len = pointAtLength(cmds,0,1), // total-length
    t = len / (len * opts.sampleFactor),
    pts = [];

  for (var i = 0; i < len; i += t) {
    pts.push(pointAtLength(cmds, i));
  }

  if (opts.simplifyThreshold) {
    /*var count = */simplify(pts, opts.simplifyThreshold);
    //console.log('Simplify: removed ' + count + ' pts');
  }

  return pts;
}

function simplify(pts, angle) {

  angle = (typeof angle === 'undefined') ? 0 : angle;

  var num = 0;
  for (var i = pts.length - 1; pts.length > 3 && i >= 0; --i) {

    if (collinear(at(pts, i - 1), at(pts, i), at(pts, i + 1), angle)) {

      // Remove the middle point
      pts.splice(i % pts.length, 1);
      num++;
    }
  }
  return num;
}

function splitPaths(cmds) {

  var paths = [], current;
  for (var i = 0; i < cmds.length; i++) {
    if (cmds[i].type === 'M') {
      if (current) {
        paths.push(current);
      }
      current = [];
    }
    current.push(cmdToArr(cmds[i]));
  }
  paths.push(current);

  return paths;
}

function cmdToArr(cmd) {

  var arr = [ cmd.type ];
  if (cmd.type === 'M' || cmd.type === 'L') { // moveto or lineto
    arr.push(cmd.x, cmd.y);
  } else if (cmd.type === 'C') {
    arr.push(cmd.x1, cmd.y1, cmd.x2, cmd.y2, cmd.x, cmd.y);
  } else if (cmd.type === 'Q') {
    arr.push(cmd.x1, cmd.y1, cmd.x, cmd.y);
  }
  // else if (cmd.type === 'Z') { /* no-op */ }
  return arr;
}

function parseOpts(options, defaults) {

  if (typeof options !== 'object') {
    options = defaults;
  }
  else {
    for (var key in defaults) {
      if (typeof options[key] === 'undefined') {
        options[key] = defaults[key];
      }
    }
  }
  return options;
}

//////////////////////// Helpers ////////////////////////////

function at(v, i) {
  var s = v.length;
  return v[i < 0 ? i % s + s : i % s];
}

function collinear(a, b, c, thresholdAngle) {

  if (!thresholdAngle) {
    return areaTriangle(a, b, c) === 0;
  }

  if (typeof collinear.tmpPoint1 === 'undefined') {
    collinear.tmpPoint1 = [];
    collinear.tmpPoint2 = [];
  }

  var ab = collinear.tmpPoint1, bc = collinear.tmpPoint2;
  ab.x = b.x - a.x;
  ab.y = b.y - a.y;
  bc.x = c.x - b.x;
  bc.y = c.y - b.y;

  var dot = ab.x * bc.x + ab.y * bc.y,
    magA = Math.sqrt(ab.x * ab.x + ab.y * ab.y),
    magB = Math.sqrt(bc.x * bc.x + bc.y * bc.y),
    angle = Math.acos(dot / (magA * magB));

  return angle < thresholdAngle;
}

function areaTriangle(a, b, c) {
  return (((b[0] - a[0]) * (c[1] - a[1])) - ((c[0] - a[0]) * (b[1] - a[1])));
}

// Portions of below code copyright 2008 Dmitry Baranovskiy (via MIT license)

function findDotsAtSegment(p1x, p1y, c1x, c1y, c2x, c2y, p2x, p2y, t) {

  var t1 = 1 - t, t13 = Math.pow(t1, 3), t12 = Math.pow(t1, 2), t2 = t * t,
    t3 = t2 * t, x = t13 * p1x + t12 * 3 * t * c1x + t1 * 3 * t * t * c2x +
    t3 * p2x, y = t13 * p1y + t12 * 3 * t * c1y + t1 * 3 * t * t * c2y +
    t3 * p2y, mx = p1x + 2 * t * (c1x - p1x) + t2 * (c2x - 2 * c1x + p1x),
    my = p1y + 2 * t * (c1y - p1y) + t2 * (c2y - 2 * c1y + p1y),
    nx = c1x + 2 * t * (c2x - c1x) + t2 * (p2x - 2 * c2x + c1x),
    ny = c1y + 2 * t * (c2y - c1y) + t2 * (p2y - 2 * c2y + c1y),
    ax = t1 * p1x + t * c1x, ay = t1 * p1y + t * c1y,
    cx = t1 * c2x + t * p2x, cy = t1 * c2y + t * p2y,
    alpha = (90 - Math.atan2(mx - nx, my - ny) * 180 / Math.PI);

  if (mx > nx || my < ny) { alpha += 180; }

  return { x: x, y: y, m: { x: mx, y: my }, n: { x: nx, y: ny },
    start: { x: ax, y: ay }, end: { x: cx, y: cy }, alpha: alpha
  };
}

function getPointAtSegmentLength(p1x,p1y,c1x,c1y,c2x,c2y,p2x,p2y,length) {
  return (length == null) ? bezlen(p1x, p1y, c1x, c1y, c2x, c2y, p2x, p2y) :
    findDotsAtSegment(p1x, p1y, c1x, c1y, c2x, c2y, p2x, p2y,
      getTatLen(p1x, p1y, c1x, c1y, c2x, c2y, p2x, p2y, length));
}

function pointAtLength(path, length, istotal) {
  path = path2curve(path);
  var x, y, p, l, sp = '', subpaths = {}, point, len = 0;
  for (var i = 0, ii = path.length; i < ii; i++) {
    p = path[i];
    if (p[0] === 'M') {
      x = +p[1];
      y = +p[2];
    } else {
      l = getPointAtSegmentLength(x, y, p[1], p[2], p[3], p[4], p[5], p[6]);
      if (len + l > length) {
        if (!istotal) {
          point = getPointAtSegmentLength(x, y, p[1], p[2], p[3], p[4], p[5],
            p[6], length - len);
          return { x: point.x, y: point.y, alpha: point.alpha };
        }
      }
      len += l;
      x = +p[5];
      y = +p[6];
    }
    sp += p.shift() + p;
  }
  subpaths.end = sp;

  point = istotal ? len : findDotsAtSegment
    (x, y, p[0], p[1], p[2], p[3], p[4], p[5], 1);

  if (point.alpha) {
    point = { x: point.x, y: point.y, alpha: point.alpha };
  }

  return point;
}

function pathToAbsolute(pathArray) {

  var res = [], x = 0, y = 0, mx = 0, my = 0, start = 0;
  if (pathArray[0][0] === 'M') {
    x = +pathArray[0][1];
    y = +pathArray[0][2];
    mx = x;
    my = y;
    start++;
    res[0] = ['M', x, y];
  }

  var dots,crz = pathArray.length===3 && pathArray[0][0]==='M' &&
    pathArray[1][0].toUpperCase()==='R' && pathArray[2][0].toUpperCase()==='Z';

  for (var r, pa, i = start, ii = pathArray.length; i < ii; i++) {
    res.push(r = []);
    pa = pathArray[i];
    if (pa[0] !== String.prototype.toUpperCase.call(pa[0])) {
      r[0] = String.prototype.toUpperCase.call(pa[0]);
      switch (r[0]) {
        case 'A':
          r[1] = pa[1];
          r[2] = pa[2];
          r[3] = pa[3];
          r[4] = pa[4];
          r[5] = pa[5];
          r[6] = +(pa[6] + x);
          r[7] = +(pa[7] + y);
          break;
        case 'V':
          r[1] = +pa[1] + y;
          break;
        case 'H':
          r[1] = +pa[1] + x;
          break;
        case 'R':
          dots = [x, y].concat(pa.slice(1));
          for (var j = 2, jj = dots.length; j < jj; j++) {
            dots[j] = +dots[j] + x;
            dots[++j] = +dots[j] + y;
          }
          res.pop();
          res = res.concat(catmullRom2bezier(dots, crz));
          break;
        case 'M':
          mx = +pa[1] + x;
          my = +pa[2] + y;
          break;
        default:
          for (j = 1, jj = pa.length; j < jj; j++) {
            r[j] = +pa[j] + ((j % 2) ? x : y);
          }
      }
    } else if (pa[0] === 'R') {
      dots = [x, y].concat(pa.slice(1));
      res.pop();
      res = res.concat(catmullRom2bezier(dots, crz));
      r = ['R'].concat(pa.slice(-2));
    } else {
      for (var k = 0, kk = pa.length; k < kk; k++) {
        r[k] = pa[k];
      }
    }
    switch (r[0]) {
      case 'Z':
        x = mx;
        y = my;
        break;
      case 'H':
        x = r[1];
        break;
      case 'V':
        y = r[1];
        break;
      case 'M':
        mx = r[r.length - 2];
        my = r[r.length - 1];
        break;
      default:
        x = r[r.length - 2];
        y = r[r.length - 1];
    }
  }
  return res;
}

function path2curve(path, path2) {

  var p = pathToAbsolute(path), p2 = path2 && pathToAbsolute(path2),
    attrs = { x: 0, y: 0, bx: 0, by: 0, X: 0, Y: 0, qx: null, qy: null },
    attrs2 = { x: 0, y: 0, bx: 0, by: 0, X: 0, Y: 0, qx: null, qy: null },

    processPath = function(path, d, pcom) {
      var nx, ny, tq = { T: 1, Q: 1 };
      if (!path) { return ['C', d.x, d.y, d.x, d.y, d.x, d.y]; }
      if (!(path[0] in tq)) { d.qx = d.qy = null; }
      switch (path[0]) {
        case 'M':
          d.X = path[1];
          d.Y = path[2];
          break;
        case 'A':
          path = ['C'].concat(a2c.apply(0, [d.x, d.y].concat(path.slice(1))));
          break;
        case 'S':
          if (pcom === 'C' || pcom === 'S') {
            nx = d.x * 2 - d.bx;
            ny = d.y * 2 - d.by;
          } else {
            nx = d.x;
            ny = d.y;
          }
          path = ['C', nx, ny].concat(path.slice(1));
          break;
        case 'T':
          if (pcom === 'Q' || pcom === 'T') {
            d.qx = d.x * 2 - d.qx;
            d.qy = d.y * 2 - d.qy;
          } else {
            d.qx = d.x;
            d.qy = d.y;
          }
          path = ['C'].concat(q2c(d.x, d.y, d.qx, d.qy, path[1], path[2]));
          break;
        case 'Q':
          d.qx = path[1];
          d.qy = path[2];
          path = ['C'].concat(q2c(d.x,d.y,path[1],path[2],path[3],path[4]));
          break;
        case 'L':
          path = ['C'].concat(l2c(d.x, d.y, path[1], path[2]));
          break;
        case 'H':
          path = ['C'].concat(l2c(d.x, d.y, path[1], d.y));
          break;
        case 'V':
          path = ['C'].concat(l2c(d.x, d.y, d.x, path[1]));
          break;
        case 'Z':
          path = ['C'].concat(l2c(d.x, d.y, d.X, d.Y));
          break;
      }
      return path;
    },

    fixArc = function(pp, i) {
      if (pp[i].length > 7) {
        pp[i].shift();
        var pi = pp[i];
        while (pi.length) {
          pcoms1[i] = 'A';
          if (p2) { pcoms2[i] = 'A'; }
          pp.splice(i++, 0, ['C'].concat(pi.splice(0, 6)));
        }
        pp.splice(i, 1);
        ii = Math.max(p.length, p2 && p2.length || 0);
      }
    },

    fixM = function(path1, path2, a1, a2, i) {
      if (path1 && path2 && path1[i][0] === 'M' && path2[i][0] !== 'M') {
        path2.splice(i, 0, ['M', a2.x, a2.y]);
        a1.bx = 0;
        a1.by = 0;
        a1.x = path1[i][1];
        a1.y = path1[i][2];
        ii = Math.max(p.length, p2 && p2.length || 0);
      }
    },

    pcoms1 = [], // path commands of original path p
    pcoms2 = [], // path commands of original path p2
    pfirst = '', // temporary holder for original path command
    pcom = ''; // holder for previous path command of original path

  for (var i = 0, ii = Math.max(p.length, p2 && p2.length || 0); i < ii; i++) {
    if (p[i]) { pfirst = p[i][0]; } // save current path command

    if (pfirst !== 'C') {
      pcoms1[i] = pfirst; // Save current path command
      if (i) { pcom = pcoms1[i - 1]; } // Get previous path command pcom
    }
    p[i] = processPath(p[i], attrs, pcom);

    if (pcoms1[i] !== 'A' && pfirst === 'C') { pcoms1[i] = 'C'; }

    fixArc(p, i); // fixArc adds also the right amount of A:s to pcoms1

    if (p2) { // the same procedures is done to p2
      if (p2[i]) { pfirst = p2[i][0]; }
      if (pfirst !== 'C') {
        pcoms2[i] = pfirst;
        if (i) { pcom = pcoms2[i - 1]; }
      }
      p2[i] = processPath(p2[i], attrs2, pcom);

      if (pcoms2[i] !== 'A' && pfirst === 'C') { pcoms2[i] = 'C'; }

      fixArc(p2, i);
    }
    fixM(p, p2, attrs, attrs2, i);
    fixM(p2, p, attrs2, attrs, i);
    var seg = p[i], seg2 = p2 && p2[i], seglen = seg.length,
      seg2len = p2 && seg2.length;
    attrs.x = seg[seglen - 2];
    attrs.y = seg[seglen - 1];
    attrs.bx = parseFloat(seg[seglen - 4]) || attrs.x;
    attrs.by = parseFloat(seg[seglen - 3]) || attrs.y;
    attrs2.bx = p2 && (parseFloat(seg2[seg2len - 4]) || attrs2.x);
    attrs2.by = p2 && (parseFloat(seg2[seg2len - 3]) || attrs2.y);
    attrs2.x = p2 && seg2[seg2len - 2];
    attrs2.y = p2 && seg2[seg2len - 1];
  }

  return p2 ? [p, p2] : p;
}

function a2c(x1, y1, rx, ry, angle, lac, sweep_flag, x2, y2, recursive) {
  // for more information of where this Math came from visit:
  // http://www.w3.org/TR/SVG11/implnote.html#ArcImplementationNotes
  var PI = Math.PI, _120 = PI * 120 / 180, f1, f2, cx, cy,
    rad = PI / 180 * (+angle || 0), res = [], xy,
    rotate = function (x, y, rad) {
      var X = x * Math.cos(rad) - y * Math.sin(rad),
        Y = x * Math.sin(rad) + y * Math.cos(rad);
      return { x: X, y: Y };
    };
  if (!recursive) {
    xy = rotate(x1, y1, -rad);
    x1 = xy.x;
    y1 = xy.y;
    xy = rotate(x2, y2, -rad);
    x2 = xy.x;
    y2 = xy.y;
    var x = (x1 - x2) / 2, y = (y1 - y2) / 2,
      h = (x * x) / (rx * rx) + (y * y) / (ry * ry);
    if (h > 1) {
      h = Math.sqrt(h);
      rx = h * rx;
      ry = h * ry;
    }
    var rx2 = rx * rx, ry2 = ry * ry,
      k = (lac === sweep_flag ? -1 : 1) * Math.sqrt(Math.abs
        ((rx2 * ry2 - rx2 * y * y - ry2 * x * x)/(rx2 * y * y + ry2 * x * x)));

    cx = k * rx * y / ry + (x1 + x2) / 2;
    cy = k * -ry * x / rx + (y1 + y2) / 2;
    f1 = Math.asin(((y1 - cy) / ry).toFixed(9));
    f2 = Math.asin(((y2 - cy) / ry).toFixed(9));

    f1 = x1 < cx ? PI - f1 : f1;
    f2 = x2 < cx ? PI - f2 : f2;

    if (f1 < 0) { f1 = PI * 2 + f1; }
    if (f2 < 0) { f2 = PI * 2 + f2; }

    if (sweep_flag && f1 > f2) {
      f1 = f1 - PI * 2;
    }
    if (!sweep_flag && f2 > f1) {
      f2 = f2 - PI * 2;
    }
  } else {
    f1 = recursive[0];
    f2 = recursive[1];
    cx = recursive[2];
    cy = recursive[3];
  }
  var df = f2 - f1;
  if (Math.abs(df) > _120) {
    var f2old = f2, x2old = x2, y2old = y2;
    f2 = f1 + _120 * (sweep_flag && f2 > f1 ? 1 : -1);
    x2 = cx + rx * Math.cos(f2);
    y2 = cy + ry * Math.sin(f2);
    res = a2c(x2, y2, rx, ry, angle, 0, sweep_flag, x2old, y2old,
      [f2, f2old, cx, cy]);
  }
  df = f2 - f1;
  var c1 = Math.cos(f1),
    s1 = Math.sin(f1),
    c2 = Math.cos(f2),
    s2 = Math.sin(f2),
    t = Math.tan(df / 4),
    hx = 4 / 3 * rx * t,
    hy = 4 / 3 * ry * t,
    m1 = [x1, y1],
    m2 = [x1 + hx * s1, y1 - hy * c1],
    m3 = [x2 + hx * s2, y2 - hy * c2],
    m4 = [x2, y2];
  m2[0] = 2 * m1[0] - m2[0];
  m2[1] = 2 * m1[1] - m2[1];
  if (recursive) {
    return [m2, m3, m4].concat(res);
  } else {
    res = [m2, m3, m4].concat(res).join().split(',');
    var newres = [];
    for (var i = 0, ii = res.length; i < ii; i++) {
      newres[i] = i % 2 ? rotate(res[i - 1], res[i], rad).y : rotate(res[i],
        res[i + 1], rad).x;
    }
    return newres;
  }
}

// http://schepers.cc/getting-to-the-point
function catmullRom2bezier(crp, z) {
  var d = [];
  for (var i = 0, iLen = crp.length; iLen - 2 * !z > i; i += 2) {
    var p = [{
      x: +crp[i - 2],
      y: +crp[i - 1]
    }, {
      x: +crp[i],
      y: +crp[i + 1]
    }, {
      x: +crp[i + 2],
      y: +crp[i + 3]
    }, {
      x: +crp[i + 4],
      y: +crp[i + 5]
    }];
    if (z) {
      if (!i) {
        p[0] = {
          x: +crp[iLen - 2],
          y: +crp[iLen - 1]
        };
      } else if (iLen - 4 === i) {
        p[3] = {
          x: +crp[0],
          y: +crp[1]
        };
      } else if (iLen - 2 === i) {
        p[2] = {
          x: +crp[0],
          y: +crp[1]
        };
        p[3] = {
          x: +crp[2],
          y: +crp[3]
        };
      }
    } else {
      if (iLen - 4 === i) {
        p[3] = p[2];
      } else if (!i) {
        p[0] = {
          x: +crp[i],
          y: +crp[i + 1]
        };
      }
    }
    d.push(['C', (-p[0].x + 6 * p[1].x + p[2].x) / 6, (-p[0].y + 6 * p[1].y +
      p[2].y) / 6, (p[1].x + 6 * p[2].x - p[3].x) / 6, (p[1].y + 6 * p[2].y -
      p[3].y) / 6, p[2].x, p[2].y ]);
  }

  return d;
}

function l2c(x1, y1, x2, y2) { return [x1, y1, x2, y2, x2, y2]; }

function q2c(x1, y1, ax, ay, x2, y2) {
  var _13 = 1 / 3, _23 = 2 / 3;
  return [
    _13 * x1 + _23 * ax, _13 * y1 + _23 * ay,
    _13 * x2 + _23 * ax, _13 * y2 + _23 * ay, x2, y2
  ];
}

function bezlen(x1, y1, x2, y2, x3, y3, x4, y4, z) {
  if (z == null) { z = 1; }
  z = z > 1 ? 1 : z < 0 ? 0 : z;
  var z2 = z / 2,
    n = 12, Tvalues = [-0.1252, 0.1252, -0.3678, 0.3678, -0.5873, 0.5873,
       -0.7699, 0.7699, -0.9041, 0.9041, -0.9816, 0.9816],
    sum = 0, Cvalues = [0.2491, 0.2491, 0.2335, 0.2335, 0.2032, 0.2032,
      0.1601, 0.1601, 0.1069, 0.1069, 0.0472, 0.0472 ];
  for (var i = 0; i < n; i++) {
    var ct = z2 * Tvalues[i] + z2,
      xbase = base3(ct, x1, x2, x3, x4),
      ybase = base3(ct, y1, y2, y3, y4),
      comb = xbase * xbase + ybase * ybase;
    sum += Cvalues[i] * Math.sqrt(comb);
  }
  return z2 * sum;
}

function getTatLen(x1, y1, x2, y2, x3, y3, x4, y4, ll) {
  if (ll < 0 || bezlen(x1, y1, x2, y2, x3, y3, x4, y4) < ll) {
    return;
  }
  var t = 1, step = t / 2, t2 = t - step, l, e = 0.01;
  l = bezlen(x1, y1, x2, y2, x3, y3, x4, y4, t2);
  while (Math.abs(l - ll) > e) {
    step /= 2;
    t2 += (l < ll ? 1 : -1) * step;
    l = bezlen(x1, y1, x2, y2, x3, y3, x4, y4, t2);
  }
  return t2;
}

function base3(t, p1, p2, p3, p4) {
  var t1 = -3 * p1 + 9 * p2 - 9 * p3 + 3 * p4,
    t2 = t * t1 + 6 * p1 - 12 * p2 + 6 * p3;
  return t * t2 - 3 * p1 + 3 * p2;
}

function cacheKey() {
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  i = args.length;
  var hash = '';
  while (i--) {
    hash += (args[i] === Object(args[i])) ?
      JSON.stringify(args[i]) : args[i];
  }
  return hash;
}

module.exports = p5.Font;

},{"../core/constants":38,"../core/core":39}],75:[function(_dereq_,module,exports){
/**
 * @module Data
 * @submodule Array Functions
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * Adds a value to the end of an array. Extends the length of
 * the array by one. Maps to Array.push().
 *
 * @method append
 * @param {Array} array Array to append
 * @param {any} value to be added to the Array
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *
 * var myArray = new Array("Mango", "Apple", "Papaya")
 * print(myArray) // ["Mango", "Apple", "Papaya"]
 *
 * append(myArray, "Peach")
 * print(myArray) // ["Mango", "Apple", "Papaya", "Peach"]
 *
 * }
 * </div></code>
 */
p5.prototype.append = function(array, value) {
  array.push(value);
  return array;
};

/**
 * Copies an array (or part of an array) to another array. The src array is
 * copied to the dst array, beginning at the position specified by
 * srcPosition and into the position specified by dstPosition. The number of
 * elements to copy is determined by length. Note that copying values
 * overwrites existing values in the destination array. To append values
 * instead of overwriting them, use concat().
 * <br><br>
 * The simplified version with only two arguments, arrayCopy(src, dst),
 * copies an entire array to another of the same size. It is equivalent to
 * arrayCopy(src, 0, dst, 0, src.length).
 * <br><br>
 * Using this function is far more efficient for copying array data than
 * iterating through a for() loop and copying each element individually.
 *
 * @method arrayCopy
 * @param {Array}  src           the source Array
 * @param {Number} [srcPosition] starting position in the source Array
 * @param {Array}  dst           the destination Array
 * @param {Number} [dstPosition] starting position in the destination Array
 * @param {Number} [length]      number of Array elements to be copied
 *
 * @example
 *  <div class="norender"><code>
 *  function setup() {
 *
 *    var src = new Array("A", "B", "C");
 *    var dst = new Array( 1 ,  2 ,  3 );
 *    var srcPosition = 1;
 *    var dstPosition = 0;
 *    var length = 2;
 *
 *    print(src); // ["A", "B", "C"]
 *    print(dst); // [ 1 ,  2 ,  3 ]
 *
 *    arrayCopy(src, srcPosition, dst, dstPosition, length);
 *    print(dst); // ["B", "C", 3]
 *
 *    }
 *  </div></code>
 */
p5.prototype.arrayCopy = function(
  src,
  srcPosition,
  dst,
  dstPosition,
  length) {

  // the index to begin splicing from dst array
  var start,
      end;

  if (typeof length !== 'undefined') {

    end = Math.min(length, src.length);
    start = dstPosition;
    src = src.slice(srcPosition, end + srcPosition);

  } else {

    if (typeof dst !== 'undefined') { // src, dst, length
      // rename  so we don't get confused
      end = dst;
      end = Math.min(end, src.length);
    } else { // src, dst
      end = src.length;
    }

    start = 0;
    // rename  so we don't get confused
    dst = srcPosition;
    src = src.slice(0, end);
  }

  // Since we are not returning the array and JavaScript is pass by reference
  // we must modify the actual values of the array
  // instead of reassigning arrays
  Array.prototype.splice.apply(dst, [start, end].concat(src));

};

/**
 * Concatenates two arrays, maps to Array.concat(). Does not modify the
 * input arrays.
 *
 * @method concat
 * @param {Array} a first Array to concatenate
 * @param {Array} b second Array to concatenate
 * @return {Array} concatenated array
 *
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var arr1 = new Array("A", "B", "C");
 *   var arr2 = new Array( 1 ,  2 ,  3 );
 *
 *   print(arr1); // ["A","B","C"]
 *   print(arr2); // [1,2,3]
 *
 *   var arr3 = concat(arr1, arr2);
 *
 *   print(arr1); // ["A","B","C"]
 *   print(arr2); // [1,2,3]
 *   print(arr3); // ["A","B","C",1,2,3]
 *
 * }
 * </div></code>
 */
p5.prototype.concat = function(list0, list1) {
  return list0.concat(list1);
};

/**
 * Reverses the order of an array, maps to Array.reverse()
 *
 * @method reverse
 * @param {Array} list Array to reverse
 * @example
 * <div class="norender"><code>
 * function setup() {
 *   var myArray = new Array("A", "B", "C");
 *   print(myArray); // ["A","B","C"]
 *
 *   reverse(myArray);
 *   print(myArray); // ["C","B","A"]
 * }
 * </div></code>
 */
p5.prototype.reverse = function(list) {
  return list.reverse();
};

/**
 * Decreases an array by one element and returns the shortened array,
 * maps to Array.pop().
 *
 * @method shorten
 * @param  {Array} list Array to shorten
 * @return {Array} shortened Array
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var myArray = new Array("A", "B", "C");
 *   print(myArray); // ["A","B","C"]
 *
 *   var newArray = shorten(myArray);
 *   print(myArray); // ["A","B","C"]
 *   print(newArray); // ["A","B"]
 * }
 * </div></code>
 */
p5.prototype.shorten = function(list) {
  list.pop();
  return list;
};

/**
 * Randomizes the order of the elements of an array. Implements
 * <a href="http://Bost.Ocks.org/mike/shuffle/" target=_blank>
 * Fisher-Yates Shuffle Algorithm</a>.
 *
 * @method shuffle
 * @param  {Array}   array  Array to shuffle
 * @param  {Boolean} [bool] modify passed array
 * @return {Array}   shuffled Array
 * @example
 * <div><code>
 * function setup() {
 *   var regularArr = ['ABC', 'def', createVector(), TAU, Math.E];
 *   print(regularArr);
 *   shuffle(regularArr, true); // force modifications to passed array
 *   print(regularArr);
 *
 *   // By default shuffle() returns a shuffled cloned array:
 *   var newArr = shuffle(regularArr);
 *   print(regularArr);
 *   print(newArr);
 * }
 * </code></div>
 */
p5.prototype.shuffle = function(arr, bool) {
  var isView = ArrayBuffer && ArrayBuffer.isView && ArrayBuffer.isView(arr);
  arr = bool || isView ? arr : arr.slice();

  var rnd, tmp, idx = arr.length;
  while (idx > 1) {
    rnd = Math.random()*idx | 0;

    tmp = arr[--idx];
    arr[idx] = arr[rnd];
    arr[rnd] = tmp;
  }

  return arr;
};

/**
 * Sorts an array of numbers from smallest to largest, or puts an array of
 * words in alphabetical order. The original array is not modified; a
 * re-ordered array is returned. The count parameter states the number of
 * elements to sort. For example, if there are 12 elements in an array and
 * count is set to 5, only the first 5 elements in the array will be sorted.
 *
 * @method sort
 * @param {Array} list Array to sort
 * @param {Number} [count] number of elements to sort, starting from 0
 *
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var words = new Array("banana", "apple", "pear","lime");
 *   print(words); // ["banana", "apple", "pear", "lime"]
 *   var count = 4; // length of array
 *
 *   words = sort(words, count);
 *   print(words); // ["apple", "banana", "lime", "pear"]
 * }
 * </div></code>
 * <div class = "norender"><code>
 * function setup() {
 *   var numbers = new Array(2,6,1,5,14,9,8,12);
 *   print(numbers); // [2,6,1,5,14,9,8,12]
 *   var count = 5; // Less than the length of the array
 *
 *   numbers = sort(numbers, count);
 *   print(numbers); // [1,2,5,6,14,9,8,12]
 * }
 * </div></code>
 */
p5.prototype.sort = function(list, count) {
  var arr = count ? list.slice(0, Math.min(count, list.length)) : list;
  var rest = count ? list.slice(Math.min(count, list.length)) : [];
  if (typeof arr[0] === 'string') {
    arr = arr.sort();
  } else {
    arr = arr.sort(function(a,b){return a-b;});
  }
  return arr.concat(rest);
};

/**
 * Inserts a value or an array of values into an existing array. The first
 * parameter specifies the initial array to be modified, and the second
 * parameter defines the data to be inserted. The third parameter is an index
 * value which specifies the array position from which to insert data.
 * (Remember that array index numbering starts at zero, so the first position
 * is 0, the second position is 1, and so on.)
 *
 * @method splice
 * @param {Array}  list Array to splice into
 * @param {any}    value value to be spliced in
 * @param {Number} position in the array from which to insert data
 *
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var myArray = new Array(0,1,2,3,4);
 *   var insArray = new Array("A","B","C");
 *   print(myArray); // [0,1,2,3,4]
 *   print(insArray); // ["A","B","C"]
 *
 *   splice(myArray, insArray, 3);
 *   print(myArray); // [0,1,2,"A","B","C",3,4]
 * }
 * </div></code>
 */
p5.prototype.splice = function(list, value, index) {

  // note that splice returns spliced elements and not an array
  Array.prototype.splice.apply(list, [index, 0].concat(value));

  return list;
};

/**
 * Extracts an array of elements from an existing array. The list parameter
 * defines the array from which the elements will be copied, and the start
 * and count parameters specify which elements to extract. If no count is
 * given, elements will be extracted from the start to the end of the array.
 * When specifying the start, remember that the first array element is 0.
 * This function does not change the source array.
 *
 * @method subset
 * @param  {Array}  list    Array to extract from
 * @param  {Number} start   position to begin
 * @param  {Number} [count] number of values to extract
 * @return {Array}          Array of extracted elements
 *
 * @example
 * <div class = "norender"><code>
 * function setup() {
 *   var myArray = new Array(1,2,3,4,5);
 *   print(myArray); // [1,2,3,4,5]
 *
 *   var sub1 = subset(myArray, 0, 3);
 *   var sub2 = subset(myArray, 2, 2);
 *   print(sub1); // [1,2,3]
 *   print(sub2); // [3,4]
 * }
 * </div></code>
 */
p5.prototype.subset = function(list, start, count) {
  if (typeof count !== 'undefined') {
    return list.slice(start, start + count);
  } else {
    return list.slice(start, list.length);
  }
};

module.exports = p5;

},{"../core/core":39}],76:[function(_dereq_,module,exports){
/**
 * @module Data
 * @submodule Conversion
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * Converts a string to its floating point representation. The contents of a
 * string must resemble a number, or NaN (not a number) will be returned.
 * For example, float("1234.56") evaluates to 1234.56, but float("giraffe")
 * will return NaN.
 *
 * @method float
 * @param {String}  str float string to parse
 * @return {Number}     floating point representation of string
 * @example
 * <div><code>
 * var str = '20';
 * var diameter = float(str);
 * ellipse(width/2, height/2, diameter, diameter);
 * </code></div>
 *
 * @alt
 * 20 by 20 white ellipse in the center of the canvas
 *
 */
p5.prototype.float = function(str) {
  return parseFloat(str);
};

/**
 * Converts a boolean, string, or float to its integer representation.
 * When an array of values is passed in, then an int array of the same length
 * is returned.
 *
 * @method int
 * @param {String|Boolean|Number|Array} n value to parse
 * @return {Number}                     integer representation of value
 * @example
 * <div class='norender'><code>
 * print(int("10")); // 10
 * print(int(10.31)); // 10
 * print(int(-10)); // -10
 * print(int(true)); // 1
 * print(int(false)); // 0
 * print(int([false, true, "10.3", 9.8])); // [0, 1, 10, 9]
 * </code></div>
 */
p5.prototype.int = function(n, radix) {
  if (typeof n === 'string') {
    radix = radix || 10;
    return parseInt(n, radix);
  } else if (typeof n === 'number') {
    return n | 0;
  } else if (typeof n === 'boolean') {
    return n ? 1 : 0;
  } else if (n instanceof Array) {
    return n.map(function(n) { return p5.prototype.int(n, radix); });
  }
};

/**
 * Converts a boolean, string or number to its string representation.
 * When an array of values is passed in, then an array of strings of the same
 * length is returned.
 *
 * @method str
 * @param {String|Boolean|Number|Array} n value to parse
 * @return {String}                     string representation of value
 * @example
 * <div class='norender'><code>
 * print(str("10"));  // "10"
 * print(str(10.31)); // "10.31"
 * print(str(-10));   // "-10"
 * print(str(true));  // "true"
 * print(str(false)); // "false"
 * print(str([true, "10.3", 9.8])); // [ "true", "10.3", "9.8" ]
 * </code></div>
 */
p5.prototype.str = function(n) {
  if (n instanceof Array) {
    return n.map(p5.prototype.str);
  } else {
    return String(n);
  }
};

/**
 * Converts a number or string to its boolean representation.
 * For a number, any non-zero value (positive or negative) evaluates to true,
 * while zero evaluates to false. For a string, the value "true" evaluates to
 * true, while any other value evaluates to false. When an array of number or
 * string values is passed in, then a array of booleans of the same length is
 * returned.
 *
 * @method boolean
 * @param {String|Boolean|Number|Array} n value to parse
 * @return {Boolean}                    boolean representation of value
 * @example
 * <div class='norender'><code>
 * print(boolean(0));               // false
 * print(boolean(1));               // true
 * print(boolean("true"));          // true
 * print(boolean("abcd"));          // false
 * print(boolean([0, 12, "true"])); // [false, true, false]
 * </code></div>
 */
p5.prototype.boolean = function(n) {
  if (typeof n === 'number') {
    return n !== 0;
  } else if (typeof n === 'string') {
    return n.toLowerCase() === 'true';
  } else if (typeof n === 'boolean') {
    return n;
  } else if (n instanceof Array) {
    return n.map(p5.prototype.boolean);
  }
};

/**
 * Converts a number, string or boolean to its byte representation.
 * A byte can be only a whole number between -128 and 127, so when a value
 * outside of this range is converted, it wraps around to the corresponding
 * byte representation. When an array of number, string or boolean values is
 * passed in, then an array of bytes the same length is returned.
 *
 * @method byte
 * @param {String|Boolean|Number|Array} n value to parse
 * @return {Number}                     byte representation of value
 * @example
 * <div class='norender'><code>
 * print(byte(127));               // 127
 * print(byte(128));               // -128
 * print(byte(23.4));              // 23
 * print(byte("23.4"));            // 23
 * print(byte(true));              // 1
 * print(byte([0, 255, "100"]));   // [0, -1, 100]
 * </code></div>
 */
p5.prototype.byte = function(n) {
  var nn = p5.prototype.int(n, 10);
  if (typeof nn === 'number') {
    return ((nn + 128) % 256) - 128;
  } else if (nn instanceof Array) {
    return nn.map(p5.prototype.byte);
  }
};

/**
 * Converts a number or string to its corresponding single-character
 * string representation. If a string parameter is provided, it is first
 * parsed as an integer and then translated into a single-character string.
 * When an array of number or string values is passed in, then an array of
 * single-character strings of the same length is returned.
 *
 * @method char
 * @param {String|Number|Array} n value to parse
 * @return {String}             string representation of value
 * @example
 * <div class='norender'><code>
 * print(char(65));                     // "A"
 * print(char("65"));                   // "A"
 * print(char([65, 66, 67]));           // [ "A", "B", "C" ]
 * print(join(char([65, 66, 67]), '')); // "ABC"
 * </code></div>
 */
p5.prototype.char = function(n) {
  if (typeof n === 'number' && !isNaN(n)) {
    return String.fromCharCode(n);
  } else if (n instanceof Array) {
    return n.map(p5.prototype.char);
  } else if (typeof n === 'string') {
    return p5.prototype.char(parseInt(n, 10));
  }
};

/**
 * Converts a single-character string to its corresponding integer
 * representation. When an array of single-character string values is passed
 * in, then an array of integers of the same length is returned.
 *
 * @method unchar
 * @param {String|Array} n value to parse
 * @return {Number}      integer representation of value
 * @example
 * <div class='norender'><code>
 * print(unchar("A"));               // 65
 * print(unchar(["A", "B", "C"]));   // [ 65, 66, 67 ]
 * print(unchar(split("ABC", "")));  // [ 65, 66, 67 ]
 * </code></div>
 */
p5.prototype.unchar = function(n) {
  if (typeof n === 'string' && n.length === 1) {
    return n.charCodeAt(0);
  } else if (n instanceof Array) {
    return n.map(p5.prototype.unchar);
  }
};

/**
 * Converts a number to a string in its equivalent hexadecimal notation. If a
 * second parameter is passed, it is used to set the number of characters to
 * generate in the hexadecimal notation. When an array is passed in, an
 * array of strings in hexadecimal notation of the same length is returned.
 *
 * @method hex
 * @param {Number|Array} n value to parse
 * @return {String}      hexadecimal string representation of value
 * @example
 * <div class='norender'><code>
 * print(hex(255));               // "000000FF"
 * print(hex(255, 6));            // "0000FF"
 * print(hex([0, 127, 255], 6));  // [ "000000", "00007F", "0000FF" ]
 * </code></div>
 */
p5.prototype.hex = function(n, digits) {
  digits = (digits === undefined || digits === null) ? digits = 8 : digits;
  if (n instanceof Array) {
    return n.map(function(n) { return p5.prototype.hex(n, digits); });
  } else if (typeof n === 'number') {
    if (n < 0) {
      n = 0xFFFFFFFF + n + 1;
    }
    var hex = Number(n).toString(16).toUpperCase();
    while (hex.length < digits) {
      hex = '0' + hex;
    }
    if (hex.length >= digits) {
      hex = hex.substring(hex.length - digits, hex.length);
    }
    return hex;
  }
};

/**
 * Converts a string representation of a hexadecimal number to its equivalent
 * integer value. When an array of strings in hexadecimal notation is passed
 * in, an array of integers of the same length is returned.
 *
 * @method unhex
 * @param {String|Array} n value to parse
 * @return {Number}      integer representation of hexadecimal value
 * @example
 * <div class='norender'><code>
 * print(unhex("A"));                // 10
 * print(unhex("FF"));               // 255
 * print(unhex(["FF", "AA", "00"])); // [ 255, 170, 0 ]
 * </code></div>
 */
p5.prototype.unhex = function(n) {
  if (n instanceof Array) {
    return n.map(p5.prototype.unhex);
  } else {
    return parseInt('0x' + n, 16);
  }
};

module.exports = p5;

},{"../core/core":39}],77:[function(_dereq_,module,exports){
/**
 * @module Data
 * @submodule String Functions
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

//return p5; //LM is this a mistake?

/**
 * Combines an array of Strings into one String, each separated by the
 * character(s) used for the separator parameter. To join arrays of ints or
 * floats, it's necessary to first convert them to Strings using nf() or
 * nfs().
 *
 * @method join
 * @param  {Array}  list      array of Strings to be joined
 * @param  {String} separator String to be placed between each item
 * @return {String}           joined String
 * @example
 * <div>
 * <code>
 * var array = ["Hello", "world!"]
 * var separator = " "
 * var message = join(array, separator);
 * text(message, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * "hello world!" displayed middle left of canvas.
 *
 */
p5.prototype.join = function(list, separator) {
  return list.join(separator);
};

/**
 * This function is used to apply a regular expression to a piece of text,
 * and return matching groups (elements found inside parentheses) as a
 * String array. If there are no matches, a null value will be returned.
 * If no groups are specified in the regular expression, but the sequence
 * matches, an array of length 1 (with the matched text as the first element
 * of the array) will be returned.
 * <br><br>
 * To use the function, first check to see if the result is null. If the
 * result is null, then the sequence did not match at all. If the sequence
 * did match, an array is returned.
 * <br><br>
 * If there are groups (specified by sets of parentheses) in the regular
 * expression, then the contents of each will be returned in the array.
 * Element [0] of a regular expression match returns the entire matching
 * string, and the match groups start at element [1] (the first group is [1],
 * the second [2], and so on).
 *
 * @method match
 * @param  {String} str    the String to be searched
 * @param  {String} regexp the regexp to be used for matching
 * @return {Array}         Array of Strings found
 * @example
 * <div>
 * <code>
 * var string = "Hello p5js*!"
 * var regexp = "p5js\\*"
 * var match = match(string, regexp);
 * text(match, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * "p5js*" displayed middle left of canvas.
 *
 */
p5.prototype.match =  function(str, reg) {
  return str.match(reg);
};

/**
 * This function is used to apply a regular expression to a piece of text,
 * and return a list of matching groups (elements found inside parentheses)
 * as a two-dimensional String array. If there are no matches, a null value
 * will be returned. If no groups are specified in the regular expression,
 * but the sequence matches, a two dimensional array is still returned, but
 * the second dimension is only of length one.
 * <br><br>
 * To use the function, first check to see if the result is null. If the
 * result is null, then the sequence did not match at all. If the sequence
 * did match, a 2D array is returned.
 * <br><br>
 * If there are groups (specified by sets of parentheses) in the regular
 * expression, then the contents of each will be returned in the array.
 * Assuming a loop with counter variable i, element [i][0] of a regular
 * expression match returns the entire matching string, and the match groups
 * start at element [i][1] (the first group is [i][1], the second [i][2],
 * and so on).
 *
 * @method matchAll
 * @param  {String} str    the String to be searched
 * @param  {String} regexp the regexp to be used for matching
 * @return {Array}         2d Array of Strings found
 * @example
 * <div class="norender">
 * <code>
 * var string = "Hello p5js*! Hello world!"
 * var regexp = "Hello"
 * matchAll(string, regexp);
 * </code>
 * </div>

 */
p5.prototype.matchAll = function(str, reg) {
  var re = new RegExp(reg, 'g');
  var match = re.exec(str);
  var matches = [];
  while (match !== null) {
    matches.push(match);
    // matched text: match[0]
    // match start: match.index
    // capturing group n: match[n]
    match = re.exec(str);
  }
  return matches;
};

/**
 * Utility function for formatting numbers into strings. There are two
 * versions: one for formatting floats, and one for formatting ints.
 * The values for the digits, left, and right parameters should always
 * be positive integers.
 *
 * @method nf
 * @param {Number|Array} num      the Number to format
 * @param {Number}       [left]   number of digits to the left of the
 *                                decimal point
 * @param {Number}       [right]  number of digits to the right of the
 *                                decimal point
 * @return {String|Array}         formatted String
 * @example
 * <div>
 * <code>
 * function setup() {
 *   background(200);
 *   var num = 112.53106115;
 *
 *   noStroke();
 *   fill(0);
 *   textSize(14);
 *   // Draw formatted numbers
 *   text(nf(num, 5, 2), 10, 20);
 *
 *   text(nf(num, 4, 3), 10, 55);
 *
 *   text(nf(num, 3, 6), 10, 85);
 *
 *   // Draw dividing lines
 *   stroke(120);
 *   line(0, 30, width, 30);
 *   line(0, 65, width, 65);
 * }
 * </code>
 * </div>
 *
 * @alt
 * "0011253" top left, "0112.531" mid left, "112.531061" bottom left canvas
 *
 */
p5.prototype.nf = function () {
  if (arguments[0] instanceof Array) {
    var a = arguments[1];
    var b = arguments[2];
    return arguments[0].map(function (x) {
      return doNf(x, a, b);
    });
  }
  else{
    var typeOfFirst = Object.prototype.toString.call(arguments[0]);
    if(typeOfFirst === '[object Arguments]'){
      if(arguments[0].length===3){
        return this.nf(arguments[0][0],arguments[0][1],arguments[0][2]);
      }
      else if(arguments[0].length===2){
        return this.nf(arguments[0][0],arguments[0][1]);
      }
      else{
        return this.nf(arguments[0][0]);
      }
    }
    else {
      return doNf.apply(this, arguments);
    }
  }
};

function doNf() {
  var num = arguments[0];
  var neg = num < 0;
  var n = neg ? num.toString().substring(1) : num.toString();
  var decimalInd = n.indexOf('.');
  var intPart = decimalInd !== -1 ? n.substring(0, decimalInd) : n;
  var decPart = decimalInd !== -1 ? n.substring(decimalInd + 1) : '';
  var str = neg ? '-' : '';
  if (arguments.length === 3) {
    var decimal = '';
    if(decimalInd !== -1 || arguments[2] - decPart.length > 0){
      decimal = '.';
    }
    if (decPart.length > arguments[2]) {
      decPart = decPart.substring(0, arguments[2]);
    }
    for (var i = 0; i < arguments[1] - intPart.length; i++) {
      str += '0';
    }
    str += intPart;
    str += decimal;
    str += decPart;
    for (var j = 0; j < arguments[2] - decPart.length; j++) {
      str += '0';
    }
    return str;
  }
  else {
    for (var k = 0; k < Math.max(arguments[1] - intPart.length, 0); k++) {
      str += '0';
    }
    str += n;
    return str;
  }
}

/**
 * Utility function for formatting numbers into strings and placing
 * appropriate commas to mark units of 1000. There are two versions: one
 * for formatting ints, and one for formatting an array of ints. The value
 * for the right parameter should always be a positive integer.
 *
 * @method nfc
 * @param  {Number|Array}   num     the Number to format
 * @param  {Number}         [right] number of digits to the right of the
 *                                  decimal point
 * @return {String|Array}           formatted String
 * @example
 * <div>
 * <code>
 * function setup() {
 *   background(200);
 *   var num = 11253106.115;
 *   var numArr = new Array(1,1,2);
 *
 *   noStroke();
 *   fill(0);
 *   textSize(12);
 *
 *   // Draw formatted numbers
 *   text(nfc(num, 4, 2), 10, 30);
 *   text(nfc(numArr, 2, 1), 10, 80);
 *
 *   // Draw dividing line
 *   stroke(120);
 *   line(0, 50, width, 50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * "11,253,106.115" top middle and "1.00,1.00,2.00" displayed bottom mid
 *
 */
p5.prototype.nfc = function () {
  if (arguments[0] instanceof Array) {
    var a = arguments[1];
    return arguments[0].map(function (x) {
      return doNfc(x, a);
    });
  } else {
    return doNfc.apply(this, arguments);
  }
};
function doNfc() {
  var num = arguments[0].toString();
  var dec = num.indexOf('.');
  var rem = dec !== -1 ? num.substring(dec) : '';
  var n = dec !== -1 ? num.substring(0, dec) : num;
  n = n.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
  if (arguments[1] === 0) {
    rem = '';
  }
  else if(arguments[1] !== undefined){
    if(arguments[1] > rem.length){
      rem+= dec === -1 ? '.' : '';
      var len = arguments[1] - rem.length + 1;
      for(var i =0; i< len; i++){
        rem += '0';
      }
    }
    else{
      rem = rem.substring(0, arguments[1] + 1);
    }
  }
  return n + rem;
}

/**
 * Utility function for formatting numbers into strings. Similar to nf() but
 * puts a "+" in front of positive numbers and a "-" in front of negative
 * numbers. There are two versions: one for formatting floats, and one for
 * formatting ints. The values for left, and right parameters
 * should always be positive integers.
 *
 * @method nfp
 * @param {Number|Array} num      the Number to format
 * @param {Number}       [left]   number of digits to the left of the decimal
 *                                point
 * @param {Number}       [right]  number of digits to the right of the
 *                                decimal point
 * @return {String|Array}         formatted String
 * @example
 * <div>
 * <code>
 * function setup() {
 *   background(200);
 *   var num1 = 11253106.115;
 *   var num2 = -11253106.115;
 *
 *   noStroke();
 *   fill(0);
 *   textSize(12);
 *
 *   // Draw formatted numbers
 *   text(nfp(num1, 4, 2), 10, 30);
 *   text(nfp(num2, 4, 2), 10, 80);
 *
 *   // Draw dividing line
 *   stroke(120);
 *   line(0, 50, width, 50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * "+11253106.11" top middle and "-11253106.11" displayed bottom middle
 *
 */
p5.prototype.nfp = function() {
  var nfRes = this.nf.apply(this, arguments);
  if (nfRes instanceof Array) {
    return nfRes.map(addNfp);
  } else {
    return addNfp(nfRes);
  }
};

function addNfp() {
  return (
    parseFloat(arguments[0]) > 0) ?
    '+'+arguments[0].toString() :
    arguments[0].toString();
}

/**
 * Utility function for formatting numbers into strings. Similar to nf() but
 * puts a " " (space) in front of positive numbers and a "-" in front of
 * negative numbers. There are two versions: one for formatting floats, and
 * one for formatting ints. The values for the digits, left, and right
 * parameters should always be positive integers.
 *
 * @method nfs
 * @param {Number|Array} num      the Number to format
 * @param {Number}       [left]   number of digits to the left of the decimal
 *                                point
 * @param {Number}       [right]  number of digits to the right of the
 *                                decimal point
 * @return {String|Array}         formatted String
 * @example
 * <div>
 * <code>
 * function setup() {
 *   background(200);
 *   var num1 = 11253106.115;
 *   var num2 = -11253106.115;
 *
 *   noStroke();
 *   fill(0);
 *   textSize(12);
 *   // Draw formatted numbers
 *   text(nfs(num1, 4, 2), 10, 30);
 *
 *   text(nfs(num2, 4, 2), 10, 80);
 *
 *   // Draw dividing line
 *   stroke(120);
 *   line(0, 50, width, 50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * "11253106.11" top middle and "-11253106.11" displayed bottom middle
 *
 */
p5.prototype.nfs = function() {
  var nfRes = this.nf.apply(this, arguments);
  if (nfRes instanceof Array) {
    return nfRes.map(addNfs);
  } else {
    return addNfs(nfRes);
  }
};

function addNfs() {
  return (
    parseFloat(arguments[0]) > 0) ?
    ' '+arguments[0].toString() :
    arguments[0].toString();
}

/**
 * The split() function maps to String.split(), it breaks a String into
 * pieces using a character or string as the delimiter. The delim parameter
 * specifies the character or characters that mark the boundaries between
 * each piece. A String[] array is returned that contains each of the pieces.
 *
 * The splitTokens() function works in a similar fashion, except that it
 * splits using a range of characters instead of a specific character or
 * sequence.
 *
 * @method split
 * @param  {String} value the String to be split
 * @param  {String} delim the String used to separate the data
 * @return {Array}  Array of Strings
 * @example
 * <div>
 * <code>
 * var names = "Pat,Xio,Alex"
 * var splitString = split(names, ",");
 * text(splitString[0], 5, 30);
 * text(splitString[1], 5, 50);
 * text(splitString[2], 5, 70);
 * </code>
 * </div>
 *
 * @alt
 * "pat" top left, "Xio" mid left and "Alex" displayed bottom left
 *
 */
p5.prototype.split = function(str, delim) {
  return str.split(delim);
};

/**
 * The splitTokens() function splits a String at one or many character
 * delimiters or "tokens." The delim parameter specifies the character or
 * characters to be used as a boundary.
 * <br><br>
 * If no delim characters are specified, any whitespace character is used to
 * split. Whitespace characters include tab (\t), line feed (\n), carriage
 * return (\r), form feed (\f), and space.
 *
 * @method splitTokens
 * @param  {String} value   the String to be split
 * @param  {String} [delim] list of individual Strings that will be used as
 *                          separators
 * @return {Array}          Array of Strings
 * @example
 * <div class = "norender">
 * <code>
 * function setup() {
 *   var myStr = "Mango, Banana, Lime";
 *   var myStrArr = splitTokens(myStr, ",");
 *
 *   print(myStrArr); // prints : ["Mango"," Banana"," Lime"]
 * }
 * </code>
 * </div>
 */
p5.prototype.splitTokens = function() {
  var d,sqo,sqc,str;
  str = arguments[1];
  if (arguments.length > 1) {
    sqc = /\]/g.exec(str);
    sqo = /\[/g.exec(str);
    if ( sqo && sqc ) {
      str = str.slice(0, sqc.index) + str.slice(sqc.index+1);
      sqo = /\[/g.exec(str);
      str = str.slice(0, sqo.index) + str.slice(sqo.index+1);
      d = new RegExp('[\\['+str+'\\]]','g');
    } else if ( sqc ) {
      str = str.slice(0, sqc.index) + str.slice(sqc.index+1);
      d = new RegExp('[' + str + '\\]]', 'g');
    } else if(sqo) {
      str = str.slice(0, sqo.index) + str.slice(sqo.index+1);
      d = new RegExp('[' + str + '\\[]', 'g');
    } else {
      d = new RegExp('[' + str + ']', 'g');
    }
  } else {
    d = /\s/g;
  }
  return arguments[0].split(d).filter(function(n){return n;});
};

/**
 * Removes whitespace characters from the beginning and end of a String. In
 * addition to standard whitespace characters such as space, carriage return,
 * and tab, this function also removes the Unicode "nbsp" character.
 *
 * @method trim
 * @param  {String|Array} str a String or Array of Strings to be trimmed
 * @return {String|Array}       a trimmed String or Array of Strings
 * @example
 * <div>
 * <code>
 * var string = trim("  No new lines\n   ");
 * text(string +" here", 2, 50);
 * </code>
 * </div>
 *
 * @alt
 * "No new lines here" displayed center canvas
 *
 */
p5.prototype.trim = function(str) {
  if (str instanceof Array) {
    return str.map(this.trim);
  } else {
    return str.trim();
  }
};

module.exports = p5;

},{"../core/core":39}],78:[function(_dereq_,module,exports){
/**
 * @module IO
 * @submodule Time & Date
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * p5.js communicates with the clock on your computer. The day() function
 * returns the current day as a value from 1 - 31.
 *
 * @method day
 * @return {Number} the current day
 * @example
 * <div>
 * <code>
 * var d = day();
 * text("Current day: \n" + d, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * Current day is displayed
 *
 */
p5.prototype.day = function() {
  return new Date().getDate();
};

/**
 * p5.js communicates with the clock on your computer. The hour() function
 * returns the current hour as a value from 0 - 23.
 *
 * @method hour
 * @return {Number} the current hour
 * @example
 * <div>
 * <code>
 * var h = hour();
 * text("Current hour:\n" + h, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * Current hour is displayed
 *
 */
p5.prototype.hour = function() {
  return new Date().getHours();
};

/**
 * p5.js communicates with the clock on your computer. The minute() function
 * returns the current minute as a value from 0 - 59.
 *
 * @method minute
 * @return {Number} the current minute
 * @example
 * <div>
 * <code>
 * var m = minute();
 * text("Current minute: \n" + m, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * Current minute is displayed
 *
 */
p5.prototype.minute = function() {
  return new Date().getMinutes();
};

/**
 * Returns the number of milliseconds (thousandths of a second) since
 * starting the program. This information is often used for timing events and
 * animation sequences.
 *
 * @method millis
 * @return {Number} the number of milliseconds since starting the program
 * @example
 * <div>
 * <code>
 * var millisecond = millis();
 * text("Milliseconds \nrunning: \n" + millisecond, 5, 40);
 * </code>
 * </div>
 *
 * @alt
 * number of milliseconds since program has started displayed
 *
 */
p5.prototype.millis = function() {
  return window.performance.now();
};

/**
 * p5.js communicates with the clock on your computer. The month() function
 * returns the current month as a value from 1 - 12.
 *
 * @method month
 * @return {Number} the current month
 * @example
 * <div>
 * <code>
 * var m = month();
 * text("Current month: \n" + m, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * Current month is displayed
 *
 */
p5.prototype.month = function() {
  return new Date().getMonth() + 1; //January is 0!
};

/**
 * p5.js communicates with the clock on your computer. The second() function
 * returns the current second as a value from 0 - 59.
 *
 * @method second
 * @return {Number} the current second
 * @example
 * <div>
 * <code>
 * var s = second();
 * text("Current second: \n" + s, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * Current second is displayed
 *
 */
p5.prototype.second = function() {
  return new Date().getSeconds();
};

/**
 * p5.js communicates with the clock on your computer. The year() function
 * returns the current year as an integer (2014, 2015, 2016, etc).
 *
 * @method year
 * @return {Number} the current year
 * @example
 * <div>
 * <code>
 * var y = year();
 * text("Current year: \n" + y, 5, 50);
 * </code>
 * </div>
 *
 * @alt
 * Current year is displayed
 *
 */
p5.prototype.year = function() {
  return new Date().getFullYear();
};

module.exports = p5;

},{"../core/core":39}],79:[function(_dereq_,module,exports){
/**
 * @module Lights, Camera
 * @submodule Camera
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * Sets camera position
 * @method camera
 * @param  {Number} x  camera position value on x axis
 * @param  {Number} y  camera position value on y axis
 * @param  {Number} z  camera position value on z axis
 * @return {p5}        the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 * function draw(){
 *  //move the camera away from the plane by a sin wave
 *  camera(0, 0, sin(frameCount * 0.01) * 100);
 *  plane(120, 120);
 * }
 * </code>
 * </div>
 *
 * @alt
 * blue square shrinks in size grows to fill canvas. disappears then loops.
 *
 */
p5.prototype.camera = function(x, y, z){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  this._validateParameters(
    'camera',
    args,
    ['Number', 'Number', 'Number']
  );
  //what it manipulates is the model view matrix
  this._renderer.translate(-x, -y, -z);
};

/**
 * Sets perspective camera
 * @method  perspective
 * @param  {Number} fovy   camera frustum vertical field of view,
 *                         from bottom to top of view, in degrees
 * @param  {Number} aspect camera frustum aspect ratio
 * @param  {Number} near   frustum near plane length
 * @param  {Number} far    frustum far plane length
 * @return {p5}            the p5 object
 * @example
 * <div>
 * <code>
 * //drag mouse to toggle the world!
 * //you will see there's a vanish point
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 *   perspective(60 / 180 * PI, width/height, 0.1, 100);
 * }
 * function draw(){
 *  background(200);
 *  orbitControl();
 *  for(var i = -1; i < 2; i++){
 *     for(var j = -2; j < 3; j++){
 *       push();
 *       translate(i*160, 0, j*160);
 *       box(40, 40, 40);
 *       pop();
 *     }
 *   }
 * }
 * </code>
 * </div>
 *
 * @alt
 * colored 3d boxes toggleable with mouse position
 *
 */
p5.prototype.perspective = function(fovy,aspect,near,far) {
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  this._validateParameters(
    'perspective',
    args,
    ['Number', 'Number', 'Number', 'Number']
  );
  this._renderer.uPMatrix = p5.Matrix.identity();
  this._renderer.uPMatrix.perspective(fovy,aspect,near,far);
  this._renderer._curCamera = 'custom';
};

/**
 * Setup ortho camera
 * @method  ortho
 * @param  {Number} left   camera frustum left plane
 * @param  {Number} right  camera frustum right plane
 * @param  {Number} bottom camera frustum bottom plane
 * @param  {Number} top    camera frustum top plane
 * @param  {Number} near   camera frustum near plane
 * @param  {Number} far    camera frustum far plane
 * @return {p5}            the p5 object
 * @example
 * <div>
 * <code>
 * //drag mouse to toggle the world!
 * //there's no vanish point
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 *   ortho(-width/2, width/2, height/2, -height/2, 0.1, 100);
 * }
 * function draw(){
 *  background(200);
 *  orbitControl();
 *  for(var i = -1; i < 2; i++){
 *     for(var j = -2; j < 3; j++){
 *       push();
 *       translate(i*160, 0, j*160);
 *       box(40, 40, 40);
 *       pop();
 *     }
 *   }
 * }
 * </code>
 * </div>
 *
 * @alt
 * 3 3d boxes, reveal several more boxes on 3d plane when mouse used to toggle
 *
 */
p5.prototype.ortho = function(left,right,bottom,top,near,far) {
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  this._validateParameters(
    'ortho',
    args,
      ['Number', 'Number', 'Number', 'Number', 'Number', 'Number']
  );
  left /= this.width;
  right /= this.width;
  top /= this.height;
  bottom /= this.height;
  this._renderer.uPMatrix = p5.Matrix.identity();
  this._renderer.uPMatrix.ortho(left,right,bottom,top,near,far);
  this._renderer._curCamera = 'custom';
};

module.exports = p5;

},{"../core/core":39}],80:[function(_dereq_,module,exports){
'use strict';

var p5 = _dereq_('../core/core');

//@TODO: implement full orbit controls including
//pan, zoom, quaternion rotation, etc.
p5.prototype.orbitControl = function(){
  if(this.mouseIsPressed){
    this.rotateY((this.mouseX - this.width / 2) / (this.width / 2));
    this.rotateX((this.mouseY - this.height / 2) / (this.width / 2));
  }
  return this;
};

module.exports = p5;
},{"../core/core":39}],81:[function(_dereq_,module,exports){
/**
 * @module Lights, Camera
 * @submodule Lights
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');

/**
 * Creates an ambient light with a color
 * @method  ambientLight
 * @param  {Number|Array|String|p5.Color} v1  gray value,
 * red or hue value (depending on the current color mode),
 * or color Array, or CSS color string
 * @param  {Number}            [v2] optional: green or saturation value
 * @param  {Number}            [v3] optional: blue or brightness value
 * @param  {Number}            [a]  optional: opacity
 * @return {p5}                the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 * function draw(){
 *   background(0);
 *   ambientLight(150);
 *   ambientMaterial(250);
 *   sphere(50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * nothing displayed
 *
 */
p5.prototype.ambientLight = function(v1, v2, v3, a){
  var gl = this._renderer.GL;
  var shaderProgram = this._renderer._getShader(
    'lightVert', 'lightTextureFrag');

  gl.useProgram(shaderProgram);
  shaderProgram.uAmbientColor = gl.getUniformLocation(
    shaderProgram,
    'uAmbientColor[' + this._renderer.ambientLightCount + ']');

  var color = this._renderer._pInst.color.apply(
    this._renderer._pInst, arguments);
  var colors = color._array;

  gl.uniform3f( shaderProgram.uAmbientColor,
    colors[0], colors[1], colors[2]);

  //in case there's no material color for the geometry
  shaderProgram.uMaterialColor = gl.getUniformLocation(
    shaderProgram, 'uMaterialColor' );
  gl.uniform4f( shaderProgram.uMaterialColor, 1, 1, 1, 1);

  this._renderer.ambientLightCount ++;
  shaderProgram.uAmbientLightCount =
    gl.getUniformLocation(shaderProgram, 'uAmbientLightCount');
  gl.uniform1i(shaderProgram.uAmbientLightCount,
    this._renderer.ambientLightCount);

  return this;
};

/**
 * Creates a directional light with a color and a direction
 * @method  directionalLight
 * @param  {Number|Array|String|p5.Color} v1   gray value,
 * red or hue value (depending on the current color mode),
 * or color Array, or CSS color string
 * @param  {Number}          [v2] optional: green or saturation value
 * @param  {Number}          [v3] optional: blue or brightness value
 * @param  {Number}          [a]  optional: opacity
 * @param  {Number|p5.Vector} x   x axis direction or a p5.Vector
 * @param  {Number}          [y]  optional: y axis direction
 * @param  {Number}          [z]  optional: z axis direction
 * @return {p5}              the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 * function draw(){
 *   background(0);
 *   //move your mouse to change light direction
 *   var dirX = (mouseX / width - 0.5) *2;
 *   var dirY = (mouseY / height - 0.5) *(-2);
 *   directionalLight(250, 250, 250, dirX, dirY, 0.25);
 *   ambientMaterial(250);
 *   sphere(50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * light source on canvas changeable with mouse position
 *
 */
p5.prototype.directionalLight = function(v1, v2, v3, a, x, y, z) {
  // TODO(jgessner): Find an example using this and profile it.
  // var args = new Array(arguments.length);
  // for (var i = 0; i < args.length; ++i) {
  //   args[i] = arguments[i];
  // }
  // this._validateParameters(
  //   'directionalLight',
  //   args,
  //   [
  //     //rgbaxyz
  //     ['Number', 'Number', 'Number', 'Number', 'Number', 'Number', 'Number'],
  //     //rgbxyz
  //     ['Number', 'Number', 'Number', 'Number', 'Number', 'Number'],
  //     //caxyz
  //     ['Number', 'Number', 'Number', 'Number', 'Number'],
  //     //cxyz
  //     ['Number', 'Number', 'Number', 'Number'],
  //     ['String', 'Number', 'Number', 'Number'],
  //     ['Array', 'Number', 'Number', 'Number'],
  //     ['Object', 'Number', 'Number', 'Number'],
  //     //rgbavector
  //     ['Number', 'Number', 'Number', 'Number', 'Object'],
  //     //rgbvector
  //     ['Number', 'Number', 'Number', 'Object'],
  //     //cavector
  //     ['Number', 'Number', 'Object'],
  //     //cvector
  //     ['Number', 'Object'],
  //     ['String', 'Object'],
  //     ['Array', 'Object'],
  //     ['Object', 'Object']
  //   ]
  // );

  var gl = this._renderer.GL;
  var shaderProgram = this._renderer._getShader(
    'lightVert', 'lightTextureFrag');

  gl.useProgram(shaderProgram);
  shaderProgram.uDirectionalColor = gl.getUniformLocation(
    shaderProgram,
    'uDirectionalColor[' + this._renderer.directionalLightCount + ']');

  //@TODO: check parameters number
  var color = this._renderer._pInst.color.apply(
    this._renderer._pInst, [v1, v2, v3]);
  var colors = color._array;

  gl.uniform3f( shaderProgram.uDirectionalColor,
    colors[0], colors[1], colors[2]);

  var _x, _y, _z;

  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  if(typeof args[args.length-1] === 'number'){
    _x = args[args.length-3];
    _y = args[args.length-2];
    _z = args[args.length-1];

  }else{
    try{
      _x = args[args.length-1].x;
      _y = args[args.length-1].y;
      _z = args[args.length-1].z;
    }
    catch(error){
      throw error;
    }
  }

  shaderProgram.uLightingDirection = gl.getUniformLocation(
    shaderProgram,
    'uLightingDirection[' + this._renderer.directionalLightCount + ']');
  gl.uniform3f( shaderProgram.uLightingDirection, _x, _y, _z);

  //in case there's no material color for the geometry
  shaderProgram.uMaterialColor = gl.getUniformLocation(
    shaderProgram, 'uMaterialColor' );
  gl.uniform4f( shaderProgram.uMaterialColor, 1, 1, 1, 1);

  this._renderer.directionalLightCount ++;
  shaderProgram.uDirectionalLightCount =
    gl.getUniformLocation(shaderProgram, 'uDirectionalLightCount');
  gl.uniform1i(shaderProgram.uDirectionalLightCount,
    this._renderer.directionalLightCount);

  return this;
};

/**
 * Creates a point light with a color and a light position
 * @method  pointLight
 * @param  {Number|Array|String|p5.Color} v1   gray value,
 * red or hue value (depending on the current color mode),
 * or color Array, or CSS color string
 * @param  {Number}          [v2] optional: green or saturation value
 * @param  {Number}          [v3] optional: blue or brightness value
 * @param  {Number}          [a]  optional: opacity
 * @param  {Number|p5.Vector} x   x axis position or a p5.Vector
 * @param  {Number}          [y]  optional: y axis position
 * @param  {Number}          [z]  optional: z axis position
 * @return {p5}              the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 * function draw(){
 *   background(0);
 *   //move your mouse to change light position
 *   var locY = (mouseY / height - 0.5) *(-2);
 *   var locX = (mouseX / width - 0.5) *2;
 *   //to set the light position,
 *   //think of the world's coordinate as:
 *   // -1,1 -------- 1,1
 *   //   |            |
 *   //   |            |
 *   //   |            |
 *   // -1,-1---------1,-1
 *   pointLight(250, 250, 250, locX, locY, 0);
 *   ambientMaterial(250);
 *   sphere(50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * spot light on canvas changes position with mouse
 *
 */
p5.prototype.pointLight = function(v1, v2, v3, a, x, y, z) {
  // TODO(jgessner): Find an example using this and profile it.
  // var args = new Array(arguments.length);
  // for (var i = 0; i < args.length; ++i) {
  //   args[i] = arguments[i];
  // }
  // this._validateParameters(
  //   'pointLight',
  //   arguments,
  //   [
  //     //rgbaxyz
  //     ['Number', 'Number', 'Number', 'Number', 'Number', 'Number', 'Number'],
  //     //rgbxyz
  //     ['Number', 'Number', 'Number', 'Number', 'Number', 'Number'],
  //     //caxyz
  //     ['Number', 'Number', 'Number', 'Number', 'Number'],
  //     //cxyz
  //     ['Number', 'Number', 'Number', 'Number'],
  //     ['String', 'Number', 'Number', 'Number'],
  //     ['Array', 'Number', 'Number', 'Number'],
  //     ['Object', 'Number', 'Number', 'Number'],
  //     //rgbavector
  //     ['Number', 'Number', 'Number', 'Number', 'Object'],
  //     //rgbvector
  //     ['Number', 'Number', 'Number', 'Object'],
  //     //cavector
  //     ['Number', 'Number', 'Object'],
  //     //cvector
  //     ['Number', 'Object'],
  //     ['String', 'Object'],
  //     ['Array', 'Object'],
  //     ['Object', 'Object']
  //   ]
  // );

  var gl = this._renderer.GL;
  var shaderProgram = this._renderer._getShader(
    'lightVert', 'lightTextureFrag');

  gl.useProgram(shaderProgram);
  shaderProgram.uPointLightColor = gl.getUniformLocation(
    shaderProgram,
    'uPointLightColor[' + this._renderer.pointLightCount + ']');

  //@TODO: check parameters number
  var color = this._renderer._pInst.color.apply(
    this._renderer._pInst, [v1, v2, v3]);
  var colors = color._array;

  gl.uniform3f( shaderProgram.uPointLightColor,
    colors[0], colors[1], colors[2]);

  var _x, _y, _z;

  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  if(typeof args[args.length-1] === 'number'){
    _x = args[args.length-3];
    _y = args[args.length-2];
    _z = args[args.length-1];

  }else{
    try{
      _x = args[args.length-1].x;
      _y = args[args.length-1].y;
      _z = args[args.length-1].z;
    }
    catch(error){
      throw error;
    }
  }

  shaderProgram.uPointLightLocation = gl.getUniformLocation(
    shaderProgram,
    'uPointLightLocation[' + this._renderer.pointLightCount + ']');
  gl.uniform3f( shaderProgram.uPointLightLocation, _x, _y, _z);

  //in case there's no material color for the geometry
  shaderProgram.uMaterialColor = gl.getUniformLocation(
    shaderProgram, 'uMaterialColor' );
  gl.uniform4f( shaderProgram.uMaterialColor, 1, 1, 1, 1);

  this._renderer.pointLightCount ++;
  shaderProgram.uPointLightCount =
    gl.getUniformLocation(shaderProgram, 'uPointLightCount');
  gl.uniform1i(shaderProgram.uPointLightCount,
    this._renderer.pointLightCount);

  return this;
};

module.exports = p5;

},{"../core/core":39}],82:[function(_dereq_,module,exports){
/**
 * @module Shape
 * @submodule 3D Models
 * @for p5
 * @requires core
 * @requires p5.Geometry3D
 */

'use strict';

var p5 = _dereq_('../core/core');
_dereq_('./p5.Geometry');

/**
 * Load a 3d model from an OBJ file.
 * <br><br>
 * One of the limitations of the OBJ format is that it doesn't have a built-in
 * sense of scale. This means that models exported from different programs might
 * be very different sizes. If your model isn't displaying, try calling
 * loadModel() with the normalized parameter set to true. This will resize the
 * model to a scale appropriate for p5. You can also make additional changes to
 * the final size of your model with the scale() function.
 *
 * @method loadModel
 * @param  {String} path Path of the model to be loaded
 * @param  {Boolean} [normalize] If true, scale the model to a
 *                                standardized size when loading
 * @param  {Function(p5.Geometry3D)} [successCallback] Function to be called
 *                                   once the model is loaded. Will be passed
 *                                   the 3D model object.
 * @param  {Function(Event)}    [failureCallback] called with event error if
 *                                the image fails to load.
 * @return {p5.Geometry} the p5.Geometry3D object
 * @example
 * <div>
 * <code>
 * //draw a spinning teapot
 * var teapot;
 *
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 *
 *   teapot = loadModel('assets/teapot.obj');
 * }
 *
 * function draw(){
 *   background(200);
 *   rotateX(frameCount * 0.01);
 *   rotateY(frameCount * 0.01);
 *   model(teapot);
 * }
 * </code>
 * </div>
 *
 * @alt
 * Vertically rotating 3-d teapot with red, green and blue gradient.
 *
 */
p5.prototype.loadModel = function () {
  var path = arguments[0];
  var normalize;
  var successCallback;
  var failureCallback;
  if(typeof arguments[1] === 'boolean') {
    normalize = arguments[1];
    successCallback = arguments[2];
    failureCallback = arguments[3];
  } else {
    normalize = false;
    successCallback = arguments[1];
    failureCallback = arguments[2];
  }

  var model = new p5.Geometry();
  model.gid = path + '|' + normalize;
  this.loadStrings(path, function(strings) {
    parseObj(model, strings);

    if (normalize) {
      model.normalize();
    }

    if (typeof successCallback === 'function') {
      successCallback(model);
    }
  }.bind(this), failureCallback);

  return model;
};

/**
 * Parse OBJ lines into model. For reference, this is what a simple model of a
 * square might look like:
 *
 * v -0.5 -0.5 0.5
 * v -0.5 -0.5 -0.5
 * v -0.5 0.5 -0.5
 * v -0.5 0.5 0.5
 *
 * f 4 3 2 1
 */
function parseObj( model, lines ) {
  // OBJ allows a face to specify an index for a vertex (in the above example),
  // but it also allows you to specify a custom combination of vertex, UV
  // coordinate, and vertex normal. So, "3/4/3" would mean, "use vertex 3 with
  // UV coordinate 4 and vertex normal 3". In WebGL, every vertex with different
  // parameters must be a different vertex, so loadedVerts is used to
  // temporarily store the parsed vertices, normals, etc., and indexedVerts is
  // used to map a specific combination (keyed on, for example, the string
  // "3/4/3"), to the actual index of the newly created vertex in the final
  // object.
  var loadedVerts = {'v' : [],
                    'vt' : [],
                    'vn' : []};
  var indexedVerts = {};

  for (var line = 0; line < lines.length; ++line) {
    // Each line is a separate object (vertex, face, vertex normal, etc)
    // For each line, split it into tokens on whitespace. The first token
    // describes the type.
    var tokens = lines[line].trim().split(/\b\s+/);

    if (tokens.length > 0) {
      if (tokens[0] === 'v' || tokens[0] === 'vn') {
        // Check if this line describes a vertex or vertex normal.
        // It will have three numeric parameters.
        var vertex = new p5.Vector(parseFloat(tokens[1]),
                                   parseFloat(tokens[2]),
                                   parseFloat(tokens[3]));
        loadedVerts[tokens[0]].push(vertex);
      } else if (tokens[0] === 'vt') {
        // Check if this line describes a texture coordinate.
        // It will have two numeric parameters.
        var texVertex = [parseFloat(tokens[1]), parseFloat(tokens[2])];
        loadedVerts[tokens[0]].push(texVertex);
      } else if (tokens[0] === 'f') {
        // Check if this line describes a face.
        // OBJ faces can have more than three points. Triangulate points.
        for (var tri = 3; tri < tokens.length; ++tri) {
          var face = [];

          var vertexTokens = [1, tri - 1, tri];

          for (var tokenInd = 0; tokenInd < vertexTokens.length; ++tokenInd) {
            // Now, convert the given token into an index
            var vertString = tokens[vertexTokens[tokenInd]];
            var vertIndex = 0;

            // TODO: Faces can technically use negative numbers to refer to the
            // previous nth vertex. I haven't seen this used in practice, but
            // it might be good to implement this in the future.

            if (indexedVerts[vertString] !== undefined) {
              vertIndex = indexedVerts[vertString];
            } else {
              var vertParts = vertString.split('/');
              for (var i = 0; i < vertParts.length; i++) {
                vertParts[i] = parseInt(vertParts[i]) - 1;
              }

              vertIndex = indexedVerts[vertString] = model.vertices.length;
              model.vertices.push(loadedVerts.v[vertParts[0]].copy());
              if (loadedVerts.vt[vertParts[1]]) {
                model.uvs.push(loadedVerts.vt[vertParts[1]].slice());
              } else {
                model.uvs.push([0, 0]);
              }

              if (loadedVerts.vn[vertParts[2]]) {
                model.vertexNormals.push(loadedVerts.vn[vertParts[2]].copy());
              }
            }

            face.push(vertIndex);
          }

          model.faces.push(face);
        }
      }
    }
  }

  // If the model doesn't have normals, compute the normals
  if(model.vertexNormals.length === 0) {
    model.computeNormals();
  }

  return model;
}

/**
 * Render a 3d model to the screen.
 *
 * @method model
 * @param  {p5.Geometry} model Loaded 3d model to be rendered
 * @example
 * <div>
 * <code>
 * //draw a spinning teapot
 * var teapot;
 *
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 *
 *   teapot = loadModel('assets/teapot.obj');
 * }
 *
 * function draw(){
 *   background(200);
 *   rotateX(frameCount * 0.01);
 *   rotateY(frameCount * 0.01);
 *   model(teapot);
 * }
 * </code>
 * </div>
 *
 * @alt
 * Vertically rotating 3-d teapot with red, green and blue gradient.
 *
 */
p5.prototype.model = function ( model ) {
  if (model.vertices.length > 0) {
    if (!this._renderer.geometryInHash(model.gid)) {
      this._renderer.createBuffers(model.gid, model);
    }

    this._renderer.drawBuffers(model.gid);
  }
};

module.exports = p5;

},{"../core/core":39,"./p5.Geometry":84}],83:[function(_dereq_,module,exports){
/**
 * @module Lights, Camera
 * @submodule Material
 * @for p5
 * @requires core
 */

'use strict';

var p5 = _dereq_('../core/core');
//require('./p5.Texture');

/**
 * Normal material for geometry. You can view all
 * possible materials in this
 * <a href="https://p5js.org/examples/examples/3D_Materials.php">example</a>.
 * @method normalMaterial
 * @return {p5}                the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *  background(200);
 *  normalMaterial();
 *  sphere(50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * Red, green and blue gradient.
 *
 */
p5.prototype.normalMaterial = function(){
  this._renderer._getShader('normalVert', 'normalFrag');
  return this;
};

/**
 * Texture for geometry.  You can view other possible materials in this
 * <a href="https://p5js.org/examples/examples/3D_Materials.php">example</a>.
 * @method texture
 * @param {p5.Image | p5.MediaElement | p5.Graphics} tex 2-dimensional graphics
 *                    to render as texture
 * @return {p5}                the p5 object
 * @example
 * <div>
 * <code>
 * var img;
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 *   img = loadImage("assets/laDefense.jpg");
 * }
 *
 * function draw(){
 *   background(0);
 *   rotateZ(frameCount * 0.01);
 *   rotateX(frameCount * 0.01);
 *   rotateY(frameCount * 0.01);
 *   //pass image as texture
 *   texture(img);
 *   box(200, 200, 200);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var pg;
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 *   pg = createGraphics(200, 200);
 *   pg.textSize(100);
 * }
 *
 * function draw(){
 *   background(0);
 *   pg.background(255);
 *   pg.text('hello!', 0, 100);
 *   //pass image as texture
 *   texture(pg);
 *   plane(200);
 * }
 * </code>
 * </div>
 *
 * <div>
 * <code>
 * var vid;
 * function preload(){
 *   vid = createVideo("assets/fingers.mov");
 *   vid.hide();
 *   vid.loop();
 * }
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(0);
 *   //pass video frame as texture
 *   texture(vid);
 *   plane(200);
 * }
 * </code>
 * </div>
 *
 * @alt
 * Rotating view of many images umbrella and grid roof on a 3d plane
 * black canvas
 * black canvas
 *
 */
p5.prototype.texture = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  var gl = this._renderer.GL;
  var shaderProgram = this._renderer._getShader('lightVert',
    'lightTextureFrag');
  gl.useProgram(shaderProgram);
  var textureData;
  //if argument is not already a texture
  //create a new one
  if(!args[0].isTexture){
    if (args[0] instanceof p5.Image) {
      textureData = args[0].canvas;
    }
    //if param is a video
    else if (typeof p5.MediaElement !== 'undefined' &&
            args[0] instanceof p5.MediaElement){
      if(!args[0].loadedmetadata) {return;}
      textureData = args[0].elt;
    }
    //used with offscreen 2d graphics renderer
    else if(args[0] instanceof p5.Graphics){
      textureData = args[0].elt;
    }
    var tex = gl.createTexture();
    args[0]._setProperty('tex', tex);
    args[0]._setProperty('isTexture', true);
    this._renderer._bind.call(this, tex, textureData);
  }
  else {
    if(args[0] instanceof p5.Graphics ||
      (typeof p5.MediaElement !== 'undefined' &&
      args[0] instanceof p5.MediaElement)){
      textureData = args[0].elt;
    }
    else if(args[0] instanceof p5.Image){
      textureData = args[0].canvas;
    }
    this._renderer._bind.call(this, args[0].tex, textureData);
  }
  //this is where we'd activate multi textures
  //eg. gl.activeTexture(gl.TEXTURE0 + (unit || 0));
  //but for now we just have a single texture.
  //@TODO need to extend this functionality
  gl.activeTexture(gl.TEXTURE0);
  gl.bindTexture(gl.TEXTURE_2D, args[0].tex);
  gl.uniform1i(gl.getUniformLocation(shaderProgram, 'isTexture'), true);
  gl.uniform1i(gl.getUniformLocation(shaderProgram, 'uSampler'), 0);
  return this;
};

/**
 * Texture Util functions
 */
p5.RendererGL.prototype._bind = function(tex, data){
  var gl = this._renderer.GL;
  gl.bindTexture(gl.TEXTURE_2D, tex);
  gl.pixelStorei(gl.UNPACK_FLIP_Y_WEBGL, true);
  gl.texImage2D(gl.TEXTURE_2D, 0,
    gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, data);
  gl.pixelStorei(gl.UNPACK_FLIP_Y_WEBGL, true);
  gl.texParameteri(gl.TEXTURE_2D,
  gl.TEXTURE_MAG_FILTER, gl.LINEAR);
  gl.texParameteri(gl.TEXTURE_2D,
  gl.TEXTURE_MIN_FILTER, gl.LINEAR);
  gl.texParameteri(gl.TEXTURE_2D,
  gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE);
  gl.texParameteri(gl.TEXTURE_2D,
  gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE);
  gl.bindTexture(gl.TEXTURE_2D, null);
};

/**
 * Checks whether val is a pot
 * more info on power of 2 here:
 * https://www.opengl.org/wiki/NPOT_Texture
 * @param  {Number}  value
 * @return {Boolean}
 */
// function _isPowerOf2 (value){
//   return (value & (value - 1)) === 0;
// }

/**
 * returns the next highest power of 2 value
 * @param  {Number} value [description]
 * @return {Number}       [description]
 */
// function _nextHighestPOT (value){
//   --value;
//   for (var i = 1; i < 32; i <<= 1) {
//     value = value | value >> i;
//   }
//   return value + 1;

/**
 * Ambient material for geometry with a given color. You can view all
 * possible materials in this
 * <a href="https://p5js.org/examples/examples/3D_Materials.php">example</a>.
 * @method  ambientMaterial
 * @param  {Number|Array|String|p5.Color} v1  gray value,
 * red or hue value (depending on the current color mode),
 * or color Array, or CSS color string
 * @param  {Number}            [v2] optional: green or saturation value
 * @param  {Number}            [v3] optional: blue or brightness value
 * @param  {Number}            [a]  optional: opacity
* @return {p5}                 the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 * function draw(){
 *  background(0);
 *  ambientLight(100);
 *  pointLight(250, 250, 250, 100, 100, 0);
 *  ambientMaterial(250);
 *  sphere(50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * radiating light source from top right of canvas
 *
 */
p5.prototype.ambientMaterial = function(v1, v2, v3, a) {
  var gl = this._renderer.GL;
  var shaderProgram =
    this._renderer._getShader('lightVert', 'lightTextureFrag');

  gl.useProgram(shaderProgram);
  shaderProgram.uMaterialColor = gl.getUniformLocation(
    shaderProgram, 'uMaterialColor' );
  var colors = this._renderer._applyColorBlend.apply(this._renderer, arguments);

  gl.uniform4f(shaderProgram.uMaterialColor,
    colors[0], colors[1], colors[2], colors[3]);

  shaderProgram.uSpecular = gl.getUniformLocation(
    shaderProgram, 'uSpecular' );
  gl.uniform1i(shaderProgram.uSpecular, false);

  gl.uniform1i(gl.getUniformLocation(shaderProgram, 'isTexture'), false);

  return this;
};

/**
 * Specular material for geometry with a given color. You can view all
 * possible materials in this
 * <a href="https://p5js.org/examples/examples/3D_Materials.php">example</a>.
 * @method specularMaterial
 * @param  {Number|Array|String|p5.Color} v1  gray value,
 * red or hue value (depending on the current color mode),
 * or color Array, or CSS color string
 * @param  {Number}            [v2] optional: green or saturation value
 * @param  {Number}            [v3] optional: blue or brightness value
 * @param  {Number}            [a]  optional: opacity
 * @return {p5}                the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 * function draw(){
 *  background(0);
 *  ambientLight(100);
 *  pointLight(250, 250, 250, 100, 100, 0);
 *  specularMaterial(250);
 *  sphere(50);
 * }
 * </code>
 * </div>
 *
 * @alt
 * diffused radiating light source from top right of canvas
 *
 */
p5.prototype.specularMaterial = function(v1, v2, v3, a) {
  var gl = this._renderer.GL;
  var shaderProgram =
    this._renderer._getShader('lightVert', 'lightTextureFrag');
  gl.useProgram(shaderProgram);
  gl.uniform1i(gl.getUniformLocation(shaderProgram, 'isTexture'), false);
  shaderProgram.uMaterialColor = gl.getUniformLocation(
    shaderProgram, 'uMaterialColor' );
  var colors = this._renderer._applyColorBlend.apply(this._renderer, arguments);
  gl.uniform4f(shaderProgram.uMaterialColor,
    colors[0], colors[1], colors[2], colors[3]);
  shaderProgram.uSpecular = gl.getUniformLocation(
    shaderProgram, 'uSpecular' );
  gl.uniform1i(shaderProgram.uSpecular, true);

  return this;
};

/**
 * @private blends colors according to color components.
 * If alpha value is less than 1, we need to enable blending
 * on our gl context.  Otherwise opaque objects need to a depthMask.
 * @param  {Number} v1 [description]
 * @param  {Number} v2 [description]
 * @param  {Number} v3 [description]
 * @param  {Number} a  [description]
 * @return {[Number]}  Normalized numbers array
 */
p5.RendererGL.prototype._applyColorBlend = function(v1,v2,v3,a){
  var gl = this.GL;
  var color = this._pInst.color.apply(
    this._pInst, arguments);
  var colors = color._array;
  if(colors[colors.length-1] < 1.0){
    gl.depthMask(false);
    gl.enable(gl.BLEND);
    gl.blendEquation( gl.FUNC_ADD );
    gl.blendFunc( gl.SRC_ALPHA, gl.ONE_MINUS_SRC_ALPHA );
  } else {
    gl.depthMask(true);
    gl.disable(gl.BLEND);
  }
  return colors;
};

module.exports = p5;

},{"../core/core":39}],84:[function(_dereq_,module,exports){
//some of the functions are adjusted from Three.js(http://threejs.org)

'use strict';

var p5 = _dereq_('../core/core');

/**
 * p5 Geometry class
 * @constructor
 * @param  {Function | Object} vertData callback function or Object
 *                     containing routine(s) for vertex data generation
 * @param  {Number} [detailX] number of vertices on horizontal surface
 * @param  {Number} [detailY] number of vertices on horizontal surface
 * @param {Function} [callback] function to call upon object instantiation.
 *
 */
p5.Geometry = function
(detailX, detailY, callback){
  //an array containing every vertex
  //@type [p5.Vector]
  this.vertices = [];
  //an array containing 1 normal per vertex
  //@type [p5.Vector]
  //[p5.Vector, p5.Vector, p5.Vector,p5.Vector, p5.Vector, p5.Vector,...]
  this.vertexNormals = [];
  //an array containing each three vertex indices that form a face
  //[[0, 1, 2], [2, 1, 3], ...]
  this.faces = [];
  //a 2D array containing uvs for every vertex
  //[[0.0,0.0],[1.0,0.0], ...]
  this.uvs = [];
  this.detailX = (detailX !== undefined) ? detailX: 1;
  this.detailY = (detailY !== undefined) ? detailY: 1;
  if(callback instanceof Function){
    callback.call(this);
  }
  return this;
};

p5.Geometry.prototype.computeFaces = function(){
  var sliceCount = this.detailX + 1;
  var a, b, c, d;
  for (var i = 0; i < this.detailY; i++){
    for (var j = 0; j < this.detailX; j++){
      a = i * sliceCount + j;// + offset;
      b = i * sliceCount + j + 1;// + offset;
      c = (i + 1)* sliceCount + j + 1;// + offset;
      d = (i + 1)* sliceCount + j;// + offset;
      this.faces.push([a, b, d]);
      this.faces.push([d, b, c]);
    }
  }
  return this;
};

p5.Geometry.prototype._getFaceNormal = function(faceId,vertId){
  //This assumes that vA->vB->vC is a counter-clockwise ordering
  var face = this.faces[faceId];
  var vA = this.vertices[face[vertId%3]];
  var vB = this.vertices[face[(vertId+1)%3]];
  var vC = this.vertices[face[(vertId+2)%3]];
  var n = p5.Vector.cross(
    p5.Vector.sub(vB,vA),
    p5.Vector.sub(vC,vA));
  var sinAlpha = p5.Vector.mag(n) /
  (p5.Vector.mag(p5.Vector.sub(vB,vA))*
    p5.Vector.mag(p5.Vector.sub(vC,vA)));
  n = n.normalize();
  return n.mult(Math.asin(sinAlpha));
};
/**
 * computes smooth normals per vertex as an average of each
 * face.
 */
p5.Geometry.prototype.computeNormals = function (){
  for(var v=0; v < this.vertices.length; v++){
    var normal = new p5.Vector();
    for(var i=0; i < this.faces.length; i++){
      //if our face contains a given vertex
      //calculate an average of the normals
      //of the triangles adjacent to that vertex
      if(this.faces[i][0] === v ||
        this.faces[i][1] === v ||
        this.faces[i][2] === v)
      {
        normal = normal.add(this._getFaceNormal(i, v));
      }
    }
    normal = normal.normalize();
    this.vertexNormals.push(normal);
  }
  return this;
};

/**
 * Averages the vertex normals. Used in curved
 * surfaces
 * @return {p5.Geometry}
 */
p5.Geometry.prototype.averageNormals = function() {

  for(var i = 0; i <= this.detailY; i++){
    var offset = this.detailX + 1;
    var temp = p5.Vector
      .add(this.vertexNormals[i*offset],
        this.vertexNormals[i*offset + this.detailX]);
    temp = p5.Vector.div(temp, 2);
    this.vertexNormals[i*offset] = temp;
    this.vertexNormals[i*offset + this.detailX] = temp;
  }
  return this;
};

/**
 * Averages pole normals.  Used in spherical primitives
 * @return {p5.Geometry}
 */
p5.Geometry.prototype.averagePoleNormals = function() {

  //average the north pole
  var sum = new p5.Vector(0, 0, 0);
  for(var i = 0; i < this.detailX; i++){
    sum.add(this.vertexNormals[i]);
  }
  sum = p5.Vector.div(sum, this.detailX);

  for(i = 0; i < this.detailX; i++){
    this.vertexNormals[i] = sum;
  }

  //average the south pole
  sum = new p5.Vector(0, 0, 0);
  for(i = this.vertices.length - 1;
    i > this.vertices.length - 1 - this.detailX; i--){
    sum.add(this.vertexNormals[i]);
  }
  sum = p5.Vector.div(sum, this.detailX);

  for(i = this.vertices.length - 1;
    i > this.vertices.length - 1 - this.detailX; i--){
    this.vertexNormals[i] = sum;
  }
  return this;
};

/**
 * Modifies all vertices to be centered within the range -100 to 100.
 * @return {p5.Geometry}
 */
p5.Geometry.prototype.normalize = function() {
  if(this.vertices.length > 0) {
    // Find the corners of our bounding box
    var maxPosition = this.vertices[0].copy();
    var minPosition = this.vertices[0].copy();

    for(var i = 0; i < this.vertices.length; i++) {
      maxPosition.x = Math.max(maxPosition.x, this.vertices[i].x);
      minPosition.x = Math.min(minPosition.x, this.vertices[i].x);
      maxPosition.y = Math.max(maxPosition.y, this.vertices[i].y);
      minPosition.y = Math.min(minPosition.y, this.vertices[i].y);
      maxPosition.z = Math.max(maxPosition.z, this.vertices[i].z);
      minPosition.z = Math.min(minPosition.z, this.vertices[i].z);
    }

    var center = p5.Vector.lerp(maxPosition, minPosition, 0.5);
    var dist = p5.Vector.sub(maxPosition, minPosition);
    var longestDist = Math.max(Math.max(dist.x, dist.y), dist.z);
    var scale = 200 / longestDist;

    for(i = 0; i < this.vertices.length; i++) {
      this.vertices[i].sub(center);
      this.vertices[i].mult(scale);
    }
  }
  return this;
};

module.exports = p5.Geometry;

},{"../core/core":39}],85:[function(_dereq_,module,exports){
/**
* @requires constants
* @todo see methods below needing further implementation.
* future consideration: implement SIMD optimizations
* when browser compatibility becomes available
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/
*   Reference/Global_Objects/SIMD
*/

'use strict';

var p5 = _dereq_('../core/core');
var polarGeometry = _dereq_('../math/polargeometry');
var constants = _dereq_('../core/constants');
var GLMAT_ARRAY_TYPE = (
    typeof Float32Array !== 'undefined') ?
  Float32Array : Array;

/**
 * A class to describe a 4x4 matrix
 * for model and view matrix manipulation in the p5js webgl renderer.
 * class p5.Matrix
 * @constructor
 * @param {Array} [mat4] array literal of our 4x4 matrix
 */
p5.Matrix = function() {
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  // This is default behavior when object
  // instantiated using createMatrix()
  // @todo implement createMatrix() in core/math.js
  if(args[0] instanceof p5) {
    // save reference to p5 if passed in
    this.p5 = args[0];
    if(args[1] === 'mat3'){
      this.mat3 = args[2] || new GLMAT_ARRAY_TYPE([
        1, 0, 0,
        0, 1, 0,
        0, 0, 1
      ]);
    }
    else {
      this.mat4  = args[1] || new GLMAT_ARRAY_TYPE([
        1, 0, 0, 0,
        0, 1, 0, 0,
        0, 0, 1, 0,
        0, 0, 0, 1
      ]);
    }
    // default behavior when object
    // instantiated using new p5.Matrix()
  } else {
    if(args[0] === 'mat3'){
      this.mat3 = args[1] || new GLMAT_ARRAY_TYPE([
        1, 0, 0,
        0, 1, 0,
        0, 0, 1
      ]);
    }
    else {
      this.mat4 = args[0] || new GLMAT_ARRAY_TYPE([
        1, 0, 0, 0,
        0, 1, 0, 0,
        0, 0, 1, 0,
        0, 0, 0, 1
      ]);
    }
  }
  return this;
};

/**
 * Sets the x, y, and z component of the vector using two or three separate
 * variables, the data from a p5.Matrix, or the values from a float array.
 *
 * @param {p5.Matrix|Array} [inMatrix] the input p5.Matrix or
 *                                     an Array of length 16
 */
p5.Matrix.prototype.set = function (inMatrix) {
  if (inMatrix instanceof p5.Matrix) {
    this.mat4 = inMatrix.mat4;
    return this;
  }
  else if (inMatrix instanceof GLMAT_ARRAY_TYPE) {
    this.mat4 = inMatrix;
    return this;
  }
  return this;
};

/**
 * Gets a copy of the vector, returns a p5.Matrix object.
 *
 * @return {p5.Matrix} the copy of the p5.Matrix object
 */
p5.Matrix.prototype.get = function () {
  return new p5.Matrix(this.mat4);
};

/**
 * return a copy of a matrix
 * @return {p5.Matrix}   the result matrix
 */
p5.Matrix.prototype.copy = function(){
  var copied = new p5.Matrix();
  copied.mat4[0] = this.mat4[0];
  copied.mat4[1] = this.mat4[1];
  copied.mat4[2] = this.mat4[2];
  copied.mat4[3] = this.mat4[3];
  copied.mat4[4] = this.mat4[4];
  copied.mat4[5] = this.mat4[5];
  copied.mat4[6] = this.mat4[6];
  copied.mat4[7] = this.mat4[7];
  copied.mat4[8] = this.mat4[8];
  copied.mat4[9] = this.mat4[9];
  copied.mat4[10] = this.mat4[10];
  copied.mat4[11] = this.mat4[11];
  copied.mat4[12] = this.mat4[12];
  copied.mat4[13] = this.mat4[13];
  copied.mat4[14] = this.mat4[14];
  copied.mat4[15] = this.mat4[15];
  return copied;
};

/**
 * return an identity matrix
 * @return {p5.Matrix}   the result matrix
 */
p5.Matrix.identity = function(){
  return new p5.Matrix();
};

/**
 * transpose according to a given matrix
 * @param  {p5.Matrix | Typed Array} a  the matrix to be based on to transpose
 * @return {p5.Matrix}                  this
 */
p5.Matrix.prototype.transpose = function(a){
  var a01, a02, a03, a12, a13, a23;
  if(a instanceof p5.Matrix){
    a01 = a.mat4[1];
    a02 = a.mat4[2];
    a03 = a.mat4[3];
    a12 = a.mat4[6];
    a13 = a.mat4[7];
    a23 = a.mat4[11];

    this.mat4[0] = a.mat4[0];
    this.mat4[1] = a.mat4[4];
    this.mat4[2] = a.mat4[8];
    this.mat4[3] = a.mat4[12];
    this.mat4[4] = a01;
    this.mat4[5] = a.mat4[5];
    this.mat4[6] = a.mat4[9];
    this.mat4[7] = a.mat4[13];
    this.mat4[8] = a02;
    this.mat4[9] = a12;
    this.mat4[10] = a.mat4[10];
    this.mat4[11] = a.mat4[14];
    this.mat4[12] = a03;
    this.mat4[13] = a13;
    this.mat4[14] = a23;
    this.mat4[15] = a.mat4[15];

  }else if(a instanceof GLMAT_ARRAY_TYPE){
    a01 = a[1];
    a02 = a[2];
    a03 = a[3];
    a12 = a[6];
    a13 = a[7];
    a23 = a[11];

    this.mat4[0] = a[0];
    this.mat4[1] = a[4];
    this.mat4[2] = a[8];
    this.mat4[3] = a[12];
    this.mat4[4] = a01;
    this.mat4[5] = a[5];
    this.mat4[6] = a[9];
    this.mat4[7] = a[13];
    this.mat4[8] = a02;
    this.mat4[9] = a12;
    this.mat4[10] = a[10];
    this.mat4[11] = a[14];
    this.mat4[12] = a03;
    this.mat4[13] = a13;
    this.mat4[14] = a23;
    this.mat4[15] = a[15];
  }
  return this;
};

/**
 * invert  matrix according to a give matrix
 * @param  {p5.Matrix or Typed Array} a   the matrix to be based on to invert
 * @return {p5.Matrix}                    this
 */
p5.Matrix.prototype.invert = function(a){
  var a00, a01, a02, a03, a10, a11, a12, a13,
  a20, a21, a22, a23, a30, a31, a32, a33;
  if(a instanceof p5.Matrix){
    a00 = a.mat4[0];
    a01 = a.mat4[1];
    a02 = a.mat4[2];
    a03 = a.mat4[3];
    a10 = a.mat4[4];
    a11 = a.mat4[5];
    a12 = a.mat4[6];
    a13 = a.mat4[7];
    a20 = a.mat4[8];
    a21 = a.mat4[9];
    a22 = a.mat4[10];
    a23 = a.mat4[11];
    a30 = a.mat4[12];
    a31 = a.mat4[13];
    a32 = a.mat4[14];
    a33 = a.mat4[15];
  }else if(a instanceof GLMAT_ARRAY_TYPE){
    a00 = a[0];
    a01 = a[1];
    a02 = a[2];
    a03 = a[3];
    a10 = a[4];
    a11 = a[5];
    a12 = a[6];
    a13 = a[7];
    a20 = a[8];
    a21 = a[9];
    a22 = a[10];
    a23 = a[11];
    a30 = a[12];
    a31 = a[13];
    a32 = a[14];
    a33 = a[15];
  }
  var b00 = a00 * a11 - a01 * a10,
  b01 = a00 * a12 - a02 * a10,
  b02 = a00 * a13 - a03 * a10,
  b03 = a01 * a12 - a02 * a11,
  b04 = a01 * a13 - a03 * a11,
  b05 = a02 * a13 - a03 * a12,
  b06 = a20 * a31 - a21 * a30,
  b07 = a20 * a32 - a22 * a30,
  b08 = a20 * a33 - a23 * a30,
  b09 = a21 * a32 - a22 * a31,
  b10 = a21 * a33 - a23 * a31,
  b11 = a22 * a33 - a23 * a32,

  // Calculate the determinant
  det = b00 * b11 - b01 * b10 + b02 * b09 + b03 * b08 -
  b04 * b07 + b05 * b06;

  if (!det) {
    return null;
  }
  det = 1.0 / det;

  this.mat4[0] = (a11 * b11 - a12 * b10 + a13 * b09) * det;
  this.mat4[1] = (a02 * b10 - a01 * b11 - a03 * b09) * det;
  this.mat4[2] = (a31 * b05 - a32 * b04 + a33 * b03) * det;
  this.mat4[3] = (a22 * b04 - a21 * b05 - a23 * b03) * det;
  this.mat4[4] = (a12 * b08 - a10 * b11 - a13 * b07) * det;
  this.mat4[5] = (a00 * b11 - a02 * b08 + a03 * b07) * det;
  this.mat4[6] = (a32 * b02 - a30 * b05 - a33 * b01) * det;
  this.mat4[7] = (a20 * b05 - a22 * b02 + a23 * b01) * det;
  this.mat4[8] = (a10 * b10 - a11 * b08 + a13 * b06) * det;
  this.mat4[9] = (a01 * b08 - a00 * b10 - a03 * b06) * det;
  this.mat4[10] = (a30 * b04 - a31 * b02 + a33 * b00) * det;
  this.mat4[11] = (a21 * b02 - a20 * b04 - a23 * b00) * det;
  this.mat4[12] = (a11 * b07 - a10 * b09 - a12 * b06) * det;
  this.mat4[13] = (a00 * b09 - a01 * b07 + a02 * b06) * det;
  this.mat4[14] = (a31 * b01 - a30 * b03 - a32 * b00) * det;
  this.mat4[15] = (a20 * b03 - a21 * b01 + a22 * b00) * det;

  return this;
};

/**
 * Inverts a 3x3 matrix
 * @return {[type]} [description]
 */
p5.Matrix.prototype.invert3x3 = function (){
  var a00 = this.mat3[0],
  a01 = this.mat3[1],
  a02 = this.mat3[2],
  a10 = this.mat3[3],
  a11 = this.mat3[4],
  a12 = this.mat3[5],
  a20 = this.mat3[6],
  a21 = this.mat3[7],
  a22 = this.mat3[8],
  b01 = a22 * a11 - a12 * a21,
  b11 = -a22 * a10 + a12 * a20,
  b21 = a21 * a10 - a11 * a20,

  // Calculate the determinant
  det = a00 * b01 + a01 * b11 + a02 * b21;
  if (!det) {
    return null;
  }
  det = 1.0 / det;
  this.mat3[0] = b01 * det;
  this.mat3[1] = (-a22 * a01 + a02 * a21) * det;
  this.mat3[2] = (a12 * a01 - a02 * a11) * det;
  this.mat3[3] = b11 * det;
  this.mat3[4] = (a22 * a00 - a02 * a20) * det;
  this.mat3[5] = (-a12 * a00 + a02 * a10) * det;
  this.mat3[6] = b21 * det;
  this.mat3[7] = (-a21 * a00 + a01 * a20) * det;
  this.mat3[8] = (a11 * a00 - a01 * a10) * det;
  return this;
};

/**
 * transposes a 3x3 p5.Matrix by a mat3
 * @param  {[Number]} mat3 1-dimensional array
 * @return {p5.Matrix} this
 */
p5.Matrix.prototype.transpose3x3 = function (mat3){
  var a01 = mat3[1], a02 = mat3[2], a12 = mat3[5];
  this.mat3[1] = mat3[3];
  this.mat3[2] = mat3[6];
  this.mat3[3] = a01;
  this.mat3[5] = mat3[7];
  this.mat3[6] = a02;
  this.mat3[7] = a12;
  return this;
};

/**
 * converts a 4x4 matrix to its 3x3 inverse tranform
 * commonly used in MVMatrix to NMatrix conversions.
 * @param  {p5.Matrix} mat4 the matrix to be based on to invert
 * @return {p5.Matrix} this with mat3
 * @todo  finish implementation
 */
p5.Matrix.prototype.inverseTranspose = function (matrix){
  if(this.mat3 === undefined){
    console.error('sorry, this function only works with mat3');
  }
  else {
    //convert mat4 -> mat3
    this.mat3[0] = matrix.mat4[0];
    this.mat3[1] = matrix.mat4[1];
    this.mat3[2] = matrix.mat4[2];
    this.mat3[3] = matrix.mat4[4];
    this.mat3[4] = matrix.mat4[5];
    this.mat3[5] = matrix.mat4[6];
    this.mat3[6] = matrix.mat4[8];
    this.mat3[7] = matrix.mat4[9];
    this.mat3[8] = matrix.mat4[10];
  }

  this.invert3x3().transpose3x3(this.mat3);
  return this;
};

/**
 * inspired by Toji's mat4 determinant
 * @return {Number} Determinant of our 4x4 matrix
 */
p5.Matrix.prototype.determinant = function(){
  var d00 = (this.mat4[0] * this.mat4[5]) - (this.mat4[1] * this.mat4[4]),
    d01 = (this.mat4[0] * this.mat4[6]) - (this.mat4[2] * this.mat4[4]),
    d02 = (this.mat4[0] * this.mat4[7]) - (this.mat4[3] * this.mat4[4]),
    d03 = (this.mat4[1] * this.mat4[6]) - (this.mat4[2] * this.mat4[5]),
    d04 = (this.mat4[1] * this.mat4[7]) - (this.mat4[3] * this.mat4[5]),
    d05 = (this.mat4[2] * this.mat4[7]) - (this.mat4[3] * this.mat4[6]),
    d06 = (this.mat4[8] * this.mat4[13]) - (this.mat4[9] * this.mat4[12]),
    d07 = (this.mat4[8] * this.mat4[14]) - (this.mat4[10] * this.mat4[12]),
    d08 = (this.mat4[8] * this.mat4[15]) - (this.mat4[11] * this.mat4[12]),
    d09 = (this.mat4[9] * this.mat4[14]) - (this.mat4[10] * this.mat4[13]),
    d10 = (this.mat4[9] * this.mat4[15]) - (this.mat4[11] * this.mat4[13]),
    d11 = (this.mat4[10] * this.mat4[15]) - (this.mat4[11] * this.mat4[14]);

  // Calculate the determinant
  return d00 * d11 - d01 * d10 + d02 * d09 +
    d03 * d08 - d04 * d07 + d05 * d06;
};

/**
 * multiply two mat4s
 * @param {p5.Matrix | Array}  multMatrix The matrix we want to multiply by
 * @return {p5.Matrix}         this
 */
p5.Matrix.prototype.mult = function(multMatrix){
  var _dest = new GLMAT_ARRAY_TYPE(16);
  var _src = new GLMAT_ARRAY_TYPE(16);

  if(multMatrix instanceof p5.Matrix) {
    _src = multMatrix.mat4;
  }
  else if(multMatrix instanceof GLMAT_ARRAY_TYPE){
    _src = multMatrix;
  }

  // each row is used for the multiplier
  var b0  = this.mat4[0], b1 = this.mat4[1],
    b2 = this.mat4[2], b3 = this.mat4[3];
  _dest[0] = b0*_src[0] + b1*_src[4] + b2*_src[8] + b3*_src[12];
  _dest[1] = b0*_src[1] + b1*_src[5] + b2*_src[9] + b3*_src[13];
  _dest[2] = b0*_src[2] + b1*_src[6] + b2*_src[10] + b3*_src[14];
  _dest[3] = b0*_src[3] + b1*_src[7] + b2*_src[11] + b3*_src[15];

  b0 = this.mat4[4];
  b1 = this.mat4[5];
  b2 = this.mat4[6];
  b3 = this.mat4[7];
  _dest[4] = b0*_src[0] + b1*_src[4] + b2*_src[8] + b3*_src[12];
  _dest[5] = b0*_src[1] + b1*_src[5] + b2*_src[9] + b3*_src[13];
  _dest[6] = b0*_src[2] + b1*_src[6] + b2*_src[10] + b3*_src[14];
  _dest[7] = b0*_src[3] + b1*_src[7] + b2*_src[11] + b3*_src[15];

  b0 = this.mat4[8];
  b1 = this.mat4[9];
  b2 = this.mat4[10];
  b3 = this.mat4[11];
  _dest[8] = b0*_src[0] + b1*_src[4] + b2*_src[8] + b3*_src[12];
  _dest[9] = b0*_src[1] + b1*_src[5] + b2*_src[9] + b3*_src[13];
  _dest[10] = b0*_src[2] + b1*_src[6] + b2*_src[10] + b3*_src[14];
  _dest[11] = b0*_src[3] + b1*_src[7] + b2*_src[11] + b3*_src[15];

  b0 = this.mat4[12];
  b1 = this.mat4[13];
  b2 = this.mat4[14];
  b3 = this.mat4[15];
  _dest[12] = b0*_src[0] + b1*_src[4] + b2*_src[8] + b3*_src[12];
  _dest[13] = b0*_src[1] + b1*_src[5] + b2*_src[9] + b3*_src[13];
  _dest[14] = b0*_src[2] + b1*_src[6] + b2*_src[10] + b3*_src[14];
  _dest[15] = b0*_src[3] + b1*_src[7] + b2*_src[11] + b3*_src[15];

  this.mat4 = _dest;

  return this;
};

/**
 * scales a p5.Matrix by scalars or a vector
 * @param  {p5.Vector | Array }
 *                      vector to scale by
 * @return {p5.Matrix}  this
 */
p5.Matrix.prototype.scale = function() {
  var x,y,z;
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  //if our 1st arg is a type p5.Vector
  if (args[0] instanceof p5.Vector){
    x = args[0].x;
    y = args[0].y;
    z = args[0].z;
  }
  //otherwise if it's an array
  else if (args[0] instanceof Array){
    x = args[0][0];
    y = args[0][1];
    z = args[0][2];
  }
  var _dest = new GLMAT_ARRAY_TYPE(16);
  _dest[0] = this.mat4[0] * x;
  _dest[1] = this.mat4[1] * x;
  _dest[2] = this.mat4[2] * x;
  _dest[3] = this.mat4[3] * x;
  _dest[4] = this.mat4[4] * y;
  _dest[5] = this.mat4[5] * y;
  _dest[6] = this.mat4[6] * y;
  _dest[7] = this.mat4[7] * y;
  _dest[8] = this.mat4[8] * z;
  _dest[9] = this.mat4[9] * z;
  _dest[10] = this.mat4[10] * z;
  _dest[11] = this.mat4[11] * z;
  _dest[12] = this.mat4[12];
  _dest[13] = this.mat4[13];
  _dest[14] = this.mat4[14];
  _dest[15] = this.mat4[15];

  this.mat4 = _dest;
  return this;
};

/**
 * rotate our Matrix around an axis by the given angle.
 * @param  {Number} a The angle of rotation in radians
 * @param  {p5.Vector | Array} axis  the axis(es) to rotate around
 * @return {p5.Matrix}                    this
 * inspired by Toji's gl-matrix lib, mat4 rotation
 */
p5.Matrix.prototype.rotate = function(a, axis){
  var x, y, z, _a, len;

  if (this.p5) {
    if (this.p5._angleMode === constants.DEGREES) {
      _a = polarGeometry.degreesToRadians(a);
    }
  }
  else {
    _a = a;
  }
  if (axis instanceof p5.Vector) {
    x = axis.x;
    y = axis.y;
    z = axis.z;
  }
  else if (axis instanceof Array) {
    x = axis[0];
    y = axis[1];
    z = axis[2];
  }

  len = Math.sqrt(x * x + y * y + z * z);
  x *= (1/len);
  y *= (1/len);
  z *= (1/len);

  var a00 = this.mat4[0];
  var a01 = this.mat4[1];
  var a02 = this.mat4[2];
  var a03 = this.mat4[3];
  var a10 = this.mat4[4];
  var a11 = this.mat4[5];
  var a12 = this.mat4[6];
  var a13 = this.mat4[7];
  var a20 = this.mat4[8];
  var a21 = this.mat4[9];
  var a22 = this.mat4[10];
  var a23 = this.mat4[11];

  //sin,cos, and tan of respective angle
  var sA = Math.sin(_a);
  var cA = Math.cos(_a);
  var tA = 1 - cA;
  // Construct the elements of the rotation matrix
  var b00 = x * x * tA + cA;
  var b01 = y * x * tA + z * sA;
  var b02 = z * x * tA - y * sA;
  var b10 = x * y * tA - z * sA;
  var b11 = y * y * tA + cA;
  var b12 = z * y * tA + x * sA;
  var b20 = x * z * tA + y * sA;
  var b21 = y * z * tA - x * sA;
  var b22 = z * z * tA + cA;

  // rotation-specific matrix multiplication
  this.mat4[0] = a00 * b00 + a10 * b01 + a20 * b02;
  this.mat4[1] = a01 * b00 + a11 * b01 + a21 * b02;
  this.mat4[2] = a02 * b00 + a12 * b01 + a22 * b02;
  this.mat4[3] = a03 * b00 + a13 * b01 + a23 * b02;
  this.mat4[4] = a00 * b10 + a10 * b11 + a20 * b12;
  this.mat4[5] = a01 * b10 + a11 * b11 + a21 * b12;
  this.mat4[6] = a02 * b10 + a12 * b11 + a22 * b12;
  this.mat4[7] = a03 * b10 + a13 * b11 + a23 * b12;
  this.mat4[8] = a00 * b20 + a10 * b21 + a20 * b22;
  this.mat4[9] = a01 * b20 + a11 * b21 + a21 * b22;
  this.mat4[10] = a02 * b20 + a12 * b21 + a22 * b22;
  this.mat4[11] = a03 * b20 + a13 * b21 + a23 * b22;

  return this;
};

/**
 * @todo  finish implementing this method!
 * translates
 * @param  {Array} v vector to translate by
 * @return {p5.Matrix}                    this
 */
p5.Matrix.prototype.translate = function(v){
  var x = v[0],
    y = v[1],
    z = v[2] || 0;
  this.mat4[12] =
    this.mat4[0] * x +this.mat4[4] * y +this.mat4[8] * z +this.mat4[12];
  this.mat4[13] =
    this.mat4[1] * x +this.mat4[5] * y +this.mat4[9] * z +this.mat4[13];
  this.mat4[14] =
    this.mat4[2] * x +this.mat4[6] * y +this.mat4[10] * z +this.mat4[14];
  this.mat4[15] =
    this.mat4[3] * x +this.mat4[7] * y +this.mat4[11] * z +this.mat4[15];
};

p5.Matrix.prototype.rotateX = function(a){
  this.rotate(a, [1,0,0]);
};
p5.Matrix.prototype.rotateY = function(a){
  this.rotate(a, [0,1,0]);
};
p5.Matrix.prototype.rotateZ = function(a){
  this.rotate(a, [0,0,1]);
};

/**
 * sets the perspective matrix
 * @param  {Number} fovy   [description]
 * @param  {Number} aspect [description]
 * @param  {Number} near   near clipping plane
 * @param  {Number} far    far clipping plane
 * @return {void}
 */
p5.Matrix.prototype.perspective = function(fovy,aspect,near,far){

  var f = 1.0 / Math.tan(fovy / 2),
    nf = 1 / (near - far);

  this.mat4[0] = f / aspect;
  this.mat4[1] = 0;
  this.mat4[2] = 0;
  this.mat4[3] = 0;
  this.mat4[4] = 0;
  this.mat4[5] = f;
  this.mat4[6] = 0;
  this.mat4[7] = 0;
  this.mat4[8] = 0;
  this.mat4[9] = 0;
  this.mat4[10] = (far + near) * nf;
  this.mat4[11] = -1;
  this.mat4[12] = 0;
  this.mat4[13] = 0;
  this.mat4[14] = (2 * far * near) * nf;
  this.mat4[15] = 0;

  return this;

};

/**
 * sets the ortho matrix
 * @param  {Number} left   [description]
 * @param  {Number} right  [description]
 * @param  {Number} bottom [description]
 * @param  {Number} top    [description]
 * @param  {Number} near   near clipping plane
 * @param  {Number} far    far clipping plane
 * @return {void}
 */
p5.Matrix.prototype.ortho = function(left,right,bottom,top,near,far){

  var lr = 1 / (left - right),
    bt = 1 / (bottom - top),
    nf = 1 / (near - far);
  this.mat4[0] = -2 * lr;
  this.mat4[1] = 0;
  this.mat4[2] = 0;
  this.mat4[3] = 0;
  this.mat4[4] = 0;
  this.mat4[5] = -2 * bt;
  this.mat4[6] = 0;
  this.mat4[7] = 0;
  this.mat4[8] = 0;
  this.mat4[9] = 0;
  this.mat4[10] = 2 * nf;
  this.mat4[11] = 0;
  this.mat4[12] = (left + right) * lr;
  this.mat4[13] = (top + bottom) * bt;
  this.mat4[14] = (far + near) * nf;
  this.mat4[15] = 1;

  return this;
};

/**
 * PRIVATE
 */
// matrix methods adapted from:
// https://developer.mozilla.org/en-US/docs/Web/WebGL/
// gluPerspective
//
// function _makePerspective(fovy, aspect, znear, zfar){
//    var ymax = znear * Math.tan(fovy * Math.PI / 360.0);
//    var ymin = -ymax;
//    var xmin = ymin * aspect;
//    var xmax = ymax * aspect;
//    return _makeFrustum(xmin, xmax, ymin, ymax, znear, zfar);
//  }

////
//// glFrustum
////
//function _makeFrustum(left, right, bottom, top, znear, zfar){
//  var X = 2*znear/(right-left);
//  var Y = 2*znear/(top-bottom);
//  var A = (right+left)/(right-left);
//  var B = (top+bottom)/(top-bottom);
//  var C = -(zfar+znear)/(zfar-znear);
//  var D = -2*zfar*znear/(zfar-znear);
//  var frustrumMatrix =[
//  X, 0, A, 0,
//  0, Y, B, 0,
//  0, 0, C, D,
//  0, 0, -1, 0
//];
//return frustrumMatrix;
// }

// function _setMVPMatrices(){
////an identity matrix
////@TODO use the p5.Matrix class to abstract away our MV matrices and
///other math
//var _mvMatrix =
//[
//  1.0,0.0,0.0,0.0,
//  0.0,1.0,0.0,0.0,
//  0.0,0.0,1.0,0.0,
//  0.0,0.0,0.0,1.0
//];

module.exports = p5.Matrix;

},{"../core/constants":38,"../core/core":39,"../math/polargeometry":69}],86:[function(_dereq_,module,exports){
/**
 * Welcome to RendererGL Immediate Mode.
 * Immediate mode is used for drawing custom shapes
 * from a set of vertices.  Immediate Mode is activated
 * when you call beginShape() & de-activated when you call endShape().
 * Immediate mode is a style of programming borrowed
 * from OpenGL's (now-deprecated) immediate mode.
 * It differs from p5.js' default, Retained Mode, which caches
 * geometries and buffers on the CPU to reduce the number of webgl
 * draw calls. Retained mode is more efficient & performative,
 * however, Immediate Mode is useful for sketching quick
 * geometric ideas.
 */
'use strict';

var p5 = _dereq_('../core/core');
var constants = _dereq_('../core/constants');

/**
 * Begin shape drawing.  This is a helpful way of generating
 * custom shapes quickly.  However in WEBGL mode, application
 * performance will likely drop as a result of too many calls to
 * beginShape() / endShape().  As a high performance alternative,
 * please use p5.js geometry primitives.
 * @param  {Number} mode webgl primitives mode.  beginShape supports the
 *                       following modes:
 *                       POINTS,LINES,LINE_STRIP,LINE_LOOP,TRIANGLES,
 *                       TRIANGLE_STRIP,and TRIANGLE_FAN.
 * @return {[type]}      [description]
 */
p5.RendererGL.prototype.beginShape = function(mode){
  //default shape mode is line_strip
  this.immediateMode.shapeMode = (mode !== undefined ) ?
    mode : constants.LINE_STRIP;
  //if we haven't yet initialized our
  //immediateMode vertices & buffers, create them now!
  if(this.immediateMode.vertexPositions === undefined){
    this.immediateMode.vertexPositions = [];
    this.immediateMode.vertexColors = [];
    this.immediateMode.vertexBuffer = this.GL.createBuffer();
    this.immediateMode.colorBuffer = this.GL.createBuffer();
  } else {
    this.immediateMode.vertexPositions.length = 0;
    this.immediateMode.vertexColors.length = 0;
  }
  this.isImmediateDrawing = true;
  return this;
};
/**
 * adds a vertex to be drawn in a custom Shape.
 * @param  {Number} x x-coordinate of vertex
 * @param  {Number} y y-coordinate of vertex
 * @param  {Number} z z-coordinate of vertex
 * @return {p5.RendererGL}   [description]
 * @TODO implement handling of p5.Vector args
 */
p5.RendererGL.prototype.vertex = function(x, y, z){
  this.immediateMode.vertexPositions.push(x, y, z);
  var vertexColor = this.curFillColor || [0.5, 0.5, 0.5, 1.0];
  this.immediateMode.vertexColors.push(
    vertexColor[0],
    vertexColor[1],
    vertexColor[2],
    vertexColor[3]);
  return this;
};

/**
 * End shape drawing and render vertices to screen.
 * @return {p5.RendererGL} [description]
 */
p5.RendererGL.prototype.endShape =
function(mode, isCurve, isBezier,isQuadratic, isContour, shapeKind){
  var gl = this.GL;
  this._bindImmediateBuffers(
    this.immediateMode.vertexPositions,
    this.immediateMode.vertexColors);
  if(mode){
    if(this.drawMode === 'fill'){
      switch(this.immediateMode.shapeMode){
        case constants.LINE_STRIP:
          this.immediateMode.shapeMode = constants.TRIANGLE_FAN;
          break;
        case constants.LINES:
          this.immediateMode.shapeMode = constants.TRIANGLE_FAN;
          break;
        case constants.TRIANGLES:
          this.immediateMode.shapeMode = constants.TRIANGLE_FAN;
          break;
      }
    } else {
      switch(this.immediateMode.shapeMode){
        case constants.LINE_STRIP:
          this.immediateMode.shapeMode = constants.LINE_LOOP;
          break;
        case constants.LINES:
          this.immediateMode.shapeMode = constants.LINE_LOOP;
          break;
      }
    }
  }
  //QUADS & QUAD_STRIP are not supported primitives modes
  //in webgl.
  if(this.immediateMode.shapeMode === constants.QUADS ||
    this.immediateMode.shapeMode === constants.QUAD_STRIP){
    throw new Error('sorry, ' + this.immediateMode.shapeMode+
      ' not yet implemented in webgl mode.');
  }
  else {
    gl.enable(gl.BLEND);
    gl.drawArrays(this.immediateMode.shapeMode, 0,
      this.immediateMode.vertexPositions.length / 3);
  }
  //clear out our vertexPositions & colors arrays
  //after rendering
  this.immediateMode.vertexPositions.length = 0;
  this.immediateMode.vertexColors.length = 0;
  this.isImmediateDrawing = false;
  return this;
};
/**
 * Bind immediateMode buffers to data,
 * then draw gl arrays
 * @param  {Array} vertices Numbers array representing
 *                          vertex positions
 * @return {p5.RendererGL}
 */
p5.RendererGL.prototype._bindImmediateBuffers = function(vertices, colors){
  this._setDefaultCamera();
  var gl = this.GL;
  var shaderKey = this._getCurShaderId();
  var shaderProgram = this.mHash[shaderKey];
  //vertex position Attribute
  shaderProgram.vertexPositionAttribute =
    gl.getAttribLocation(shaderProgram, 'aPosition');
  gl.enableVertexAttribArray(shaderProgram.vertexPositionAttribute);
  gl.bindBuffer(gl.ARRAY_BUFFER, this.immediateMode.vertexBuffer);
  gl.bufferData(
    gl.ARRAY_BUFFER, new Float32Array(vertices), gl.DYNAMIC_DRAW);
  gl.vertexAttribPointer(shaderProgram.vertexPositionAttribute,
    3, gl.FLOAT, false, 0, 0);

  shaderProgram.vertexColorAttribute =
    gl.getAttribLocation(shaderProgram, 'aVertexColor');
  gl.enableVertexAttribArray(shaderProgram.vertexColorAttribute);
  gl.bindBuffer(gl.ARRAY_BUFFER, this.immediateMode.colorBuffer);
  gl.bufferData(gl.ARRAY_BUFFER,
    new Float32Array(colors),gl.DYNAMIC_DRAW);
  gl.vertexAttribPointer(shaderProgram.vertexColorAttribute,
    4, gl.FLOAT, false, 0, 0);
  //matrix
  this._setMatrixUniforms(shaderKey);
  //@todo implement in all shaders (not just immediateVert)
  //set our default point size
  // this._setUniform1f(shaderKey,
  //   'uPointSize',
  //   this.pointSize);
  return this;
};

//////////////////////////////////////////////
// COLOR
//////////////////////////////////////////////

p5.RendererGL.prototype._getColorVertexShader = function(){
  var gl = this.GL;
  var mId = 'immediateVert|vertexColorFrag';
  var shaderProgram;

  if(!this.materialInHash(mId)){
    shaderProgram =
      this._initShaders('immediateVert', 'vertexColorFrag', true);
    this.mHash[mId] = shaderProgram;
    shaderProgram.vertexColorAttribute =
    gl.getAttribLocation(shaderProgram, 'aVertexColor');
    gl.enableVertexAttribArray(shaderProgram.vertexColorAttribute);
  }else{
    shaderProgram = this.mHash[mId];
  }
  return shaderProgram;
};

module.exports = p5.RendererGL;
},{"../core/constants":38,"../core/core":39}],87:[function(_dereq_,module,exports){
//Retained Mode. The default mode for rendering 3D primitives
//in WEBGL.
'use strict';

var p5 = _dereq_('../core/core');
var hashCount = 0;
/**
 * _initBufferDefaults
 * @description initializes buffer defaults. runs each time a new geometry is
 * registered
 * @param  {String} gId  key of the geometry object
 */
p5.RendererGL.prototype._initBufferDefaults = function(gId) {
  //@TODO remove this limit on hashes in gHash
  hashCount ++;
  if(hashCount > 1000){
    var key = Object.keys(this.gHash)[0];
    delete this.gHash[key];
    hashCount --;
  }

  var gl = this.GL;
  //create a new entry in our gHash
  this.gHash[gId] = {};
  this.gHash[gId].vertexBuffer = gl.createBuffer();
  this.gHash[gId].normalBuffer = gl.createBuffer();
  this.gHash[gId].uvBuffer = gl.createBuffer();
  this.gHash[gId].indexBuffer = gl.createBuffer();
};
/**
 * createBuffers description
 * @param  {String} gId    key of the geometry object
 * @param  {p5.Geometry}  obj contains geometry data
 */
p5.RendererGL.prototype.createBuffers = function(gId, obj) {
  var gl = this.GL;
  this._setDefaultCamera();
  //initialize the gl buffers for our geom groups
  this._initBufferDefaults(gId);
  //return the current shaderProgram from our material hash
  var shaderProgram = this.mHash[this._getCurShaderId()];
  //@todo rename "numberOfItems" property to something more descriptive
  //we mult the num geom faces by 3
  this.gHash[gId].numberOfItems = obj.faces.length * 3;
  gl.bindBuffer(gl.ARRAY_BUFFER, this.gHash[gId].vertexBuffer);
  gl.bufferData(
    gl.ARRAY_BUFFER,
    new Float32Array( vToNArray(obj.vertices) ),
    gl.STATIC_DRAW);
  //vertex position
  shaderProgram.vertexPositionAttribute =
    gl.getAttribLocation(shaderProgram, 'aPosition');
  gl.enableVertexAttribArray(shaderProgram.vertexPositionAttribute);

  gl.vertexAttribPointer(
    shaderProgram.vertexPositionAttribute,
    3, gl.FLOAT, false, 0, 0);

  gl.bindBuffer(gl.ARRAY_BUFFER, this.gHash[gId].normalBuffer);
  gl.bufferData(
    gl.ARRAY_BUFFER,
    new Float32Array( vToNArray(obj.vertexNormals) ),
    gl.STATIC_DRAW);
  //vertex normal
  shaderProgram.vertexNormalAttribute =
    gl.getAttribLocation(shaderProgram, 'aNormal');
  gl.enableVertexAttribArray(shaderProgram.vertexNormalAttribute);

  gl.vertexAttribPointer(
    shaderProgram.vertexNormalAttribute,
    3, gl.FLOAT, false, 0, 0);

  gl.bindBuffer(gl.ARRAY_BUFFER, this.gHash[gId].uvBuffer);
  gl.bufferData(
    gl.ARRAY_BUFFER,
    new Float32Array( flatten(obj.uvs) ),
    gl.STATIC_DRAW);
  //texture coordinate Attribute
  shaderProgram.textureCoordAttribute =
    gl.getAttribLocation(shaderProgram, 'aTexCoord');
  gl.enableVertexAttribArray(shaderProgram.textureCoordAttribute);
  gl.vertexAttribPointer(
    shaderProgram.textureCoordAttribute,
    2, gl.FLOAT, false, 0, 0);

  gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, this.gHash[gId].indexBuffer);
  gl.bufferData(
    gl.ELEMENT_ARRAY_BUFFER,
    new Uint16Array( flatten(obj.faces) ),
    gl.STATIC_DRAW);
};

/**
 * Draws buffers given a geometry key ID
 * @param  {String} gId     ID in our geom hash
 * @return {p5.RendererGL} this
 */
p5.RendererGL.prototype.drawBuffers = function(gId) {
  this._setDefaultCamera();
  var gl = this.GL;
  var shaderKey = this._getCurShaderId();
  var shaderProgram = this.mHash[shaderKey];
  //vertex position buffer
  gl.bindBuffer(gl.ARRAY_BUFFER, this.gHash[gId].vertexBuffer);
  gl.vertexAttribPointer(
    shaderProgram.vertexPositionAttribute,
    3, gl.FLOAT, false, 0, 0);
  //normal buffer
  gl.bindBuffer(gl.ARRAY_BUFFER, this.gHash[gId].normalBuffer);
  gl.vertexAttribPointer(
    shaderProgram.vertexNormalAttribute,
    3, gl.FLOAT, false, 0, 0);
  // uv buffer
  gl.bindBuffer(gl.ARRAY_BUFFER, this.gHash[gId].uvBuffer);
  gl.vertexAttribPointer(
    shaderProgram.textureCoordAttribute,
    2, gl.FLOAT, false, 0, 0);
  //vertex index buffer
  gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, this.gHash[gId].indexBuffer);
  this._setMatrixUniforms(shaderKey);
  gl.drawElements(
    gl.TRIANGLES, this.gHash[gId].numberOfItems,
    gl.UNSIGNED_SHORT, 0);
  return this;
};
///////////////////////////////
//// UTILITY FUNCTIONS
//////////////////////////////
/**
 * turn a two dimensional array into one dimensional array
 * @param  {Array} arr 2-dimensional array
 * @return {Array}     1-dimensional array
 * [[1, 2, 3],[4, 5, 6]] -> [1, 2, 3, 4, 5, 6]
 */
function flatten(arr){
  if (arr.length>0){
    return arr.reduce(function(a, b){
      return a.concat(b);
    });
  } else {
    return [];
  }
}

/**
 * turn a p5.Vector Array into a one dimensional number array
 * @param  {Array} arr  an array of p5.Vector
 * @return {Array]}     a one dimensional array of numbers
 * [p5.Vector(1, 2, 3), p5.Vector(4, 5, 6)] ->
 * [1, 2, 3, 4, 5, 6]
 */
function vToNArray(arr){
  return flatten(arr.map(function(item){
    return [item.x, item.y, item.z];
  }));
}
module.exports = p5.RendererGL;

},{"../core/core":39}],88:[function(_dereq_,module,exports){
'use strict';

var p5 = _dereq_('../core/core');
var shader = _dereq_('./shader');
_dereq_('../core/p5.Renderer');
_dereq_('./p5.Matrix');
var uMVMatrixStack = [];
var RESOLUTION = 1000;

//@TODO should implement public method
//to override these attributes
var attributes = {
  alpha: true,
  depth: true,
  stencil: true,
  antialias: false,
  premultipliedAlpha: false,
  preserveDrawingBuffer: false
};

/**
 * @class p5.RendererGL
 * @constructor
 * @extends p5.Renderer
 * 3D graphics class.
 * @todo extend class to include public method for offscreen
 * rendering (FBO).
 *
 */
p5.RendererGL = function(elt, pInst, isMainCanvas) {
  p5.Renderer.call(this, elt, pInst, isMainCanvas);
  this._initContext();

  this.isP3D = true; //lets us know we're in 3d mode
  this.GL = this.drawingContext;
  //lights
  this.ambientLightCount = 0;
  this.directionalLightCount = 0;
  this.pointLightCount = 0;
  //camera
  this._curCamera = null;

  /**
   * model view, projection, & normal
   * matrices
   */
  this.uMVMatrix = new p5.Matrix();
  this.uPMatrix  = new p5.Matrix();
  this.uNMatrix = new p5.Matrix('mat3');
  //Geometry & Material hashes
  this.gHash = {};
  this.mHash = {};
  //Imediate Mode
  //default drawing is done in Retained Mode
  this.isImmediateDrawing = false;
  this.immediateMode = {};
  this.curFillColor = [0.5,0.5,0.5,1.0];
  this.curStrokeColor = [0.5,0.5,0.5,1.0];
  this.pointSize = 5.0;//default point/stroke
  return this;
};

p5.RendererGL.prototype = Object.create(p5.Renderer.prototype);

//////////////////////////////////////////////
// Setting
//////////////////////////////////////////////

p5.RendererGL.prototype._initContext = function() {
  try {
    this.drawingContext = this.canvas.getContext('webgl', attributes) ||
      this.canvas.getContext('experimental-webgl', attributes);
    if (this.drawingContext === null) {
      throw new Error('Error creating webgl context');
    } else {
      console.log('p5.RendererGL: enabled webgl context');
      var gl = this.drawingContext;
      gl.enable(gl.DEPTH_TEST);
      gl.depthFunc(gl.LEQUAL);
      gl.viewport(0, 0, gl.drawingBufferWidth, gl.drawingBufferHeight);
    }
  } catch (er) {
    throw new Error(er);
  }
};
//detect if user didn't set the camera
//then call this function below
p5.RendererGL.prototype._setDefaultCamera = function(){
  if(this._curCamera === null){
    var _w = this.width;
    var _h = this.height;
    this.uPMatrix = p5.Matrix.identity();
    this.uPMatrix.perspective(60 / 180 * Math.PI, _w / _h, 0.1, 100);
    this._curCamera = 'default';
  }
};

p5.RendererGL.prototype._update = function() {
  this.uMVMatrix = p5.Matrix.identity();
  this.translate(0, 0, -(this.height / 2) / Math.tan(Math.PI * 30 / 180));
  this.ambientLightCount = 0;
  this.directionalLightCount = 0;
  this.pointLightCount = 0;
};

/**
 * [background description]
 * @return {[type]} [description]
 */
p5.RendererGL.prototype.background = function() {
  var gl = this.GL;
  var _col = this._pInst.color.apply(this._pInst, arguments);
  var _r = (_col.levels[0]) / 255;
  var _g = (_col.levels[1]) / 255;
  var _b = (_col.levels[2]) / 255;
  var _a = (_col.levels[3]) / 255;
  gl.clearColor(_r, _g, _b, _a);
  gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
};

//@TODO implement this
// p5.RendererGL.prototype.clear = function() {
//@TODO
// };

//////////////////////////////////////////////
// SHADER
//////////////////////////////////////////////

/**
 * [_initShaders description]
 * @param  {string} vertId [description]
 * @param  {string} fragId [description]
 * @return {[type]}        [description]
 */
p5.RendererGL.prototype._initShaders =
function(vertId, fragId, isImmediateMode) {
  var gl = this.GL;
  //set up our default shaders by:
  // 1. create the shader,
  // 2. load the shader source,
  // 3. compile the shader
  var _vertShader = gl.createShader(gl.VERTEX_SHADER);
  //load in our default vertex shader
  gl.shaderSource(_vertShader, shader[vertId]);
  gl.compileShader(_vertShader);
  // if our vertex shader failed compilation?
  if (!gl.getShaderParameter(_vertShader, gl.COMPILE_STATUS)) {
    alert('Yikes! An error occurred compiling the shaders:' +
      gl.getShaderInfoLog(_vertShader));
    return null;
  }

  var _fragShader = gl.createShader(gl.FRAGMENT_SHADER);
  //load in our material frag shader
  gl.shaderSource(_fragShader, shader[fragId]);
  gl.compileShader(_fragShader);
  // if our frag shader failed compilation?
  if (!gl.getShaderParameter(_fragShader, gl.COMPILE_STATUS)) {
    alert('Darn! An error occurred compiling the shaders:' +
      gl.getShaderInfoLog(_fragShader));
    return null;
  }

  var shaderProgram = gl.createProgram();
  gl.attachShader(shaderProgram, _vertShader);
  gl.attachShader(shaderProgram, _fragShader);
  gl.linkProgram(shaderProgram);
  if (!gl.getProgramParameter(shaderProgram, gl.LINK_STATUS)) {
    alert('Snap! Error linking shader program');
  }
  //END SHADERS SETUP

  this._getLocation(shaderProgram, isImmediateMode);

  return shaderProgram;
};

p5.RendererGL.prototype._getLocation =
function(shaderProgram, isImmediateMode) {
  var gl = this.GL;
  gl.useProgram(shaderProgram);
  shaderProgram.uResolution =
    gl.getUniformLocation(shaderProgram, 'uResolution');
  gl.uniform1f(shaderProgram.uResolution, RESOLUTION);

  //projection Matrix uniform
  shaderProgram.uPMatrixUniform =
    gl.getUniformLocation(shaderProgram, 'uProjectionMatrix');
  //model view Matrix uniform
  shaderProgram.uMVMatrixUniform =
    gl.getUniformLocation(shaderProgram, 'uModelViewMatrix');

  //@TODO: figure out a better way instead of if statement
  if(isImmediateMode === undefined){
    //normal Matrix uniform
    shaderProgram.uNMatrixUniform =
    gl.getUniformLocation(shaderProgram, 'uNormalMatrix');

    shaderProgram.samplerUniform =
    gl.getUniformLocation(shaderProgram, 'uSampler');
  }
};

/**
 * Sets a shader uniform given a shaderProgram and uniform string
 * @param {String} shaderKey key to material Hash.
 * @param {String} uniform location in shader.
 * @param { Number} data data to bind uniform.  Float data type.
 * @todo currently this function sets uniform1f data.
 * Should generalize function to accept any uniform
 * data type.
 */
p5.RendererGL.prototype._setUniform1f = function(shaderKey,uniform,data)
{
  var gl = this.GL;
  var shaderProgram = this.mHash[shaderKey];
  gl.useProgram(shaderProgram);
  shaderProgram[uniform] = gl.getUniformLocation(shaderProgram, uniform);
  gl.uniform1f(shaderProgram[uniform], data);
  return this;
};

p5.RendererGL.prototype._setMatrixUniforms = function(shaderKey) {
  var gl = this.GL;
  var shaderProgram = this.mHash[shaderKey];

  gl.useProgram(shaderProgram);

  gl.uniformMatrix4fv(
    shaderProgram.uPMatrixUniform,
    false, this.uPMatrix.mat4);

  gl.uniformMatrix4fv(
    shaderProgram.uMVMatrixUniform,
    false, this.uMVMatrix.mat4);

  this.uNMatrix.inverseTranspose(this.uMVMatrix);

  gl.uniformMatrix3fv(
    shaderProgram.uNMatrixUniform,
    false, this.uNMatrix.mat3);
};
//////////////////////////////////////////////
// GET CURRENT | for shader and color
//////////////////////////////////////////////
p5.RendererGL.prototype._getShader = function(vertId, fragId, isImmediateMode) {
  var mId = vertId + '|' + fragId;
  //create it and put it into hashTable
  if(!this.materialInHash(mId)){
    var shaderProgram = this._initShaders(vertId, fragId, isImmediateMode);
    this.mHash[mId] = shaderProgram;
  }
  this.curShaderId = mId;

  return this.mHash[this.curShaderId];
};

p5.RendererGL.prototype._getCurShaderId = function(){
  //if the shader ID is not yet defined
  var mId, shaderProgram;
  if(this.drawMode !== 'fill' && this.curShaderId === undefined){
    //default shader: normalMaterial()
    mId = 'normalVert|normalFrag';
    shaderProgram = this._initShaders('normalVert', 'normalFrag');
    this.mHash[mId] = shaderProgram;
    this.curShaderId = mId;
  } else if(this.isImmediateDrawing && this.drawMode === 'fill'){
    mId = 'immediateVert|vertexColorFrag';
    shaderProgram = this._initShaders('immediateVert', 'vertexColorFrag');
    this.mHash[mId] = shaderProgram;
    this.curShaderId = mId;
  }
  return this.curShaderId;
};

//////////////////////////////////////////////
// COLOR
//////////////////////////////////////////////
/**
 * Basic fill material for geometry with a given color
 * @method  fill
 * @param  {Number|Array|String|p5.Color} v1  gray value,
 * red or hue value (depending on the current color mode),
 * or color Array, or CSS color string
 * @param  {Number}            [v2] optional: green or saturation value
 * @param  {Number}            [v3] optional: blue or brightness value
 * @param  {Number}            [a]  optional: opacity
 * @return {p5}                the p5 object
 * @example
 * <div>
 * <code>
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *  background(0);
 *  fill(250, 0, 0);
 *  rotateX(frameCount * 0.01);
 *  rotateY(frameCount * 0.01);
 *  rotateZ(frameCount * 0.01);
 *  box(200, 200, 200);
 * }
 * </code>
 * </div>
 *
 * @alt
 * red canvas
 *
 */
p5.RendererGL.prototype.fill = function(v1, v2, v3, a) {
  var gl = this.GL;
  var shaderProgram;
  //see material.js for more info on color blending in webgl
  var colors = this._applyColorBlend.apply(this, arguments);
  this.curFillColor = colors;
  this.drawMode = 'fill';
  if(this.isImmediateDrawing){
    shaderProgram =
    this._getShader('immediateVert','vertexColorFrag');
    gl.useProgram(shaderProgram);
  } else {
    shaderProgram =
    this._getShader('normalVert', 'basicFrag');
    gl.useProgram(shaderProgram);
    //RetainedMode uses a webgl uniform to pass color vals
    //in ImmediateMode, we want access to each vertex so therefore
    //we cannot use a uniform.
    shaderProgram.uMaterialColor = gl.getUniformLocation(
      shaderProgram, 'uMaterialColor' );
    gl.uniform4f( shaderProgram.uMaterialColor,
      colors[0],
      colors[1],
      colors[2],
      colors[3]);
  }
  return this;
};
p5.RendererGL.prototype.stroke = function(r, g, b, a) {
  var color = this._pInst.color.apply(this._pInst, arguments);
  var colorNormalized = color._array;
  this.curStrokeColor = colorNormalized;
  this.drawMode = 'stroke';
  return this;
};

//@TODO
p5.RendererGL.prototype._strokeCheck = function(){
  if(this.drawMode === 'stroke'){
    throw new Error(
      'stroke for shapes in 3D not yet implemented, use fill for now :('
    );
  }
};

/**
 * [strokeWeight description]
 * @param  {Number} pointSize stroke point size
 * @return {[type]}           [description]
 * @todo  strokeWeight currently works on points only.
 * implement on all wireframes and strokes.
 */
p5.RendererGL.prototype.strokeWeight = function(pointSize) {
  this.pointSize = pointSize;
  return this;
};
//////////////////////////////////////////////
// HASH | for material and geometry
//////////////////////////////////////////////

p5.RendererGL.prototype.geometryInHash = function(gId){
  return this.gHash[gId] !== undefined;
};

p5.RendererGL.prototype.materialInHash = function(mId){
  return this.mHash[mId] !== undefined;
};

/**
 * [resize description]
 * @param  {[type]} w [description]
 * @param  {[tyoe]} h [description]
 * @return {[type]}   [description]
 */
p5.RendererGL.prototype.resize = function(w,h) {
  var gl = this.GL;
  p5.Renderer.prototype.resize.call(this, w, h);
  gl.viewport(0, 0, gl.drawingBufferWidth, gl.drawingBufferHeight);
  // If we're using the default camera, update the aspect ratio
  if(this._curCamera === 'default') {
    this._curCamera = null;
    this._setDefaultCamera();
  }
};

/**
 * clears color and depth buffers
 * with r,g,b,a
 * @param {Number} r normalized red val.
 * @param {Number} g normalized green val.
 * @param {Number} b normalized blue val.
 * @param {Number} a normalized alpha val.
 */
p5.RendererGL.prototype.clear = function() {
  var gl = this.GL;
  gl.clearColor(arguments[0],
    arguments[1],
    arguments[2],
    arguments[3]);
  gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
};

/**
 * [translate description]
 * @param  {[type]} x [description]
 * @param  {[type]} y [description]
 * @param  {[type]} z [description]
 * @return {[type]}   [description]
 * @todo implement handle for components or vector as args
 */
p5.RendererGL.prototype.translate = function(x, y, z) {
  //@TODO: figure out how to fit the resolution
  x = x / RESOLUTION;
  y = -y / RESOLUTION;
  z = z / RESOLUTION;
  this.uMVMatrix.translate([x,y,z]);
  return this;
};

/**
 * Scales the Model View Matrix by a vector
 * @param  {Number | p5.Vector | Array} x [description]
 * @param  {Number} [y] y-axis scalar
 * @param  {Number} [z] z-axis scalar
 * @return {this}   [description]
 */
p5.RendererGL.prototype.scale = function(x,y,z) {
  this.uMVMatrix.scale([x,y,z]);
  return this;
};

p5.RendererGL.prototype.rotate = function(rad, axis){
  this.uMVMatrix.rotate(rad, axis);
  return this;
};

p5.RendererGL.prototype.rotateX = function(rad) {
  this.rotate(rad, [1,0,0]);
  return this;
};

p5.RendererGL.prototype.rotateY = function(rad) {
  this.rotate(rad, [0,1,0]);
  return this;
};

p5.RendererGL.prototype.rotateZ = function(rad) {
  this.rotate(rad, [0,0,1]);
  return this;
};

/**
 * pushes a copy of the model view matrix onto the
 * MV Matrix stack.
 */
p5.RendererGL.prototype.push = function() {
  uMVMatrixStack.push(this.uMVMatrix.copy());
};

/**
 * [pop description]
 * @return {[type]} [description]
 */
p5.RendererGL.prototype.pop = function() {
  if (uMVMatrixStack.length === 0) {
    throw new Error('Invalid popMatrix!');
  }
  this.uMVMatrix = uMVMatrixStack.pop();
};

p5.RendererGL.prototype.resetMatrix = function() {
  this.uMVMatrix = p5.Matrix.identity();
  this.translate(0, 0, -800);
  return this;
};

// Text/Typography
// @TODO:
p5.RendererGL.prototype._applyTextProperties = function() {
  //@TODO finish implementation
  console.error('text commands not yet implemented in webgl');
};
module.exports = p5.RendererGL;

},{"../core/core":39,"../core/p5.Renderer":45,"./p5.Matrix":85,"./shader":90}],89:[function(_dereq_,module,exports){
/**
 * @module Shape
 * @submodule 3D Primitives
 * @for p5
 * @requires core
 * @requires p5.Geometry
 */

'use strict';

var p5 = _dereq_('../core/core');
_dereq_('./p5.Geometry');
/**
 * Draw a plane with given a width and height
 * @method plane
 * @param  {Number} width      width of the plane
 * @param  {Number} height     height of the plane
 * @param  {Number} [detailX]  Optional number of triangle
 *                             subdivisions in x-dimension
 * @param {Number} [detailY]   Optional number of triangle
 *                             subdivisions in y-dimension
 * @return {p5}                the p5 object
 * @example
 * <div>
 * <code>
 * //draw a plane with width 200 and height 200
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(200);
 *   plane(200, 200);
 * }
 * </code>
 * </div>
 *
 * @alt
 * Nothing displayed on canvas
 * Rotating interior view of a box with sides that change color.
 * 3d red and green gradient.
 * Rotating interior view of a cylinder with sides that change color.
 * Rotating view of a cylinder with sides that change color.
 * 3d red and green gradient.
 * rotating view of a multi-colored cylinder with concave sides.
 */
p5.prototype.plane = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  var width = args[0] || 50;
  var height = args[1] || width;
  var detailX = typeof args[2] === 'number' ? args[2] : 1;
  var detailY = typeof args[3] === 'number' ? args[3] : 1;

  var gId = 'plane|'+width+'|'+height+'|'+detailX+'|'+detailY;

  if(!this._renderer.geometryInHash(gId)){
    var _plane = function(){
      var u,v,p;
      for (var i = 0; i <= this.detailY; i++){
        v = i / this.detailY;
        for (var j = 0; j <= this.detailX; j++){
          u = j / this.detailX;
          p = new p5.Vector(width * u - width/2,
            height * v - height/2,
            0);
          this.vertices.push(p);
          this.uvs.push([u,v]);
        }
      }
    };
    var planeGeom =
    new p5.Geometry(detailX, detailY, _plane);
    planeGeom
      .computeFaces()
      .computeNormals();
    this._renderer.createBuffers(gId, planeGeom);
  }

  this._renderer.drawBuffers(gId);

};

/**
 * Draw a box with given width, height and depth
 * @method  box
 * @param  {Number} width     width of the box
 * @param  {Number} Height    height of the box
 * @param  {Number} depth     depth of the box
 * @param {Number} [detailX]  Optional number of triangle
 *                            subdivisions in x-dimension
 * @param {Number} [detailY]  Optional number of triangle
 *                            subdivisions in y-dimension
 * @return {p5}               the p5 object
 * @example
 * <div>
 * <code>
 * //draw a spinning box with width, height and depth 200
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(200);
 *   rotateX(frameCount * 0.01);
 *   rotateY(frameCount * 0.01);
 *   box(200, 200, 200);
 * }
 * </code>
 * </div>
 */
p5.prototype.box = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  var width = args[0] || 50;
  var height = args[1] || width;
  var depth = args[2] || width;

  var detailX = typeof args[3] === 'number' ? args[3] : 4;
  var detailY = typeof args[4] === 'number' ? args[4] : 4;
  var gId = 'box|'+width+'|'+height+'|'+depth+'|'+detailX+'|'+detailY;

  if(!this._renderer.geometryInHash(gId)){
    var _box = function(){
      var cubeIndices = [
        [0, 4, 2, 6],// -1, 0, 0],// -x
        [1, 3, 5, 7],// +1, 0, 0],// +x
        [0, 1, 4, 5],// 0, -1, 0],// -y
        [2, 6, 3, 7],// 0, +1, 0],// +y
        [0, 2, 1, 3],// 0, 0, -1],// -z
        [4, 5, 6, 7]// 0, 0, +1] // +z
      ];
      var id=0;
      for (var i = 0; i < cubeIndices.length; i++) {
        var cubeIndex = cubeIndices[i];
        var v = i * 4;
        for (var j = 0; j < 4; j++) {
          var d = cubeIndex[j];
          //inspired by lightgl:
          //https://github.com/evanw/lightgl.js
          //octants:https://en.wikipedia.org/wiki/Octant_(solid_geometry)
          var octant = new p5.Vector(
            ((d & 1) * 2 - 1)*width/2,
            ((d & 2) - 1) *height/2,
            ((d & 4) / 2 - 1) * depth/2);
          this.vertices.push( octant );
          this.uvs.push([j & 1, (j & 2) / 2]);
          id++;
        }
        this.faces.push([v, v + 1, v + 2]);
        this.faces.push([v + 2, v + 1, v + 3]);
      }
    };
    var boxGeom = new p5.Geometry(detailX,detailY, _box);
    boxGeom.computeNormals();
    //initialize our geometry buffer with
    //the key val pair:
    //geometry Id, Geom object
    this._renderer.createBuffers(gId, boxGeom);
  }
  this._renderer.drawBuffers(gId);

  return this;

};

/**
 * Draw a sphere with given radius
 * @method sphere
 * @param  {Number} radius            radius of circle
 * @param  {Number} [detailX]         optional: number of segments,
 *                                    the more segments the smoother geometry
 *                                    default is 24
 * @param  {Number} [detailY]         optional: number of segments,
 *                                    the more segments the smoother geometry
 *                                    default is 16
 * @return {p5}                       the p5 object
 * @example
 * <div>
 * <code>
 * // draw a sphere with radius 200
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(200);
 *   sphere(50);
 * }
 * </code>
 * </div>
 */
p5.prototype.sphere = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  //@todo validate params here
  //
  var radius = args[0] || 50;
  var detailX = typeof args[1] === 'number' ? args[1] : 24;
  var detailY = typeof args[2] === 'number' ? args[2] : 16;
  var gId = 'sphere|'+radius+'|'+detailX+'|'+detailY;
  if(!this._renderer.geometryInHash(gId)){
    var _sphere = function(){
      var u,v,p;
      for (var i = 0; i <= this.detailY; i++){
        v = i / this.detailY;
        for (var j = 0; j <= this.detailX; j++){
          u = j / this.detailX;
          var theta = 2 * Math.PI * u;
          var phi = Math.PI * v - Math.PI / 2;
          p = new p5.Vector(radius * Math.cos(phi) * Math.sin(theta),
            radius * Math.sin(phi),
            radius * Math.cos(phi) * Math.cos(theta));
          this.vertices.push(p);
          this.uvs.push([u,v]);
        }
      }
    };
    var sphereGeom = new p5.Geometry(detailX, detailY, _sphere);
    sphereGeom
      .computeFaces()
      .computeNormals()
      .averageNormals()
      .averagePoleNormals();
    this._renderer.createBuffers(gId, sphereGeom);
  }
  this._renderer.drawBuffers(gId);

  return this;
};


/**
* @private
* helper function for creating both cones and cyllinders
*/
var _truncatedCone = function(
  bottomRadius,
  topRadius,
  height,
  detailX,
  detailY,
  topCap,
  bottomCap) {
  detailX = (detailX < 3) ? 3 : detailX;
  detailY = (detailY < 1) ? 1 : detailY;
  topCap = (topCap === undefined) ? true : topCap;
  bottomCap = (bottomCap === undefined) ? true : bottomCap;
  var extra = (topCap ? 2 : 0) + (bottomCap ? 2 : 0);
  var vertsAroundEdge = detailX + 1;

  // ensure constant slant
  var slant = Math.atan2(bottomRadius - topRadius, height);
  var start = topCap ? -2 : 0;
  var end = detailY + (bottomCap ? 2 : 0);
  var yy, ii;
  for (yy = start; yy <= end; ++yy) {
    var v = yy / detailY;
    var y = height * v;
    var ringRadius;
    if (yy < 0) {
      y = 0;
      v = 1;
      ringRadius = bottomRadius;
    } else if (yy > detailY) {
      y = height;
      v = 1;
      ringRadius = topRadius;
    } else {
      ringRadius = bottomRadius +
        (topRadius - bottomRadius) * (yy / detailY);
    }
    if (yy === -2 || yy === detailY + 2) {
      ringRadius = 0;
      v = 0;
    }
    y -= height / 2;
    for (ii = 0; ii < vertsAroundEdge; ++ii) {
      //VERTICES
      this.vertices.push(
        new p5.Vector(
          Math.sin(ii*Math.PI * 2 /detailX) * ringRadius,
          y,
          Math.cos(ii*Math.PI * 2 /detailX) * ringRadius)
        );
      //VERTEX NORMALS
      this.vertexNormals.push(
        new p5.Vector(
          (yy < 0 || yy > detailY) ? 0 :
          (Math.sin(ii * Math.PI * 2 / detailX) * Math.cos(slant)),
          (yy < 0) ? -1 : (yy > detailY ? 1 : Math.sin(slant)),
          (yy < 0 || yy > detailY) ? 0 :
          (Math.cos(ii * Math.PI * 2 / detailX) * Math.cos(slant)))
        );
      //UVs
      this.uvs.push([(ii / detailX), v]);
    }
  }
  for (yy = 0; yy < detailY + extra; ++yy) {
    for (ii = 0; ii < detailX; ++ii) {
      this.faces.push([vertsAroundEdge * (yy + 0) + 0 + ii,
        vertsAroundEdge * (yy + 0) + 1 + ii,
        vertsAroundEdge * (yy + 1) + 1 + ii]);
      this.faces.push([vertsAroundEdge * (yy + 0) + 0 + ii,
        vertsAroundEdge * (yy + 1) + 1 + ii,
        vertsAroundEdge * (yy + 1) + 0 + ii]);
    }
  }
};

/**
 * Draw a cylinder with given radius and height
 * @method  cylinder
 * @param  {Number} radius     radius of the surface
 * @param  {Number} height     height of the cylinder
 * @param  {Number} [detailX]  optional: number of segments,
 *                             the more segments the smoother geometry
 *                             default is 24
 * @param {Number} [detailY]   optional: number of segments in y-dimension,
 *                             the more segments the smoother geometry
 *                             default is 16
 * @return {p5}                the p5 object
 * @example
 * <div>
 * <code>
 * //draw a spinning cylinder with radius 200 and height 200
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(200);
 *   rotateX(frameCount * 0.01);
 *   rotateZ(frameCount * 0.01);
 *   cylinder(200, 200);
 * }
 * </code>
 * </div>
 */
p5.prototype.cylinder = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  var radius = args[0] || 50;
  var height = args[1] || radius;
  var detailX = typeof args[2] === 'number' ? args[2] : 24;
  var detailY = typeof args[3] === 'number' ? args[3] : 16;
  var gId = 'cylinder|'+radius+'|'+height+'|'+detailX+'|'+detailY;
  if(!this._renderer.geometryInHash(gId)){
    var cylinderGeom = new p5.Geometry(detailX, detailY);
    _truncatedCone.call(
      cylinderGeom,
      radius,
      radius,
      height,
      detailX,
      detailY,
      true,true);
    cylinderGeom.computeNormals();
    this._renderer.createBuffers(gId, cylinderGeom);
  }

  this._renderer.drawBuffers(gId);

  return this;
};


/**
 * Draw a cone with given radius and height
 * @method cone
 * @param  {Number} radius            radius of the bottom surface
 * @param  {Number} height            height of the cone
 * @param  {Number} [detailX]         optional: number of segments,
 *                                    the more segments the smoother geometry
 *                                    default is 24
 * @param  {Number} [detailY]         optional: number of segments,
 *                                    the more segments the smoother geometry
 *                                    default is 16
 * @return {p5}                       the p5 object
 * @example
 * <div>
 * <code>
 * //draw a spinning cone with radius 200 and height 200
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(200);
 *   rotateX(frameCount * 0.01);
 *   rotateZ(frameCount * 0.01);
 *   cone(200, 200);
 * }
 * </code>
 * </div>
 */
p5.prototype.cone = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  var baseRadius = args[0] || 50;
  var height = args[1] || baseRadius;
  var detailX = typeof args[2] === 'number' ? args[2] : 24;
  var detailY = typeof args[3] === 'number' ? args[3] : 16;
  var gId = 'cone|'+baseRadius+'|'+height+'|'+detailX+'|'+detailY;
  if(!this._renderer.geometryInHash(gId)){
    var coneGeom = new p5.Geometry(detailX, detailY);
    _truncatedCone.call(coneGeom,
      baseRadius,
      0,//top radius 0
      height,
      detailX,
      detailY,
      true,
      true);
    //for cones we need to average Normals
    coneGeom
      .computeNormals();
    this._renderer.createBuffers(gId, coneGeom);
  }

  this._renderer.drawBuffers(gId);

  return this;
};

/**
 * Draw an ellipsoid with given raduis
 * @method ellipsoid
 * @param  {Number} radiusx           xradius of circle
 * @param  {Number} radiusy           yradius of circle
 * @param  {Number} radiusz           zradius of circle
 * @param  {Number} [detailX]         optional: number of segments,
 *                                    the more segments the smoother geometry
 *                                    default is 24. Avoid detail number above
 *                                    150, it may crash the browser.
 * @param  {Number} [detailY]         optional: number of segments,
 *                                    the more segments the smoother geometry
 *                                    default is 16. Avoid detail number above
 *                                    150, it may crash the browser.
 * @return {p5}                       the p5 object
 * @example
 * <div>
 * <code>
 * // draw an ellipsoid with radius 20, 30 and 40.
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(200);
 *   ellipsoid(20, 30, 40);
 * }
 * </code>
 * </div>
 */
p5.prototype.ellipsoid = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  var detailX = typeof args[3] === 'number' ? args[3] : 24;
  var detailY = typeof args[4] === 'number' ? args[4] : 24;
  var radiusX = args[0] || 50;
  var radiusY = args[1] || radiusX;
  var radiusZ = args[2] || radiusX;

  var gId = 'ellipsoid|'+radiusX+'|'+radiusY+
  '|'+radiusZ+'|'+detailX+'|'+detailY;


  if(!this._renderer.geometryInHash(gId)){
    var _ellipsoid = function(){
      var u,v,p;
      for (var i = 0; i <= this.detailY; i++){
        v = i / this.detailY;
        for (var j = 0; j <= this.detailX; j++){
          u = j / this.detailX;
          var theta = 2 * Math.PI * u;
          var phi = Math.PI * v - Math.PI / 2;
          p = new p5.Vector(radiusX * Math.cos(phi) * Math.sin(theta),
            radiusY * Math.sin(phi),
            radiusZ * Math.cos(phi) * Math.cos(theta));
          this.vertices.push(p);
          this.uvs.push([u,v]);
        }
      }
    };
    var ellipsoidGeom = new p5.Geometry(detailX, detailY,_ellipsoid);
    ellipsoidGeom
      .computeFaces()
      .computeNormals();
    this._renderer.createBuffers(gId, ellipsoidGeom);
  }

  this._renderer.drawBuffers(gId);

  return this;
};

/**
 * Draw a torus with given radius and tube radius
 * @method torus
 * @param  {Number} radius        radius of the whole ring
 * @param  {Number} tubeRadius    radius of the tube
 * @param  {Number} [detailX]     optional: number of segments in x-dimension,
 *                                the more segments the smoother geometry
 *                                default is 24
 * @param  {Number} [detailY]     optional: number of segments in y-dimension,
 *                                the more segments the smoother geometry
 *                                default is 16
 * @return {p5}                   the p5 object
 * @example
 * <div>
 * <code>
 * //draw a spinning torus with radius 200 and tube radius 60
 * function setup(){
 *   createCanvas(100, 100, WEBGL);
 * }
 *
 * function draw(){
 *   background(200);
 *   rotateX(frameCount * 0.01);
 *   rotateY(frameCount * 0.01);
 *   torus(200, 60);
 * }
 * </code>
 * </div>
 */
p5.prototype.torus = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  var detailX = typeof args[2] === 'number' ? args[2] : 24;
  var detailY = typeof args[3] === 'number' ? args[3] : 16;

  var radius = args[0] || 50;
  var tubeRadius = args[1] || 10;

  var gId = 'torus|'+radius+'|'+tubeRadius+'|'+detailX+'|'+detailY;

  if(!this._renderer.geometryInHash(gId)){
    var _torus = function(){
      var u,v,p;
      for (var i = 0; i <= this.detailY; i++){
        v = i / this.detailY;
        for (var j = 0; j <= this.detailX; j++){
          u = j / this.detailX;
          var theta = 2 * Math.PI * u;
          var phi = 2 * Math.PI * v;
          p = new p5.Vector(
            (radius + tubeRadius * Math.cos(phi)) * Math.cos(theta),
            (radius + tubeRadius * Math.cos(phi)) * Math.sin(theta),
            tubeRadius * Math.sin(phi));
          this.vertices.push(p);
          this.uvs.push([u,v]);
        }
      }
    };
    var torusGeom = new p5.Geometry(detailX, detailY, _torus);
    torusGeom
      .computeFaces()
      .computeNormals()
      .averageNormals();
    this._renderer.createBuffers(gId, torusGeom);
  }

  this._renderer.drawBuffers(gId);

  return this;
};

///////////////////////
/// 2D primitives
/////////////////////////

//@TODO
p5.RendererGL.prototype.point = function(x, y, z){
  console.log('point not yet implemented in webgl');
  return this;
};

p5.RendererGL.prototype.triangle = function
(args){
  var x1=args[0], y1=args[1];
  var x2=args[2], y2=args[3];
  var x3=args[4], y3=args[5];
  var gId = 'tri|'+x1+'|'+y1+'|'+
  x2+'|'+y2+'|'+
  x3+'|'+y3;
  if(!this.geometryInHash(gId)){
    var _triangle = function(){
      var vertices = [];
      vertices.push(new p5.Vector(x1,y1,0));
      vertices.push(new p5.Vector(x2,y2,0));
      vertices.push(new p5.Vector(x3,y3,0));
      this.vertices = vertices;
      this.faces = [[0,1,2]];
      this.uvs = [[0,0],[0,1],[1,1]];
    };
    var triGeom = new p5.Geometry(1,1,_triangle);
    triGeom.computeNormals();
    this.createBuffers(gId, triGeom);
  }

  this.drawBuffers(gId);
  return this;
};

p5.RendererGL.prototype.ellipse = function
(args){
  var x = args[0];
  var y = args[1];
  var width = args[2];
  var height = args[3];
  //detailX and Y are optional 6th & 7th
  //arguments
  var detailX = args[4] || 24;
  var detailY = args[5] || 16;
  var gId = 'ellipse|'+args[0]+'|'+args[1]+'|'+args[2]+'|'+
  args[3];
  if(!this.geometryInHash(gId)){
    var _ellipse = function(){
      var u,v,p;
      var centerX = x+width*0.5;
      var centerY = y+height*0.5;
      for (var i = 0; i <= this.detailY; i++){
        v = i / this.detailY;
        for (var j = 0; j <= this.detailX; j++){
          u = j / this.detailX;
          var theta = 2 * Math.PI * u;
          if(v === 0){
            p = new p5.Vector(centerX, centerY, 0);
          }
          else{
            var _x = centerX + width*0.5 * Math.cos(theta);
            var _y = centerY + height*0.5 * Math.sin(theta);
            p = new p5.Vector(_x, _y, 0);
          }
          this.vertices.push(p);
          this.uvs.push([u,v]);
        }
      }
    };
    var ellipseGeom = new p5.Geometry(detailX,detailY,_ellipse);
    ellipseGeom
      .computeFaces()
      .computeNormals();
    this.createBuffers(gId, ellipseGeom);
  }
  this.drawBuffers(gId);
  return this;
};

p5.RendererGL.prototype.rect = function
(args){
  var gId = 'rect|'+args[0]+'|'+args[1]+'|'+args[2]+'|'+
  args[3];
  var x = args[0];
  var y = args[1];
  var width = args[2];
  var height = args[3];
  var detailX = args[4] || 24;
  var detailY = args[5] || 16;
  if(!this.geometryInHash(gId)){
    var _rect = function(){
      var u,v,p;
      for (var i = 0; i <= this.detailY; i++){
        v = i / this.detailY;
        for (var j = 0; j <= this.detailX; j++){
          u = j / this.detailX;
          // var _x = x-width/2;
          // var _y = y-height/2;
          p = new p5.Vector(
            x + (width*u),
            y + (height*v),
            0
          );
          this.vertices.push(p);
          this.uvs.push([u,v]);
        }
      }
    };
    var rectGeom = new p5.Geometry(detailX,detailY,_rect);
    rectGeom
      .computeFaces()
      .computeNormals();
    this.createBuffers(gId, rectGeom);
  }
  this.drawBuffers(gId);
  return this;
};

p5.RendererGL.prototype.quad = function(){
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }
  //@todo validate params here
  //
  var x1 = args[0],
    y1 = args[1],
    x2 = args[2],
    y2 = args[3],
    x3 = args[4],
    y3 = args[5],
    x4 = args[6],
    y4 = args[7];
  var gId = 'quad|'+x1+'|'+y1+'|'+
  x2+'|'+y2+'|'+
  x3+'|'+y3+'|'+
  x4+'|'+y4;
  if(!this.geometryInHash(gId)){
    var _quad = function(){
      this.vertices.push(new p5.Vector(x1,y1,0));
      this.vertices.push(new p5.Vector(x2,y2,0));
      this.vertices.push(new p5.Vector(x3,y3,0));
      this.vertices.push(new p5.Vector(x4,y4,0));
      this.uvs.push([0, 0], [1, 0], [1, 1], [0, 1]);
    };
    var quadGeom = new p5.Geometry(2,2,_quad);
    quadGeom.computeNormals();
    quadGeom.faces = [[0,1,2],[2,3,0]];
    this.createBuffers(gId, quadGeom);
  }
  this.drawBuffers(gId);
  return this;
};

//this implementation of bezier curve
//is based on Bernstein polynomial
p5.RendererGL.prototype.bezier = function
(args){
  var bezierDetail=args[12] || 20;//value of Bezier detail
  this.beginShape();
  var coeff=[0,0,0,0];//  Bernstein polynomial coeffecients
  var vertex=[0,0,0]; //(x,y,z) coordinates of points in bezier curve
  for(var i=0; i<=bezierDetail; i++){
    coeff[0]=Math.pow(1-(i/bezierDetail),3);
    coeff[1]=(3*(i/bezierDetail)) * (Math.pow(1-(i/bezierDetail),2));
    coeff[2]=(3*Math.pow(i/bezierDetail,2)) * (1-(i/bezierDetail));
    coeff[3]=Math.pow(i/bezierDetail,3);
    vertex[0]=args[0]*coeff[0] + args[3]*coeff[1] +
              args[6]*coeff[2] + args[9]*coeff[3];
    vertex[1]=args[1]*coeff[0] + args[4]*coeff[1] +
              args[7]*coeff[2] + args[10]*coeff[3];
    vertex[2]=args[2]*coeff[0] + args[5]*coeff[1] +
              args[8]*coeff[2] + args[11]*coeff[3];
    this.vertex(vertex[0],vertex[1],vertex[2]);
  }
  this.endShape();
  return this;
};

p5.RendererGL.prototype.curve=function
(args){
  var curveDetail=args[12];
  this.beginShape();
  var coeff=[0,0,0,0];//coeffecients of the equation
  var vertex=[0,0,0]; //(x,y,z) coordinates of points in bezier curve
  for(var i=0; i<=curveDetail; i++){
    coeff[0]=Math.pow((i/curveDetail),3) * 0.5;
    coeff[1]=Math.pow((i/curveDetail),2) * 0.5;
    coeff[2]=(i/curveDetail) * 0.5;
    coeff[3]=0.5;
    vertex[0]=coeff[0]*(-args[0] + (3*args[3]) - (3*args[6]) +args[9]) +
              coeff[1]*((2*args[0]) - (5*args[3]) + (4*args[6]) - args[9]) +
              coeff[2]*(-args[0] + args[6]) +
              coeff[3]*(2*args[3]);
    vertex[1]=coeff[0]*(-args[1] + (3*args[4]) - (3*args[7]) +args[10]) +
              coeff[1]*((2*args[1]) - (5*args[4]) + (4*args[7]) - args[10]) +
              coeff[2]*(-args[1] + args[7]) +
              coeff[3]*(2*args[4]);
    vertex[2]=coeff[0]*(-args[2] + (3*args[5]) - (3*args[8]) +args[11]) +
              coeff[1]*((2*args[2]) - (5*args[5]) + (4*args[8]) - args[11]) +
              coeff[2]*(-args[2] + args[8]) +
              coeff[3]*(2*args[5]);
    this.vertex(vertex[0],vertex[1],vertex[2]);
  }
  this.endShape();
  return this;
};

module.exports = p5;

},{"../core/core":39,"./p5.Geometry":84}],90:[function(_dereq_,module,exports){


module.exports = {
  immediateVert:
    "attribute vec3 aPosition;\nattribute vec4 aVertexColor;\n\nuniform mat4 uModelViewMatrix;\nuniform mat4 uProjectionMatrix;\nuniform float uResolution;\nuniform float uPointSize;\n\nvarying vec4 vColor;\nvoid main(void) {\n  vec4 positionVec4 = vec4(aPosition / uResolution *vec3(1.0, -1.0, 1.0), 1.0);\n  gl_Position = uProjectionMatrix * uModelViewMatrix * positionVec4;\n  vColor = aVertexColor;\n  gl_PointSize = uPointSize;\n}\n",
  vertexColorVert:
    "attribute vec3 aPosition;\nattribute vec4 aVertexColor;\n\nuniform mat4 uModelViewMatrix;\nuniform mat4 uProjectionMatrix;\nuniform float uResolution;\n\nvarying vec4 vColor;\n\nvoid main(void) {\n  vec4 positionVec4 = vec4(aPosition / uResolution * vec3(1.0, -1.0, 1.0), 1.0);\n  gl_Position = uProjectionMatrix * uModelViewMatrix * positionVec4;\n  vColor = aVertexColor;\n}\n",
  vertexColorFrag:
    "precision mediump float;\nvarying vec4 vColor;\nvoid main(void) {\n  gl_FragColor = vColor;\n}",
  normalVert:
    "attribute vec3 aPosition;\nattribute vec3 aNormal;\nattribute vec2 aTexCoord;\n\nuniform mat4 uModelViewMatrix;\nuniform mat4 uProjectionMatrix;\nuniform mat3 uNormalMatrix;\nuniform float uResolution;\n\nvarying vec3 vVertexNormal;\nvarying highp vec2 vVertTexCoord;\n\nvoid main(void) {\n  vec4 positionVec4 = vec4(aPosition / uResolution * vec3(1.0, -1.0, 1.0), 1.0);\n  gl_Position = uProjectionMatrix * uModelViewMatrix * positionVec4;\n  vVertexNormal = vec3( uNormalMatrix * aNormal );\n  vVertTexCoord = aTexCoord;\n}\n",
  normalFrag:
    "precision mediump float;\nvarying vec3 vVertexNormal;\nvoid main(void) {\n  gl_FragColor = vec4(vVertexNormal, 1.0);\n}",
  basicFrag:
    "precision mediump float;\nvarying vec3 vVertexNormal;\nuniform vec4 uMaterialColor;\nvoid main(void) {\n  gl_FragColor = uMaterialColor;\n}",
  lightVert:
    "attribute vec3 aPosition;\nattribute vec3 aNormal;\nattribute vec2 aTexCoord;\n\nuniform mat4 uModelViewMatrix;\nuniform mat4 uProjectionMatrix;\nuniform mat3 uNormalMatrix;\nuniform float uResolution;\nuniform int uAmbientLightCount;\nuniform int uDirectionalLightCount;\nuniform int uPointLightCount;\n\nuniform vec3 uAmbientColor[8];\nuniform vec3 uLightingDirection[8];\nuniform vec3 uDirectionalColor[8];\nuniform vec3 uPointLightLocation[8];\nuniform vec3 uPointLightColor[8];\nuniform bool uSpecular;\n\nvarying vec3 vVertexNormal;\nvarying vec2 vVertTexCoord;\nvarying vec3 vLightWeighting;\n\nvec3 ambientLightFactor = vec3(0.0, 0.0, 0.0);\nvec3 directionalLightFactor = vec3(0.0, 0.0, 0.0);\nvec3 pointLightFactor = vec3(0.0, 0.0, 0.0);\nvec3 pointLightFactor2 = vec3(0.0, 0.0, 0.0);\n\nvoid main(void){\n\n  vec4 positionVec4 = vec4(aPosition / uResolution, 1.0);\n  gl_Position = uProjectionMatrix * uModelViewMatrix * positionVec4;\n\n  vec3 vertexNormal = vec3( uNormalMatrix * aNormal );\n  vVertexNormal = vertexNormal;\n  vVertTexCoord = aTexCoord;\n\n  vec4 mvPosition = uModelViewMatrix * vec4(aPosition / uResolution, 1.0);\n  vec3 eyeDirection = normalize(-mvPosition.xyz);\n\n  float shininess = 32.0;\n  float specularFactor = 2.0;\n  float diffuseFactor = 0.3;\n\n  for(int i = 0; i < 8; i++){\n    if(uAmbientLightCount == i) break;\n    ambientLightFactor += uAmbientColor[i];\n  }\n\n  for(int j = 0; j < 8; j++){\n    if(uDirectionalLightCount == j) break;\n    vec3 dir = uLightingDirection[j];\n    float directionalLightWeighting = max(dot(vertexNormal, dir), 0.0);\n    directionalLightFactor += uDirectionalColor[j] * directionalLightWeighting;\n  }\n\n  for(int k = 0; k < 8; k++){\n    if(uPointLightCount == k) break;\n    vec3 loc = uPointLightLocation[k];\n    //loc = loc / uResolution;\n    vec3 lightDirection = normalize(loc - mvPosition.xyz);\n\n    float directionalLightWeighting = max(dot(vertexNormal, lightDirection), 0.0);\n    pointLightFactor += uPointLightColor[k] * directionalLightWeighting;\n\n    //factor2 for specular\n    vec3 reflectionDirection = reflect(-lightDirection, vertexNormal);\n    float specularLightWeighting = pow(max(dot(reflectionDirection, eyeDirection), 0.0), shininess);\n\n    pointLightFactor2 += uPointLightColor[k] * (specularFactor * specularLightWeighting\n      +  directionalLightWeighting * diffuseFactor);\n  }\n\n  if(!uSpecular){\n    vLightWeighting =  ambientLightFactor + directionalLightFactor + pointLightFactor;\n  }else{\n    vLightWeighting = ambientLightFactor + directionalLightFactor + pointLightFactor2;\n  }\n\n}\n",
  lightTextureFrag:
    "precision mediump float;\n\nuniform vec4 uMaterialColor;\nuniform sampler2D uSampler;\nuniform bool isTexture;\n\nvarying vec3 vLightWeighting;\nvarying highp vec2 vVertTexCoord;\n\nvoid main(void) {\n  if(!isTexture){\n    gl_FragColor = vec4(vec3(uMaterialColor.rgb * vLightWeighting), uMaterialColor.a);\n  }else{\n    vec4 textureColor = texture2D(uSampler, vVertTexCoord);\n    if(vLightWeighting == vec3(0., 0., 0.)){\n      gl_FragColor = textureColor;\n    }else{\n      gl_FragColor = vec4(vec3(textureColor.rgb * vLightWeighting), textureColor.a);\n    }\n  }\n}"
};
},{}]},{},[30])(30)
});

/*
p5.play
by Paolo Pedercini/molleindustria, 2015
http://molleindustria.org/
*/

(function(root, factory) {
if (typeof define === 'function' && define.amd)
define('p5.play', ['@code-dot-org/p5'], function(p5) { (factory(p5)); });
else if (typeof exports === 'object')
factory(require('@code-dot-org/p5'));
else
factory(root.p5);
}(this, function(p5) {
/**
 * p5.play is a library for p5.js to facilitate the creation of games and gamelike
 * projects.
 *
 * It provides a flexible Sprite class to manage visual objects in 2D space
 * and features such as animation support, basic collision detection
 * and resolution, mouse and keyboard interactions, and a virtual camera.
 *
 * p5.play is not a box2D-derived physics engine, it doesn't use events, and it's
 * designed to be understood and possibly modified by intermediate programmers.
 *
 * See the examples folder for more info on how to use this library.
 *
 * @module p5.play
 * @submodule p5.play
 * @for p5.play
 * @main
 */

// =============================================================================
//                         initialization
// =============================================================================

var DEFAULT_FRAME_RATE = 30;

// This is the new way to initialize custom p5 properties for any p5 instance.
// The goal is to migrate lazy P5 properties over to this method.
// @see https://github.com/molleindustria/p5.play/issues/46
p5.prototype.registerMethod('init', function p5PlayInit() {
  /**
   * The sketch camera automatically created at the beginning of a sketch.
   * A camera facilitates scrolling and zooming for scenes extending beyond
   * the canvas. A camera has a position, a zoom factor, and the mouse
   * coordinates relative to the view.
   *
   * In p5.js terms the camera wraps the whole drawing cycle in a
   * transformation matrix but it can be disabled anytime during the draw
   * cycle, for example to draw interface elements in an absolute position.
   *
   * @property camera
   * @type {camera}
   */
  this.camera = new Camera(this, 0, 0, 1);
  this.camera.init = false;

  this.angleMode(this.DEGREES);
  this.frameRate(DEFAULT_FRAME_RATE);

  this._defaultCanvasSize = {
    width: 400,
    height: 400
  };

  var startDate = new Date();
  this._startTime = startDate.getTime();

  // Temporary canvas for supporting tint operations from image elements;
  // see p5.prototype.imageElement()
  this._tempCanvas = document.createElement('canvas');
});

// This provides a way for us to lazily define properties that
// are global to p5 instances.
//
// Note that this isn't just an optimization: p5 currently provides no
// way for add-ons to be notified when new p5 instances are created, so
// lazily creating these properties is the *only* mechanism available
// to us. For more information, see:
//
// https://github.com/processing/p5.js/issues/1263
function defineLazyP5Property(name, getter) {
  Object.defineProperty(p5.prototype, name, {
    configurable: true,
    enumerable: true,
    get: function() {
      var context = (this instanceof p5 && !this._isGlobal) ? this : window;

      if (typeof(context._p5PlayProperties) === 'undefined') {
        context._p5PlayProperties = {};
      }
      if (!(name in context._p5PlayProperties)) {
        context._p5PlayProperties[name] = getter.call(context);
      }
      return context._p5PlayProperties[name];
    }
  });
}

// This returns a factory function, suitable for passing to
// defineLazyP5Property, that returns a subclass of the given
// constructor that is always bound to a particular p5 instance.
function boundConstructorFactory(constructor) {
  if (typeof(constructor) !== 'function')
    throw new Error('constructor must be a function');

  return function createBoundConstructor() {
    var pInst = this;

    function F() {
      var args = Array.prototype.slice.call(arguments);

      return constructor.apply(this, [pInst].concat(args));
    }
    F.prototype = constructor.prototype;

    return F;
  };
}

// This is a utility that makes it easy to define convenient aliases to
// pre-bound p5 instance methods.
//
// For example:
//
//   var pInstBind = createPInstBinder(pInst);
//
//   var createVector = pInstBind('createVector');
//   var loadImage = pInstBind('loadImage');
//
// The above will create functions createVector and loadImage, which can be
// used similar to p5 global mode--however, they're bound to specific p5
// instances, and can thus be used outside of global mode.
function createPInstBinder(pInst) {
  return function pInstBind(methodName) {
    var method = pInst[methodName];

    if (typeof(method) !== 'function')
      throw new Error('"' + methodName + '" is not a p5 method');
    return method.bind(pInst);
  };
}

// These are utility p5 functions that don't depend on p5 instance state in
// order to work properly, so we'll go ahead and make them easy to
// access without needing to bind them to a p5 instance.
var abs = p5.prototype.abs;
var radians = p5.prototype.radians;
var degrees = p5.prototype.degrees;

// =============================================================================
//                         p5 overrides
// =============================================================================

// Make the fill color default to gray (127, 127, 127) each time a new canvas is
// created.
if (!p5.prototype.originalCreateCanvas_) {
  p5.prototype.originalCreateCanvas_ = p5.prototype.createCanvas;
  p5.prototype.createCanvas = function() {
    var result = this.originalCreateCanvas_.apply(this, arguments);
    this.fill(this.color(127, 127, 127));
    return result;
  };
}

// Make width and height optional for ellipse() - default to 50
// Save the original implementation to allow for optional parameters.
if (!p5.prototype.originalEllipse_) {
  p5.prototype.originalEllipse_ = p5.prototype.ellipse;
  p5.prototype.ellipse = function(x, y, w, h) {
    w = (w === undefined) ? 50 : w;
    h = (h === undefined) ? w : h;
    this.originalEllipse_(x, y, w, h);
  };
}

// Make width and height optional for rect() - default to 50
// Save the original implementation to allow for optional parameters.
if (!p5.prototype.originalRect_) {
  p5.prototype.originalRect_ = p5.prototype.rect;
  p5.prototype.rect = function(x, y, w, h, tl, tr, br, bl) {
    w = (w === undefined) ? 50 : w;
    h = (h === undefined) ? w : h;
    this.originalRect_(x, y, w, h, tl, tr, br, bl);
  };
}

// Modify p5 to ignore out-of-bounds positions before setting touchIsDown
p5.prototype._ontouchstart = function(e) {
  if (!this._curElement) {
    return;
  }
  var validTouch;
  for (var i = 0; i < e.touches.length; i++) {
    validTouch = getTouchInfo(this._curElement.elt, e, i);
    if (validTouch) {
      break;
    }
  }
  if (!validTouch) {
    // No in-bounds (valid) touches, return and ignore:
    return;
  }
  var context = this._isGlobal ? window : this;
  var executeDefault;
  this._updateNextTouchCoords(e);
  this._updateNextMouseCoords(e);
  this._setProperty('touchIsDown', true);
  if (typeof context.touchStarted === 'function') {
    executeDefault = context.touchStarted(e);
    if (executeDefault === false) {
      e.preventDefault();
    }
  } else if (typeof context.mousePressed === 'function') {
    executeDefault = context.mousePressed(e);
    if (executeDefault === false) {
      e.preventDefault();
    }
    //this._setMouseButton(e);
  }
};

// Modify p5 to handle CSS transforms (scale) and ignore out-of-bounds
// positions before reporting touch coordinates
//
// NOTE: _updateNextTouchCoords() is nearly identical, but calls a modified
// getTouchInfo() function below that scales the touch postion with the play
// space and can return undefined
p5.prototype._updateNextTouchCoords = function(e) {
  var x = this.touchX;
  var y = this.touchY;
  if (e.type === 'mousedown' || e.type === 'mousemove' ||
      e.type === 'mouseup' || !e.touches) {
    x = this.mouseX;
    y = this.mouseY;
  } else {
    if (this._curElement !== null) {
      var touchInfo = getTouchInfo(this._curElement.elt, e, 0);
      if (touchInfo) {
        x = touchInfo.x;
        y = touchInfo.y;
      }

      var touches = [];
      var touchIndex = 0;
      for (var i = 0; i < e.touches.length; i++) {
        // Only some touches are valid - only push valid touches into the
        // array for the `touches` property.
        touchInfo = getTouchInfo(this._curElement.elt, e, i);
        if (touchInfo) {
          touches[touchIndex] = touchInfo;
          touchIndex++;
        }
      }
      this._setProperty('touches', touches);
    }
  }
  this._setProperty('touchX', x);
  this._setProperty('touchY', y);
  if (!this._hasTouchInteracted) {
    // For first draw, make previous and next equal
    this._updateTouchCoords();
    this._setProperty('_hasTouchInteracted', true);
  }
};

// NOTE: returns undefined if the position is outside of the valid range
function getTouchInfo(canvas, e, i) {
  i = i || 0;
  var rect = canvas.getBoundingClientRect();
  var touch = e.touches[i] || e.changedTouches[i];
  var xPos = touch.clientX - rect.left;
  var yPos = touch.clientY - rect.top;
  if (xPos >= 0 && xPos < rect.width && yPos >= 0 && yPos < rect.height) {
    return {
      x: Math.round(xPos * canvas.offsetWidth / rect.width),
      y: Math.round(yPos * canvas.offsetHeight / rect.height),
      id: touch.identifier
    };
  }
}

// Modify p5 to ignore out-of-bounds positions before setting mouseIsPressed
// and isMousePressed
p5.prototype._onmousedown = function(e) {
  if (!this._curElement) {
    return;
  }
  if (!getMousePos(this._curElement.elt, e)) {
    // Not in-bounds, return and ignore:
    return;
  }
  var context = this._isGlobal ? window : this;
  var executeDefault;
  this._setProperty('isMousePressed', true);
  this._setProperty('mouseIsPressed', true);
  this._setMouseButton(e);
  this._updateNextMouseCoords(e);
  this._updateNextTouchCoords(e);
  if (typeof context.mousePressed === 'function') {
    executeDefault = context.mousePressed(e);
    if (executeDefault === false) {
      e.preventDefault();
    }
  } else if (typeof context.touchStarted === 'function') {
    executeDefault = context.touchStarted(e);
    if (executeDefault === false) {
      e.preventDefault();
    }
  }
};

// Modify p5 to handle CSS transforms (scale) and ignore out-of-bounds
// positions before reporting mouse coordinates
//
// NOTE: _updateNextMouseCoords() is nearly identical, but calls a modified
// getMousePos() function below that scales the mouse position with the play
// space and can return undefined.
p5.prototype._updateNextMouseCoords = function(e) {
  var x = this.mouseX;
  var y = this.mouseY;
  if (e.type === 'touchstart' || e.type === 'touchmove' ||
      e.type === 'touchend' || e.touches) {
    x = this.touchX;
    y = this.touchY;
  } else if (this._curElement !== null) {
    var mousePos = getMousePos(this._curElement.elt, e);
    if (mousePos) {
      x = mousePos.x;
      y = mousePos.y;
    }
  }
  this._setProperty('mouseX', x);
  this._setProperty('mouseY', y);
  this._setProperty('winMouseX', e.pageX);
  this._setProperty('winMouseY', e.pageY);
  if (!this._hasMouseInteracted) {
    // For first draw, make previous and next equal
    this._updateMouseCoords();
    this._setProperty('_hasMouseInteracted', true);
  }
};

// NOTE: returns undefined if the position is outside of the valid range
function getMousePos(canvas, evt) {
  var rect = canvas.getBoundingClientRect();
  var xPos = evt.clientX - rect.left;
  var yPos = evt.clientY - rect.top;
  if (xPos >= 0 && xPos < rect.width && yPos >= 0 && yPos < rect.height) {
    return {
      x: Math.round(xPos * canvas.offsetWidth / rect.width),
      y: Math.round(yPos * canvas.offsetHeight / rect.height)
    };
  }
}

// =============================================================================
//                         p5 extensions
// eslint-disable-next-line no-warning-comments
// TODO: It'd be nice to get these accepted upstream in p5
// =============================================================================

/**
 * Projects a vector onto the line parallel to a second vector, giving a third
 * vector which is the orthogonal projection of that vector onto the line.
 * @see https://en.wikipedia.org/wiki/Vector_projection
 * @method project
 * @for p5.Vector
 * @static
 * @param {p5.Vector} a - vector being projected
 * @param {p5.Vector} b - vector defining the projection target line.
 * @return {p5.Vector} projection of a onto the line parallel to b.
 */
p5.Vector.project = function(a, b) {
  return p5.Vector.mult(b, p5.Vector.dot(a, b) / p5.Vector.dot(b, b));
};

/**
 * Ask whether a vector is parallel to this one.
 * @method isParallel
 * @for p5.Vector
 * @param {p5.Vector} v2
 * @param {number} [tolerance] - margin of error for comparisons, comes into
 *        play when comparing rotated vectors.  For example, we want
 *        <1, 0> to be parallel to <0, 1>.rot(Math.PI/2) but float imprecision
 *        can get in the way of that.
 * @return {boolean}
 */
p5.Vector.prototype.isParallel = function(v2, tolerance) {
  tolerance = typeof tolerance === 'number' ? tolerance : 1e-14;
  return (
      Math.abs(this.x) < tolerance && Math.abs(v2.x) < tolerance
    ) || (
      Math.abs(this.y ) < tolerance && Math.abs(v2.y) < tolerance
    ) || (
      Math.abs(this.x / v2.x - this.y / v2.y) < tolerance
    );
};

// =============================================================================
//                         p5 additions
// =============================================================================

/**
 * Loads an image from a path and creates an Image from it.
 * <br><br>
 * The image may not be immediately available for rendering
 * If you want to ensure that the image is ready before doing
 * anything with it, place the loadImageElement() call in preload().
 * You may also supply a callback function to handle the image when it's ready.
 * <br><br>
 * The path to the image should be relative to the HTML file
 * that links in your sketch. Loading an from a URL or other
 * remote location may be blocked due to your browser's built-in
 * security.
 *
 * @method loadImageElement
 * @param  {String} path Path of the image to be loaded
 * @param  {Function(Image)} [successCallback] Function to be called once
 *                                the image is loaded. Will be passed the
 *                                Image.
 * @param  {Function(Event)}    [failureCallback] called with event error if
 *                                the image fails to load.
 * @return {Image}                the Image object
 */
p5.prototype.loadImageElement = function(path, successCallback, failureCallback) {
  var img = new Image();
  var decrementPreload = p5._getDecrementPreload.apply(this, arguments);

  img.onload = function() {
    if (typeof successCallback === 'function') {
      successCallback(img);
    }
    if (decrementPreload && (successCallback !== decrementPreload)) {
      decrementPreload();
    }
  };
  img.onerror = function(e) {
    p5._friendlyFileLoadError(0, img.src);
    // don't get failure callback mixed up with decrementPreload
    if ((typeof failureCallback === 'function') &&
      (failureCallback !== decrementPreload)) {
      failureCallback(e);
    }
  };

  //set crossOrigin in case image is served which CORS headers
  //this will let us draw to canvas without tainting it.
  //see https://developer.mozilla.org/en-US/docs/HTML/CORS_Enabled_Image
  // When using data-uris the file will be loaded locally
  // so we don't need to worry about crossOrigin with base64 file types
  if(path.indexOf('data:image/') !== 0) {
    img.crossOrigin = 'Anonymous';
  }

  //start loading the image
  img.src = path;

  return img;
};

/**
 * Draw an image element to the main canvas of the p5js sketch
 *
 * @method imageElement
 * @param  {Image}    imgEl    the image to display
 * @param  {Number}   [sx=0]   The X coordinate of the top left corner of the
 *                             sub-rectangle of the source image to draw into
 *                             the destination canvas.
 * @param  {Number}   [sy=0]   The Y coordinate of the top left corner of the
 *                             sub-rectangle of the source image to draw into
 *                             the destination canvas.
 * @param {Number} [sWidth=imgEl.width] The width of the sub-rectangle of the
 *                                      source image to draw into the destination
 *                                      canvas.
 * @param {Number} [sHeight=imgEl.height] The height of the sub-rectangle of the
 *                                        source image to draw into the
 *                                        destination context.
 * @param  {Number}   [dx=0]    The X coordinate in the destination canvas at
 *                              which to place the top-left corner of the
 *                              source image.
 * @param  {Number}   [dy=0]    The Y coordinate in the destination canvas at
 *                              which to place the top-left corner of the
 *                              source image.
 * @param  {Number}   [dWidth]  The width to draw the image in the destination
 *                              canvas. This allows scaling of the drawn image.
 * @param  {Number}   [dHeight] The height to draw the image in the destination
 *                              canvas. This allows scaling of the drawn image.
 * @example
 * <div>
 * <code>
 * var imgEl;
 * function preload() {
 *   imgEl = loadImageElement("assets/laDefense.jpg");
 * }
 * function setup() {
 *   imageElement(imgEl, 0, 0);
 *   imageElement(imgEl, 0, 0, 100, 100);
 *   imageElement(imgEl, 0, 0, 100, 100, 0, 0, 100, 100);
 * }
 * </code>
 * </div>
 * <div>
 * <code>
 * function setup() {
 *   // here we use a callback to display the image after loading
 *   loadImageElement("assets/laDefense.jpg", function(imgEl) {
 *     imageElement(imgEl, 0, 0);
 *   });
 * }
 * </code>
 * </div>
 *
 * @alt
 * image of the underside of a white umbrella and grided ceiling above
 * image of the underside of a white umbrella and grided ceiling above
 *
 */
p5.prototype.imageElement = function(imgEl, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight) {
  /**
   * Validates clipping params. Per drawImage spec sWidth and sHight cannot be
   * negative or greater than image intrinsic width and height
   * @private
   * @param {Number} sVal
   * @param {Number} iVal
   * @returns {Number}
   * @private
   */
  function _sAssign(sVal, iVal) {
    if (sVal > 0 && sVal < iVal) {
      return sVal;
    }
    else {
      return iVal;
    }
  }

  function modeAdjust(a, b, c, d, mode) {
    if (mode === p5.prototype.CORNER) {
      return {x: a, y: b, w: c, h: d};
    } else if (mode === p5.prototype.CORNERS) {
      return {x: a, y: b, w: c-a, h: d-b};
    } else if (mode === p5.prototype.RADIUS) {
      return {x: a-c, y: b-d, w: 2*c, h: 2*d};
    } else if (mode === p5.prototype.CENTER) {
      return {x: a-c*0.5, y: b-d*0.5, w: c, h: d};
    }
  }

  if (arguments.length <= 5) {
    dx = sx || 0;
    dy = sy || 0;
    sx = 0;
    sy = 0;
    dWidth = sWidth || imgEl.width;
    dHeight = sHeight || imgEl.height;
    sWidth = imgEl.width;
    sHeight = imgEl.height;
  } else if (arguments.length === 9) {
    sx = sx || 0;
    sy = sy || 0;
    sWidth = _sAssign(sWidth, imgEl.width);
    sHeight = _sAssign(sHeight, imgEl.height);

    dx = dx || 0;
    dy = dy || 0;
    dWidth = dWidth || imgEl.width;
    dHeight = dHeight || imgEl.height;
  } else {
    throw 'Wrong number of arguments to imageElement()';
  }

  var vals = modeAdjust(dx, dy, dWidth, dHeight,
    this._renderer._imageMode);

  if (this._renderer._tint) {
    // Just-in-time create/draw into a temp canvas so tinting can
    // work within the renderer as it would for a p5.Image
    // Only resize canvas if it's too small
    var context = this._tempCanvas.getContext('2d');
    if (this._tempCanvas.width < vals.w || this._tempCanvas.height < vals.h) {
      this._tempCanvas.width = Math.max(this._tempCanvas.width, vals.w);
      this._tempCanvas.height = Math.max(this._tempCanvas.height, vals.h);
    } else {
      context.clearRect(0, 0, vals.w, vals.h);
    }
    context.drawImage(imgEl,
      sx, sy, sWidth, sHeight,
      0, 0, vals.w, vals.h);
    // Call the renderer's image() method with an object that contains the Image
    // as an 'elt' property and the temp canvas as well (when needed):
    this._renderer.image({canvas: this._tempCanvas},
      0, 0, vals.w, vals.h,
      vals.x, vals.y, vals.w, vals.h);
  } else {
    this._renderer.image({elt: imgEl},
      sx, sy, sWidth, sHeight,
      vals.x, vals.y, vals.w, vals.h);
  }
};

/**
* A Group containing all the sprites in the sketch.
*
* @property allSprites
* @for p5.play
* @type {Group}
*/

defineLazyP5Property('allSprites', function() {
  return new p5.prototype.Group();
});

p5.prototype._mouseButtonIsPressed = function(buttonCode) {
  return (this.mouseIsPressed && this.mouseButton === buttonCode) ||
    (this.touchIsDown && buttonCode === this.LEFT);
};

p5.prototype.mouseDidMove = function() {
  return this.pmouseX !== this.mouseX || this.pmouseY !== this.mouseY;
};

p5.prototype.mouseIsOver = function(sprite) {
  if (!sprite) {
    return false;
  }

  if (!sprite.collider) {
    sprite.setDefaultCollider();
  }

  var mousePosition;
  if (this.camera.active) {
    mousePosition = this.createVector(this.camera.mouseX, this.camera.mouseY);
  } else {
    mousePosition = this.createVector(this.mouseX, this.mouseY);
  }

  return sprite.collider.overlap(new window.p5.PointCollider(mousePosition));
};

p5.prototype.mousePressedOver = function(sprite) {
  return (this.mouseIsPressed || this.touchIsDown) && this.mouseIsOver(sprite);
};

var styleEmpty = 'rgba(0,0,0,0)';

p5.Renderer2D.prototype.regularPolygon = function(x, y, sides, size, rotation) {
  var ctx = this.drawingContext;
  var doFill = this._doFill, doStroke = this._doStroke;
  if (doFill && !doStroke) {
    if (ctx.fillStyle === styleEmpty) {
      return this;
    }
  } else if (!doFill && doStroke) {
    if (ctx.strokeStyle === styleEmpty) {
      return this;
    }
  }
  if (sides < 3) {
    return;
  }
  ctx.beginPath();
  ctx.moveTo(x + size * Math.cos(rotation), y + size * Math.sin(rotation));
  for (var i = 1; i < sides; i++) {
    var angle = rotation + (i * 2 * Math.PI / sides);
    ctx.lineTo(x + size * Math.cos(angle), y + size * Math.sin(angle));
  }
  ctx.closePath();
  if (doFill) {
    ctx.fill();
  }
  if (doStroke) {
    ctx.stroke();
  }
};

p5.prototype.regularPolygon = function(x, y, sides, size, rotation) {
  if (!this._renderer._doStroke && !this._renderer._doFill) {
    return this;
  }
  var args = new Array(arguments.length);
  for (var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }

  if (typeof rotation === 'undefined') {
    rotation = -(Math.PI / 2);
    if (0 === sides % 2) {
      rotation += Math.PI / sides;
    }
  } else if (this._angleMode === this.DEGREES) {
    rotation = this.radians(rotation);
  }

  // NOTE: only implemented for non-3D
  if (!this._renderer.isP3D) {
    this._validateParameters(
      'regularPolygon',
      args,
      [
        ['Number', 'Number', 'Number', 'Number'],
        ['Number', 'Number', 'Number', 'Number', 'Number']
      ]
    );
    this._renderer.regularPolygon(
      args[0],
      args[1],
      args[2],
      args[3],
      rotation
    );
  }
  return this;
};

p5.Renderer2D.prototype.shape = function() {
  var ctx = this.drawingContext;
  var doFill = this._doFill, doStroke = this._doStroke;
  if (doFill && !doStroke) {
    if (ctx.fillStyle === styleEmpty) {
      return this;
    }
  } else if (!doFill && doStroke) {
    if (ctx.strokeStyle === styleEmpty) {
      return this;
    }
  }
  var numCoords = arguments.length / 2;
  if (numCoords < 1) {
    return;
  }
  ctx.beginPath();
  ctx.moveTo(arguments[0], arguments[1]);
  for (var i = 1; i < numCoords; i++) {
    ctx.lineTo(arguments[i * 2], arguments[i * 2 + 1]);
  }
  ctx.closePath();
  if (doFill) {
    ctx.fill();
  }
  if (doStroke) {
    ctx.stroke();
  }
};

p5.prototype.shape = function() {
  if (!this._renderer._doStroke && !this._renderer._doFill) {
    return this;
  }
  // NOTE: only implemented for non-3D
  if (!this._renderer.isP3D) {
    // eslint-disable-next-line no-warning-comments
    // TODO: call this._validateParameters, once it is working in p5.js and
    // we understand if it can be used for var args functions like this
    this._renderer.shape.apply(this._renderer, arguments);
  }
  return this;
};

p5.prototype.rgb = function(r, g, b, a) {
  // convert a from 0 to 255 to 0 to 1
  if (!a) {
    a = 1;
  }
  a = a * 255;

  return this.color(r, g, b, a);
};

p5.prototype.createGroup = function() {
  return new this.Group();
};

defineLazyP5Property('World', function() {
  var World = {
    pInst: this
  };

  function createReadOnlyP5PropertyAlias(name) {
    Object.defineProperty(World, name, {
      enumerable: true,
      get: function() {
        return this.pInst[name];
      }
    });
  }

  createReadOnlyP5PropertyAlias('width');
  createReadOnlyP5PropertyAlias('height');
  createReadOnlyP5PropertyAlias('mouseX');
  createReadOnlyP5PropertyAlias('mouseY');
  createReadOnlyP5PropertyAlias('allSprites');
  createReadOnlyP5PropertyAlias('frameCount');

  Object.defineProperty(World, 'frameRate', {
    enumerable: true,
    get: function() {
      return this.pInst.frameRate();
    },
    set: function(value) {
      this.pInst.frameRate(value);
    }
  });

  Object.defineProperty(World, 'seconds', {
    enumerable: true,
    get: function() {
      var currentDate = new Date();
      var currentTime = currentDate.getTime();
      return Math.round((currentTime - this.pInst._startTime) / 1000);
    }
  });

  return World;
});

p5.prototype.spriteUpdate = true;

/**
   * A Sprite is the main building block of p5.play:
   * an element able to store images or animations with a set of
   * properties such as position and visibility.
   * A Sprite can have a collider that defines the active area to detect
   * collisions or overlappings with other sprites and mouse interactions.
   *
   * Sprites created using createSprite (the preferred way) are added to the
   * allSprites group and given a depth value that puts it in front of all
   * other sprites.
   *
   * @method createSprite
   * @param {Number} x Initial x coordinate
   * @param {Number} y Initial y coordinate
   * @param {Number} width Width of the placeholder rectangle and of the
   *                       collider until an image or new collider are set
   * @param {Number} height Height of the placeholder rectangle and of the
   *                       collider until an image or new collider are set
   * @return {Object} The new sprite instance
   */

p5.prototype.createSprite = function(x, y, width, height) {
  var s = new Sprite(this, x, y, width, height);
  s.depth = this.allSprites.maxDepth()+1;
  this.allSprites.add(s);
  return s;
};


/**
   * Removes a Sprite from the sketch.
   * The removed Sprite won't be drawn or updated anymore.
   * Equivalent to Sprite.remove()
   *
   * @method removeSprite
   * @param {Object} sprite Sprite to be removed
*/
p5.prototype.removeSprite = function(sprite) {
  sprite.remove();
};

/**
* Updates all the sprites in the sketch (position, animation...)
* it's called automatically at every draw().
* It can be paused by passing a parameter true or false;
* Note: it does not render the sprites.
*
* @method updateSprites
* @param {Boolean} updating false to pause the update, true to resume
*/
p5.prototype.updateSprites = function(upd) {

  if(upd === false)
    this.spriteUpdate = false;
  if(upd === true)
    this.spriteUpdate = true;

  if(this.spriteUpdate)
  for(var i = 0; i<this.allSprites.size(); i++)
  {
    this.allSprites.get(i).update();
  }
};

/**
* Returns all the sprites in the sketch as an array
*
* @method getSprites
* @return {Array} Array of Sprites
*/
p5.prototype.getSprites = function() {

  //draw everything
  if(arguments.length===0)
  {
    return this.allSprites.toArray();
  }
  else
  {
    var arr = [];
    //for every tag
    for(var j=0; j<arguments.length; j++)
    {
      for(var i = 0; i<this.allSprites.size(); i++)
      {
        if(this.allSprites.get(i).isTagged(arguments[j]))
          arr.push(this.allSprites.get(i));
      }
    }

    return arr;
  }

};

/**
* Displays a Group of sprites.
* If no parameter is specified, draws all sprites in the
* sketch.
* The drawing order is determined by the Sprite property "depth"
*
* @method drawSprites
* @param {Group} [group] Group of Sprites to be displayed
*/
p5.prototype.drawSprites = function(group) {
  // If no group is provided, draw the allSprites group.
  group = group || this.allSprites;

  if (typeof group.draw !== 'function')
  {
    throw('Error: with drawSprites you can only draw all sprites or a group');
  }

  group.draw();
};

/**
* Displays a Sprite.
* To be typically used in the main draw function.
*
* @method drawSprite
* @param {Sprite} sprite Sprite to be displayed
*/
p5.prototype.drawSprite = function(sprite) {
  if(sprite)
  sprite.display();
};

/**
* Loads an animation.
* To be typically used in the preload() function of the sketch.
*
* @method loadAnimation
* @param {Sprite} sprite Sprite to be displayed
*/
p5.prototype.loadAnimation = function() {
  return construct(this.Animation, arguments);
};

/**
 * Loads a Sprite Sheet.
 * To be typically used in the preload() function of the sketch.
 *
 * @method loadSpriteSheet
 */
p5.prototype.loadSpriteSheet = function() {
  return construct(this.SpriteSheet, arguments);
};

/**
* Displays an animation.
*
* @method animation
* @param {Animation} anim Animation to be displayed
* @param {Number} x X coordinate
* @param {Number} y Y coordinate
*
*/
p5.prototype.animation = function(anim, x, y) {
  anim.draw(x, y);
};

//variable to detect instant presses
defineLazyP5Property('_p5play', function() {
  return {
    keyStates: {},
    mouseStates: {}
  };
});

var KEY_IS_UP = 0;
var KEY_WENT_DOWN = 1;
var KEY_IS_DOWN = 2;
var KEY_WENT_UP = 3;

/**
* Detects if a key was pressed during the last cycle.
* It can be used to trigger events once, when a key is pressed or released.
* Example: Super Mario jumping.
*
* @method keyWentDown
* @param {Number|String} key Key code or character
* @return {Boolean} True if the key was pressed
*/
p5.prototype.keyWentDown = function(key) {
  return this._isKeyInState(key, KEY_WENT_DOWN);
};


/**
* Detects if a key was released during the last cycle.
* It can be used to trigger events once, when a key is pressed or released.
* Example: Spaceship shooting.
*
* @method keyWentUp
* @param {Number|String} key Key code or character
* @return {Boolean} True if the key was released
*/
p5.prototype.keyWentUp = function(key) {
  return this._isKeyInState(key, KEY_WENT_UP);
};

/**
* Detects if a key is currently pressed
* Like p5 keyIsDown but accepts strings and codes
*
* @method keyDown
* @param {Number|String} key Key code or character
* @return {Boolean} True if the key is down
*/
p5.prototype.keyDown = function(key) {
  return this._isKeyInState(key, KEY_IS_DOWN);
};

/**
 * Detects if a key is in the given state during the last cycle.
 * Helper method encapsulating common key state logic; it may be preferable
 * to call keyDown or other methods directly.
 *
 * @private
 * @method _isKeyInState
 * @param {Number|String} key Key code or character
 * @param {Number} state Key state to check against
 * @return {Boolean} True if the key is in the given state
 */
p5.prototype._isKeyInState = function(key, state) {
  var keyCode;
  var keyStates = this._p5play.keyStates;

  if(typeof key === 'string')
  {
    keyCode = this._keyCodeFromAlias(key);
  }
  else
  {
    keyCode = key;
  }

  //if undefined start checking it
  if(keyStates[keyCode]===undefined)
  {
    if(this.keyIsDown(keyCode))
      keyStates[keyCode] = KEY_IS_DOWN;
    else
      keyStates[keyCode] = KEY_IS_UP;
  }

  return (keyStates[keyCode] === state);
};

/**
* Detects if a mouse button is currently down
* Combines mouseIsPressed and mouseButton of p5
*
* @method mouseDown
* @param {Number} [buttonCode] Mouse button constant LEFT, RIGHT or CENTER
* @return {Boolean} True if the button is down
*/
p5.prototype.mouseDown = function(buttonCode) {
  return this._isMouseButtonInState(buttonCode, KEY_IS_DOWN);
};

/**
* Detects if a mouse button is currently up
* Combines mouseIsPressed and mouseButton of p5
*
* @method mouseUp
* @param {Number} [buttonCode] Mouse button constant LEFT, RIGHT or CENTER
* @return {Boolean} True if the button is up
*/
p5.prototype.mouseUp = function(buttonCode) {
  return this._isMouseButtonInState(buttonCode, KEY_IS_UP);
};

/**
 * Detects if a mouse button was released during the last cycle.
 * It can be used to trigger events once, to be checked in the draw cycle
 *
 * @method mouseWentUp
 * @param {Number} [buttonCode] Mouse button constant LEFT, RIGHT or CENTER
 * @return {Boolean} True if the button was just released
 */
p5.prototype.mouseWentUp = function(buttonCode) {
  return this._isMouseButtonInState(buttonCode, KEY_WENT_UP);
};


/**
 * Detects if a mouse button was pressed during the last cycle.
 * It can be used to trigger events once, to be checked in the draw cycle
 *
 * @method mouseWentDown
 * @param {Number} [buttonCode] Mouse button constant LEFT, RIGHT or CENTER
 * @return {Boolean} True if the button was just pressed
 */
p5.prototype.mouseWentDown = function(buttonCode) {
  return this._isMouseButtonInState(buttonCode, KEY_WENT_DOWN);
};

/**
 * Returns a constant for a mouse state given a string or a mouse button constant.
 *
 * @private
 * @method _clickKeyFromString
 * @param {Number|String} [buttonCode] Mouse button constant LEFT, RIGHT or CENTER
 *   or string 'leftButton', 'rightButton', or 'centerButton'
 * @return {Number} Mouse button constant LEFT, RIGHT or CENTER or value of buttonCode
 */
p5.prototype._clickKeyFromString = function(buttonCode) {
  if (this.CLICK_KEY[buttonCode]) {
    return this.CLICK_KEY[buttonCode];
  } else {
    return buttonCode;
  }
};

// Map of strings to constants for mouse states.
p5.prototype.CLICK_KEY = {
  'leftButton': p5.prototype.LEFT,
  'rightButton': p5.prototype.RIGHT,
  'centerButton': p5.prototype.CENTER
};

/**
 * Detects if a mouse button is in the given state during the last cycle.
 * Helper method encapsulating common mouse button state logic; it may be
 * preferable to call mouseWentUp, etc, directly.
 *
 * @private
 * @method _isMouseButtonInState
 * @param {Number|String} [buttonCode] Mouse button constant LEFT, RIGHT or CENTER
 *   or string 'leftButton', 'rightButton', or 'centerButton'
 * @param {Number} state
 * @return {boolean} True if the button was in the given state
 */
p5.prototype._isMouseButtonInState = function(buttonCode, state) {
  var mouseStates = this._p5play.mouseStates;

  buttonCode = this._clickKeyFromString(buttonCode);

  if(buttonCode === undefined)
    buttonCode = this.LEFT;

  //undefined = not tracked yet, start tracking
  if(mouseStates[buttonCode]===undefined)
  {
  if (this._mouseButtonIsPressed(buttonCode))
    mouseStates[buttonCode] = KEY_IS_DOWN;
  else
    mouseStates[buttonCode] = KEY_IS_UP;
  }

  return (mouseStates[buttonCode] === state);
};


/**
 * An object storing all useful keys for easy access
 * Key.tab = 9
 *
 * @private
 * @property KEY
 * @type {Object}
 */
p5.prototype.KEY = {
    'BACKSPACE': 8,
    'TAB': 9,
    'ENTER': 13,
    'SHIFT': 16,
    'CTRL': 17,
    'ALT': 18,
    'PAUSE': 19,
    'CAPS_LOCK': 20,
    'ESC': 27,
    'SPACE': 32,
    ' ': 32,
    'PAGE_UP': 33,
    'PAGE_DOWN': 34,
    'END': 35,
    'HOME': 36,
    'LEFT_ARROW': 37,
    'LEFT': 37,
    'UP_ARROW': 38,
    'UP': 38,
    'RIGHT_ARROW': 39,
    'RIGHT': 39,
    'DOWN_ARROW': 40,
    'DOWN': 40,
    'INSERT': 45,
    'DELETE': 46,
    '0': 48,
    '1': 49,
    '2': 50,
    '3': 51,
    '4': 52,
    '5': 53,
    '6': 54,
    '7': 55,
    '8': 56,
    '9': 57,
    'A': 65,
    'B': 66,
    'C': 67,
    'D': 68,
    'E': 69,
    'F': 70,
    'G': 71,
    'H': 72,
    'I': 73,
    'J': 74,
    'K': 75,
    'L': 76,
    'M': 77,
    'N': 78,
    'O': 79,
    'P': 80,
    'Q': 81,
    'R': 82,
    'S': 83,
    'T': 84,
    'U': 85,
    'V': 86,
    'W': 87,
    'X': 88,
    'Y': 89,
    'Z': 90,
    '0NUMPAD': 96,
    '1NUMPAD': 97,
    '2NUMPAD': 98,
    '3NUMPAD': 99,
    '4NUMPAD': 100,
    '5NUMPAD': 101,
    '6NUMPAD': 102,
    '7NUMPAD': 103,
    '8NUMPAD': 104,
    '9NUMPAD': 105,
    'MULTIPLY': 106,
    'PLUS': 107,
    'MINUS': 109,
    'DOT': 110,
    'SLASH1': 111,
    'F1': 112,
    'F2': 113,
    'F3': 114,
    'F4': 115,
    'F5': 116,
    'F6': 117,
    'F7': 118,
    'F8': 119,
    'F9': 120,
    'F10': 121,
    'F11': 122,
    'F12': 123,
    'EQUAL': 187,
    'COMMA': 188,
    'SLASH': 191,
    'BACKSLASH': 220
};

/**
 * An object storing deprecated key aliases, which we still support but
 * should be mapped to valid aliases and generate warnings.
 *
 * @private
 * @property KEY_DEPRECATIONS
 * @type {Object}
 */
p5.prototype.KEY_DEPRECATIONS = {
  'MINUT': 'MINUS',
  'COMA': 'COMMA'
};

/**
 * Given a string key alias (as defined in the KEY property above), look up
 * and return the numeric JavaScript key code for that key.  If a deprecated
 * alias is passed (as defined in the KEY_DEPRECATIONS property) it will be
 * mapped to a valid key code, but will also generate a warning about use
 * of the deprecated alias.
 *
 * @private
 * @method _keyCodeFromAlias
 * @param {!string} alias - a case-insensitive key alias
 * @return {number|undefined} a numeric JavaScript key code, or undefined
 *          if no key code matching the given alias is found.
 */
p5.prototype._keyCodeFromAlias = function(alias) {
  alias = alias.toUpperCase();
  if (this.KEY_DEPRECATIONS[alias]) {
    this._warn('Key literal "' + alias + '" is deprecated and may be removed ' +
      'in a future version of p5.play. ' +
      'Please use "' + this.KEY_DEPRECATIONS[alias] + '" instead.');
    alias = this.KEY_DEPRECATIONS[alias];
  }
  return this.KEY[alias];
};

//pre draw: detect keyStates
p5.prototype.readPresses = function() {
  var keyStates = this._p5play.keyStates;
  var mouseStates = this._p5play.mouseStates;

  for (var key in keyStates) {
    if(this.keyIsDown(key)) //if is down
    {
      if(keyStates[key] === KEY_IS_UP)//and was up
        keyStates[key] = KEY_WENT_DOWN;
      else
        keyStates[key] = KEY_IS_DOWN; //now is simply down
    }
    else //if it's up
    {
      if(keyStates[key] === KEY_IS_DOWN)//and was up
        keyStates[key] = KEY_WENT_UP;
      else
        keyStates[key] = KEY_IS_UP; //now is simply down
    }
  }

  //mouse
  for (var btn in mouseStates) {

    if(this._mouseButtonIsPressed(btn)) //if is down
    {
      if(mouseStates[btn] === KEY_IS_UP)//and was up
        mouseStates[btn] = KEY_WENT_DOWN;
      else
        mouseStates[btn] = KEY_IS_DOWN; //now is simply down
    }
    else //if it's up
    {
      if(mouseStates[btn] === KEY_IS_DOWN)//and was up
        mouseStates[btn] = KEY_WENT_UP;
      else
        mouseStates[btn] = KEY_IS_UP; //now is simply down
    }
  }

};

/**
* Turns the quadTree on or off.
* A quadtree is a data structure used to optimize collision detection.
* It can improve performance when there is a large number of Sprites to be
* checked continuously for overlapping.
*
* p5.play will create and update a quadtree automatically, however it is
* inactive by default.
*
* @method useQuadTree
* @param {Boolean} use Pass true to enable, false to disable
*/
p5.prototype.useQuadTree = function(use) {

  if(this.quadTree !== undefined)
  {
    if(use === undefined)
      return this.quadTree.active;
    else if(use)
      this.quadTree.active = true;
    else
      this.quadTree.active = false;
  }
  else
    return false;
};

//the actual quadTree
defineLazyP5Property('quadTree', function() {
  var quadTree = new Quadtree({
    x: 0,
    y: 0,
    width: 0,
    height: 0
  }, 4);
  quadTree.active = false;
  return quadTree;
});

/*
//framerate independent delta, doesn't really work
p5.prototype.deltaTime = 1;

var now = Date.now();
var then = Date.now();
var INTERVAL_60 = 0.0166666; //60 fps

function updateDelta() {
then = now;
now = Date.now();
deltaTime = ((now - then) / 1000)/INTERVAL_60; // seconds since last frame
}
*/

/**
   * A Sprite is the main building block of p5.play:
   * an element able to store images or animations with a set of
   * properties such as position and visibility.
   * A Sprite can have a collider that defines the active area to detect
   * collisions or overlappings with other sprites and mouse interactions.
   *
   * To create a Sprite, use
   * {{#crossLink "p5.play/createSprite:method"}}{{/crossLink}}.
   *
   * @class Sprite
   */

// For details on why these docs aren't in a YUIDoc comment block, see:
//
// https://github.com/molleindustria/p5.play/pull/67
//
// @param {Number} x Initial x coordinate
// @param {Number} y Initial y coordinate
// @param {Number} width Width of the placeholder rectangle and of the
//                       collider until an image or new collider are set
// @param {Number} height Height of the placeholder rectangle and of the
//                        collider until an image or new collider are set
function Sprite(pInst, _x, _y, _w, _h) {
  var pInstBind = createPInstBinder(pInst);

  var createVector = pInstBind('createVector');
  var color = pInstBind('color');
  var print = pInstBind('print');
  var push = pInstBind('push');
  var pop = pInstBind('pop');
  var colorMode = pInstBind('colorMode');
  var tint = pInstBind('tint');
  var alphaTint = pInstBind('alphaTint');
  var lerpColor = pInstBind('lerpColor');
  var noStroke = pInstBind('noStroke');
  var rectMode = pInstBind('rectMode');
  var ellipseMode = pInstBind('ellipseMode');
  var imageMode = pInstBind('imageMode');
  var translate = pInstBind('translate');
  var scale = pInstBind('scale');
  var rotate = pInstBind('rotate');
  var stroke = pInstBind('stroke');
  var strokeWeight = pInstBind('strokeWeight');
  var line = pInstBind('line');
  var noFill = pInstBind('noFill');
  var fill = pInstBind('fill');
  var textAlign = pInstBind('textAlign');
  var textSize = pInstBind('textSize');
  var text = pInstBind('text');
  var rect = pInstBind('rect');
  var cos = pInstBind('cos');
  var sin = pInstBind('sin');
  var atan2 = pInstBind('atan2');

  var quadTree = pInst.quadTree;
  var camera = pInst.camera;


  // These are p5 constants that we'd like easy access to.
  var RGB = p5.prototype.RGB;
  var CENTER = p5.prototype.CENTER;
  var LEFT = p5.prototype.LEFT;
  var BOTTOM = p5.prototype.BOTTOM;

  /**
  * The sprite's position of the sprite as a vector (x,y).
  * @property position
  * @type {p5.Vector}
  */
  this.position = createVector(_x, _y);

  /**
  * The sprite's position at the beginning of the last update as a vector (x,y).
  * @property previousPosition
  * @type {p5.Vector}
  */
  this.previousPosition = createVector(_x, _y);

  /*
  The sprite's position at the end of the last update as a vector (x,y).
  Note: this will differ from position whenever the position is changed
  directly by assignment.
  */
  this.newPosition = createVector(_x, _y);

  //Position displacement on the x coordinate since the last update
  this.deltaX = 0;
  this.deltaY = 0;

  /**
  * The sprite's velocity as a vector (x,y)
  * Velocity is speed broken down to its vertical and horizontal components.
  *
  * @property velocity
  * @type {p5.Vector}
  */
  this.velocity = createVector(0, 0);

  /**
  * Set a limit to the sprite's scalar speed regardless of the direction.
  * The value can only be positive. If set to -1, there's no limit.
  *
  * @property maxSpeed
  * @type {Number}
  * @default -1
  */
  this.maxSpeed = -1;

  /**
  * Friction factor, reduces the sprite's velocity.
  * The friction should be close to 0 (eg. 0.01)
  * 0: no friction
  * 1: full friction
  *
  * @property friction
  * @type {Number}
  * @default 0
  */
  this.friction = 0;

  /**
  * The sprite's current collider.
  * It can either be an Axis Aligned Bounding Box (a non-rotated rectangle)
  * or a circular collider.
  * If the sprite is checked for collision, bounce, overlapping or mouse events the
  * collider is automatically created from the width and height
  * of the sprite or from the image dimension in case of animate sprites
  *
  * You can set a custom collider with Sprite.setCollider
  *
  * @property collider
  * @type {Object}
  */
  this.collider = undefined;

  /**
  * Object containing information about the most recent collision/overlapping
  * To be typically used in combination with Sprite.overlap or Sprite.collide
  * functions.
  * The properties are touching.left, touching.right, touching.top,
  * touching.bottom and are either true or false depending on the side of the
  * collider.
  *
  * @property touching
  * @type {Object}
  */
  this.touching = {};
  this.touching.left = false;
  this.touching.right = false;
  this.touching.top = false;
  this.touching.bottom = false;

  /**
  * The mass determines the velocity transfer when sprites bounce
  * against each other. See Sprite.bounce
  * The higher the mass the least the sprite will be affected by collisions.
  *
  * @property mass
  * @type {Number}
  * @default 1
  */
  this.mass = 1;

  /**
  * If set to true the sprite won't bounce or be displaced by collisions
  * Simulates an infinite mass or an anchored object.
  *
  * @property immovable
  * @type {Boolean}
  * @default false
  */
  this.immovable = false;

  //Coefficient of restitution - velocity lost in the bouncing
  //0 perfectly inelastic , 1 elastic, > 1 hyper elastic

  /**
  * Coefficient of restitution. The velocity lost after bouncing.
  * 1: perfectly elastic, no energy is lost
  * 0: perfectly inelastic, no bouncing
  * less than 1: inelastic, this is the most common in nature
  * greater than 1: hyper elastic, energy is increased like in a pinball bumper
  *
  * @property restitution
  * @type {Number}
  * @default 1
  */
  this.restitution = 1;

  /**
  * Rotation in degrees of the visual element (image or animation)
  * Note: this is not the movement's direction, see getDirection.
  *
  * @property rotation
  * @type {Number}
  * @default 0
  */
  Object.defineProperty(this, 'rotation', {
    enumerable: true,
    get: function() {
      return this._rotation;
    },
    set: function(value) {
      this._rotation = value;
      if (this.rotateToDirection) {
        this.setSpeed(this.getSpeed(), value);
      }
    }
  });

  /**
  * Internal rotation variable (expressed in degrees).
  * Note: external callers access this through the rotation property above.
  *
  * @private
  * @property _rotation
  * @type {Number}
  * @default 0
  */
  this._rotation = 0;

  /**
  * Rotation change in degrees per frame of thevisual element (image or animation)
  * Note: this is not the movement's direction, see getDirection.
  *
  * @property rotationSpeed
  * @type {Number}
  * @default 0
  */
  this.rotationSpeed = 0;


  /**
  * Automatically lock the rotation property of the visual element
  * (image or animation) to the sprite's movement direction and vice versa.
  *
  * @property rotateToDirection
  * @type {Boolean}
  * @default false
  */
  this.rotateToDirection = false;


  /**
  * Determines the rendering order within a group: a sprite with
  * lower depth will appear below the ones with higher depth.
  *
  * Note: drawing a group before another with drawSprites will make
  * its members appear below the second one, like in normal p5 canvas
  * drawing.
  *
  * @property depth
  * @type {Number}
  * @default One more than the greatest existing sprite depth, when calling
  *          createSprite().  When calling new Sprite() directly, depth will
  *          initialize to 0 (not recommended).
  */
  this.depth = 0;

  /**
  * Determines the sprite's scale.
  * Example: 2 will be twice the native size of the visuals,
  * 0.5 will be half. Scaling up may make images blurry.
  *
  * @property scale
  * @type {Number}
  * @default 1
  */
  this.scale = 1;

  var dirX = 1;
  var dirY = 1;

  /**
  * The sprite's visibility.
  *
  * @property visible
  * @type {Boolean}
  * @default true
  */
  this.visible = true;

  /**
  * If set to true sprite will track its mouse state.
  * the properties mouseIsPressed and mouseIsOver will be updated.
  * Note: automatically set to true if the functions
  * onMouseReleased or onMousePressed are set.
  *
  * @property mouseActive
  * @type {Boolean}
  * @default false
  */
  this.mouseActive = false;

  /**
  * True if mouse is on the sprite's collider.
  * Read only.
  *
  * @property mouseIsOver
  * @type {Boolean}
  */
  this.mouseIsOver = false;

  /**
  * True if mouse is pressed on the sprite's collider.
  * Read only.
  *
  * @property mouseIsPressed
  * @type {Boolean}
  */
  this.mouseIsPressed = false;

  /**
  * Represents the opacity of the sprite, on a scale from 0 to 1, with 1 being fully
  * opaque. Default value is 1.
  * Read only.
  *
  * @property alpha
  * @type {Number}
  * @default 1
  */
  this.alpha = 1;

  /*
  * Width of the sprite's current image.
  * If no images or animations are set it's the width of the
  * placeholder rectangle.
  * Used internally to make calculations and draw the sprite.
  *
  * @private
  * @property _internalWidth
  * @type {Number}
  * @default 100
  */
  this._internalWidth = _w;

  /*
  * Height of the sprite's current image.
  * If no images or animations are set it's the height of the
  * placeholder rectangle.
  * Used internally to make calculations and draw the sprite.
  *
  * @private
  * @property _internalHeight
  * @type {Number}
  * @default 100
  */
  this._internalHeight = _h;

  /*
   * @type {number}
   * @private
   * _horizontalStretch is the value to scale animation sprites in the X direction
   */
  this._horizontalStretch = 1;

  /*
   * @type {number}
   * @private
   * _verticalStretch is the value to scale animation sprites in the Y direction
   */
  this._verticalStretch = 1;

  /*
   * _internalWidth and _internalHeight are used for all p5.play
   * calculations, but width and height can be extended. For example,
   * you may want users to always get and set a scaled width:
      Object.defineProperty(this, 'width', {
        enumerable: true,
        configurable: true,
        get: function() {
          return this._internalWidth * this.scale;
        },
        set: function(value) {
          this._internalWidth = value / this.scale;
        }
      });
   */

  /**
  * Width of the sprite's current image.
  * If no images or animations are set it's the width of the
  * placeholder rectangle.
  *
  * @property width
  * @type {Number}
  * @default 100
  */
  Object.defineProperty(this, 'width', {
    enumerable: true,
    configurable: true,
    get: function() {
      if (this._internalWidth === undefined) {
        return 100;
      } else if (this.animation && pInst._fixedSpriteAnimationFrameSizes) {
        return this._internalWidth * this._horizontalStretch;
      } else {
        return this._internalWidth;
      }
    },
    set: function(value) {
      if (this.animation && pInst._fixedSpriteAnimationFrameSizes) {
        this._horizontalStretch = value / this._internalWidth;
      } else {
        this._internalWidth = value;
      }
    }
  });

  if(_w === undefined)
    this.width = 100;
  else
    this.width = _w;

  /**
  * Height of the sprite's current image.
  * If no images or animations are set it's the height of the
  * placeholder rectangle.
  *
  * @property height
  * @type {Number}
  * @default 100
  */
  Object.defineProperty(this, 'height', {
    enumerable: true,
    configurable: true,
    get: function() {
      if (this._internalHeight === undefined) {
        return 100;
      } else if (this.animation && pInst._fixedSpriteAnimationFrameSizes) {
        return this._internalHeight * this._verticalStretch;
      } else {
        return this._internalHeight;
      }
    },
    set: function(value) {
      if (this.animation && pInst._fixedSpriteAnimationFrameSizes) {
        this._verticalStretch = value / this._internalHeight;
      } else {
        this._internalHeight = value;
      }
    }
  });

  if(_h === undefined)
    this.height = 100;
  else
    this.height = _h;

  /**
  * Unscaled width of the sprite
  * If no images or animations are set it's the width of the
  * placeholder rectangle.
  *
  * @property originalWidth
  * @type {Number}
  * @default 100
  */
  this.originalWidth = this._internalWidth;

  /**
  * Unscaled height of the sprite
  * If no images or animations are set it's the height of the
  * placeholder rectangle.
  *
  * @property originalHeight
  * @type {Number}
  * @default 100
  */
  this.originalHeight = this._internalHeight;

  /**
   * Gets the scaled width of the sprite.
   *
   * @method getScaledWidth
   * @return {Number} Scaled width
   */
  this.getScaledWidth = function() {
    return this.width * this.scale;
  };

  /**
   * Gets the scaled height of the sprite.
   *
   * @method getScaledHeight
   * @return {Number} Scaled height
   */
  this.getScaledHeight = function() {
    return this.height * this.scale;
  };

  /**
  * True if the sprite has been removed.
  *
  * @property removed
  * @type {Boolean}
  */
  this.removed = false;

  /**
  * Cycles before self removal.
  * Set it to initiate a countdown, every draw cycle the property is
  * reduced by 1 unit. At 0 it will call a sprite.remove()
  * Disabled if set to -1.
  *
  * @property life
  * @type {Number}
  * @default -1
  */
  this.life = -1;

  /**
  * If set to true, draws an outline of the collider, the depth, and center.
  *
  * @property debug
  * @type {Boolean}
  * @default false
  */
  this.debug = false;

  /**
  * If no image or animations are set this is the color of the
  * placeholder rectangle
  *
  * @property shapeColor
  * @type {color}
  */
  this.shapeColor = color(127, 127, 127);

  /**
  * Groups the sprite belongs to, including allSprites
  *
  * @property groups
  * @type {Array}
  */
  this.groups = [];

  var animations = {};

  //The current animation's label.
  var currentAnimation = '';

  /**
  * Reference to the current animation.
  *
  * @property animation
  * @type {Animation}
  */
  this.animation = undefined;

  /**
   * Swept collider oriented along the current velocity vector, extending to
   * cover the old and new positions of the sprite.
   *
   * The corners of the swept collider will extend beyond the actual swept
   * shape, but it should be sufficient for broad-phase detection of collision
   * candidates.
   *
   * Note that this collider will have no dimensions if the source sprite has no
   * velocity.
   */
  this._sweptCollider = undefined;

  /**
  * Sprite x position (alias to position.x).
  *
  * @property x
  * @type {Number}
  */
  Object.defineProperty(this, 'x', {
    enumerable: true,
    get: function() {
      return this.position.x;
    },
    set: function(value) {
      this.position.x = value;
    }
  });

  /**
  * Sprite y position (alias to position.y).
  *
  * @property y
  * @type {Number}
  */
  Object.defineProperty(this, 'y', {
    enumerable: true,
    get: function() {
      return this.position.y;
    },
    set: function(value) {
      this.position.y = value;
    }
  });

  /**
  * Sprite x velocity (alias to velocity.x).
  *
  * @property velocityX
  * @type {Number}
  */
  Object.defineProperty(this, 'velocityX', {
    enumerable: true,
    get: function() {
      return this.velocity.x;
    },
    set: function(value) {
      this.velocity.x = value;
    }
  });

  /**
  * Sprite y velocity (alias to velocity.y).
  *
  * @property velocityY
  * @type {Number}
  */
  Object.defineProperty(this, 'velocityY', {
    enumerable: true,
    get: function() {
      return this.velocity.y;
    },
    set: function(value) {
      this.velocity.y = value;
    }
  });

  /**
  * Sprite lifetime (alias to life).
  *
  * @property lifetime
  * @type {Number}
  */
  Object.defineProperty(this, 'lifetime', {
    enumerable: true,
    get: function() {
      return this.life;
    },
    set: function(value) {
      this.life = value;
    }
  });

  /**
  * Sprite bounciness (alias to restitution).
  *
  * @property bounciness
  * @type {Number}
  */
  Object.defineProperty(this, 'bounciness', {
    enumerable: true,
    get: function() {
      return this.restitution;
    },
    set: function(value) {
      this.restitution = value;
    }
  });

  /**
  * Sprite animation frame delay (alias to animation.frameDelay).
  *
  * @property frameDelay
  * @type {Number}
  */
  Object.defineProperty(this, 'frameDelay', {
    enumerable: true,
    get: function() {
      return this.animation && this.animation.frameDelay;
    },
    set: function(value) {
      if (this.animation) {
        this.animation.frameDelay = value;
      }
    }
  });

  /**
   * If the sprite is moving, use the swept collider. Otherwise use the actual
   * collider.
   */
  this._getBroadPhaseCollider = function() {
    return (this.velocity.magSq() > 0) ? this._sweptCollider : this.collider;
  };

  /**
   * Returns true if the two sprites crossed paths in the current frame,
   * indicating a possible collision.
   */
  this._doSweptCollidersOverlap = function(target) {
    var displacement = this._getBroadPhaseCollider().collide(target._getBroadPhaseCollider());
    return displacement.x !== 0 || displacement.y !== 0;
  };

  /*
   * @private
   * Keep animation properties in sync with how the animation changes.
   */
  this._syncAnimationSizes = function(animations, currentAnimation) {
    if (pInst._fixedSpriteAnimationFrameSizes) {
      return;
    }
    if(animations[currentAnimation].frameChanged || this.width === undefined || this.height === undefined)
    {
      this._internalWidth = animations[currentAnimation].getWidth()*abs(this._getScaleX());
      this._internalHeight = animations[currentAnimation].getHeight()*abs(this._getScaleY());
    }
  };

  /**
  * Updates the sprite.
  * Called automatically at the beginning of the draw cycle.
  *
  * @method update
  */
  this.update = function() {

    if(!this.removed)
    {
      if (this._sweptCollider && this.velocity.magSq() > 0) {
        this._sweptCollider.updateSweptColliderFromSprite(this);
      }

      //if there has been a change somewhere after the last update
      //the old position is the last position registered in the update
      if(this.newPosition !== this.position)
        this.previousPosition = createVector(this.newPosition.x, this.newPosition.y);
      else
        this.previousPosition = createVector(this.position.x, this.position.y);

      this.velocity.x *= 1 - this.friction;
      this.velocity.y *= 1 - this.friction;

      if(this.maxSpeed !== -1)
        this.limitSpeed(this.maxSpeed);

      if(this.rotateToDirection && this.velocity.mag() > 0)
        this._rotation = this.getDirection();

      this.rotation += this.rotationSpeed;

      this.position.x += this.velocity.x;
      this.position.y += this.velocity.y;

      this.newPosition = createVector(this.position.x, this.position.y);

      this.deltaX = this.position.x - this.previousPosition.x;
      this.deltaY = this.position.y - this.previousPosition.y;

      //if there is an animation
      if(animations[currentAnimation])
      {
        //update it
        animations[currentAnimation].update();

        this._syncAnimationSizes(animations, currentAnimation);
      }

      //a collider is created either manually with setCollider or
      //when I check this sprite for collisions or overlaps
      if (this.collider) {
        this.collider.updateFromSprite(this);
      }

      //mouse actions
      if (this.mouseActive)
      {
        //if no collider set it
          if(!this.collider)
            this.setDefaultCollider();

        this.mouseUpdate();
      }
      else
      {
        if (typeof(this.onMouseOver) === 'function' ||
            typeof(this.onMouseOut) === 'function' ||
            typeof(this.onMousePressed) === 'function' ||
            typeof(this.onMouseReleased) === 'function')
        {
          //if a mouse function is set
          //it's implied we want to have it mouse active so
          //we do this automatically
          this.mouseActive = true;

          //if no collider set it
          if(!this.collider)
            this.setDefaultCollider();

          this.mouseUpdate();
        }
      }

      //self destruction countdown
      if (this.life>0)
        this.life--;
      if (this.life === 0)
        this.remove();
    }
  };//end update

  /**
   * Creates a default collider matching the size of the
   * placeholder rectangle or the bounding box of the image.
   *
   * @method setDefaultCollider
   */
  this.setDefaultCollider = function() {
    if(animations[currentAnimation] && animations[currentAnimation].getWidth() === 1 && animations[currentAnimation].getHeight() === 1) {
      //animation is still loading
      return;
    }
    this.setCollider('rectangle');
  };

  /**
   * Updates the sprite mouse states and triggers the mouse events:
   * onMouseOver, onMouseOut, onMousePressed, onMouseReleased
   *
   * @method mouseUpdate
   */
  this.mouseUpdate = function() {
    var mouseWasOver = this.mouseIsOver;
    var mouseWasPressed = this.mouseIsPressed;

    this.mouseIsOver = false;
    this.mouseIsPressed = false;

    //rollover
    if(this.collider) {
      var mousePosition;

      if(camera.active)
        mousePosition = createVector(camera.mouseX, camera.mouseY);
      else
        mousePosition = createVector(pInst.mouseX, pInst.mouseY);

      this.mouseIsOver = this.collider.overlap(new p5.PointCollider(mousePosition));

      //global p5 var
      if(this.mouseIsOver && (pInst.mouseIsPressed || pInst.touchIsDown))
        this.mouseIsPressed = true;

      //event change - call functions
      if(!mouseWasOver && this.mouseIsOver && this.onMouseOver !== undefined)
        if(typeof(this.onMouseOver) === 'function')
          this.onMouseOver.call(this, this);
        else
          print('Warning: onMouseOver should be a function');

      if(mouseWasOver && !this.mouseIsOver && this.onMouseOut !== undefined)
        if(typeof(this.onMouseOut) === 'function')
          this.onMouseOut.call(this, this);
        else
          print('Warning: onMouseOut should be a function');

      if(!mouseWasPressed && this.mouseIsPressed && this.onMousePressed !== undefined)
        if(typeof(this.onMousePressed) === 'function')
          this.onMousePressed.call(this, this);
        else
          print('Warning: onMousePressed should be a function');

      if(mouseWasPressed && !pInst.mouseIsPressed && !this.mouseIsPressed && this.onMouseReleased !== undefined)
        if(typeof(this.onMouseReleased) === 'function')
          this.onMouseReleased.call(this, this);
        else
          print('Warning: onMouseReleased should be a function');

    }
  };

  /**
  * Sets a collider for the sprite.
  *
  * In p5.play a Collider is an invisible circle or rectangle
  * that can have any size or position relative to the sprite and which
  * will be used to detect collisions and overlapping with other sprites,
  * or the mouse cursor.
  *
  * If the sprite is checked for collision, bounce, overlapping or mouse events
  * a rectangle collider is automatically created from the width and height
  * parameter passed at the creation of the sprite or the from the image
  * dimension in case of animated sprites.
  *
  * Often the image bounding box is not appropriate as the active area for
  * collision detection so you can set a circular or rectangular sprite with
  * different dimensions and offset from the sprite's center.
  *
  * There are many ways to call this method.  The first argument determines the
  * type of collider you are creating, which in turn changes the remaining
  * arguments.  Valid collider types are:
  *
  * * `point` - A point collider with no dimensions, only a position.
  *
  *   `setCollider("point"[, offsetX, offsetY])`
  *
  * * `circle` - A circular collider with a set radius.
  *
  *   `setCollider("circle"[, offsetX, offsetY[, radius])`
  *
  * * `rectangle` - An alias for `aabb`, below.
  *
  * * `aabb` - An axis-aligned bounding box - has width and height but no rotation.
  *
  *   `setCollider("aabb"[, offsetX, offsetY[, width, height]])`
  *
  * * `obb` - An oriented bounding box - has width, height, and rotation.
  *
  *   `setCollider("obb"[, offsetX, offsetY[, width, height[, rotation]]])`
  *
  *
  * @method setCollider
  * @param {String} type One of "point", "circle", "rectangle", "aabb" or "obb"
  * @param {Number} [offsetX] Collider x position from the center of the sprite
  * @param {Number} [offsetY] Collider y position from the center of the sprite
  * @param {Number} [width] Collider width or radius
  * @param {Number} [height] Collider height
  * @param {Number} [rotation] Collider rotation in degrees
  * @throws {TypeError} if given invalid parameters.
  */
  this.setCollider = function(type, offsetX, offsetY, width, height, rotation) {
    var _type = type ? type.toLowerCase() : '';
    if (_type === 'rectangle') {
      // Map 'rectangle' to AABB.  Change this if you want it to default to OBB.
      _type = 'obb';
    }

    // Check correct arguments, provide context-sensitive usage message if wrong.
    if (!(_type === 'point' || _type === 'circle' || _type === 'obb' || _type === 'aabb')) {
      throw new TypeError('setCollider expects the first argument to be one of "point", "circle", "rectangle", "aabb" or "obb"');
    } else if (_type === 'point' && !(arguments.length === 1 || arguments.length === 3)) {
      throw new TypeError('Usage: setCollider("' + type + '"[, offsetX, offsetY])');
    } else if (_type === 'circle' && !(arguments.length === 1 || arguments.length === 3 || arguments.length === 4)) {
      throw new TypeError('Usage: setCollider("' + type + '"[, offsetX, offsetY[, radius]])');
    } else if (_type === 'aabb' && !(arguments.length === 1 || arguments.length === 3 || arguments.length === 5)) {
      throw new TypeError('Usage: setCollider("' + type + '"[, offsetX, offsetY[, width, height]])');
    } else if (_type === 'obb' && !(arguments.length === 1 || arguments.length === 3 || arguments.length === 5 || arguments.length === 6)) {
      throw new TypeError('Usage: setCollider("' + type + '"[, offsetX, offsetY[, width, height[, rotation]]])');
    }

    //var center = this.position;
    var offset = createVector(offsetX, offsetY);

    if (_type === 'point') {
      this.collider = p5.PointCollider.createFromSprite(this, offset);
    } else if (_type === 'circle') {
      this.collider = p5.CircleCollider.createFromSprite(this, offset, width);
    } else if (_type === 'aabb') {
      this.collider = p5.AxisAlignedBoundingBoxCollider.createFromSprite(this, offset, width, height);
    } else if (_type === 'obb') {
      this.collider = p5.OrientedBoundingBoxCollider.createFromSprite(this, offset, width, height, radians(rotation));
    }

    this._sweptCollider = new p5.OrientedBoundingBoxCollider();

    // Disabled for Code.org, since perf seems better without the quadtree:
    // quadTree.insert(this);
  };

  /**
  * Sets the sprite's horizontal mirroring.
  * If 1 the images displayed normally
  * If -1 the images are flipped horizontally
  * If no argument returns the current x mirroring
  *
  * @method mirrorX
  * @param {Number} dir Either 1 or -1
  * @return {Number} Current mirroring if no parameter is specified
  */
  this.mirrorX = function(dir) {
    if(dir === 1 || dir === -1)
      dirX = dir;
    else
      return dirX;
  };

  /**
  * Sets the sprite's vertical mirroring.
  * If 1 the images displayed normally
  * If -1 the images are flipped vertically
  * If no argument returns the current y mirroring
  *
  * @method mirrorY
  * @param {Number} dir Either 1 or -1
  * @return {Number} Current mirroring if no parameter is specified
  */
  this.mirrorY = function(dir) {
    if(dir === 1 || dir === -1)
      dirY = dir;
    else
      return dirY;
  };

  /*
   * Returns the value the sprite should be scaled in the X direction.
   * Used to calculate rendering and collisions.
   * When _fixedSpriteAnimationFrameSizes is set, the scale value should
   * include the horizontal stretch for animations.
   * @private
   */
  this._getScaleX = function()
  {
    if (pInst._fixedSpriteAnimationFrameSizes) {
      return this.scale * this._horizontalStretch;
    }
    return this.scale;
  };

  /*
   * Returns the value the sprite should be scaled in the Y direction.
   * Used to calculate rendering and collisions.
   * When _fixedSpriteAnimationFrameSizes is set, the scale value should
   * include the vertical stretch for animations.
   * @private
   */
  this._getScaleY = function()
  {
    if (pInst._fixedSpriteAnimationFrameSizes) {
      return this.scale * this._verticalStretch;
    }
    return this.scale;
  };

  /**
   * Manages the positioning, scale and rotation of the sprite
   * Called automatically, it should not be overridden
   * @private
   * @final
   * @method display
   */
  this.display = function()
  {
    if (this.visible && !this.removed)
    {
      push();
      colorMode(RGB);

      noStroke();
      rectMode(CENTER);
      ellipseMode(CENTER);
      imageMode(CENTER);

      translate(this.position.x, this.position.y);
      if (pInst._angleMode === pInst.RADIANS) {
        rotate(radians(this.rotation));
      } else {
        rotate(this.rotation);
      }
      scale(this._getScaleX()*dirX, this._getScaleY()*dirY);
      this.draw();
      //draw debug info
      pop();


      if(this.debug)
      {
        push();
        //draw the anchor point
        stroke(0, 255, 0);
        strokeWeight(1);
        line(this.position.x-10, this.position.y, this.position.x+10, this.position.y);
        line(this.position.x, this.position.y-10, this.position.x, this.position.y+10);
        noFill();

        //depth number
        noStroke();
        fill(0, 255, 0);
        textAlign(LEFT, BOTTOM);
        textSize(16);
        text(this.depth+'', this.position.x+4, this.position.y-2);

        noFill();
        stroke(0, 255, 0);

        // Draw collision shape
        if (this.collider === undefined) {
          this.setDefaultCollider();
        }
        if(this.collider) {
          this.collider.draw(pInst);
        }
        pop();
      }

    }
  };


  /**
  * Manages the visuals of the sprite.
  * It can be overridden with a custom drawing function.
  * The 0,0 point will be the center of the sprite.
  * Example:
  * sprite.draw = function() { ellipse(0,0,10,10) }
  * Will display the sprite as circle.
  *
  * @method draw
  */
  this.draw = function()
  {
    if(currentAnimation !== '' && animations)
    {
      if(animations[currentAnimation]) {
        if(this.tint) {
          push();
          tint(this.tint);
        }
        if(this.alpha < 1) {
          push();
          alphaTint(this.alpha);
        }
        animations[currentAnimation].draw(0, 0, 0);
        if(this.alpha < 1) {
          pop();
        }
        if(this.tint) {
          pop();
        }
      }
    }
    else
    {
      var fillColor = this.shapeColor;
      if (this.tint) {
        fillColor = lerpColor(color(fillColor), color(this.tint), 0.5);
      }
      noStroke();
      fill(fillColor);
      rect(0, 0, this._internalWidth, this._internalHeight);
    }
  };

  /**
   * Removes the Sprite from the sketch.
   * The removed Sprite won't be drawn or updated anymore.
   *
   * @method remove
   */
  this.remove = function() {
    this.removed = true;

    quadTree.removeObject(this);

    //when removed from the "scene" also remove all the references in all the groups
    while (this.groups.length > 0) {
      this.groups[0].remove(this);
    }
  };

  /**
   * Alias for <a href='#method-remove'>remove()</a>
   *
   * @method destroy
   */
  this.destroy = this.remove;

  /**
  * Sets the velocity vector.
  *
  * @method setVelocity
  * @param {Number} x X component
  * @param {Number} y Y component
  */
  this.setVelocity = function(x, y) {
    this.velocity.x = x;
    this.velocity.y = y;
  };

  /**
  * Calculates the scalar speed.
  *
  * @method getSpeed
  * @return {Number} Scalar speed
  */
  this.getSpeed = function() {
    return this.velocity.mag();
  };

  /**
  * Calculates the movement's direction in degrees.
  *
  * @method getDirection
  * @return {Number} Angle in degrees
  */
  this.getDirection = function() {

    var direction = atan2(this.velocity.y, this.velocity.x);

    if(isNaN(direction))
      direction = 0;

    // Unlike Math.atan2, the atan2 method above will return degrees if
    // the current p5 angleMode is DEGREES, and radians if the p5 angleMode is
    // RADIANS.  This method should always return degrees (for now).
    // See https://github.com/molleindustria/p5.play/issues/94
    if (pInst._angleMode === pInst.RADIANS) {
      direction = degrees(direction);
    }

    return direction;
  };

  /**
  * Adds the sprite to an existing group
  *
  * @method addToGroup
  * @param {Object} group
  */
  this.addToGroup = function(group) {
    if(group instanceof Array)
      group.add(this);
    else
      print('addToGroup error: '+group+' is not a group');
  };

  /**
  * Limits the scalar speed.
  *
  * @method limitSpeed
  * @param {Number} max Max speed: positive number
  */
  this.limitSpeed = function(max) {

    //update linear speed
    var speed = this.getSpeed();

    if(abs(speed)>max)
    {
      //find reduction factor
      var k = max/abs(speed);
      this.velocity.x *= k;
      this.velocity.y *= k;
    }
  };

  /**
  * Set the speed and direction of the sprite.
  * The action overwrites the current velocity.
  * If direction is not supplied, the current direction is maintained.
  * If direction is not supplied and there is no current velocity, the current
  * rotation angle used for the direction.
  *
  * @method setSpeed
  * @param {Number}  speed Scalar speed
  * @param {Number}  [angle] Direction in degrees
  */
  this.setSpeed = function(speed, angle) {
    var a;
    if (typeof angle === 'undefined') {
      if (this.velocity.x !== 0 || this.velocity.y !== 0) {
        a = pInst.atan2(this.velocity.y, this.velocity.x);
      } else {
        if (pInst._angleMode === pInst.RADIANS) {
          a = radians(this._rotation);
        } else {
          a = this._rotation;
        }
      }
    } else {
      if (pInst._angleMode === pInst.RADIANS) {
        a = radians(angle);
      } else {
        a = angle;
      }
    }
    this.velocity.x = cos(a)*speed;
    this.velocity.y = sin(a)*speed;
  };

  /**
   * Alias for <a href='#method-setSpeed'>setSpeed()</a>
   *
   * @method setSpeedAndDirection
   * @param {Number}  speed Scalar speed
   * @param {Number}  [angle] Direction in degrees
   */
  this.setSpeedAndDirection = this.setSpeed;

  /**
  * Alias for <a href='Animation.html#method-changeFrame'>animation.changeFrame()</a>
  *
  * @method setFrame
  * @param {Number} frame Frame number (starts from 0).
  */
  this.setFrame = function(f) {
    if (this.animation) {
      this.animation.changeFrame(f);
    }
  };

  /**
  * Alias for <a href='Animation.html#method-nextFrame'>animation.nextFrame()</a>
  *
  * @method nextFrame
  */
  this.nextFrame = function() {
    if (this.animation) {
      this.animation.nextFrame();
    }
  };

  /**
  * Alias for <a href='Animation.html#method-previousFrame'>animation.previousFrame()</a>
  *
  * @method previousFrame
  */
  this.previousFrame = function() {
    if (this.animation) {
      this.animation.previousFrame();
    }
  };

  /**
  * Alias for <a href='Animation.html#method-stop'>animation.stop()</a>
  *
  * @method pause
  */
  this.pause = function() {
    if (this.animation) {
      this.animation.stop();
    }
  };

  /**
   * Alias for <a href='Animation.html#method-play'>animation.play()</a> with extra logic
   *
   * Plays/resumes the sprite's current animation.
   * If the animation is currently playing this has no effect.
   * If the animation has stopped at its last frame, this will start it over
   * at the beginning.
   *
   * @method play
   */
  this.play = function() {
    if (!this.animation) {
      return;
    }
    // Normally this just sets the 'playing' flag without changing the animation
    // frame, which will cause the animation to continue on the next update().
    // If the animation is non-looping and is stopped at the last frame
    // we also rewind the animation to the beginning.
    if (!this.animation.looping && !this.animation.playing && this.animation.getFrame() === this.animation.images.length - 1) {
      this.animation.rewind();
    }
    this.animation.play();
  };

  /**
   * Wrapper to access <a href='Animation.html#prop-frameChanged'>animation.frameChanged</a>
   *
   * @method frameDidChange
   * @return {Boolean} true if the animation frame has changed
   */
  this.frameDidChange = function() {
    return this.animation ? this.animation.frameChanged : false;
  };

  /**
  * Rotate the sprite towards a specific position
  *
  * @method setFrame
  * @param {Number} x Horizontal coordinate to point to
  * @param {Number} y Vertical coordinate to point to
  */
  this.pointTo = function(x, y) {
    var yDelta = y - this.position.y;
    var xDelta = x - this.position.x;
    if (!isNaN(xDelta) && !isNaN(yDelta) && (xDelta !== 0 || yDelta !== 0)) {
      var radiansAngle = Math.atan2(yDelta, xDelta);
      this.rotation = 360 * radiansAngle / (2 * Math.PI);
    }
  };

  /**
  * Pushes the sprite in a direction defined by an angle.
  * The force is added to the current velocity.
  *
  * @method addSpeed
  * @param {Number}  speed Scalar speed to add
  * @param {Number}  angle Direction in degrees
  */
  this.addSpeed = function(speed, angle) {
    var a;
    if (pInst._angleMode === pInst.RADIANS) {
      a = radians(angle);
    } else {
      a = angle;
    }
    this.velocity.x += cos(a) * speed;
    this.velocity.y += sin(a) * speed;
  };

  /**
  * Pushes the sprite toward a point.
  * The force is added to the current velocity.
  *
  * @method attractionPoint
  * @param {Number}  magnitude Scalar speed to add
  * @param {Number}  pointX Direction x coordinate
  * @param {Number}  pointY Direction y coordinate
  */
  this.attractionPoint = function(magnitude, pointX, pointY) {
    var angle = atan2(pointY-this.position.y, pointX-this.position.x);
    this.velocity.x += cos(angle) * magnitude;
    this.velocity.y += sin(angle) * magnitude;
  };


  /**
  * Adds an image to the sprite.
  * An image will be considered a one-frame animation.
  * The image should be preloaded in the preload() function using p5 loadImage.
  * Animations require a identifying label (string) to change them.
  * The image is stored in the sprite but not necessarily displayed
  * until Sprite.changeAnimation(label) is called
  *
  * Usages:
  * - sprite.addImage(label, image);
  * - sprite.addImage(image);
  *
  * If only an image is passed no label is specified
  *
  * @method addImage
  * @param {String|p5.Image} label Label or image
  * @param {p5.Image} [img] Image
  */
  this.addImage = function()
  {
    if(typeof arguments[0] === 'string' && arguments[1] instanceof p5.Image)
      this.addAnimation(arguments[0], arguments[1]);
    else if(arguments[0] instanceof p5.Image)
      this.addAnimation('normal', arguments[0]);
    else
      throw('addImage error: allowed usages are <image> or <label>, <image>');
  };

  /**
  * Adds an animation to the sprite.
  * The animation should be preloaded in the preload() function
  * using loadAnimation.
  * Animations require a identifying label (string) to change them.
  * Animations are stored in the sprite but not necessarily displayed
  * until Sprite.changeAnimation(label) is called.
  *
  * Usage:
  * - sprite.addAnimation(label, animation);
  *
  * Alternative usages. See Animation for more information on file sequences:
  * - sprite.addAnimation(label, firstFrame, lastFrame);
  * - sprite.addAnimation(label, frame1, frame2, frame3...);
  *
  * @method addAnimation
  * @param {String} label Animation identifier
  * @param {Animation} animation The preloaded animation
  */
  this.addAnimation = function(label)
  {
    var anim;

    if(typeof label !== 'string')
    {
      print('Sprite.addAnimation error: the first argument must be a label (String)');
      return -1;
    }
    else if(arguments.length < 2)
    {
      print('addAnimation error: you must specify a label and n frame images');
      return -1;
    }
    else if(arguments[1] instanceof Animation)
    {

      var sourceAnimation = arguments[1];

      var newAnimation = sourceAnimation.clone();

      animations[label] = newAnimation;

      if(currentAnimation === '')
      {
        currentAnimation = label;
        this.animation = newAnimation;
      }

      newAnimation.isSpriteAnimation = true;

      this._internalWidth = newAnimation.getWidth()*abs(this._getScaleX());
      this._internalHeight = newAnimation.getHeight()*abs(this._getScaleY());

      return newAnimation;
    }
    else
    {
      var animFrames = [];
      for(var i=1; i<arguments.length; i++)
        animFrames.push(arguments[i]);

      anim = construct(pInst.Animation, animFrames);
      animations[label] = anim;

      if(currentAnimation === '')
      {
        currentAnimation = label;
        this.animation = anim;
      }
      anim.isSpriteAnimation = true;

      this._internalWidth = anim.getWidth()*abs(this._getScaleX());
      this._internalHeight = anim.getHeight()*abs(this._getScaleY());

      return anim;
    }

  };

  /**
  * Changes the displayed image/animation.
  * Equivalent to changeAnimation
  *
  * @method changeImage
  * @param {String} label Image/Animation identifier
  */
  this.changeImage = function(label) {
    this.changeAnimation(label);
  };

   /**
  * Returns the label of the current animation
  *
  * @method getAnimationLabel
  * @return {String} label Image/Animation identifier
  */
  this.getAnimationLabel = function() {
    return currentAnimation;
  };

  /**
  * Changes the displayed animation.
  * See Animation for more control over the sequence.
  *
  * @method changeAnimation
  * @param {String} label Animation identifier
  */
  this.changeAnimation = function(label) {
    if(!animations[label])
      print('changeAnimation error: no animation labeled '+label);
    else
    {
      currentAnimation = label;
      this.animation = animations[label];
    }
  };

  /**
  * Sets the animation from a list in _predefinedSpriteAnimations.
  *
  * @method setAnimation
  * @private
  * @param {String} label Animation identifier
  */
  this.setAnimation = function(animationName) {
    if (animationName === this.getAnimationLabel()) {
      return;
    }

    var animation = pInst._predefinedSpriteAnimations &&
        pInst._predefinedSpriteAnimations[animationName];
    if (typeof animation === 'undefined') {
      throw new Error('Unable to find an animation named "' + animationName +
          '".  Please make sure the animation exists.');
    }
    this.addAnimation(animationName, animation);
    this.changeAnimation(animationName);
    if (pInst._pauseSpriteAnimationsByDefault) {
      this.pause();
    }
  };

  /**
  * Checks if the given point corresponds to a transparent pixel
  * in the sprite's current image. It can be used to check a point collision
  * against only the visible part of the sprite.
  *
  * @method overlapPixel
  * @param {Number} pointX x coordinate of the point to check
  * @param {Number} pointY y coordinate of the point to check
  * @return {Boolean} result True if non-transparent
  */
  this.overlapPixel = function(pointX, pointY) {
    var point = createVector(pointX, pointY);

    var img = this.animation.getFrameImage();

    //convert point to img relative position
    point.x -= this.position.x-img.width/2;
    point.y -= this.position.y-img.height/2;

    //out of the image entirely
    if(point.x<0 || point.x>img.width || point.y<0 || point.y>img.height)
      return false;
    else if(this.rotation === 0 && this.scale === 1)
    {
      //true if full opacity
      var values = img.get(point.x, point.y);
      return values[3] === 255;
    }
    else
    {
      print('Error: overlapPixel doesn\'t work with scaled or rotated sprites yet');
      //offscreen printing to be implemented bleurch
      return false;
    }
  };

  /**
  * Checks if the given point is inside the sprite's collider.
  *
  * @method overlapPoint
  * @param {Number} pointX x coordinate of the point to check
  * @param {Number} pointY y coordinate of the point to check
  * @return {Boolean} result True if inside
  */
  this.overlapPoint = function(pointX, pointY) {
    if(!this.collider)
      this.setDefaultCollider();

    if(this.collider) {
      var point = new p5.PointCollider(new p5.Vector(pointX, pointY));
      return this.collider.overlap(point);
    }
    return false;
  };


  /**
  * Checks if the the sprite is overlapping another sprite or a group.
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the overlap occours.
  * If the target is a group the function will be called for each single
  * sprite overlapping. The parameter of the function are respectively the
  * current sprite and the colliding sprite.
  *
  * @example
  *     sprite.overlap(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method overlap
  * @param {Object} target Sprite or group to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  this.overlap = function(target, callback) {
    return this._collideWith('overlap', target, callback);
  };

  /**
   * Alias for <a href='#method-overlap'>overlap()</a>, except without a
   * callback parameter.
   * The check is performed using the colliders. If colliders are not set
   * they will be created automatically from the image/animation bounding box.
   *
   * Returns whether or not this sprite is overlapping another sprite
   * or group. Modifies the sprite's touching property object.
   *
   * @method isTouching
   * @param {Object} target Sprite or group to check against the current one
   * @return {Boolean} True if touching
   */
  this.isTouching = this.overlap;

  /**
  * Checks if the the sprite is overlapping another sprite or a group.
  * If the overlap is positive the sprite will bounce with the target(s)
  * treated as immovable with a restitution coefficient of zero.
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the collision occours.
  * If the target is a group the function will be called for each single
  * sprite colliding. The parameter of the function are respectively the
  * current sprite and the colliding sprite.
  *
  * @example
  *     sprite.collide(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method collide
  * @param {Object} target Sprite or group to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  this.collide = function(target, callback) {
    return this._collideWith('collide', target, callback);
  };

  /**
  * Checks if the the sprite is overlapping another sprite or a group.
  * If the overlap is positive the current sprite will displace
  * the colliding one to the closest non-overlapping position.
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the collision occours.
  * If the target is a group the function will be called for each single
  * sprite colliding. The parameter of the function are respectively the
  * current sprite and the colliding sprite.
  *
  * @example
  *     sprite.displace(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method displace
  * @param {Object} target Sprite or group to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  this.displace = function(target, callback) {
    return this._collideWith('displace', target, callback);
  };

  /**
  * Checks if the the sprite is overlapping another sprite or a group.
  * If the overlap is positive the sprites will bounce affecting each
  * other's trajectories depending on their .velocity, .mass and .restitution
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the collision occours.
  * If the target is a group the function will be called for each single
  * sprite colliding. The parameter of the function are respectively the
  * current sprite and the colliding sprite.
  *
  * @example
  *     sprite.bounce(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method bounce
  * @param {Object} target Sprite or group to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  this.bounce = function(target, callback) {
    return this._collideWith('bounce', target, callback);
  };

  /**
  * Checks if the the sprite is overlapping another sprite or a group.
  * If the overlap is positive the sprite will bounce with the target(s)
  * treated as immovable.
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the collision occours.
  * If the target is a group the function will be called for each single
  * sprite colliding. The parameter of the function are respectively the
  * current sprite and the colliding sprite.
  *
  * @example
  *     sprite.bounceOff(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method bounceOff
  * @param {Object} target Sprite or group to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  this.bounceOff = function(target, callback) {
    return this._collideWith('bounceOff', target, callback);
  };

  /**
   * Internal collision detection function. Do not use directly.
   *
   * Handles collision with individual sprites or with groups, using the
   * quadtree to optimize the latter.
   *
   * @method _collideWith
   * @private
   * @param {string} type - 'overlap', 'isTouching', 'displace', 'collide',
   *   'bounce' or 'bounceOff'
   * @param {Sprite|Group} target
   * @param {function} callback - if collision occurred (ignored for 'isTouching')
   * @return {boolean} true if a collision occurred
   */
  this._collideWith = function(type, target, callback) {
    this.touching.left = false;
    this.touching.right = false;
    this.touching.top = false;
    this.touching.bottom = false;

    if (this.removed) {
      return false;
    }

    var others = [];

    if (target instanceof Sprite) {
      others.push(target);
    } else if (target instanceof Array) {
      if (pInst.quadTree !== undefined && pInst.quadTree.active) {
        others = pInst.quadTree.retrieveFromGroup(this, target);
      }

      // If the quadtree is disabled -or- no sprites in this group are in the
      // quadtree yet (because their default colliders haven't been created)
      // we should just check all of them.
      if (others.length === 0) {
        others = target;
      }
    } else {
      throw('Error: overlap can only be checked between sprites or groups');
    }

    var result = false;
    for(var i = 0; i < others.length; i++) {
      result = this._collideWithOne(type, others[i], callback) || result;
    }
    return result;
  };

  /**
   * Helper collision method for colliding this sprite with one other sprite.
   *
   * Has the side effect of setting this.touching properties to TRUE if collisions
   * occur.
   *
   * @method _collideWithOne
   * @private
   * @param {string} type - 'overlap', 'isTouching', 'displace', 'collide',
   *   'bounce' or 'bounceOff'
   * @param {Sprite} other
   * @param {function} callback - if collision occurred (ignored for 'isTouching')
   * @return {boolean} true if a collision occurred
   */
  this._collideWithOne = function(type, other, callback) {
    // Never collide with self
    if (other === this || other.removed) {
      return false;
    }

    if (this.collider === undefined) {
      this.setDefaultCollider();
    }

    if (other.collider === undefined) {
      other.setDefaultCollider();
    }

    if (!this.collider || !other.collider) {
      // We were unable to create a collider for one of the sprites.
      // This usually means its animation is not available yet; it will be soon.
      // Don't collide for now.
      return false;
    }

    // Actually compute the overlap of the two colliders
    var displacement = this._findDisplacement(other);
    if (displacement.x === 0 && displacement.y === 0) {
      // These sprites are not overlapping.
      return false;
    }

    if (displacement.x > 0)
      this.touching.left = true;
    if (displacement.x < 0)
      this.touching.right = true;
    if (displacement.y < 0)
      this.touching.bottom = true;
    if (displacement.y > 0)
      this.touching.top = true;

    // Apply displacement out of collision
    if (type === 'displace' && !other.immovable) {
      other.position.sub(displacement);
    } else if ((type === 'collide' || type === 'bounce' || type === 'bounceOff') && !this.immovable) {
      this.position.add(displacement);
      this.previousPosition = createVector(this.position.x, this.position.y);
      this.newPosition = createVector(this.position.x, this.position.y);
      this.collider.updateFromSprite(this);
    }

    // Create special behaviors for certain collision types by temporarily
    // overriding type and sprite properties.
    // See another block near the end of this method that puts them back.
    var originalType = type;
    var originalThisImmovable = this.immovable;
    var originalOtherImmovable = other.immovable;
    var originalOtherRestitution = other.restitution;
    if (originalType === 'collide') {
      type = 'bounce';
      other.immovable = true;
      other.restitution = 0;
    } else if (originalType === 'bounceOff') {
      type = 'bounce';
      other.immovable = true;
    }

    // If this is a 'bounce' collision, determine the new velocities for each sprite
    if (type === 'bounce') {
      // We are concerned only with velocities parallel to the collision normal,
      // so project our sprite velocities onto that normal (captured in the
      // displacement vector) and use these throughout the calculation
      var thisInitialVelocity = p5.Vector.project(this.velocity, displacement);
      var otherInitialVelocity = p5.Vector.project(other.velocity, displacement);

      // We only care about relative mass values, so if one of the sprites
      // is considered 'immovable' treat the _other_ sprite's mass as zero
      // to get the correct results.
      var thisMass = this.mass;
      var otherMass = other.mass;
      if (this.immovable) {
        thisMass = 1;
        otherMass = 0;
      } else if (other.immovable) {
        thisMass = 0;
        otherMass = 1;
      }

      var combinedMass = thisMass + otherMass;
      var coefficientOfRestitution = this.restitution * other.restitution;
      var initialMomentum = p5.Vector.add(
        p5.Vector.mult(thisInitialVelocity, thisMass),
        p5.Vector.mult(otherInitialVelocity, otherMass)
      );
      var thisFinalVelocity = p5.Vector.sub(otherInitialVelocity, thisInitialVelocity)
        .mult(otherMass * coefficientOfRestitution)
        .add(initialMomentum)
        .div(combinedMass);
      var otherFinalVelocity = p5.Vector.sub(thisInitialVelocity, otherInitialVelocity)
        .mult(thisMass * coefficientOfRestitution)
        .add(initialMomentum)
        .div(combinedMass);
      // Remove velocity before and apply velocity after to both members.
      this.velocity.sub(thisInitialVelocity).add(thisFinalVelocity);
      other.velocity.sub(otherInitialVelocity).add(otherFinalVelocity);
    }

    // Restore sprite properties now that velocity changes have been made.
    // See another block before velocity changes that sets these up.
    type = originalType;
    this.immovable = originalThisImmovable;
    other.immovable = originalOtherImmovable;
    other.restitution = originalOtherRestitution;

    // Finally, for all collision types except 'isTouching', call the callback
    // and record that collision occurred.
    if (typeof callback === 'function' && type !== 'isTouching') {
      callback.call(this, this, other);
    }
    return true;
  };

  this._findDisplacement = function(target) {
    // Multisample if tunneling occurs:
    // Do broad-phase detection. Check if the swept colliders overlap.
    // In that case, test interpolations between their last positions and their
    // current positions, and check for tunneling that way.
    // Use multisampling to catch collisions we might otherwise miss.
    if (this._doSweptCollidersOverlap(target)) {
      // Figure out how many samples we should take.
      // We want to limit this so that we don't take an absurd number of samples
      // when objects end up at very high velocities (as happens sometimes in
      // game engines).
      var radiusOnVelocityAxis = Math.max(
        this.collider._getMinRadius(),
        target.collider._getMinRadius());
      var relativeVelocity = p5.Vector.sub(this.velocity, target.velocity).mag();
      var timestep = Math.max(0.015, radiusOnVelocityAxis / relativeVelocity);
      // If the objects are small enough to benefit from multisampling at this
      // relative velocity
      if (timestep < 1) {
        // Move sprites back to previous positions
        // (We jump through some hoops here to avoid creating too many new
        //  vector objects)
        var thisOriginalPosition = this.position.copy();
        var targetOriginalPosition = target.position.copy();
        this.position.set(this.previousPosition);
        target.position.set(target.previousPosition);

        // Scale deltas down to timestep-deltas
        var thisDelta = p5.Vector.sub(thisOriginalPosition, this.previousPosition).mult(timestep);
        var targetDelta = p5.Vector.sub(targetOriginalPosition, target.previousPosition).mult(timestep);

        // Note: We don't have to check the original position, we can assume it's
        // non-colliding (or it would have been handled on the last frame).
        for (var i = timestep; i < 1; i += timestep) {
          // Move the sprites forward by the sub-frame timestep
          this.position.add(thisDelta);
          target.position.add(targetDelta);
          this.collider.updateFromSprite(this);
          target.collider.updateFromSprite(target);

          // Check for collision at the new sub-frame position
          var displacement = this.collider.collide(target.collider);
          if (displacement.x !== 0 || displacement.y !== 0) {
            // These sprites are overlapping - we have a displacement, and a
            // point-in-time for the collision.
            // If either sprite is immovable, it should move back to its final
            // position.  Otherwise, leave the sprites at their interpolated
            // position when the collision occurred.
            if (this.immovable) {
              this.position.set(thisOriginalPosition);
            }

            if (target.immovable) {
              target.position.set(targetOriginalPosition);
            }

            return displacement;
          }
        }

        // If we didn't find a displacement partway through,
        // restore the sprites to their original positions and fall through
        // to do the collision check at their final position.
        this.position.set(thisOriginalPosition);
        target.position.set(targetOriginalPosition);
      }
    }

    // Ensure the colliders are properly updated to match their parent
    // sprites. Maybe someday we won't have to do this, but for now
    // sprites aren't guaranteed to be internally consistent we do a
    // last-minute update to make sure.
    this.collider.updateFromSprite(this);
    target.collider.updateFromSprite(target);

    return this.collider.collide(target.collider);
  };
} //end Sprite class

defineLazyP5Property('Sprite', boundConstructorFactory(Sprite));

/**
   * A camera facilitates scrolling and zooming for scenes extending beyond
   * the canvas. A camera has a position, a zoom factor, and the mouse
   * coordinates relative to the view.
   * The camera is automatically created on the first draw cycle.
   *
   * In p5.js terms the camera wraps the whole drawing cycle in a
   * transformation matrix but it can be disable anytime during the draw
   * cycle for example to draw interface elements in an absolute position.
   *
   * @class Camera
   * @constructor
   * @param {Number} x Initial x coordinate
   * @param {Number} y Initial y coordinate
   * @param {Number} zoom magnification
   **/
function Camera(pInst, x, y, zoom) {
  /**
  * Camera position. Defines the global offset of the sketch.
  *
  * @property position
  * @type {p5.Vector}
  */
  this.position = pInst.createVector(x, y);

  /**
  * Camera x position. Defines the horizontal global offset of the sketch.
  *
  * @property x
  * @type {Number}
  */
  Object.defineProperty(this, 'x', {
    enumerable: true,
    get: function() {
      return this.position.x;
    },
    set: function(value) {
      this.position.x = value;
    }
  });

  /**
  * Camera y position. Defines the horizontal global offset of the sketch.
  *
  * @property y
  * @type {Number}
  */
  Object.defineProperty(this, 'y', {
    enumerable: true,
    get: function() {
      return this.position.y;
    },
    set: function(value) {
      this.position.y = value;
    }
  });

  /**
  * Camera zoom. Defines the global scale of the sketch.
  * A scale of 1 will be the normal size. Setting it to 2 will make everything
  * twice the size. .5 will make everything half size.
  *
  * @property zoom
  * @type {Number}
  */
  this.zoom = zoom;

  /**
  * MouseX translated to the camera view.
  * Offsetting and scaling the canvas will not change the sprites' position
  * nor the mouseX and mouseY variables. Use this property to read the mouse
  * position if the camera moved or zoomed.
  *
  * @property mouseX
  * @type {Number}
  */
  this.mouseX = pInst.mouseX;

  /**
  * MouseY translated to the camera view.
  * Offsetting and scaling the canvas will not change the sprites' position
  * nor the mouseX and mouseY variables. Use this property to read the mouse
  * position if the camera moved or zoomed.
  *
  * @property mouseY
  * @type {Number}
  */
  this.mouseY = pInst.mouseY;

  /**
  * True if the camera is active.
  * Read only property. Use the methods Camera.on() and Camera.off()
  * to enable or disable the camera.
  *
  * @property active
  * @type {Boolean}
  */
  this.active = false;

  /**
  * Check to see if the camera is active.
  * Use the methods Camera.on() and Camera.off()
  * to enable or disable the camera.
  *
  * @method isActive
  * @return {Boolean} true if the camera is active
  */
  this.isActive = function() {
    return this.active;
  };

  /**
  * Activates the camera.
  * The canvas will be drawn according to the camera position and scale until
  * Camera.off() is called
  *
  * @method on
  */
  this.on = function() {
    if(!this.active)
    {
      cameraPush.call(pInst);
      this.active = true;
    }
  };

  /**
  * Deactivates the camera.
  * The canvas will be drawn normally, ignoring the camera's position
  * and scale until Camera.on() is called
  *
  * @method off
  */
  this.off = function() {
    if(this.active)
    {
      cameraPop.call(pInst);
      this.active = false;
    }
  };
} //end camera class

defineLazyP5Property('Camera', boundConstructorFactory(Camera));

//called pre draw by default
function cameraPush() {
  var pInst = this;
  var camera = pInst.camera;

  //awkward but necessary in order to have the camera at the center
  //of the canvas by default
  if(!camera.init && camera.position.x === 0 && camera.position.y === 0)
    {
    camera.position.x=pInst.width/2;
    camera.position.y=pInst.height/2;
    camera.init = true;
    }

  camera.mouseX = pInst.mouseX+camera.position.x-pInst.width/2;
  camera.mouseY = pInst.mouseY+camera.position.y-pInst.height/2;

  if(!camera.active)
  {
    camera.active = true;
    pInst.push();
    pInst.scale(camera.zoom);
    pInst.translate(-camera.position.x+pInst.width/2/camera.zoom, -camera.position.y+pInst.height/2/camera.zoom);
  }
}

//called postdraw by default
function cameraPop() {
  var pInst = this;

  if(pInst.camera.active)
  {
    pInst.pop();
    pInst.camera.active = false;
  }
}




/**
   * In p5.play groups are collections of sprites with similar behavior.
   * For example a group may contain all the sprites in the background
   * or all the sprites that "kill" the player.
   *
   * Groups are "extended" arrays and inherit all their properties
   * e.g. group.length
   *
   * Since groups contain only references, a sprite can be in multiple
   * groups and deleting a group doesn't affect the sprites themselves.
   *
   * Sprite.remove() will also remove the sprite from all the groups
   * it belongs to.
   *
   * @class Group
   * @constructor
   */
function Group() {

  //basically extending the array
  var array = [];

  /**
  * Gets the member at index i.
  *
  * @method get
  * @param {Number} i The index of the object to retrieve
  */
  array.get = function(i) {
    return array[i];
  };

  /**
  * Checks if the group contains a sprite.
  *
  * @method contains
  * @param {Sprite} sprite The sprite to search
  * @return {Number} Index or -1 if not found
  */
  array.contains = function(sprite) {
    return this.indexOf(sprite)>-1;
  };

  /**
   * Same as Group.contains
   * @method indexOf
   */
  array.indexOf = function(item) {
    for (var i = 0, len = array.length; i < len; ++i) {
      if (virtEquals(item, array[i])) {
        return i;
      }
    }
    return -1;
  };

  /**
  * Adds a sprite to the group.
  *
  * @method add
  * @param {Sprite} s The sprite to be added
  */
  array.add = function(s) {
    if(!(s instanceof Sprite)) {
      throw('Error: you can only add sprites to a group');
    }

    if (-1 === this.indexOf(s)) {
      array.push(s);
      s.groups.push(this);
    }
  };

  /**
   * Same as group.length
   * @method size
   */
  array.size = function() {
    return array.length;
  };

  /**
  * Removes all the sprites in the group
  * from the scene.
  *
  * @method removeSprites
  */
  array.removeSprites = function() {
    while (array.length > 0) {
      array[0].remove();
    }
  };

  /**
  * Removes all references to the group.
  * Does not remove the actual sprites.
  *
  * @method clear
  */
  array.clear = function() {
    array.length = 0;
  };

  /**
  * Removes a sprite from the group.
  * Does not remove the actual sprite, only the affiliation (reference).
  *
  * @method remove
  * @param {Sprite} item The sprite to be removed
  * @return {Boolean} True if sprite was found and removed
  */
  array.remove = function(item) {
    if(!(item instanceof Sprite)) {
      throw('Error: you can only remove sprites from a group');
    }

    var i, removed = false;
    for (i = array.length - 1; i >= 0; i--) {
      if (array[i] === item) {
        array.splice(i, 1);
        removed = true;
      }
    }

    if (removed) {
      for (i = item.groups.length - 1; i >= 0; i--) {
        if (item.groups[i] === this) {
          item.groups.splice(i, 1);
        }
      }
    }

    return removed;
  };

  /**
   * Returns a copy of the group as standard array.
   * @method toArray
   */
  array.toArray = function() {
    return array.slice(0);
  };

  /**
  * Returns the highest depth in a group
  *
  * @method maxDepth
  * @return {Number} The depth of the sprite drawn on the top
  */
  array.maxDepth = function() {
    if (array.length === 0) {
      return 0;
    }

    return array.reduce(function(maxDepth, sprite) {
      return Math.max(maxDepth, sprite.depth);
    }, -Infinity);
  };

  /**
  * Returns the lowest depth in a group
  *
  * @method minDepth
  * @return {Number} The depth of the sprite drawn on the bottom
  */
  array.minDepth = function() {
    if (array.length === 0) {
      return 99999;
    }

    return array.reduce(function(minDepth, sprite) {
      return Math.min(minDepth, sprite.depth);
    }, Infinity);
  };

  /**
  * Draws all the sprites in the group.
  *
  * @method draw
  */
  array.draw = function() {

    //sort by depth
    this.sort(function(a, b) {
      return a.depth - b.depth;
    });

    for(var i = 0; i<this.size(); i++)
    {
      this.get(i).display();
    }
  };

  //internal use
  function virtEquals(obj, other) {
    if (obj === null || other === null) {
      return (obj === null) && (other === null);
    }
    if (typeof (obj) === 'string') {
      return obj === other;
    }
    if (typeof(obj) !== 'object') {
      return obj === other;
    }
    if (obj.equals instanceof Function) {
      return obj.equals(other);
    }
    return obj === other;
  }

  /**
   * Collide each member of group against the target using the given collision
   * type.  Return true if any collision occurred.
   * Internal use
   *
   * @private
   * @method _groupCollide
   * @param {!string} type one of 'overlap', 'collide', 'displace', 'bounce' or 'bounceOff'
   * @param {Object} target Group or Sprite
   * @param {Function} [callback] on collision.
   * @return {boolean} True if any collision/overlap occurred
   */
  function _groupCollide(type, target, callback) {
    var didCollide = false;
    for(var i = 0; i<this.size(); i++)
      didCollide = this.get(i)._collideWith(type, target, callback) || didCollide;
    return didCollide;
  }

  /**
  * Checks if the the group is overlapping another group or sprite.
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the overlap occurs.
  * The function will be called for each single sprite overlapping.
  * The parameter of the function are respectively the
  * member of the current group and the other sprite passed as parameter.
  *
  * @example
  *     group.overlap(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method overlap
  * @param {Object} target Group or Sprite to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  array.overlap = _groupCollide.bind(array, 'overlap');

  /**
   * Alias for <a href='#method-overlap'>overlap()</a>
   *
   * Returns whether or not this group will bounce or collide with another sprite
   * or group. Modifies the each sprite's touching property object.
   *
   * @method isTouching
   * @param {Object} target Group or Sprite to check against the current one
   * @return {Boolean} True if touching
   */
  array.isTouching = array.overlap;

  /**
  * Checks if the the group is overlapping another group or sprite.
  * If the overlap is positive the sprites will bounce with the target(s)
  * treated as immovable with a restitution coefficient of zero.
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the overlap occours.
  * The function will be called for each single sprite overlapping.
  * The parameter of the function are respectively the
  * member of the current group and the other sprite passed as parameter.
  *
  * @example
  *     group.collide(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method collide
  * @param {Object} target Group or Sprite to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  array.collide = _groupCollide.bind(array, 'collide');

  /**
  * Checks if the the group is overlapping another group or sprite.
  * If the overlap is positive the sprites in the group will displace
  * the colliding ones to the closest non-overlapping positions.
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the overlap occurs.
  * The function will be called for each single sprite overlapping.
  * The parameter of the function are respectively the
  * member of the current group and the other sprite passed as parameter.
  *
  * @example
  *     group.displace(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method displace
  * @param {Object} target Group or Sprite to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  array.displace = _groupCollide.bind(array, 'displace');

  /**
  * Checks if the the group is overlapping another group or sprite.
  * If the overlap is positive the sprites will bounce affecting each
  * other's trajectories depending on their .velocity, .mass and .restitution.
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the overlap occours.
  * The function will be called for each single sprite overlapping.
  * The parameter of the function are respectively the
  * member of the current group and the other sprite passed as parameter.
  *
  * @example
  *     group.bounce(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method bounce
  * @param {Object} target Group or Sprite to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  array.bounce = _groupCollide.bind(array, 'bounce');

  /**
  * Checks if the the group is overlapping another group or sprite.
  * If the overlap is positive the sprites will bounce with the target(s)
  * treated as immovable.
  *
  * The check is performed using the colliders. If colliders are not set
  * they will be created automatically from the image/animation bounding box.
  *
  * A callback function can be specified to perform additional operations
  * when the overlap occours.
  * The function will be called for each single sprite overlapping.
  * The parameter of the function are respectively the
  * member of the current group and the other sprite passed as parameter.
  *
  * @example
  *     group.bounceOff(otherSprite, explosion);
  *
  *     function explosion(spriteA, spriteB) {
  *       spriteA.remove();
  *       spriteB.score++;
  *     }
  *
  * @method bounceOff
  * @param {Object} target Group or Sprite to check against the current one
  * @param {Function} [callback] The function to be called if overlap is positive
  * @return {Boolean} True if overlapping
  */
  array.bounceOff = _groupCollide.bind(array, 'bounceOff');

  array.setPropertyEach = function(propName, value) {
    for (var i = 0; i < this.length; i++) {
      this[i][propName] = value;
    }
  };

  array.callMethodEach = function(methodName) {
    // Copy all arguments after the first parameter into methodArgs:
    var methodArgs = Array.prototype.slice.call(arguments, 1);
    // Use a copy of the array in case the method modifies the group
    var elements = [].concat(this);
    for (var i = 0; i < elements.length; i++) {
      elements[i][methodName].apply(elements[i], methodArgs);
    }
  };

  array.setDepthEach = array.setPropertyEach.bind(array, 'depth');
  array.setLifetimeEach = array.setPropertyEach.bind(array, 'lifetime');
  array.setRotateToDirectionEach = array.setPropertyEach.bind(array, 'rotateToDirection');
  array.setRotationEach = array.setPropertyEach.bind(array, 'rotation');
  array.setRotationSpeedEach = array.setPropertyEach.bind(array, 'rotationSpeed');
  array.setScaleEach = array.setPropertyEach.bind(array, 'scale');
  array.setColorEach = array.setPropertyEach.bind(array, 'shapeColor');
  array.setTintEach = array.setPropertyEach.bind(array, 'tint');
  array.setVisibleEach = array.setPropertyEach.bind(array, 'visible');
  array.setVelocityXEach = array.setPropertyEach.bind(array, 'velocityX');
  array.setVelocityYEach = array.setPropertyEach.bind(array, 'velocityY');
  array.setHeightEach = array.setPropertyEach.bind(array, 'height');
  array.setWidthEach = array.setPropertyEach.bind(array, 'width');

  array.destroyEach = array.callMethodEach.bind(array, 'destroy');
  array.pointToEach = array.callMethodEach.bind(array, 'pointTo');
  array.setAnimationEach = array.callMethodEach.bind(array, 'setAnimation');
  array.setColliderEach = array.callMethodEach.bind(array, 'setCollider');
  array.setSpeedAndDirectionEach = array.callMethodEach.bind(array, 'setSpeedAndDirection');
  array.setVelocityEach = array.callMethodEach.bind(array, 'setVelocity');
  array.setMirrorXEach = array.callMethodEach.bind(array, 'mirrorX');
  array.setMirrorYEach = array.callMethodEach.bind(array, 'mirrorY');

  return array;
}

p5.prototype.Group = Group;

/**
 * Creates four edge sprites and adds them to a group. Each edge is just outside
 * of the canvas and has a thickness of 100. After calling this function,
 * the following properties are exposed and populated with sprites:
 * leftEdge, rightEdge, topEdge, bottomEdge
 *
 * The 'edges' property is populated with a group containing those four sprites.
 *
 * If this edge sprites have already been created, the function returns the
 * existing edges group immediately.
 *
 * @method createEdgeSprites
 * @return {Group} The edges group
 */
p5.prototype.createEdgeSprites = function() {
  var context = this._isGlobal ? window : this;
  if (context.edges) {
    return context.edges;
  }

  var edgeThickness = 100;
  var width = context.width;
  var height = context.height;

  context.leftEdge = context.createSprite(-edgeThickness / 2, height / 2, edgeThickness, height);
  context.rightEdge = context.createSprite(width + (edgeThickness / 2), height / 2, edgeThickness, height);
  context.topEdge = context.createSprite(width / 2, -edgeThickness / 2, width, edgeThickness);
  context.bottomEdge = context.createSprite(width / 2, height + (edgeThickness / 2), width, edgeThickness);

  context.edges = context.createGroup();
  context.edges.add(context.leftEdge);
  context.edges.add(context.rightEdge);
  context.edges.add(context.topEdge);
  context.edges.add(context.bottomEdge);

  return context.edges;
};

/**
 * An Animation object contains a series of images (p5.Image) that
 * can be displayed sequentially.
 *
 * All files must be png images. You must include the directory from the sketch root,
 * and the extension .png
 *
 * A sprite can have multiple labeled animations, see Sprite.addAnimation
 * and Sprite.changeAnimation, however an animation can be used independently.
 *
 * An animation can be created either by passing a series of file names,
 * no matter how many or by passing the first and the last file name
 * of a numbered sequence.
 * p5.play will try to detect the sequence pattern.
 *
 * For example if the given filenames are
 * "data/file0001.png" and "data/file0005.png" the images
 * "data/file0003.png" and "data/file0004.png" will be loaded as well.
 *
 * @example
 *     var sequenceAnimation;
 *     var glitch;
 *
 *     function preload() {
 *       sequenceAnimation = loadAnimation("data/walking0001.png", "data/walking0005.png");
 *       glitch = loadAnimation("data/dog.png", "data/horse.png", "data/cat.png", "data/snake.png");
 *     }
 *
 *     function setup() {
 *       createCanvas(800, 600);
 *     }
 *
 *     function draw() {
 *       background(0);
 *       animation(sequenceAnimation, 100, 100);
 *       animation(glitch, 200, 100);
 *     }
 *
 * @class Animation
 * @constructor
 * @param {String} fileName1 First file in a sequence OR first image file
 * @param {String} fileName2 Last file in a sequence OR second image file
 * @param {String} [...fileNameN] Any number of image files after the first two
 */
function Animation(pInst) {
  var frameArguments = Array.prototype.slice.call(arguments, 1);
  var i;

  var CENTER = p5.prototype.CENTER;

  /**
  * Array of frames (p5.Image)
  *
  * @property images
  * @type {Array}
  */
  this.images = [];

  var frame = 0;
  var cycles = 0;
  var targetFrame = -1;

  this.offX = 0;
  this.offY = 0;

  /**
  * Delay between frames in number of draw cycles.
  * If set to 4 the framerate of the anymation would be the
  * sketch framerate divided by 4 (60fps = 15fps)
  *
  * @property frameDelay
  * @type {Number}
  * @default 2
  */
  this.frameDelay = 4;

  /**
  * True if the animation is currently playing.
  *
  * @property playing
  * @type {Boolean}
  * @default true
  */
  this.playing = true;

  /**
  * Animation visibility.
  *
  * @property visible
  * @type {Boolean}
  * @default true
  */
  this.visible = true;

  /**
  * If set to false the animation will stop after reaching the last frame
  *
  * @property looping
  * @type {Boolean}
  * @default true
  */
  this.looping = true;

  /**
  * True if frame changed during the last draw cycle
  *
  * @property frameChanged
  * @type {Boolean}
  */
  this.frameChanged = false;

  //is the collider defined manually or defined
  //by the current frame size
  this.imageCollider = false;


  //sequence mode
  if(frameArguments.length === 2 && typeof frameArguments[0] === 'string' && typeof frameArguments[1] === 'string')
  {
    var from = frameArguments[0];
    var to = frameArguments[1];

    //print("sequence mode "+from+" -> "+to);

    //make sure the extensions are fine
    var ext1 = from.substring(from.length-4, from.length);
    if(ext1 !== '.png')
    {
      pInst.print('Animation error: you need to use .png files (filename '+from+')');
      from = -1;
    }

    var ext2 = to.substring(to.length-4, to.length);
    if(ext2 !== '.png')
    {
      pInst.print('Animation error: you need to use .png files (filename '+to+')');
      to = -1;
    }

    //extensions are fine
    if(from !== -1 && to !== -1)
    {
      var digits1 = 0;
      var digits2 = 0;

      //skip extension work backwards to find the numbers
      for (i = from.length-5; i >= 0; i--) {
        if(from.charAt(i) >= '0' && from.charAt(i) <= '9')
          digits1++;
      }

      for (i = to.length-5; i >= 0; i--) {
        if(to.charAt(i) >= '0' && to.charAt(i) <= '9')
          digits2++;
      }

      var prefix1 = from.substring(0, from.length-(4+digits1));
      var prefix2 = to.substring(0, to.length-(4+digits2) );

      // Our numbers likely have leading zeroes, which means that some
      // browsers (e.g., PhantomJS) will interpret them as base 8 (octal)
      // instead of decimal. To fix this, we'll explicity tell parseInt to
      // use a base of 10 (decimal). For more details on this issue, see
      // http://stackoverflow.com/a/8763427/2422398.
      var number1 = parseInt(from.substring(from.length-(4+digits1), from.length-4), 10);
      var number2 = parseInt(to.substring(to.length-(4+digits2), to.length-4), 10);

      //swap if inverted
      if(number2<number1)
      {
        var t = number2;
        number2 = number1;
        number1 = t;
      }

      //two different frames
      if(prefix1 !== prefix2 )
      {
        //print("2 separate images");
        this.images.push(pInst.loadImage(from));
        this.images.push(pInst.loadImage(to));
      }
      //same digits: case img0001, img0002
      else
      {
        var fileName;
        if(digits1 === digits2)
        {

          //load all images
          for (i = number1; i <= number2; i++) {
            // Use nf() to number format 'i' into four digits
            fileName = prefix1 + pInst.nf(i, digits1) + '.png';
            this.images.push(pInst.loadImage(fileName));

          }

        }
        else //case: case img1, img2
        {
          //print("from "+prefix1+" "+number1 +" to "+number2);
          for (i = number1; i <= number2; i++) {
            // Use nf() to number format 'i' into four digits
            fileName = prefix1 + i + '.png';
            this.images.push(pInst.loadImage(fileName));

          }

        }
      }

    }//end no ext error

  }//end sequence mode
  // Sprite sheet mode
  else if (frameArguments.length === 1 && (frameArguments[0] instanceof SpriteSheet))
  {
    this.spriteSheet = frameArguments[0];
    this.images = this.spriteSheet.frames.map( function(f) {
      if (f.spriteSourceSize && f.sourceSize) {
        return Object.assign(f.frame, {
          width: f.frame.w,
          height: f.frame.h,
          sourceX: f.spriteSourceSize.x,
          sourceY: f.spriteSourceSize.y,
          sourceW: f.sourceSize.w,
          sourceH: f.sourceSize.h,
        });
      }
      return f.frame;
    });
  }
  else if(frameArguments.length !== 0)//arbitrary list of images
  {
    //print("Animation arbitrary mode");
    for (i = 0; i < frameArguments.length; i++) {
      //print("loading "+fileNames[i]);
      if(frameArguments[i] instanceof p5.Image)
        this.images.push(frameArguments[i]);
      else
        this.images.push(pInst.loadImage(frameArguments[i]));
    }
  }

  /**
  * Objects are passed by reference so to have different sprites
  * using the same animation you need to clone it.
  *
  * @method clone
  * @return {Animation} A clone of the current animation
  */
  this.clone = function() {
    var myClone = new Animation(pInst); //empty
    myClone.images = [];

    if (this.spriteSheet) {
      myClone.spriteSheet = this.spriteSheet.clone();
    }
    myClone.images = this.images.slice();

    myClone.offX = this.offX;
    myClone.offY = this.offY;
    myClone.frameDelay = this.frameDelay;
    myClone.playing = this.playing;
    myClone.looping = this.looping;

    return myClone;
  };

  /**
   * Draws the animation at coordinate x and y.
   * Updates the frames automatically.
   *
   * @method draw
   * @param {Number} x x coordinate
   * @param {Number} y y coordinate
   * @param {Number} [r=0] rotation
   */
  this.draw = function(x, y, r) {
    this.xpos = x;
    this.ypos = y;
    this.rotation = r || 0;

    if (this.visible)
    {

      //only connection with the sprite class
      //if animation is used independently draw and update are the sam
      if(!this.isSpriteAnimation)
        this.update();

      //this.currentImageMode = g.imageMode;
      pInst.push();
      pInst.imageMode(CENTER);

      var xTranslate = this.xpos;
      var yTranslate = this.ypos;
      var image = this.images[frame];
      var frame_info = this.spriteSheet && image;

      // Adjust translation if we're dealing with a texture packed spritesheet
      // (with sourceW, sourceH, sourceX, sourceY props on our images array)
      if (frame_info) {
        var missingX = (frame_info.sourceW || frame_info.width) - frame_info.width;
        var missingY = (frame_info.sourceH || frame_info.height) - frame_info.height;
        // If the count of missing (transparent) pixels is not equally balanced on
        // the left vs. right or top vs. bottom, we adjust the translation:
        xTranslate += ((frame_info.sourceX || 0) - missingX / 2);
        yTranslate += ((frame_info.sourceY || 0) - missingY / 2);
      }

      pInst.translate(xTranslate, yTranslate);
      if (pInst._angleMode === pInst.RADIANS) {
        pInst.rotate(radians(this.rotation));
      } else {
        pInst.rotate(this.rotation);
      }

      if (frame_info) {
        if (this.spriteSheet.image instanceof Image) {
          pInst.imageElement(this.spriteSheet.image,
            frame_info.x, frame_info.y,
            frame_info.width, frame_info.height,
            this.offX, this.offY,
            frame_info.width, frame_info.height);
        } else {
          pInst.image(this.spriteSheet.image,
            frame_info.x, frame_info.y,
            frame_info.width, frame_info.height,
            this.offX, this.offY,
            frame_info.width, frame_info.height);
          }
      } else if (image) {
        if (image instanceof Image) {
          pInst.imageElement(image, this.offX, this.offY);
        } else {
          pInst.image(image, this.offX, this.offY);
        }
      } else {
        pInst.print('Warning undefined frame '+frame);
        //this.isActive = false;
      }

      pInst.pop();
    }
  };

  //called by draw
  this.update = function() {
    cycles++;
    var previousFrame = frame;
    this.frameChanged = false;


    //go to frame
    if(this.images.length === 1)
    {
      this.playing = false;
      frame = 0;
    }

    if ( this.playing && cycles%this.frameDelay === 0)
    {
      //going to target frame up
      if(targetFrame>frame && targetFrame !== -1)
      {
        frame++;
      }
      //going to taget frame down
      else if(targetFrame<frame && targetFrame !== -1)
      {
        frame--;
      }
      else if(targetFrame === frame && targetFrame !== -1)
      {
        this.playing=false;
      }
      else if (this.looping) //advance frame
      {
        //if next frame is too high
        if (frame>=this.images.length-1)
          frame = 0;
        else
          frame++;
      } else
      {
        //if next frame is too high
        if (frame<this.images.length-1)
          frame++;
        else
          this.playing = false;
      }
    }

    if(previousFrame !== frame)
      this.frameChanged = true;

  };//end update

  /**
  * Plays the animation.
  *
  * @method play
  */
  this.play = function() {
    this.playing = true;
    targetFrame = -1;
  };

  /**
  * Stops the animation.
  *
  * @method stop
  */
  this.stop = function(){
    this.playing = false;
  };

  /**
  * Rewinds the animation to the first frame.
  *
  * @method rewind
  */
  this.rewind = function() {
    frame = 0;
  };

  /**
  * Changes the current frame.
  *
  * @method changeFrame
  * @param {Number} frame Frame number (starts from 0).
  */
  this.changeFrame = function(f) {
    if (f<this.images.length)
      frame = f;
    else
      frame = this.images.length - 1;

    targetFrame = -1;
    //this.playing = false;
  };

  /**
   * Goes to the next frame and stops.
   *
   * @method nextFrame
   */
  this.nextFrame = function() {

    if (frame<this.images.length-1)
      frame = frame+1;
    else if(this.looping)
      frame = 0;

    targetFrame = -1;
    this.playing = false;
  };

  /**
   * Goes to the previous frame and stops.
   *
   * @method previousFrame
   */
  this.previousFrame = function() {

    if (frame>0)
      frame = frame-1;
    else if(this.looping)
      frame = this.images.length-1;

    targetFrame = -1;
    this.playing = false;
  };

  /**
  * Plays the animation forward or backward toward a target frame.
  *
  * @method goToFrame
  * @param {Number} toFrame Frame number destination (starts from 0)
  */
  this.goToFrame = function(toFrame) {
    if(toFrame < 0 || toFrame >= this.images.length) {
      return;
    }

    // targetFrame gets used by the update() method to decide what frame to
    // select next.  When it's not being used it gets set to -1.
    targetFrame = toFrame;

    if(targetFrame !== frame) {
      this.playing = true;
    }
  };

  /**
  * Returns the current frame number.
  *
  * @method getFrame
  * @return {Number} Current frame (starts from 0)
  */
  this.getFrame = function() {
    return frame;
  };

  /**
  * Returns the last frame number.
  *
  * @method getLastFrame
  * @return {Number} Last frame number (starts from 0)
  */
  this.getLastFrame = function() {
    return this.images.length-1;
  };

  /**
  * Returns the current frame image as p5.Image.
  *
  * @method getFrameImage
  * @return {p5.Image} Current frame image
  */
  this.getFrameImage = function() {
    return this.images[frame];
  };

  /**
  * Returns the frame image at the specified frame number.
  *
  * @method getImageAt
  * @param {Number} frame Frame number
  * @return {p5.Image} Frame image
  */
  this.getImageAt = function(f) {
    return this.images[f];
  };

  /**
  * Returns the current frame width in pixels.
  * If there is no image loaded, returns 1.
  *
  * @method getWidth
  * @return {Number} Frame width
  */
  this.getWidth = function() {
    if (this.images[frame]) {
      return this.images[frame].sourceW || this.images[frame].width;
    } else {
      return 1;
    }
  };

  /**
  * Returns the current frame height in pixels.
  * If there is no image loaded, returns 1.
  *
  * @method getHeight
  * @return {Number} Frame height
  */
  this.getHeight = function() {
    if (this.images[frame]) {
      return this.images[frame].sourceH || this.images[frame].height;
    } else {
      return 1;
    }
  };

}

defineLazyP5Property('Animation', boundConstructorFactory(Animation));

/**
 * Represents a sprite sheet and all it's frames.  To be used with Animation,
 * or static drawing single frames.
 *
 *  There are two different ways to load a SpriteSheet
 *
 * 1. Given width, height that will be used for every frame and the
 *    number of frames to cycle through. The sprite sheet must have a
 *    uniform grid with consistent rows and columns.
 *
 * 2. Given an array of frame objects that define the position and
 *    dimensions of each frame.  This is Flexible because you can use
 *    sprite sheets that don't have uniform rows and columns.
 *
 * @example
 *     // Method 1 - Using width, height for each frame and number of frames
 *     explode_sprite_sheet = loadSpriteSheet('assets/explode_sprite_sheet.png', 171, 158, 11);
 *
 *     // Method 2 - Using an array of objects that define each frame
 *     var player_frames = loadJSON('assets/tiles.json');
 *     player_sprite_sheet = loadSpriteSheet('assets/player_spritesheet.png', player_frames);
 *
 * @class SpriteSheet
 * @constructor
 * @param image String image path or p5.Image object
 */
function SpriteSheet(pInst) {
  var spriteSheetArgs = Array.prototype.slice.call(arguments, 1);

  this.image = null;
  this.frames = [];
  this.frame_width = 0;
  this.frame_height = 0;
  this.num_frames = 0;

  /**
   * Generate the frames data for this sprite sheet baesd on user params
   * @private
   * @method _generateSheetFrames
   */
  this._generateSheetFrames = function() {
    var sX = 0, sY = 0;
    for (var i = 0; i < this.num_frames; i++) {
      this.frames.push(
        {
          'name': i,
          'frame': {
            'x': sX,
            'y': sY,
            'width': this.frame_width,
            'height': this.frame_height
          }
        });
      sX += this.frame_width;
      if (sX >= this.image.width) {
        sX = 0;
        sY += this.frame_height;
        if (sY >= this.image.height) {
          sY = 0;
        }
      }
    }
  };

  var shortArgs = spriteSheetArgs.length === 2 || spriteSheetArgs.length === 3;
  var longArgs = spriteSheetArgs.length === 4 || spriteSheetArgs.length === 5;

  if (shortArgs && Array.isArray(spriteSheetArgs[1])) {
    this.frames = spriteSheetArgs[1];
    this.num_frames = this.frames.length;
  } else if (longArgs &&
    (typeof spriteSheetArgs[1] === 'number') &&
    (typeof spriteSheetArgs[2] === 'number') &&
    (typeof spriteSheetArgs[3] === 'number')) {
    this.frame_width = spriteSheetArgs[1];
    this.frame_height = spriteSheetArgs[2];
    this.num_frames = spriteSheetArgs[3];
  }

  if(spriteSheetArgs[0] instanceof p5.Image || spriteSheetArgs[0] instanceof Image) {
    this.image = spriteSheetArgs[0];
    if (longArgs) {
      this._generateSheetFrames();
    }
  } else {
    // When the final argument is present (either the 3rd or the 5th), it indicates
    // whether we should load the URL as an Image element (as opposed to the default
    // behavior, which is to load it as a p5.Image). If that argument is a function,
    // it will be called back once the load succeeds or fails. On success, the Image
    // will be supplied as the only parameter. On failure, null will be supplied.
    var callback;
    if (shortArgs) {
      if (spriteSheetArgs[2]) {
        if (typeof spriteSheetArgs[2] === 'function') {
          callback = spriteSheetArgs[2];
        }
        this.image = pInst.loadImageElement(
          spriteSheetArgs[0],
          function(img) { if (callback) return callback(img); },
          function() { if (callback) return callback(null); }
        );
      } else {
        this.image = pInst.loadImage(spriteSheetArgs[0]);
      }
    } else if (longArgs) {
      var generateSheetFrames = this._generateSheetFrames.bind(this);
      if (spriteSheetArgs[4]) {
        if (typeof spriteSheetArgs[4] === 'function') {
          callback = spriteSheetArgs[4];
        }
        this.image = pInst.loadImageElement(
          spriteSheetArgs[0],
          function(img) {
            generateSheetFrames(img);
            if (callback) return callback(img);
          },
          function() { if (callback) return callback(null); }
        );
      } else {
        this.image = pInst.loadImage(spriteSheetArgs[0], generateSheetFrames);
      }
    }
  }

  /**
   * Draws a specific frame to the canvas.
   * @param frame_name  Can either be a string name, or a numeric index.
   * @param x   x position to draw the frame at
   * @param y   y position to draw the frame at
   * @param [width]   optional width to draw the frame
   * @param [height]  optional height to draw the frame
   * @method drawFrame
   */
  this.drawFrame = function(frame_name, x, y, width, height) {
    var frameToDraw;
    if (typeof frame_name === 'number') {
      frameToDraw = this.frames[frame_name];
    } else {
      for (var i = 0; i < this.frames.length; i++) {
        if (this.frames[i].name === frame_name) {
          frameToDraw = this.frames[i];
          break;
        }
      }
    }
    var frameWidth = frameToDraw.frame.width || frameToDraw.frame.w;
    var frameHeight = frameToDraw.frame.height || frameToDraw.frame.h;
    var dWidth = width || frameWidth;
    var dHeight = height || frameHeight;

    // Adjust how we draw if we're dealing with a texture packed spritesheet
    // (in particular, we treat supplied width and height params as an intention
    //  to scale versus the sourceSize [before packing])
    if (frameToDraw.spriteSourceSize && frameToDraw.sourceSize) {
      var frameSizeScaleX = frameWidth / frameToDraw.sourceSize.w;
      var frameSizeScaleY = frameHeight / frameToDraw.sourceSize.h;
      if (width) {
        x += (frameToDraw.spriteSourceSize.x * dWidth / frameToDraw.sourceSize.w);
        dWidth = width * frameSizeScaleX;
      } else {
        x += frameToDraw.spriteSourceSize.x;
      }
      if (height) {
        y += (frameToDraw.spriteSourceSize.y * dHeight / frameToDraw.sourceSize.h);
        dHeight = height * frameSizeScaleY;
      } else {
        y += frameToDraw.spriteSourceSize.y;
      }
    }
    if (this.image instanceof Image) {
      pInst.imageElement(this.image, frameToDraw.frame.x, frameToDraw.frame.y,
        frameToDraw.frame.width, frameToDraw.frame.height, x, y, dWidth, dHeight);
    } else {
      pInst.image(this.image, frameToDraw.frame.x, frameToDraw.frame.y,
        frameToDraw.frame.width, frameToDraw.frame.height, x, y, dWidth, dHeight);
    }
  };

  /**
   * Objects are passed by reference so to have different sprites
   * using the same animation you need to clone it.
   *
   * @method clone
   * @return {SpriteSheet} A clone of the current SpriteSheet
   */
  this.clone = function() {
    var myClone = new SpriteSheet(pInst); //empty

    // Deep clone the frames by value not reference
    for(var i = 0; i < this.frames.length; i++) {
      var frame = this.frames[i].frame;
      var cloneFrame = {
        'name':frame.name,
        'frame': {
          'x':frame.x,
          'y':frame.y,
          'width':frame.width,
          'height':frame.height
        }
      };
      myClone.frames.push(cloneFrame);
    }

    // clone other fields
    myClone.image = this.image;
    myClone.frame_width = this.frame_width;
    myClone.frame_height = this.frame_height;
    myClone.num_frames = this.num_frames;

    return myClone;
  };
}

defineLazyP5Property('SpriteSheet', boundConstructorFactory(SpriteSheet));

//general constructor to be able to feed arguments as array
function construct(constructor, args) {
  function F() {
    return constructor.apply(this, args);
  }
  F.prototype = constructor.prototype;
  return new F();
}





/*
 * Javascript Quadtree
 * based on
 * https://github.com/timohausmann/quadtree-js/
 * Copyright © 2012 Timo Hausmann
*/

function Quadtree( bounds, max_objects, max_levels, level ) {

  this.active = true;
  this.max_objects	= max_objects || 10;
  this.max_levels		= max_levels || 4;

  this.level 			= level || 0;
  this.bounds 		= bounds;

  this.objects 		= [];
  this.object_refs	= [];
  this.nodes 			= [];
}

Quadtree.prototype.updateBounds = function() {

  //find maximum area
  var objects = this.getAll();
  var x = 10000;
  var y = 10000;
  var w = -10000;
  var h = -10000;

  for( var i=0; i < objects.length; i++ )
    {
      if(objects[i].position.x < x)
        x = objects[i].position.x;
      if(objects[i].position.y < y)
        y = objects[i].position.y;
      if(objects[i].position.x > w)
        w = objects[i].position.x;
      if(objects[i].position.y > h)
        h = objects[i].position.y;
    }


  this.bounds = {
    x:x,
    y:y,
    width:w,
    height:h
  };
  //print(this.bounds);
};

/*
	 * Split the node into 4 subnodes
	 */
Quadtree.prototype.split = function() {

  var nextLevel	= this.level + 1,
      subWidth	= Math.round( this.bounds.width / 2 ),
      subHeight 	= Math.round( this.bounds.height / 2 ),
      x 			= Math.round( this.bounds.x ),
      y 			= Math.round( this.bounds.y );

  //top right node
  this.nodes[0] = new Quadtree({
    x	: x + subWidth,
    y	: y,
    width	: subWidth,
    height	: subHeight
  }, this.max_objects, this.max_levels, nextLevel);

  //top left node
  this.nodes[1] = new Quadtree({
    x	: x,
    y	: y,
    width	: subWidth,
    height	: subHeight
  }, this.max_objects, this.max_levels, nextLevel);

  //bottom left node
  this.nodes[2] = new Quadtree({
    x	: x,
    y	: y + subHeight,
    width	: subWidth,
    height	: subHeight
  }, this.max_objects, this.max_levels, nextLevel);

  //bottom right node
  this.nodes[3] = new Quadtree({
    x	: x + subWidth,
    y	: y + subHeight,
    width	: subWidth,
    height	: subHeight
  }, this.max_objects, this.max_levels, nextLevel);
};


/*
	 * Determine the quadtrant for an area in this node
	 */
Quadtree.prototype.getIndex = function( pRect ) {
  if(!pRect.collider)
    return -1;
  else
  {
    var colliderBounds = pRect.collider.getBoundingBox();
    var index 				= -1,
        verticalMidpoint 	= this.bounds.x + (this.bounds.width / 2),
        horizontalMidpoint 	= this.bounds.y + (this.bounds.height / 2),

        //pRect can completely fit within the top quadrants
        topQuadrant = (colliderBounds.top < horizontalMidpoint && colliderBounds.bottom < horizontalMidpoint),

        //pRect can completely fit within the bottom quadrants
        bottomQuadrant = (colliderBounds.top > horizontalMidpoint);

    //pRect can completely fit within the left quadrants
    if (colliderBounds.left < verticalMidpoint && colliderBounds.right < verticalMidpoint ) {
      if( topQuadrant ) {
        index = 1;
      } else if( bottomQuadrant ) {
        index = 2;
      }

      //pRect can completely fit within the right quadrants
    } else if( colliderBounds.left > verticalMidpoint ) {
      if( topQuadrant ) {
        index = 0;
      } else if( bottomQuadrant ) {
        index = 3;
      }
    }

    return index;
  }
};


/*
	 * Insert an object into the node. If the node
	 * exceeds the capacity, it will split and add all
	 * objects to their corresponding subnodes.
	 */
Quadtree.prototype.insert = function( obj ) {
  //avoid double insertion
  if(this.objects.indexOf(obj) === -1)
  {

    var i = 0,
        index;

    //if we have subnodes ...
    if( typeof this.nodes[0] !== 'undefined' ) {
      index = this.getIndex( obj );

      if( index !== -1 ) {
        this.nodes[index].insert( obj );
        return;
      }
    }

    this.objects.push( obj );

    if( this.objects.length > this.max_objects && this.level < this.max_levels ) {

      //split if we don't already have subnodes
      if( typeof this.nodes[0] === 'undefined' ) {
        this.split();
      }

      //add all objects to there corresponding subnodes
      while( i < this.objects.length ) {

        index = this.getIndex( this.objects[i] );

        if( index !== -1 ) {
          this.nodes[index].insert( this.objects.splice(i, 1)[0] );
        } else {
          i = i + 1;
        }
      }
    }
  }
};


/*
	 * Return all objects that could collide with a given area
	 */
Quadtree.prototype.retrieve = function( pRect ) {


  var index = this.getIndex( pRect ),
      returnObjects = this.objects;

  //if we have subnodes ...
  if( typeof this.nodes[0] !== 'undefined' ) {

    //if pRect fits into a subnode ..
    if( index !== -1 ) {
      returnObjects = returnObjects.concat( this.nodes[index].retrieve( pRect ) );

      //if pRect does not fit into a subnode, check it against all subnodes
    } else {
      for( var i=0; i < this.nodes.length; i=i+1 ) {
        returnObjects = returnObjects.concat( this.nodes[i].retrieve( pRect ) );
      }
    }
  }

  return returnObjects;
};

Quadtree.prototype.retrieveFromGroup = function( pRect, group ) {

  var results = [];
  var candidates = this.retrieve(pRect);

  for(var i=0; i<candidates.length; i++)
    if(group.contains(candidates[i]))
    results.push(candidates[i]);

  return results;
};

/*
	 * Get all objects stored in the quadtree
	 */
Quadtree.prototype.getAll = function() {

  var objects = this.objects;

  for( var i=0; i < this.nodes.length; i=i+1 ) {
    objects = objects.concat( this.nodes[i].getAll() );
  }

  return objects;
};


/*
	 * Get the node in which a certain object is stored
	 */
Quadtree.prototype.getObjectNode = function( obj ) {

  var index;

  //if there are no subnodes, object must be here
  if( !this.nodes.length ) {

    return this;

  } else {

    index = this.getIndex( obj );

    //if the object does not fit into a subnode, it must be here
    if( index === -1 ) {

      return this;

      //if it fits into a subnode, continue deeper search there
    } else {
      var node = this.nodes[index].getObjectNode( obj );
      if( node ) return node;
    }
  }

  return false;
};


/*
	 * Removes a specific object from the quadtree
	 * Does not delete empty subnodes. See cleanup-function
	 */
Quadtree.prototype.removeObject = function( obj ) {

  var node = this.getObjectNode( obj ),
      index = node.objects.indexOf( obj );

  if( index === -1 ) return false;

  node.objects.splice( index, 1);
};


/*
	 * Clear the quadtree and delete all objects
	 */
Quadtree.prototype.clear = function() {

  this.objects = [];

  if( !this.nodes.length ) return;

  for( var i=0; i < this.nodes.length; i=i+1 ) {

    this.nodes[i].clear();
  }

  this.nodes = [];
};


/*
	 * Clean up the quadtree
	 * Like clear, but objects won't be deleted but re-inserted
	 */
Quadtree.prototype.cleanup = function() {

  var objects = this.getAll();

  this.clear();

  for( var i=0; i < objects.length; i++ ) {
    this.insert( objects[i] );
  }
};



function updateTree() {
  if(this.quadTree.active)
  {
    this.quadTree.updateBounds();
    this.quadTree.cleanup();
  }
}

//keyboard input
p5.prototype.registerMethod('pre', p5.prototype.readPresses);

//automatic sprite update
p5.prototype.registerMethod('pre', p5.prototype.updateSprites);

//quadtree update
p5.prototype.registerMethod('post', updateTree);

//camera push and pop
p5.prototype.registerMethod('pre', cameraPush);
p5.prototype.registerMethod('post', cameraPop);

p5.prototype.registerPreloadMethod('loadImageElement', p5.prototype);

//deltaTime
//p5.prototype.registerMethod('pre', updateDelta);

/**
 * Log a warning message to the host console, using native `console.warn`
 * if it is available but falling back on `console.log` if not.  If no
 * console is available, this method will fail silently.
 * @method _warn
 * @param {!string} message
 * @private
 */
p5.prototype._warn = function(message) {
  var console = window.console;

  if(console)
  {
    if('function' === typeof console.warn)
    {
      console.warn(message);
    }
    else if('function' === typeof console.log)
    {
      console.log('Warning: ' + message);
    }
  }
};

  /**
   * Collision Shape Base Class
   *
   * We have a set of collision shapes available that all conform to
   * a simple interface so that they can be checked against one another
   * using the Separating Axis Theorem.
   *
   * This base class implements all the required methods for a collision
   * shape and can be used as a collision point with no changes.
   * Other shapes should inherit from this and override most methods.
   *
   * @class p5.CollisionShape
   * @constructor
   * @param {p5.Vector} [center] (zero if omitted)
   * @param {number} [rotation] (zero if omitted)
   */
  p5.CollisionShape = function(center, rotation) {
    /**
     * Transform of this shape relative to its parent.  If there is no parent,
     * this is pretty much the world-space transform.
     * This should stay consistent with _offset, _rotation and _scale properties.
     * @property _localTransform
     * @type {p5.Transform2D}
     * @protected
     */
    this._localTransform = new p5.Transform2D();
    if (rotation) {
      this._localTransform.rotate(rotation);
    }
    if (center) {
      this._localTransform.translate(center);
    }

    /**
     * Transform of whatever parent object (probably a sprite) this shape is
     * associated with.  If this is a free-floating shape, the parent transform
     * will remain an identity matrix.
     * @property _parentTransform
     * @type {p5.Transform2D}
     * @protected
     */
    this._parentTransform = new p5.Transform2D();

    /**
     * The center of the collision shape in world-space.
     * @property _center
     * @private
     * @type {p5.Vector}
     */
    this._center = new p5.Vector();

    /**
     * The center of the collision shape in local-space; also, the offset of the
     * collision shape's center from its parent sprite's center.
     * @property _offset
     * @type {p5.Vector}
     * @private
     */
    this._offset = new p5.Vector();

    /**
     * Rotation in radians in local space (relative to parent).
     * Note that this will only be meaningful for shapes that can rotate,
     * i.e. Oriented Bounding Boxes
     * @property _rotation
     * @private
     * @type {number}
     */
    this._rotation = 0;

    /**
     * Scale X and Y in local space.  Note that this will only be meaningful
     * for shapes that have dimensions (e.g. not for point colliders)
     * @property _scale
     * @type {p5.Vector}
     * @private
     */
    this._scale = new p5.Vector(1, 1);

    /**
     * If true, when calling `updateFromSprite` this collider will adopt the
     * base dimensions of the sprite in addition to adopting its transform.
     * If false, only the transform (position/rotation/scale) will be adopted.
     * @property getsDimensionsFromSprite
     * @type {boolean}
     */
    this.getsDimensionsFromSprite = false;

    // Public getters/setters
    Object.defineProperties(this, {

      /**
       * The center of the collision shape in world-space.
       * Note: You can set this property with a value in world-space, but it will
       * actually modify the collision shape's local transform.
       * @property center
       * @type {p5.Vector}
       */
      'center': {
        enumerable: true,
        get: function() {
          return this._center.copy();
        }.bind(this),
        set: function(c) {
          this._localTransform
            .translate(p5.Vector.mult(this._center, -1))
            .translate(c);
          this._onTransformChanged();
        }.bind(this)
      },

      /**
       * The center of the collision shape in local-space - if this collider is
       * owned by a sprite, the offset of the collider center from the sprite center.
       * @property offset
       * @type {p5.Vector}
       */
      'offset': {
        enumerable: true,
        get: function() {
          return this._offset.copy();
        }.bind(this),
        set: function(o) {
          this._localTransform
            .translate(p5.Vector.mult(this._offset, -1))
            .translate(o);
          this._onTransformChanged();
        }.bind(this)
      },

      /**
       * The local-space rotation of the collider, in radians.
       * @property rotation
       * @type {number}
       */
      'rotation': {
        enumerable: true,
        get: function() {
          return this._rotation;
        }.bind(this),
        set: function(r) {
          this._localTransform
            .clear()
            .scale(this._scale)
            .rotate(r)
            .translate(this._offset);
          this._onTransformChanged();
        }.bind(this)
      },

      /**
       * The local-space scale of the collider
       * @property scale
       * @type {p5.Vector}
       */
      'scale': {
        enumerable: true,
        get: function() {
          return this._scale.copy();
        }.bind(this),
        set: function(s) {
          this._localTransform
            .clear()
            .scale(s)
            .rotate(this._rotation)
            .translate(this._offset);
          this._onTransformChanged();
        }.bind(this)
      }
    });

    this._onTransformChanged();
  };

  /**
   * Update this collider based on the properties of a parent Sprite.
   * Descendant classes should override this method to adopt the dimensions
   * of the sprite if `getsDimensionsFromSprite` is true.
   * @method updateFromSprite
   * @param {Sprite} sprite
   * @see p5.CollisionShape.prototype.getsDimensionsFromSprite
   */
  p5.CollisionShape.prototype.updateFromSprite = function(sprite) {
    this.setParentTransform(sprite);
  };

  /**
   * Update this collider's parent transform, which will in turn adjust its
   * position, rotation and scale in world-space and recompute cached values
   * if necessary.
   * If a Sprite is passed as the 'parent' then a new transform will be computed
   * from the sprite's position/rotation/scale and used.
   * @method setParentTransform
   * @param {p5.Transform2D|Sprite} parent
   */
  p5.CollisionShape.prototype.setParentTransform = function(parent) {
    if (parent instanceof Sprite) {
      this._parentTransform
        .clear()
        .scale(parent._getScaleX(), parent._getScaleY())
        .rotate(radians(parent.rotation))
        .translate(parent.position);
    } else if (parent instanceof p5.Transform2D) {
      this._parentTransform = parent.copy();
    } else {
      throw new TypeError('Bad argument to setParentTransform: ' + parent);
    }
    this._onTransformChanged();
  };

  /**
   * Recalculate cached properties, relevant vectors, etc. when at least one
   * of the shape's transforms changes.  The base CollisionShape (and PointCollider)
   * only need to recompute the shape's center, but other shapes may need to
   * override this method and do additional recomputation.
   * @method _onTransformChanged
   * @protected
   */
  p5.CollisionShape.prototype._onTransformChanged = function() {
    // Recompute internal properties from transforms

    // Rotation in local space
    this._rotation = this._localTransform.getRotation();

    // Scale in local space
    this._scale = this._localTransform.getScale();

    // Offset in local-space
    this._offset
      .set(0, 0)
      .transform(this._localTransform);

    // Center in world-space
    this._center
      .set(this._offset.x, this._offset.y)
      .transform(this._parentTransform);
  };

  /**
   * Compute the smallest movement needed to move this collision shape out of
   * another collision shape.  If the shapes are not overlapping, returns a
   * zero vector to indicate that no displacement is necessary.
   * @method collide
   * @param {p5.CollisionShape} other
   * @return {p5.Vector}
   */
  p5.CollisionShape.prototype.collide = function(other) {
    var displacee = this, displacer = other;

    // Compute a displacement vector using the Separating Axis Theorem
    // (Valid only for convex shapes)
    //
    // If a line (axis) exists on which the two shapes' orthogonal projections
    // do not overlap, then the shapes do not overlap.  If the shapes'
    // projections do overlap on all candidate axes, the axis that had the
    // smallest overlap gives us the smallest possible displacement.
    //
    // @see http://www.dyn4j.org/2010/01/sat/
    var smallestOverlap = Infinity;
    var smallestOverlapAxis = null;

    // We speed things up with an additional assumption that all collision
    // shapes are centrosymmetric: Circles, ellipses, and rectangles
    // are OK.  This lets us only compare the shapes' radii to the
    // distance between their centers, even for non-circular shapes.
    // Other convex shapes, (triangles, pentagons) will require more
    // complex use of their projections' positions on the axis.
    var deltaOfCenters = p5.Vector.sub(displacer.center, displacee.center);

    // It turns out we only need to check a few axes, defined by the shapes
    // being checked.  For a polygon, the normal of each face is a possible
    // separating axis.
    var candidateAxes = p5.CollisionShape._getCandidateAxesForShapes(displacee, displacer);
    var axis, deltaOfCentersOnAxis, distanceOfCentersOnAxis;
    for (var i = 0; i < candidateAxes.length; i++) {
      axis = candidateAxes[i];

      // If distance between the shape's centers as projected onto the
      // separating axis is larger than the combined radii of the shapes
      // projected onto the axis, the shapes do not overlap on this axis.
      deltaOfCentersOnAxis = p5.Vector.project(deltaOfCenters, axis);
      distanceOfCentersOnAxis = deltaOfCentersOnAxis.mag();
      var r1 = displacee._getRadiusOnAxis(axis);
      var r2 = displacer._getRadiusOnAxis(axis);
      var overlap = r1 + r2 - distanceOfCentersOnAxis;
      if (overlap <= 0) {
        // These shapes are separated along this axis.
        // Early-out, returning a zero-vector displacement.
        return new p5.Vector();
      } else if (overlap < smallestOverlap) {
        // This is the smallest overlap we've found so far - store some
        // information about it, which we can use to give the smallest
        // displacement when we're done.
        smallestOverlap = overlap;
        // Normally use the delta of centers, which gives us direction along
        // with an axis.  In the rare case that the centers exactly overlap,
        // just use the original axis
        if (deltaOfCentersOnAxis.x === 0 && deltaOfCentersOnAxis.y === 0) {
          smallestOverlapAxis = axis;
        } else {
          smallestOverlapAxis = deltaOfCentersOnAxis;
        }
      }
    }

    // If we make it here, we overlap on all possible axes and we
    // can compute the smallest vector that will displace this out of other.
    return smallestOverlapAxis.copy().setMag(-smallestOverlap);
  };


  /**
   * Check whether this shape overlaps another.
   * @method overlap
   * @param {p5.CollisionShape} other
   * @return {boolean}
   */
  p5.CollisionShape.prototype.overlap = function(other) {
    var displacement = this.collide(other);
    return displacement.x !== 0 || displacement.y !== 0;
  };

  /**
   * @method _getCanididateAxesForShapes
   * @private
   * @static
   * @param {p5.CollisionShape} shape1
   * @param {p5.CollisionShape} shape2
   * @return {Array.<p5.Vector>}
   */
  p5.CollisionShape._getCandidateAxesForShapes = function(shape1, shape2) {
    var axes = shape1._getCandidateAxes(shape2)
      .concat(shape2._getCandidateAxes(shape1))
      .map(function(axis) {
        if (axis.x === 0 && axis.y === 0) {
          return p5.CollisionShape.X_AXIS;
        }
        return axis;
      });
    return deduplicateParallelVectors(axes);
  };

  /*
   * Reduce an array of vectors to a set of unique axes (that is, no two vectors
   * in the array should be parallel).
   * @param {Array.<p5.Vector>} array
   * @return {Array}
   */
  function deduplicateParallelVectors(array) {
    return array.filter(function(item, itemPos) {
      return !array.some(function(other, otherPos) {
        return itemPos < otherPos && item.isParallel(other);
      });
    });
  }

  /**
   * Compute candidate separating axes relative to another object.
   * Override this method in subclasses to implement collision behavior.
   * @method _getCandidateAxes
   * @protected
   * @return {Array.<p5.Vector>}
   */
  p5.CollisionShape.prototype._getCandidateAxes = function() {
    return [];
  };

  /**
   * Get this shape's radius (half-width of its projection) along the given axis.
   * Override this method in subclasses to implement collision behavior.
   * @method _getRadiusOnAxis
   * @protected
   * @param {p5.Vector} axis
   * @return {number}
   */
  p5.CollisionShape.prototype._getRadiusOnAxis = function() {
    return 0;
  };

  /**
   * Get the shape's minimum radius on any axis for tunneling checks.
   * @method _getMinRadius
   * @protected
   * @param {p5.Vector} axis
   * @return {number}
   */
  p5.CollisionShape.prototype._getMinRadius = function() {
    return 0;
  };

  /**
   * @property X_AXIS
   * @type {p5.Vector}
   * @static
   * @final
   */
  p5.CollisionShape.X_AXIS = new p5.Vector(1, 0);

  /**
   * @property Y_AXIS
   * @type {p5.Vector}
   * @static
   * @final
   */
  p5.CollisionShape.Y_AXIS = new p5.Vector(0, 1);

  /**
   * @property WORLD_AXES
   * @type {Array.<p5.Vector>}
   * @static
   * @final
   */
  p5.CollisionShape.WORLD_AXES = [
    p5.CollisionShape.X_AXIS,
    p5.CollisionShape.Y_AXIS
  ];

  /**
   * Get world-space axis-aligned bounds information for this collision shape.
   * Used primarily for the quadtree.
   * @method getBoundingBox
   * @return {{top: number, bottom: number, left: number, right: number, width: number, height: number}}
   */
  p5.CollisionShape.prototype.getBoundingBox = function() {
    var radiusOnX = this._getRadiusOnAxis(p5.CollisionShape.X_AXIS);
    var radiusOnY = this._getRadiusOnAxis(p5.CollisionShape.Y_AXIS);
    return {
      top: this.center.y - radiusOnY,
      bottom: this.center.y + radiusOnY,
      left: this.center.x - radiusOnX,
      right: this.center.x + radiusOnX,
      width: radiusOnX * 2,
      height: radiusOnY * 2
    };
  };

  /**
   * A point collision shape, used to detect overlap and displacement vectors
   * vs other collision shapes.
   * @class p5.PointCollider
   * @constructor
   * @extends p5.CollisionShape
   * @param {p5.Vector} center
   */
  p5.PointCollider = function(center) {
    p5.CollisionShape.call(this, center);
  };
  p5.PointCollider.prototype = Object.create(p5.CollisionShape.prototype);

  /**
   * Construct a new PointCollider with given offset for the given sprite.
   * @method createFromSprite
   * @static
   * @param {Sprite} sprite
   * @param {p5.Vector} [offset] from the sprite's center
   * @return {p5.PointCollider}
   */
  p5.PointCollider.createFromSprite = function(sprite, offset) {
    // Create the collision shape at the transformed offset
    var shape = new p5.PointCollider(offset);
    shape.setParentTransform(sprite);
    return shape;
  };

  /**
   * Debug-draw this point collider
   * @method draw
   * @param {p5} sketch instance to use for drawing
   */
  p5.PointCollider.prototype.draw = function(sketch) {
    sketch.push();
    sketch.rectMode(sketch.CENTER);
    sketch.translate(this.center.x, this.center.y);
    sketch.noStroke();
    sketch.fill(0, 255, 0);
    sketch.ellipse(0, 0, 2, 2);
    sketch.pop();
  };

  /**
   * A Circle collision shape, used to detect overlap and displacement vectors
   * with other collision shapes.
   * @class p5.CircleCollider
   * @constructor
   * @extends p5.CollisionShape
   * @param {p5.Vector} center
   * @param {number} radius
   */
  p5.CircleCollider = function(center, radius) {
    p5.CollisionShape.call(this, center);

    /**
     * The unscaled radius of the circle collider.
     * @property radius
     * @type {number}
     */
    this.radius = radius;

    /**
     * Final radius of this circle after being scaled by parent and local transforms,
     * cached so we don't recalculate it all the time.
     * @property _scaledRadius
     * @type {number}
     * @private
     */
    this._scaledRadius = 0;

    this._computeScaledRadius();
  };
  p5.CircleCollider.prototype = Object.create(p5.CollisionShape.prototype);

  /**
   * Construct a new CircleCollider with given offset for the given sprite.
   * @method createFromSprite
   * @static
   * @param {Sprite} sprite
   * @param {p5.Vector} [offset] from the sprite's center
   * @param {number} [radius]
   * @return {p5.CircleCollider}
   */
  p5.CircleCollider.createFromSprite = function(sprite, offset, radius) {
    var customSize = typeof radius === 'number';
    var shape = new p5.CircleCollider(
      offset,
      customSize ? radius : 1
    );
    shape.getsDimensionsFromSprite = !customSize;
    shape.updateFromSprite(sprite);
    return shape;
  };

  /**
   * Update this collider based on the properties of a parent Sprite.
   * @method updateFromSprite
   * @param {Sprite} sprite
   * @see p5.CollisionShape.prototype.getsDimensionsFromSprite
   */
  p5.CircleCollider.prototype.updateFromSprite = function(sprite) {
    if (this.getsDimensionsFromSprite) {
      if (sprite.animation) {
        this.radius = Math.max(sprite.animation.getWidth(), sprite.animation.getHeight())/2;
      } else {
        this.radius = Math.max(sprite.width, sprite.height)/2;
      }
    }
    this.setParentTransform(sprite);
  };

  /**
   * Recalculate cached properties, relevant vectors, etc. when at least one
   * of the shape's transforms changes.  The base CollisionShape (and PointCollider)
   * only need to recompute the shape's center, but other shapes may need to
   * override this method and do additional recomputation.
   * @method _onTransformChanged
   * @protected
   */
  p5.CircleCollider.prototype._onTransformChanged = function() {
    p5.CollisionShape.prototype._onTransformChanged.call(this);
    this._computeScaledRadius();
  };

  /**
   * Call to update the cached scaled radius value.
   * @method _computeScaledRadius
   * @private
   */
  p5.CircleCollider.prototype._computeScaledRadius = function() {
    this._scaledRadius = new p5.Vector(this.radius, 0)
      .transform(this._localTransform)
      .transform(this._parentTransform)
      .sub(this.center)
      .mag();
  };

  /**
   * Debug-draw this collision shape.
   * @method draw
   * @param {p5} sketch instance to use for drawing
   */
  p5.CircleCollider.prototype.draw = function(sketch) {
    sketch.push();
    sketch.noFill();
    sketch.stroke(0, 255, 0);
    sketch.rectMode(sketch.CENTER);
    sketch.ellipse(this.center.x, this.center.y, this._scaledRadius*2, this._scaledRadius*2);
    sketch.pop();
  };

    /**
   * Overrides CollisionShape.setParentTransform
   * Update this collider's parent transform, which will in turn adjust its
   * position, rotation and scale in world-space and recompute cached values
   * if necessary.
   * If a Sprite is passed as the 'parent' then a new transform will be computed
   * from the sprite's position/rotation/scale and used.
   * Use the max of the x and y scales values so the circle encompasses the sprite.
   * @method setParentTransform
   * @param {p5.Transform2D|Sprite} parent
   */
  p5.CircleCollider.prototype.setParentTransform = function(parent) {
    if (parent instanceof Sprite) {
      this._parentTransform
        .clear()
        .scale(Math.max(parent._getScaleX(), parent._getScaleY()))
        .rotate(radians(parent.rotation))
        .translate(parent.position);
    } else if (parent instanceof p5.Transform2D) {
      this._parentTransform = parent.copy();
    } else {
      throw new TypeError('Bad argument to setParentTransform: ' + parent);
    }
    this._onTransformChanged();
  };

  /**
   * Compute candidate separating axes relative to another object.
   * @method _getCandidateAxes
   * @protected
   * @param {p5.CollisionShape} other
   * @return {Array.<p5.Vector>}
   */
  p5.CircleCollider.prototype._getCandidateAxes = function(other) {
    // A circle has infinite potential candidate axes, so the ones we pick
    // depend on what we're colliding against.

    // eslint-disable-next-line no-warning-comments
    // TODO: If we can ask the other shape for a list of vertices, then we can
    //       generalize this algorithm by always using the closest one, and
    //       remove the special knowledge of OBB and AABB.

    if (other instanceof p5.OrientedBoundingBoxCollider || other instanceof p5.AxisAlignedBoundingBoxCollider) {
      // There are four possible separating axes with a box - one for each
      // of its vertices, through the center of the circle.
      // We need the closest one.
      var smallestSquareDistance = Infinity;
      var axisToClosestVertex = null;

      // Generate the set of vertices for the other shape
      var halfDiagonals = other.halfDiagonals;
      [
        p5.Vector.add(other.center, halfDiagonals[0]),
        p5.Vector.add(other.center, halfDiagonals[1]),
        p5.Vector.sub(other.center, halfDiagonals[0]),
        p5.Vector.sub(other.center, halfDiagonals[1])
      ].map(function(vertex) {
        // Transform each vertex into a vector from this collider center to
        // that vertex, which defines an axis we might want to check.
        return vertex.sub(this.center);
      }.bind(this)).forEach(function(vector) {
        // Figure out which vertex is closest and use its axis
        var squareDistance = vector.magSq();
        if (squareDistance < smallestSquareDistance) {
          smallestSquareDistance = squareDistance;
          axisToClosestVertex = vector;
        }
      });
      return [axisToClosestVertex];
    }

    // When checking against another circle or a point we only need to check the
    // axis through both shapes' centers.
    return [p5.Vector.sub(other.center, this.center)];
  };

  /**
   * Get this shape's radius (half-width of its projection) along the given axis.
   * @method _getRadiusOnAxis
   * @protected
   * @return {number}
   */
  p5.CircleCollider.prototype._getRadiusOnAxis = function() {
    return this._scaledRadius;
  };

  /**
   * Get the shape's minimum radius on any axis for tunneling checks.
   * @method _getMinRadius
   * @protected
   * @param {p5.Vector} axis
   * @return {number}
   */
  p5.CircleCollider.prototype._getMinRadius = function() {
    return this._scaledRadius;
  };

  /**
   * An Axis-Aligned Bounding Box (AABB) collision shape, used to detect overlap
   * and compute minimum displacement vectors with other collision shapes.
   *
   * Cannot be rotated - hence the name.  You might use this in place of an
   * OBB because it simplifies some of the math and may improve performance.
   *
   * @class p5.AxisAlignedBoundingBoxCollider
   * @constructor
   * @extends p5.CollisionShape
   * @param {p5.Vector} center
   * @param {number} width
   * @param {number} height
   */
  p5.AxisAlignedBoundingBoxCollider = function(center, width, height) {
    p5.CollisionShape.call(this, center);

    /**
     * Unscaled box width.
     * @property _width
     * @private
     * @type {number}
     */
    this._width = width;

    /**
     * Unscaled box height.
     * @property _width
     * @private
     * @type {number}
     */
    this._height = height;

    /**
     * Cached half-diagonals, used for computing a projected radius.
     * Already transformed into world-space.
     * @property _halfDiagonals
     * @private
     * @type {Array.<p5.Vector>}
     */
    this._halfDiagonals = [];

    Object.defineProperties(this, {

      /**
       * The untransformed width of the box collider.
       * Recomputes diagonals when set.
       * @property width
       * @type {number}
       */
      'width': {
        enumerable: true,
        get: function() {
          return this._width;
        }.bind(this),
        set: function(w) {
          this._width = w;
          this._halfDiagonals = this._computeHalfDiagonals();
        }.bind(this)
      },

      /**
       * The unrotated height of the box collider.
       * Recomputes diagonals when set.
       * @property height
       * @type {number}
       */
      'height': {
        enumerable: true,
        get: function() {
          return this._height;
        }.bind(this),
        set: function(h) {
          this._height = h;
          this._halfDiagonals = this._computeHalfDiagonals();
        }.bind(this)
      },

      /**
       * Two vectors representing adjacent half-diagonals of the box at its
       * current dimensions and orientation.
       * @property halfDiagonals
       * @readOnly
       * @type {Array.<p5.Vector>}
       */
      'halfDiagonals': {
        enumerable: true,
        get: function() {
          return this._halfDiagonals;
        }.bind(this)
      }
    });

    this._computeHalfDiagonals();
  };
  p5.AxisAlignedBoundingBoxCollider.prototype = Object.create(p5.CollisionShape.prototype);

  /**
   * Construct a new AxisAlignedBoundingBoxCollider with given offset for the given sprite.
   * @method createFromSprite
   * @static
   * @param {Sprite} sprite
   * @param {p5.Vector} [offset] from the sprite's center
   * @return {p5.CircleCollider}
   */
  p5.AxisAlignedBoundingBoxCollider.createFromSprite = function(sprite, offset, width, height) {
    var customSize = typeof width === 'number' && typeof height === 'number';
    var box = new p5.AxisAlignedBoundingBoxCollider(
      offset,
      customSize ? width : 1,
      customSize ? height : 1
    );
    box.getsDimensionsFromSprite = !customSize;
    box.updateFromSprite(sprite);
    return box;
  };

  /**
   * Update this collider based on the properties of a parent Sprite.
   * @method updateFromSprite
   * @param {Sprite} sprite
   * @see p5.CollisionShape.prototype.getsDimensionsFromSprite
   */
  p5.AxisAlignedBoundingBoxCollider.prototype.updateFromSprite = function(sprite) {
    if (this.getsDimensionsFromSprite) {
      if (sprite.animation) {
        this._width = sprite.animation.getWidth();
        this._height = sprite.animation.getHeight();
      } else {
        this._width = sprite.width;
        this._height = sprite.height;
      }
    }
    this.setParentTransform(sprite);
  };

  /**
   * Recalculate cached properties, relevant vectors, etc. when at least one
   * of the shape's transforms changes.  The base CollisionShape (and PointCollider)
   * only need to recompute the shape's center, but other shapes may need to
   * override this method and do additional recomputation.
   * @method _onTransformChanged
   * @protected
   */
  p5.AxisAlignedBoundingBoxCollider.prototype._onTransformChanged = function() {
    p5.CollisionShape.prototype._onTransformChanged.call(this);
    this._computeHalfDiagonals();
  };

  /**
   * Recompute this bounding box's half-diagonal vectors.
   * @method _computeHalfDiagonals
   * @private
   * @return {Array.<p5.Vector>}
   */
  p5.AxisAlignedBoundingBoxCollider.prototype._computeHalfDiagonals = function() {
    // We transform the rectangle (which may scale and rotate it) then compute
    // an axis-aligned bounding box _around_ it.
    var composedTransform = p5.Transform2D.mult(this._parentTransform, this._localTransform);
    var transformedDiagonals = [
      new p5.Vector(this._width / 2, -this._height / 2),
      new p5.Vector(this._width / 2, this._height / 2),
      new p5.Vector(-this._width / 2, this._height / 2)
    ].map(function(vertex) {
      return vertex.transform(composedTransform).sub(this.center);
    }.bind(this));

    var halfWidth = Math.max(
      Math.abs(transformedDiagonals[0].x),
      Math.abs(transformedDiagonals[1].x)
    );
    var halfHeight = Math.max(
      Math.abs(transformedDiagonals[1].y),
      Math.abs(transformedDiagonals[2].y)
    );

    this._halfDiagonals = [
      new p5.Vector(halfWidth, -halfHeight),
      new p5.Vector(halfWidth, halfHeight)
    ];
  };

  /**
   * Debug-draw this collider.
   * @method draw
   * @param {p5} sketch - p5 instance to use for drawing
   */
  p5.AxisAlignedBoundingBoxCollider.prototype.draw = function(sketch) {
    sketch.push();
    sketch.rectMode(sketch.CENTER);
    sketch.translate(this.center.x, this.center.y);
    sketch.noFill();
    sketch.stroke(0, 255, 0);
    sketch.strokeWeight(1);
    sketch.rect(0, 0, Math.abs(this._halfDiagonals[0].x) * 2, Math.abs(this._halfDiagonals[0].y) * 2);
    sketch.pop();
  };

  /**
   * Compute candidate separating axes relative to another object.
   * @method _getCandidateAxes
   * @protected
   * @return {Array.<p5.Vector>}
   */
  p5.AxisAlignedBoundingBoxCollider.prototype._getCandidateAxes = function() {
    return p5.CollisionShape.WORLD_AXES;
  };

  /**
   * Get this shape's radius (half-width of its projection) along the given axis.
   * @method _getRadiusOnAxis
   * @protected
   * @param {p5.Vector} axis
   * @return {number}
   */
  p5.AxisAlignedBoundingBoxCollider.prototype._getRadiusOnAxis = function(axis) {
    // How to project a rect onto an axis:
    // Project the center-corner vectors for two adjacent corners (cached here)
    // onto the axis.  The larger magnitude of the two is your projection's radius.
    return Math.max(
      p5.Vector.project(this._halfDiagonals[0], axis).mag(),
      p5.Vector.project(this._halfDiagonals[1], axis).mag());
  };

  /**
   * Get the shape's minimum radius on any axis for tunneling checks.
   * @method _getMinRadius
   * @protected
   * @param {p5.Vector} axis
   * @return {number}
   */
  p5.AxisAlignedBoundingBoxCollider.prototype._getMinRadius = function() {
    return Math.min(this._width, this._height);
  };

  /**
   * An Oriented Bounding Box (OBB) collision shape, used to detect overlap and
   * compute minimum displacement vectors with other collision shapes.
   * @class p5.OrientedBoundingBoxCollider
   * @constructor
   * @extends p5.CollisionShape
   * @param {p5.Vector} center of the rectangle in world-space
   * @param {number} width of the rectangle (when not rotated)
   * @param {number} height of the rectangle (when not rotated)
   * @param {number} rotation about center, in radians
   */
  p5.OrientedBoundingBoxCollider = function(center, width, height, rotation) {
    p5.CollisionShape.call(this, center, rotation);

    /**
     * Unscaled box width.
     * @property _width
     * @private
     * @type {number}
     */
    this._width = width;

    /**
     * Unscaled box height.
     * @property _width
     * @private
     * @type {number}
     */
    this._height = height;

    /**
     * Cached separating axes this shape contributes to a collision.
     * @property _potentialAxes
     * @private
     * @type {Array.<p5.Vector>}
     */
    this._potentialAxes = [];

    /**
     * Cached half-diagonals, used for computing a projected radius.
     * Already transformed into world-space.
     * @property _halfDiagonals
     * @private
     * @type {Array.<p5.Vector>}
     */
    this._halfDiagonals = [];

    Object.defineProperties(this, {

      /**
       * The unrotated width of the box collider.
       * Recomputes diagonals when set.
       * @property width
       * @type {number}
       */
      'width': {
        enumerable: true,
        get: function() {
          return this._width;
        }.bind(this),
        set: function(w) {
          this._width = w;
          this._onTransformChanged();
        }.bind(this)
      },

      /**
       * The unrotated height of the box collider.
       * Recomputes diagonals when set.
       * @property height
       * @type {number}
       */
      'height': {
        enumerable: true,
        get: function() {
          return this._height;
        }.bind(this),
        set: function(h) {
          this._height = h;
          this._onTransformChanged();
        }.bind(this)
      },

      /**
       * Two vectors representing adjacent half-diagonals of the box at its
       * current dimensions and orientation.
       * @property halfDiagonals
       * @readOnly
       * @type {Array.<p5.Vector>}
       */
      'halfDiagonals': {
        enumerable: true,
        get: function() {
          return this._halfDiagonals;
        }.bind(this)
      }
    });

    this._onTransformChanged();
  };
  p5.OrientedBoundingBoxCollider.prototype = Object.create(p5.CollisionShape.prototype);

  /**
   * Construct a new AxisAlignedBoundingBoxCollider with given offset for the given sprite.
   * @method createFromSprite
   * @static
   * @param {Sprite} sprite
   * @param {p5.Vector} [offset] from the sprite's center
   * @param {number} [width]
   * @param {number} [height]
   * @param {number} [rotation] in radians
   * @return {p5.CircleCollider}
   */
  p5.OrientedBoundingBoxCollider.createFromSprite = function(sprite, offset, width, height, rotation) {
    var customSize = typeof width === 'number' && typeof height === 'number';
    var box = new p5.OrientedBoundingBoxCollider(
      offset,
      customSize ? width : 1,
      customSize ? height : 1,
      rotation
    );
    box.getsDimensionsFromSprite = !customSize;
    box.updateFromSprite(sprite);
    return box;
  };

  /**
   * Update this collider based on the properties of a parent Sprite.
   * @method updateFromSprite
   * @param {Sprite} sprite
   * @see p5.CollisionShape.prototype.getsDimensionsFromSprite
   */
  p5.OrientedBoundingBoxCollider.prototype.updateFromSprite =
    p5.AxisAlignedBoundingBoxCollider.prototype.updateFromSprite;

  /**
   * Assuming this collider is a sprite's swept collider, update it based on
   * the properties of the parent sprite so that it encloses the sprite's
   * current position and its projected position.
   * @method updateSweptColliderFromSprite
   * @param {Sprite} sprite
   */
  p5.OrientedBoundingBoxCollider.prototype.updateSweptColliderFromSprite = function(sprite) {
    var vMagnitude = sprite.velocity.mag();
    var vPerpendicular = new p5.Vector(sprite.velocity.y, -sprite.velocity.x);
    this._width = vMagnitude + 2 * sprite.collider._getRadiusOnAxis(sprite.velocity);
    this._height = 2 * sprite.collider._getRadiusOnAxis(vPerpendicular);
    var newRotation = radians(sprite.getDirection());
    var newCenter = new p5.Vector(
      sprite.newPosition.x + 0.5 * sprite.velocity.x,
      sprite.newPosition.y + 0.5 * sprite.velocity.y
    );
    // Perform this.rotation = newRotation and this.center = newCenter;
    this._localTransform
      .clear()
      .scale(this._scale)
      .rotate(newRotation)
      .translate(this._offset)
      .translate(p5.Vector.mult(this._center, -1))
      .translate(newCenter);
    this._onTransformChanged();
  };

  /**
   * Recalculate cached properties, relevant vectors, etc. when at least one
   * of the shape's transforms changes.  The base CollisionShape (and PointCollider)
   * only need to recompute the shape's center, but other shapes may need to
   * override this method and do additional recomputation.
   * @method _onTransformChanged
   * @protected
   */
  p5.OrientedBoundingBoxCollider.prototype._onTransformChanged = function() {
    p5.CollisionShape.prototype._onTransformChanged.call(this);

    // Transform each vertex by the local and global matrices
    // then use their differences to determine width, height, and halfDiagonals
    var composedTransform = p5.Transform2D.mult(this._parentTransform, this._localTransform);
    var transformedVertices = [
      new p5.Vector(this._width / 2, -this._height / 2),
      new p5.Vector(this._width / 2, this._height / 2),
      new p5.Vector(-this._width / 2, this._height / 2)
    ].map(function(vertex) {
      return vertex.transform(composedTransform);
    });

    this._halfDiagonals = [
      p5.Vector.sub(transformedVertices[0], this.center),
      p5.Vector.sub(transformedVertices[1], this.center)
    ];

    this._potentialAxes = [
      p5.Vector.sub(transformedVertices[1], transformedVertices[2]),
      p5.Vector.sub(transformedVertices[1], transformedVertices[0])
    ];
  };

  /**
   * Debug-draw this collider.
   * @method draw
   * @param {p5} sketch - p5 instance to use for drawing
   */
  p5.OrientedBoundingBoxCollider.prototype.draw = function(sketch) {
    var composedTransform = p5.Transform2D.mult(this._localTransform, this._parentTransform);
    var scale = composedTransform.getScale();
    var rotation = composedTransform.getRotation();
    sketch.push();
    sketch.translate(this.center.x, this.center.y);
    sketch.scale(scale.x, scale.y);
    if (sketch._angleMode === sketch.RADIANS) {
      sketch.rotate(rotation);
    } else {
      sketch.rotate(degrees(rotation));
    }

    sketch.noFill();
    sketch.stroke(0, 255, 0);
    sketch.strokeWeight(1);
    sketch.rectMode(sketch.CENTER);
    sketch.rect(0, 0, this._width, this._height);
    sketch.pop();
  };

  /**
   * Compute candidate separating axes relative to another object.
   * @method _getCandidateAxes
   * @protected
   * @return {Array.<p5.Vector>}
   */
  p5.OrientedBoundingBoxCollider.prototype._getCandidateAxes = function() {
    // An oriented bounding box always provides two of its face normals,
    // which we've precomputed.
    return this._potentialAxes;
  };

  /**
   * Get this shape's radius (half-width of its projection) along the given axis.
   * @method _getRadiusOnAxis
   * @protected
   * @param {p5.Vector} axis
   * @return {number}
   */
  p5.OrientedBoundingBoxCollider.prototype._getRadiusOnAxis =
    p5.AxisAlignedBoundingBoxCollider.prototype._getRadiusOnAxis;
  // We can reuse the AABB version of this method because both are projecting
  // cached half-diagonals - the same code works.

  /**
   * When checking for tunneling through a OrientedBoundingBoxCollider use a
   * worst-case of zero (e.g. if the other sprite is passing through a corner).
   * @method _getMinRadius
   * @protected
   * @param {p5.Vector} axis
   * @return {number}
   */
  p5.OrientedBoundingBoxCollider.prototype._getMinRadius =
    p5.AxisAlignedBoundingBoxCollider.prototype._getMinRadius;

  /**
   * A 2D affine transformation (translation, rotation, scale) stored as a
   * 3x3 matrix that uses homogeneous coordinates.  Used to quickly transform
   * points or vectors between reference frames.
   * @class p5.Transform2D
   * @constructor
   * @extends Array
   * @param {p5.Transform2D|Array.<number>} [source]
   */
  p5.Transform2D = function(source) {
    // We only store the first six values.
    // the last row in a 2D transform matrix is always "0 0 1" so we can
    // save space and speed up certain calculations with this assumption.
    source = source || [1, 0, 0, 0, 1, 0];
    if (source.length !== 6) {
      throw new TypeError('Transform2D must have six components');
    }
    this.length = 6;
    this[0] = source[0];
    this[1] = source[1];
    this[2] = source[2];
    this[3] = source[3];
    this[4] = source[4];
    this[5] = source[5];
  };
  p5.Transform2D.prototype = Object.create(Array.prototype);

  /**
   * Reset this transform to an identity transform, in-place.
   * @method clear
   * @return {p5.Transform2D} this transform
   */
  p5.Transform2D.prototype.clear = function() {
    this[0] = 1;
    this[1] = 0;
    this[2] = 0;
    this[3] = 0;
    this[4] = 1;
    this[5] = 0;
    return this;
  };

  /**
   * Make a copy of this transform.
   * @method copy
   * @return {p5.Transform2D}
   */
  p5.Transform2D.prototype.copy = function() {
    return new p5.Transform2D(this);
  };

  /**
   * Check whether two transforms are the same.
   * @method equals
   * @param {p5.Transform2D|Array.<number>} other
   * @return {boolean}
   */
  p5.Transform2D.prototype.equals = function(other) {
    if (!(other instanceof p5.Transform2D || Array.isArray(other))) {
      return false; // Never equal to other types.
    }

    for (var i = 0; i < 6; i++) {
      if (this[i] !== other[i]) {
        return false;
      }
    }
    return true;
  };

  /**
   * Multiply two transforms together, combining them.
   * Does not modify original transforms.  Assigns result into dest argument if
   * provided and returns it.  Otherwise returns a new transform.
   * @method mult
   * @static
   * @param {p5.Transform2D|Array.<number>} t1
   * @param {p5.Transform2D|Array.<number>} t2
   * @param {p5.Transform2D} [dest]
   * @return {p5.Transform2D}
   */
  p5.Transform2D.mult = function(t1, t2, dest) {
    dest = dest || new p5.Transform2D();

    // Capture values of original matrices in local variables, in case one of
    // them is the one we're mutating.
    var t1_0, t1_1, t1_2, t1_3, t1_4, t1_5;
    t1_0 = t1[0];
    t1_1 = t1[1];
    t1_2 = t1[2];
    t1_3 = t1[3];
    t1_4 = t1[4];
    t1_5 = t1[5];

    var t2_0, t2_1, t2_2, t2_3, t2_4, t2_5;
    t2_0 = t2[0];
    t2_1 = t2[1];
    t2_2 = t2[2];
    t2_3 = t2[3];
    t2_4 = t2[4];
    t2_5 = t2[5];

    dest[0] = t1_0*t2_0 + t1_1*t2_3;
    dest[1] = t1_0*t2_1 + t1_1*t2_4;
    dest[2] = t1_0*t2_2 + t1_1*t2_5 + t1_2;

    dest[3] = t1_3*t2_0 + t1_4*t2_3;
    dest[4] = t1_3*t2_1 + t1_4*t2_4;
    dest[5] = t1_3*t2_2 + t1_4*t2_5 + t1_5;

    return dest;
  };

  /**
   * Multiply this transform by another, combining them.
   * Modifies this transform and returns it.
   * @method mult
   * @param {p5.Transform2D|Float32Array|Array.<number>} other
   * @return {p5.Transform2D}
   */
  p5.Transform2D.prototype.mult = function(other) {
    return p5.Transform2D.mult(this, other, this);
  };

  /**
   * Modify this transform, translating it by a certain amount.
   * Returns this transform.
   * @method translate
   * @return {p5.Transform2D}
   * @example
   *     // Two different ways to call this method.
   *     var t = new p5.Transform();
   *     // 1. Two numbers
   *     t.translate(x, y);
   *     // 2. One vector
   *     t.translate(new p5.Vector(x, y));
   */
  p5.Transform2D.prototype.translate = function(arg0, arg1) {
    var x, y;
    if (arg0 instanceof p5.Vector) {
      x = arg0.x;
      y = arg0.y;
    } else if (typeof arg0 === 'number' && typeof arg1 === 'number') {
      x = arg0;
      y = arg1;
    } else {
      var args = '';
      for (var i = 0; i < arguments.length; i++) {
        args += arguments[i] + ', ';
      }
      throw new TypeError('Invalid arguments to Transform2D.translate: ' + args);
    }
    return p5.Transform2D.mult([
      1, 0, x,
      0, 1, y
    ], this, this);
  };

  /**
   * Retrieve the resolved translation of this transform.
   * @method getTranslation
   * @return {p5.Vector}
   */
  p5.Transform2D.prototype.getTranslation = function() {
    return new p5.Vector(this[2], this[5]);
  };

  /**
   * Modify this transform, scaling it by a certain amount.
   * Returns this transform.
   * @method scale
   * @return {p5.Transform2D}
   * @example
   *     // Three different ways to call this method.
   *     var t = new p5.Transform();
   *     // 1. One scalar value
   *     t.scale(uniformScale);
   *     // 1. Two scalar values
   *     t.scale(scaleX, scaleY);
   *     // 2. One vector
   *     t.translate(new p5.Vector(scaleX, scaleY));
   */
  p5.Transform2D.prototype.scale = function(arg0, arg1) {
    var sx, sy;
    if (arg0 instanceof p5.Vector) {
      sx = arg0.x;
      sy = arg0.y;
    } else if (typeof arg0 === 'number' && typeof arg1 === 'number') {
      sx = arg0;
      sy = arg1;
    } else if (typeof arg0 === 'number') {
      sx = arg0;
      sy = arg0;
    } else {
      throw new TypeError('Invalid arguments to Transform2D.scale: ' + arguments);
    }
    return p5.Transform2D.mult([
      sx, 0, 0,
      0, sy, 0
    ], this, this);
  };

  /**
   * Retrieve the scale vector of this transform.
   * @method getScale
   * @return {p5.Vector}
   */
  p5.Transform2D.prototype.getScale = function() {
    var a = this[0], b = this[1],
        c = this[3], d = this[4];
    return new p5.Vector(
      sign(a) * Math.sqrt(a*a + b*b),
      sign(d) * Math.sqrt(c*c + d*d)
    );
  };

  /*
   * Return -1, 0, or 1 depending on whether a number is negative, zero, or positive.
   */
  function sign(x) {
    x = +x; // convert to a number
    if (x === 0 || isNaN(x)) {
      return Number(x);
    }
    return x > 0 ? 1 : -1;
  }

  /**
   * Modify this transform, rotating it by a certain amount.
   * @method rotate
   * @param {number} radians
   * @return {p5.Transform2D}
   */
  p5.Transform2D.prototype.rotate = function(radians) {
    // Clockwise!
    if (typeof radians !== 'number') {
      throw new TypeError('Invalid arguments to Transform2D.rotate: ' + arguments);
    }
    var sinR = Math.sin(radians);
    var cosR = Math.cos(radians);
    return p5.Transform2D.mult([
      cosR, -sinR, 0,
      sinR, cosR, 0
    ], this, this);
  };

  /**
   * Retrieve the angle of this transform in radians.
   * @method getRotation
   * @return {number}
   */
  p5.Transform2D.prototype.getRotation = function() {
    // see http://math.stackexchange.com/a/13165
    return Math.atan2(-this[1], this[0]);
  };

  /**
   * Applies a 2D transformation matrix (using homogeneous coordinates, so 3x3)
   * to a Vector2 (<x, y, 1>) and returns a new vector2.
   * @method transform
   * @for p5.Vector
   * @static
   * @param {p5.Vector} v
   * @param {p5.Transform2D} t
   * @return {p5.Vector} a new vector
   */
  p5.Vector.transform = function(v, t) {
    return v.copy().transform(t);
  };

  /**
   * Transforms this vector by a 2D transformation matrix.
   * @method transform
   * @for p5.Vector
   * @param {p5.Transform2D} transform
   * @return {p5.Vector} this, after the change
   */
  p5.Vector.prototype.transform = function(transform) {
    // Note: We cheat a whole bunch here since this is just 2D!
    // Use a different method if looking for true matrix multiplication.
    var x = this.x;
    var y = this.y;
    this.x = transform[0]*x + transform[1]*y + transform[2];
    this.y = transform[3]*x + transform[4]*y + transform[5];
    return this;
  };

}));
s…]()

