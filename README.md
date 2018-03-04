## React Image Cropper Dynamic

[![Downloads](https://img.shields.io/npm/dt/react-image-cropper.svg)](https://www.npmjs.com/package/react-image-cropper)
[![Version](https://img.shields.io/npm/v/react-image-cropper.svg)](https://www.npmjs.com/package/react-image-cropper)

## Changes
The purpose of this repo is to give more control to image sizing. There is a bug that exists in the current source code which will force any image to be sized to the dimensions of the parent container. 

Problems: 
1) If your parent container is 600px wide and you upload a 1500px image, the 1500px image will be stretched down to 600px meaning the maxium crop size is 600px. This is a major flaw. 
2) If your container is 1500px wide and your image is 600px, the 600px image will be stretched. Even though the original image is only 600px wide, your can crop this image to a 1500px wide segment. 

These are the problems that prompted me to make some additions to the source code. 
# How to use the changes

## Step 1) Referencing the new package
To use this package instead of the original you must edit your project's package.json to reference this repo like this:  

"react-image-cropper": "git+https://github.com/jamesdorrian/react-image-cropper-dynamic.git"

## Step 2) Finding the image Width
The react image documentation [available here](https://facebook.github.io/react-native/docs/image.html) has a method called .getSize() which is an asynchronous call returning the width and height of an image. However, This method can fail if the image cannot be found, or fails to download and as such should not be relied upon too heavily. 

A more robust (but somewhat hacky) change that can be used is to use the image src to render a background image with z-index -10 and position:absolute; Use the ```<Img ref='hiddenImage' className='hideMe' onLoad={() => this.executeFunctionName()}>``` method to access the width and height of the image when loaded. This can be done easily using refs to access the Image object's information. 

Only when the image is loaded should you allow the cropper to render (using conditional react rendering techniques [found here](https://reactjs.org/docs/conditional-rendering.html). 

## Step 3) Loading the image width prop into the component
Once these dimensions are attained and the cropper is ready to be loaded, you must enter the new width as a prop to the ```<Cropper newItem={WIDTH HERE AS INTEGER} />```


**[See the original package](https://www.npmjs.com/package/react-image-cropper)**


**[See the original demo](http://braavos.me/react-image-cropper/)**
