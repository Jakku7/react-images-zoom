# React Images Extended

![downloads](https://img.shields.io/npm/dt/react-images-zoom.svg 'NpmJS total downloads')

A simple, responsive lightbox React JS component for displaying an array of images with zooming and rotating capabilities.
This is a fork of [jossmac/react-images](https://github.com/jossmac/react-images) and [simokhalil/react-images-extended](https://github.com/simokhalil/react-images-extended)

### Why this fork?
Fork is based on xiaoman885 react-images-zoom repository. I needed it to add additional stuff and make some small fixes for zoom and rotate features. There is also "loop" prop added. If enabled, it prevents arrow images from being hidden on last/first image. 

### Quick start


```bash
npm install --save react-images-zoom
```
or
```bash
yarn add react-images-zoom
```

```jsx
import React from 'react';
import Lightbox from 'react-images-zoom';

export default class Sample extends React.Component {
  ...
  render() {
    return (
      <Lightbox
        images={[{ src: 'http://example.com/img1.jpg' }, { src: 'http://example.com/img2.jpg' }]}
        isOpen={this.state.lightboxIsOpen}
        loop
        onClickPrev={this.gotoPrevious}
        onClickNext={this.gotoNext}
        onClose={this.closeLightbox}
        rotatable={true}
        zoomable={true}
        onSave={(currentImageIndex, params) => console.log('currentImageIndex, currentImageSrc, params : ', currentImageIndex, this.props.images[currentImageIndex].src, params)}
      />
    );
  }
}
```
##  Loop example
To add a loop to your lightbox gallery you need to add a loop prop to your component and tell lightbox what to do when condition is met. Like: 

```
gotoPrevious() {
    this.setState({
      currentImage: this.state.currentImage - 1,
    });
    if (this.state.currentImage === 0) {
      this.setState({
        currentImage: this.props.images.length - 1,
      });
    }
  }
  gotoNext() {
    this.setState({
      currentImage: this.state.currentImage + 1,
    });
    if (this.state.currentImage === this.props.images.length - 1) {
      this.setState({
        currentImage: 0,
      });
    }
  }
```

##  Examples

To build the examples locally, run:

```
yarn install
yarn start
```

Then open [`localhost:8000`](http://localhost:8000) in a browser.

### Using srcSet

Example using srcSet:
```jsx
<Lightbox
  images={LIGHTBOX_IMAGE_SET}
  ...
/>

const LIGHTBOX_IMAGE_SET = [
  {
    src: 'http://example.com/example/img1.jpg',
    caption: 'A forest'
    srcSet: [
      'http://example.com/example/img1_1024.jpg 1024w',
      'http://example.com/example/img1_800.jpg 800w',
      'http://example.com/example/img1_500.jpg 500w',
      'http://example.com/example/img1_320.jpg 320w',
    ],
  },
  {
    src: 'http://example.com/example/img2.jpg',
    srcSet: [
      'http://example.com/example/img2_1024.jpg 1024w',
      'http://example.com/example/img2_800.jpg 800w',
      'http://example.com/example/img2_500.jpg 500w',
      'http://example.com/example/img2_320.jpg 320w',
    ],
  }
];

```

## Options

Property	|	Type		|	Default		|	Description
:-----------------------|:--------------|:--------------|:--------------------------------
backdropClosesModal	|	bool	|	false	|	Allow users to exit the lightbox by clicking the backdrop
closeButtonTitle | string | ' Close (Esc) ' | Customize close esc title
enableKeyboardInput | bool  | true  | Supports keyboard input - <code>esc</code>, <code>arrow left</code>, and <code>arrow right</code>
currentImage  | number  | 0 | The index of the image to display initially
customControls | array | undefined | An array of elements to display as custom controls on the top of lightbox
images  | array | undefined | Required. Array of image objects See image options table below
imageCountSeparator  | String  | ' of ' | Customize separator in the image count
isOpen  | bool  | false | Whether or not the lightbox is displayed
leftArrowTitle | string | ' Previous (Left arrow key) ' | Customize of left arrow title
loop | bool | false | Enables loop for lightbox gallery
onClickPrev | func | undefined | Fired on request of the previous image
onClickNext | func | undefined | Fired on request of the next image
onClose | func | undefined | Required. Handle closing of the lightbox
onClickImage | func | undefined | Handle click on image
onClickThumbnail | func | undefined | Handle click on thumbnail
onSave | func | undefined | Show save button and handle click / params : currentImageIndex, {rotation, zoom}
preloadNextImage | bool | true | Based on the direction the user is navigating, preload the next available image
rightArrowTitle | string | ' Next (Right arrow key) ' | Customize right arrow title
rotatable | bool | false | Show rotate buttons
showCloseButton | bool  | true | Optionally display a close "X" button in top right corner
showImageCount | bool  | true | Optionally display image index, e.g., "3 of 20"
width | number  | 1024 | Maximum width of the carousel; defaults to 1024px
spinner | func | DefaultSpinner | Spinner component class
spinnerColor | string | 'white' | Color of spinner
spinnerSize | number | 100 | Size of spinner
preventScroll | bool | true | Determines whether scrolling is prevented via [react-scrolllock](https://github.com/jossmac/react-scrolllock)
zoomable | bool | false | Show zoom buttons

## Images object

Property	|	Type		|	Default		|	Description
:-----------------------|:--------------|:--------------|:--------------------------------
src  | string | undefined | Required
srcSet  | array of strings | undefined | Optional
caption  | string | undefined | Optional
alt  | string | undefined | Optional
initialZoom  | number | 1 | Optional
initialRotation  | number | 0 | Optional
