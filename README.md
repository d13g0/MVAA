# MVAA

MVAA is a tool to create multivariate asymmetry brain maps. 

## pre-requisites

* **You need two images**: the unflipped (u) and the flipped (f). These images must be Ideally you want these images to be registered to a symmetric brain template so you can obtain a near-voxel correspondance. However, if the images are not registered, the script will still run as long as they have the same spatial dimensions.

* **Python dependencies**: 
    
    numpy    : http://www.numpy.org/ 
    
    PyNifti  : http://niftilib.sourceforge.net/pynifti/
   
    PyCuda   : http://mathema.tician.de/software/pycuda/


* **CPU is optional**: the code is designed to run using CUDA (through PyCuda). However if you don't have a GPU, you can still run the CPU version (way slower.. go for a coffee...). However, I recommend you to install CUDA in your machine, then PyCuda.

## Usage

- GPU version
```python
mvaa_ks.py     -u <unflipped.nii.gz>  -f <flipped.nii.gz>  -r <radius>  #GPU version     
mvaa_ks_cpu.py -u <unflipped.nii.gz>  -f <flipped.nii.gz>  -r <radius>  #CPU version
```
The radius parameter will depend on how robust your GPU is and how large you want the voxel neighbourhoods to be. I have used a value of r=3 for brain images with a voxel size of 1mm. This adds up to having neighbourhoods of 7mm in diameter/ 3.5mm in radius (center voxel + r):

<pre>
           1 + 1 + 1 + 1 + 1 + 1 + 1    = 7
         .___.___.___.___.___.___.___.
         | 3 | 2 | 1 |   |   |   |   |
         .___.___.___.___.___.___.___.
         <------------ c  ----------->
                r = 3
                d = 7
</pre>
But, the size in milimmetres will depend on your voxel resolution. Nonetheless, r>4 may hog your GPU. So make sure you have a good one (plus, why would you want larger neighbourhoods?), OR you can use the CPU version.

## Questions?
Feel free to send me an email if you have any questions

## Licence

Copyright (c) 2015 Diego Cantor

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
