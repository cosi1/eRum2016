---
title       : pdbeeR
subtitle    : 
author      : Paweł Piątkowski
job         : 
framework   : revealjs        # {io2012, html5slides, shower, dzslides, ...}
revealjs    :
  theme     : solarized
  transition: none
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : zenburn
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

# pdbeeR

Paweł Piątkowski

---

## Read-And-Delete




```r
library(pdbeeR)
pdb = read.pdb("data/1ow9_00_A.pdb")
coord = pdb$coord
showStructure(coord)
```

<script>/*
* Copyright (C) 2009 Apple Inc. All Rights Reserved.
*
* Redistribution and use in source and binary forms, with or without
* modification, are permitted provided that the following conditions
* are met:
* 1. Redistributions of source code must retain the above copyright
*    notice, this list of conditions and the following disclaimer.
* 2. Redistributions in binary form must reproduce the above copyright
*    notice, this list of conditions and the following disclaimer in the
*    documentation and/or other materials provided with the distribution.
*
* THIS SOFTWARE IS PROVIDED BY APPLE INC. ``AS IS'' AND ANY
* EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
* IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
* PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL APPLE INC. OR
* CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
* EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
* PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
* PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY
* OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
* (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
* OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
* Copyright (2016) Duncan Murdoch - fixed CanvasMatrix4.ortho,
* cleaned up.
*/
/*
CanvasMatrix4 class
This class implements a 4x4 matrix. It has functions which
duplicate the functionality of the OpenGL matrix stack and
glut functions.
IDL:
[
Constructor(in CanvasMatrix4 matrix),           // copy passed matrix into new CanvasMatrix4
Constructor(in sequence<float> array)           // create new CanvasMatrix4 with 16 floats (row major)
Constructor()                                   // create new CanvasMatrix4 with identity matrix
]
interface CanvasMatrix4 {
attribute float m11;
attribute float m12;
attribute float m13;
attribute float m14;
attribute float m21;
attribute float m22;
attribute float m23;
attribute float m24;
attribute float m31;
attribute float m32;
attribute float m33;
attribute float m34;
attribute float m41;
attribute float m42;
attribute float m43;
attribute float m44;
void load(in CanvasMatrix4 matrix);                 // copy the values from the passed matrix
void load(in sequence<float> array);                // copy 16 floats into the matrix
sequence<float> getAsArray();                       // return the matrix as an array of 16 floats
WebGLFloatArray getAsCanvasFloatArray();           // return the matrix as a WebGLFloatArray with 16 values
void makeIdentity();                                // replace the matrix with identity
void transpose();                                   // replace the matrix with its transpose
void invert();                                      // replace the matrix with its inverse
void translate(in float x, in float y, in float z); // multiply the matrix by passed translation values on the right
void scale(in float x, in float y, in float z);     // multiply the matrix by passed scale values on the right
void rotate(in float angle,                         // multiply the matrix by passed rotation values on the right
in float x, in float y, in float z);    // (angle is in degrees)
void multRight(in CanvasMatrix matrix);             // multiply the matrix by the passed matrix on the right
void multLeft(in CanvasMatrix matrix);              // multiply the matrix by the passed matrix on the left
void ortho(in float left, in float right,           // multiply the matrix by the passed ortho values on the right
in float bottom, in float top,
in float near, in float far);
void frustum(in float left, in float right,         // multiply the matrix by the passed frustum values on the right
in float bottom, in float top,
in float near, in float far);
void perspective(in float fovy, in float aspect,    // multiply the matrix by the passed perspective values on the right
in float zNear, in float zFar);
void lookat(in float eyex, in float eyey, in float eyez,    // multiply the matrix by the passed lookat
in float ctrx, in float ctry, in float ctrz,    // values on the right
in float upx, in float upy, in float upz);
}
*/
CanvasMatrix4 = function(m)
{
if (typeof m == 'object') {
if ("length" in m && m.length >= 16) {
this.load(m[0], m[1], m[2], m[3], m[4], m[5], m[6], m[7], m[8], m[9], m[10], m[11], m[12], m[13], m[14], m[15]);
return;
}
else if (m instanceof CanvasMatrix4) {
this.load(m);
return;
}
}
this.makeIdentity();
};
CanvasMatrix4.prototype.load = function()
{
if (arguments.length == 1 && typeof arguments[0] == 'object') {
var matrix = arguments[0];
if ("length" in matrix && matrix.length == 16) {
this.m11 = matrix[0];
this.m12 = matrix[1];
this.m13 = matrix[2];
this.m14 = matrix[3];
this.m21 = matrix[4];
this.m22 = matrix[5];
this.m23 = matrix[6];
this.m24 = matrix[7];
this.m31 = matrix[8];
this.m32 = matrix[9];
this.m33 = matrix[10];
this.m34 = matrix[11];
this.m41 = matrix[12];
this.m42 = matrix[13];
this.m43 = matrix[14];
this.m44 = matrix[15];
return;
}
if (arguments[0] instanceof CanvasMatrix4) {
this.m11 = matrix.m11;
this.m12 = matrix.m12;
this.m13 = matrix.m13;
this.m14 = matrix.m14;
this.m21 = matrix.m21;
this.m22 = matrix.m22;
this.m23 = matrix.m23;
this.m24 = matrix.m24;
this.m31 = matrix.m31;
this.m32 = matrix.m32;
this.m33 = matrix.m33;
this.m34 = matrix.m34;
this.m41 = matrix.m41;
this.m42 = matrix.m42;
this.m43 = matrix.m43;
this.m44 = matrix.m44;
return;
}
}
this.makeIdentity();
};
CanvasMatrix4.prototype.getAsArray = function()
{
return [
this.m11, this.m12, this.m13, this.m14,
this.m21, this.m22, this.m23, this.m24,
this.m31, this.m32, this.m33, this.m34,
this.m41, this.m42, this.m43, this.m44
];
};
CanvasMatrix4.prototype.getAsWebGLFloatArray = function()
{
return new WebGLFloatArray(this.getAsArray());
};
CanvasMatrix4.prototype.makeIdentity = function()
{
this.m11 = 1;
this.m12 = 0;
this.m13 = 0;
this.m14 = 0;
this.m21 = 0;
this.m22 = 1;
this.m23 = 0;
this.m24 = 0;
this.m31 = 0;
this.m32 = 0;
this.m33 = 1;
this.m34 = 0;
this.m41 = 0;
this.m42 = 0;
this.m43 = 0;
this.m44 = 1;
};
CanvasMatrix4.prototype.transpose = function()
{
var tmp = this.m12;
this.m12 = this.m21;
this.m21 = tmp;
tmp = this.m13;
this.m13 = this.m31;
this.m31 = tmp;
tmp = this.m14;
this.m14 = this.m41;
this.m41 = tmp;
tmp = this.m23;
this.m23 = this.m32;
this.m32 = tmp;
tmp = this.m24;
this.m24 = this.m42;
this.m42 = tmp;
tmp = this.m34;
this.m34 = this.m43;
this.m43 = tmp;
};
CanvasMatrix4.prototype.invert = function()
{
// Calculate the 4x4 determinant
// If the determinant is zero,
// then the inverse matrix is not unique.
var det = this._determinant4x4();
if (Math.abs(det) < 1e-8)
return null;
this._makeAdjoint();
// Scale the adjoint matrix to get the inverse
this.m11 /= det;
this.m12 /= det;
this.m13 /= det;
this.m14 /= det;
this.m21 /= det;
this.m22 /= det;
this.m23 /= det;
this.m24 /= det;
this.m31 /= det;
this.m32 /= det;
this.m33 /= det;
this.m34 /= det;
this.m41 /= det;
this.m42 /= det;
this.m43 /= det;
this.m44 /= det;
};
CanvasMatrix4.prototype.translate = function(x,y,z)
{
if (x === undefined)
x = 0;
if (y === undefined)
y = 0;
if (z === undefined)
z = 0;
var matrix = new CanvasMatrix4();
matrix.m41 = x;
matrix.m42 = y;
matrix.m43 = z;
this.multRight(matrix);
};
CanvasMatrix4.prototype.scale = function(x,y,z)
{
if (x === undefined)
x = 1;
if (z === undefined) {
if (y === undefined) {
y = x;
z = x;
}
else
z = 1;
}
else if (y === undefined)
y = x;
var matrix = new CanvasMatrix4();
matrix.m11 = x;
matrix.m22 = y;
matrix.m33 = z;
this.multRight(matrix);
};
CanvasMatrix4.prototype.rotate = function(angle,x,y,z)
{
// angles are in degrees. Switch to radians
angle = angle / 180 * Math.PI;
angle /= 2;
var sinA = Math.sin(angle);
var cosA = Math.cos(angle);
var sinA2 = sinA * sinA;
// normalize
var length = Math.sqrt(x * x + y * y + z * z);
if (length === 0) {
// bad vector, just use something reasonable
x = 0;
y = 0;
z = 1;
} else if (length != 1) {
x /= length;
y /= length;
z /= length;
}
var mat = new CanvasMatrix4();
// optimize case where axis is along major axis
if (x == 1 && y === 0 && z === 0) {
mat.m11 = 1;
mat.m12 = 0;
mat.m13 = 0;
mat.m21 = 0;
mat.m22 = 1 - 2 * sinA2;
mat.m23 = 2 * sinA * cosA;
mat.m31 = 0;
mat.m32 = -2 * sinA * cosA;
mat.m33 = 1 - 2 * sinA2;
mat.m14 = mat.m24 = mat.m34 = 0;
mat.m41 = mat.m42 = mat.m43 = 0;
mat.m44 = 1;
} else if (x === 0 && y == 1 && z === 0) {
mat.m11 = 1 - 2 * sinA2;
mat.m12 = 0;
mat.m13 = -2 * sinA * cosA;
mat.m21 = 0;
mat.m22 = 1;
mat.m23 = 0;
mat.m31 = 2 * sinA * cosA;
mat.m32 = 0;
mat.m33 = 1 - 2 * sinA2;
mat.m14 = mat.m24 = mat.m34 = 0;
mat.m41 = mat.m42 = mat.m43 = 0;
mat.m44 = 1;
} else if (x === 0 && y === 0 && z == 1) {
mat.m11 = 1 - 2 * sinA2;
mat.m12 = 2 * sinA * cosA;
mat.m13 = 0;
mat.m21 = -2 * sinA * cosA;
mat.m22 = 1 - 2 * sinA2;
mat.m23 = 0;
mat.m31 = 0;
mat.m32 = 0;
mat.m33 = 1;
mat.m14 = mat.m24 = mat.m34 = 0;
mat.m41 = mat.m42 = mat.m43 = 0;
mat.m44 = 1;
} else {
var x2 = x*x;
var y2 = y*y;
var z2 = z*z;
mat.m11 = 1 - 2 * (y2 + z2) * sinA2;
mat.m12 = 2 * (x * y * sinA2 + z * sinA * cosA);
mat.m13 = 2 * (x * z * sinA2 - y * sinA * cosA);
mat.m21 = 2 * (y * x * sinA2 - z * sinA * cosA);
mat.m22 = 1 - 2 * (z2 + x2) * sinA2;
mat.m23 = 2 * (y * z * sinA2 + x * sinA * cosA);
mat.m31 = 2 * (z * x * sinA2 + y * sinA * cosA);
mat.m32 = 2 * (z * y * sinA2 - x * sinA * cosA);
mat.m33 = 1 - 2 * (x2 + y2) * sinA2;
mat.m14 = mat.m24 = mat.m34 = 0;
mat.m41 = mat.m42 = mat.m43 = 0;
mat.m44 = 1;
}
this.multRight(mat);
};
CanvasMatrix4.prototype.multRight = function(mat)
{
var m11 = (this.m11 * mat.m11 + this.m12 * mat.m21 +
this.m13 * mat.m31 + this.m14 * mat.m41);
var m12 = (this.m11 * mat.m12 + this.m12 * mat.m22 +
this.m13 * mat.m32 + this.m14 * mat.m42);
var m13 = (this.m11 * mat.m13 + this.m12 * mat.m23 +
this.m13 * mat.m33 + this.m14 * mat.m43);
var m14 = (this.m11 * mat.m14 + this.m12 * mat.m24 +
this.m13 * mat.m34 + this.m14 * mat.m44);
var m21 = (this.m21 * mat.m11 + this.m22 * mat.m21 +
this.m23 * mat.m31 + this.m24 * mat.m41);
var m22 = (this.m21 * mat.m12 + this.m22 * mat.m22 +
this.m23 * mat.m32 + this.m24 * mat.m42);
var m23 = (this.m21 * mat.m13 + this.m22 * mat.m23 +
this.m23 * mat.m33 + this.m24 * mat.m43);
var m24 = (this.m21 * mat.m14 + this.m22 * mat.m24 +
this.m23 * mat.m34 + this.m24 * mat.m44);
var m31 = (this.m31 * mat.m11 + this.m32 * mat.m21 +
this.m33 * mat.m31 + this.m34 * mat.m41);
var m32 = (this.m31 * mat.m12 + this.m32 * mat.m22 +
this.m33 * mat.m32 + this.m34 * mat.m42);
var m33 = (this.m31 * mat.m13 + this.m32 * mat.m23 +
this.m33 * mat.m33 + this.m34 * mat.m43);
var m34 = (this.m31 * mat.m14 + this.m32 * mat.m24 +
this.m33 * mat.m34 + this.m34 * mat.m44);
var m41 = (this.m41 * mat.m11 + this.m42 * mat.m21 +
this.m43 * mat.m31 + this.m44 * mat.m41);
var m42 = (this.m41 * mat.m12 + this.m42 * mat.m22 +
this.m43 * mat.m32 + this.m44 * mat.m42);
var m43 = (this.m41 * mat.m13 + this.m42 * mat.m23 +
this.m43 * mat.m33 + this.m44 * mat.m43);
var m44 = (this.m41 * mat.m14 + this.m42 * mat.m24 +
this.m43 * mat.m34 + this.m44 * mat.m44);
this.m11 = m11;
this.m12 = m12;
this.m13 = m13;
this.m14 = m14;
this.m21 = m21;
this.m22 = m22;
this.m23 = m23;
this.m24 = m24;
this.m31 = m31;
this.m32 = m32;
this.m33 = m33;
this.m34 = m34;
this.m41 = m41;
this.m42 = m42;
this.m43 = m43;
this.m44 = m44;
};
CanvasMatrix4.prototype.multLeft = function(mat)
{
var m11 = (mat.m11 * this.m11 + mat.m12 * this.m21 +
mat.m13 * this.m31 + mat.m14 * this.m41);
var m12 = (mat.m11 * this.m12 + mat.m12 * this.m22 +
mat.m13 * this.m32 + mat.m14 * this.m42);
var m13 = (mat.m11 * this.m13 + mat.m12 * this.m23 +
mat.m13 * this.m33 + mat.m14 * this.m43);
var m14 = (mat.m11 * this.m14 + mat.m12 * this.m24 +
mat.m13 * this.m34 + mat.m14 * this.m44);
var m21 = (mat.m21 * this.m11 + mat.m22 * this.m21 +
mat.m23 * this.m31 + mat.m24 * this.m41);
var m22 = (mat.m21 * this.m12 + mat.m22 * this.m22 +
mat.m23 * this.m32 + mat.m24 * this.m42);
var m23 = (mat.m21 * this.m13 + mat.m22 * this.m23 +
mat.m23 * this.m33 + mat.m24 * this.m43);
var m24 = (mat.m21 * this.m14 + mat.m22 * this.m24 +
mat.m23 * this.m34 + mat.m24 * this.m44);
var m31 = (mat.m31 * this.m11 + mat.m32 * this.m21 +
mat.m33 * this.m31 + mat.m34 * this.m41);
var m32 = (mat.m31 * this.m12 + mat.m32 * this.m22 +
mat.m33 * this.m32 + mat.m34 * this.m42);
var m33 = (mat.m31 * this.m13 + mat.m32 * this.m23 +
mat.m33 * this.m33 + mat.m34 * this.m43);
var m34 = (mat.m31 * this.m14 + mat.m32 * this.m24 +
mat.m33 * this.m34 + mat.m34 * this.m44);
var m41 = (mat.m41 * this.m11 + mat.m42 * this.m21 +
mat.m43 * this.m31 + mat.m44 * this.m41);
var m42 = (mat.m41 * this.m12 + mat.m42 * this.m22 +
mat.m43 * this.m32 + mat.m44 * this.m42);
var m43 = (mat.m41 * this.m13 + mat.m42 * this.m23 +
mat.m43 * this.m33 + mat.m44 * this.m43);
var m44 = (mat.m41 * this.m14 + mat.m42 * this.m24 +
mat.m43 * this.m34 + mat.m44 * this.m44);
this.m11 = m11;
this.m12 = m12;
this.m13 = m13;
this.m14 = m14;
this.m21 = m21;
this.m22 = m22;
this.m23 = m23;
this.m24 = m24;
this.m31 = m31;
this.m32 = m32;
this.m33 = m33;
this.m34 = m34;
this.m41 = m41;
this.m42 = m42;
this.m43 = m43;
this.m44 = m44;
};
CanvasMatrix4.prototype.ortho = function(left, right, bottom, top, near, far)
{
var tx = (left + right) / (left - right);
var ty = (top + bottom) / (bottom - top);
var tz = (far + near) / (near - far);
var matrix = new CanvasMatrix4();
matrix.m11 = 2 / (right - left);
matrix.m12 = 0;
matrix.m13 = 0;
matrix.m14 = 0;
matrix.m21 = 0;
matrix.m22 = 2 / (top - bottom);
matrix.m23 = 0;
matrix.m24 = 0;
matrix.m31 = 0;
matrix.m32 = 0;
matrix.m33 = -2 / (far - near);
matrix.m34 = 0;
matrix.m41 = tx;
matrix.m42 = ty;
matrix.m43 = tz;
matrix.m44 = 1;
this.multRight(matrix);
};
CanvasMatrix4.prototype.frustum = function(left, right, bottom, top, near, far)
{
var matrix = new CanvasMatrix4();
var A = (right + left) / (right - left);
var B = (top + bottom) / (top - bottom);
var C = -(far + near) / (far - near);
var D = -(2 * far * near) / (far - near);
matrix.m11 = (2 * near) / (right - left);
matrix.m12 = 0;
matrix.m13 = 0;
matrix.m14 = 0;
matrix.m21 = 0;
matrix.m22 = 2 * near / (top - bottom);
matrix.m23 = 0;
matrix.m24 = 0;
matrix.m31 = A;
matrix.m32 = B;
matrix.m33 = C;
matrix.m34 = -1;
matrix.m41 = 0;
matrix.m42 = 0;
matrix.m43 = D;
matrix.m44 = 0;
this.multRight(matrix);
};
CanvasMatrix4.prototype.perspective = function(fovy, aspect, zNear, zFar)
{
var top = Math.tan(fovy * Math.PI / 360) * zNear;
var bottom = -top;
var left = aspect * bottom;
var right = aspect * top;
this.frustum(left, right, bottom, top, zNear, zFar);
};
CanvasMatrix4.prototype.lookat = function(eyex, eyey, eyez, centerx, centery, centerz, upx, upy, upz)
{
var matrix = new CanvasMatrix4();
// Make rotation matrix
// Z vector
var zx = eyex - centerx;
var zy = eyey - centery;
var zz = eyez - centerz;
var mag = Math.sqrt(zx * zx + zy * zy + zz * zz);
if (mag) {
zx /= mag;
zy /= mag;
zz /= mag;
}
// Y vector
var yx = upx;
var yy = upy;
var yz = upz;
// X vector = Y cross Z
xx =  yy * zz - yz * zy;
xy = -yx * zz + yz * zx;
xz =  yx * zy - yy * zx;
// Recompute Y = Z cross X
yx = zy * xz - zz * xy;
yy = -zx * xz + zz * xx;
yx = zx * xy - zy * xx;
// cross product gives area of parallelogram, which is < 1.0 for
// non-perpendicular unit-length vectors; so normalize x, y here
mag = Math.sqrt(xx * xx + xy * xy + xz * xz);
if (mag) {
xx /= mag;
xy /= mag;
xz /= mag;
}
mag = Math.sqrt(yx * yx + yy * yy + yz * yz);
if (mag) {
yx /= mag;
yy /= mag;
yz /= mag;
}
matrix.m11 = xx;
matrix.m12 = xy;
matrix.m13 = xz;
matrix.m14 = 0;
matrix.m21 = yx;
matrix.m22 = yy;
matrix.m23 = yz;
matrix.m24 = 0;
matrix.m31 = zx;
matrix.m32 = zy;
matrix.m33 = zz;
matrix.m34 = 0;
matrix.m41 = 0;
matrix.m42 = 0;
matrix.m43 = 0;
matrix.m44 = 1;
matrix.translate(-eyex, -eyey, -eyez);
this.multRight(matrix);
};
// Support functions
CanvasMatrix4.prototype._determinant2x2 = function(a, b, c, d)
{
return a * d - b * c;
};
CanvasMatrix4.prototype._determinant3x3 = function(a1, a2, a3, b1, b2, b3, c1, c2, c3)
{
return a1 * this._determinant2x2(b2, b3, c2, c3) -
b1 * this._determinant2x2(a2, a3, c2, c3) +
c1 * this._determinant2x2(a2, a3, b2, b3);
};
CanvasMatrix4.prototype._determinant4x4 = function()
{
var a1 = this.m11;
var b1 = this.m12;
var c1 = this.m13;
var d1 = this.m14;
var a2 = this.m21;
var b2 = this.m22;
var c2 = this.m23;
var d2 = this.m24;
var a3 = this.m31;
var b3 = this.m32;
var c3 = this.m33;
var d3 = this.m34;
var a4 = this.m41;
var b4 = this.m42;
var c4 = this.m43;
var d4 = this.m44;
return a1 * this._determinant3x3(b2, b3, b4, c2, c3, c4, d2, d3, d4) -
b1 * this._determinant3x3(a2, a3, a4, c2, c3, c4, d2, d3, d4) +
c1 * this._determinant3x3(a2, a3, a4, b2, b3, b4, d2, d3, d4) -
d1 * this._determinant3x3(a2, a3, a4, b2, b3, b4, c2, c3, c4);
};
CanvasMatrix4.prototype._makeAdjoint = function()
{
var a1 = this.m11;
var b1 = this.m12;
var c1 = this.m13;
var d1 = this.m14;
var a2 = this.m21;
var b2 = this.m22;
var c2 = this.m23;
var d2 = this.m24;
var a3 = this.m31;
var b3 = this.m32;
var c3 = this.m33;
var d3 = this.m34;
var a4 = this.m41;
var b4 = this.m42;
var c4 = this.m43;
var d4 = this.m44;
// Row column labeling reversed since we transpose rows & columns
this.m11  =   this._determinant3x3(b2, b3, b4, c2, c3, c4, d2, d3, d4);
this.m21  = - this._determinant3x3(a2, a3, a4, c2, c3, c4, d2, d3, d4);
this.m31  =   this._determinant3x3(a2, a3, a4, b2, b3, b4, d2, d3, d4);
this.m41  = - this._determinant3x3(a2, a3, a4, b2, b3, b4, c2, c3, c4);
this.m12  = - this._determinant3x3(b1, b3, b4, c1, c3, c4, d1, d3, d4);
this.m22  =   this._determinant3x3(a1, a3, a4, c1, c3, c4, d1, d3, d4);
this.m32  = - this._determinant3x3(a1, a3, a4, b1, b3, b4, d1, d3, d4);
this.m42  =   this._determinant3x3(a1, a3, a4, b1, b3, b4, c1, c3, c4);
this.m13  =   this._determinant3x3(b1, b2, b4, c1, c2, c4, d1, d2, d4);
this.m23  = - this._determinant3x3(a1, a2, a4, c1, c2, c4, d1, d2, d4);
this.m33  =   this._determinant3x3(a1, a2, a4, b1, b2, b4, d1, d2, d4);
this.m43  = - this._determinant3x3(a1, a2, a4, b1, b2, b4, c1, c2, c4);
this.m14  = - this._determinant3x3(b1, b2, b3, c1, c2, c3, d1, d2, d3);
this.m24  =   this._determinant3x3(a1, a2, a3, c1, c2, c3, d1, d2, d3);
this.m34  = - this._determinant3x3(a1, a2, a3, b1, b2, b3, d1, d2, d3);
this.m44  =   this._determinant3x3(a1, a2, a3, b1, b2, b3, c1, c2, c3);
};</script>
<script>
rglwidgetClass = function() {
this.canvas = null;
this.userMatrix = new CanvasMatrix4();
this.types = [];
this.prMatrix = new CanvasMatrix4();
this.mvMatrix = new CanvasMatrix4();
this.vp = null;
this.prmvMatrix = null;
this.origs = null;
this.gl = null;
this.scene = null;
};
(function() {
this.multMV = function(M, v) {
return [ M.m11 * v[0] + M.m12 * v[1] + M.m13 * v[2] + M.m14 * v[3],
M.m21 * v[0] + M.m22 * v[1] + M.m23 * v[2] + M.m24 * v[3],
M.m31 * v[0] + M.m32 * v[1] + M.m33 * v[2] + M.m34 * v[3],
M.m41 * v[0] + M.m42 * v[1] + M.m43 * v[2] + M.m44 * v[3]
];
};
this.vlen = function(v) {
return Math.sqrt(this.dotprod(v, v));
};
this.dotprod = function(a, b) {
return a[0]*b[0] + a[1]*b[1] + a[2]*b[2];
};
this.xprod = function(a, b) {
return [a[1]*b[2] - a[2]*b[1],
a[2]*b[0] - a[0]*b[2],
a[0]*b[1] - a[1]*b[0]];
};
this.cbind = function(a, b) {
return a.map(function(currentValue, index, array) {
return currentValue.concat(b[index]);
});
};
this.swap = function(a, i, j) {
var temp = a[i];
a[i] = a[j];
a[j] = temp;
};
this.flatten = function(a) {
return [].concat.apply([], a);
};
/* set element of 1d or 2d array as if it was flattened.  Column major, zero based! */
this.setElement = function(a, i, value) {
if (Array.isArray(a[0])) {
var dim = a.length,
col = Math.floor(i/dim),
row = i % dim;
a[row][col] = value;
} else {
a[i] = value;
}
};
this.transpose = function(a) {
var newArray = [],
n = a.length,
m = a[0].length,
i;
for(i = 0; i < m; i++){
newArray.push([]);
}
for(i = 0; i < n; i++){
for(var j = 0; j < m; j++){
newArray[j].push(a[i][j]);
}
}
return newArray;
};
this.sumsq = function(x) {
var result = 0, i;
for (i=0; i < x.length; i++)
result += x[i]*x[i];
return result;
};
this.toCanvasMatrix4 = function(mat) {
if (mat instanceof CanvasMatrix4)
return mat;
var result = new CanvasMatrix4();
mat = this.flatten(this.transpose(mat));
result.load(mat);
return result;
};
this.stringToRgb = function(s) {
s = s.replace("#", "");
var bigint = parseInt(s, 16);
return [((bigint >> 16) & 255)/255,
((bigint >> 8) & 255)/255,
(bigint & 255)/255];
};
this.componentProduct = function(x, y) {
if (typeof y === "undefined") {
this.alertOnce("Bad arg to componentProduct");
}
var result = new Float32Array(3), i;
for (i = 0; i<3; i++)
result[i] = x[i]*y[i];
return result;
};
this.getPowerOfTwo = function(value) {
var pow = 1;
while(pow<value) {
pow *= 2;
}
return pow;
};
this.unique = function(arr) {
arr = [].concat(arr);
return arr.filter(function(value, index, self) {
return self.indexOf(value) === index;
});
};
this.repeatToLen = function(arr, len) {
arr = [].concat(arr);
while (arr.length < len/2)
arr = arr.concat(arr);
return arr.concat(arr.slice(0, len - arr.length));
};
this.alertOnce = function(msg) {
if (typeof this.alerted !== "undefined")
return;
this.alerted = true;
alert(msg);
};
this.f_is_lit = 1;
this.f_is_smooth = 2;
this.f_has_texture = 4;
this.f_is_indexed = 8;
this.f_depth_sort = 16;
this.f_fixed_quads = 32;
this.f_is_transparent = 64;
this.f_is_lines = 128;
this.f_sprites_3d = 256;
this.f_sprite_3d = 512;
this.f_is_subscene = 1024;
this.f_is_clipplanes = 2048;
this.whichList = function(id) {
var obj = this.getObj(id),
flags = obj.flags;
if (obj.type === "light")
return "lights";
if (flags & this.f_is_subscene)
return "subscenes";
if (flags & this.f_is_clipplanes)
return "clipplanes";
if (flags & this.f_is_transparent)
return "transparent";
return "opaque";
};
this.getObj = function(id) {
if (typeof id !== "number") {
this.alertOnce("getObj id is "+typeof id);
}
return this.scene.objects[id];
};
this.getIdsByType = function(type, subscene) {
var
result = [], i, self = this;
if (typeof subscene === "undefined") {
Object.keys(this.scene.objects).forEach(
function(key) {
key = parseInt(key, 10);
if (self.getObj(key).type === type)
result.push(key);
});
} else {
ids = this.getObj(subscene).objects;
for (i=0; i < ids.length; i++) {
if (this.getObj(ids[i]).type === type) {
result.push(ids[i]);
}
}
}
return result;
};
this.getMaterial = function(id, property) {
var obj = this.getObj(id),
mat = obj.material[property];
if (typeof mat === "undefined")
mat = this.scene.material[property];
return mat;
};
this.inSubscene = function(id, subscene) {
return this.getObj(subscene).objects.indexOf(id) > -1;
};
this.addToSubscene = function(id, subscene) {
var thelist,
thesub = this.getObj(subscene),
ids = [id],
obj = this.getObj(id), i;
if (typeof obj.newIds !== "undefined") {
ids = ids.concat(obj.newIds);
}
for (i = 0; i < ids.length; i++) {
id = ids[i];
if (thesub.objects.indexOf(id) == -1) {
thelist = this.whichList(id);
thesub.objects.push(id);
thesub[thelist].push(id);
}
}
};
this.delFromSubscene = function(id, subscene) {
var thelist,
thesub = this.getObj(subscene),
obj = this.getObj(id),
ids = [id], i;
if (typeof obj.newIds !== "undefined")
ids = ids.concat(obj.newIds);
for (j=0; j<ids.length;j++) {
id = ids[j];
i = thesub.objects.indexOf(id);
if (i > -1) {
thesub.objects.splice(i, 1);
thelist = this.whichList(id);
i = thesub[thelist].indexOf(id);
thesub[thelist].splice(i, 1);
}
}
};
this.setSubsceneEntries = function(ids, subsceneid) {
var sub = this.getObj(subsceneid);
sub.objects = ids;
this.initSubscene(subsceneid);
};
this.getSubsceneEntries = function(subscene) {
return this.getObj(subscene).objects;
};
this.getChildSubscenes = function(subscene) {
return this.getObj(subscene).subscenes;
};
this.startDrawing = function() {
var value = this.drawing;
this.drawing = true;
return value;
}
this.stopDrawing = function(saved) {
this.drawing = saved;
if (!saved && this.gl && this.gl.isContextLost())
this.restartCanvas();
}
this.getVertexShader = function(id) {
var obj = this.getObj(id),
flags = obj.flags,
type = obj.type,
is_lit = flags & this.f_is_lit,
has_texture = flags & this.f_has_texture,
fixed_quads = flags & this.f_fixed_quads,
sprites_3d = flags & this.f_sprites_3d,
sprite_3d = flags & this.f_sprite_3d,
nclipplanes = this.countClipplanes(),
result;
if (type === "clipplanes" || sprites_3d) return;
result = "  /* ****** "+type+" object "+id+" vertex shader ****** */\n"+
"  attribute vec3 aPos;\n"+
"  attribute vec4 aCol;\n"+
" uniform mat4 mvMatrix;\n"+
" uniform mat4 prMatrix;\n"+
" varying vec4 vCol;\n"+
" varying vec4 vPosition;\n";
if ((is_lit && !fixed_quads) || sprite_3d)
result = result + "  attribute vec3 aNorm;\n"+
" uniform mat4 normMatrix;\n"+
" varying vec3 vNormal;\n";
if (has_texture || type === "text")
result = result + " attribute vec2 aTexcoord;\n"+
" varying vec2 vTexcoord;\n";
if (type === "text")
result = result + "  uniform vec2 textScale;\n";
if (fixed_quads)
result = result + "  attribute vec2 aOfs;\n";
else if (sprite_3d)
result = result + "  uniform vec3 uOrig;\n"+
" uniform float uSize;\n"+
" uniform mat4 usermat;\n";
result = result + "  void main(void) {\n";
if (nclipplanes || (!fixed_quads && !sprite_3d))
result = result + "    vPosition = mvMatrix * vec4(aPos, 1.);\n";
if (!fixed_quads && !sprite_3d)
result = result + "    gl_Position = prMatrix * vPosition;\n";
if (type == "points") {
var size = this.getMaterial(id, "size");
result = result + "    gl_PointSize = "+size.toFixed(1)+";\n";
}
result = result + "    vCol = aCol;\n";
if (is_lit && !fixed_quads && !sprite_3d)
result = result + "    vNormal = normalize((normMatrix * vec4(aNorm, 1.)).xyz);\n";
if (has_texture || type === "text")
result = result + "    vTexcoord = aTexcoord;\n";
if (type == "text")
result = result + "    vec4 pos = prMatrix * mvMatrix * vec4(aPos, 1.);\n"+
"   pos = pos/pos.w;\n"+
"   gl_Position = pos + vec4(aOfs*textScale, 0.,0.);\n";
if (type == "sprites")
result = result + "    vec4 pos = mvMatrix * vec4(aPos, 1.);\n"+
"   pos = pos/pos.w + vec4(aOfs, 0., 0.);\n"+
"   gl_Position = prMatrix*pos;\n";
if (sprite_3d)
result = result + "    vNormal = normalize((normMatrix * vec4(aNorm, 1.)).xyz);\n"+
"   vec4 pos = mvMatrix * vec4(uOrig, 1.);\n"+
"   vPosition = pos/pos.w + vec4(uSize*(vec4(aPos, 1.)*usermat).xyz,0.);\n"+
"   gl_Position = prMatrix * vPosition;\n";
result = result + "  }\n";
return result;
};
this.getFragmentShader = function(id) {
var obj = this.getObj(id),
flags = obj.flags,
type = obj.type,
is_lit = flags & this.f_is_lit,
has_texture = flags & this.f_has_texture,
fixed_quads = flags & this.f_fixed_quads,
sprites_3d = flags & this.f_sprites_3d,
nclipplanes = this.countClipplanes(), i,
texture_format, nlights,
result;
if (type === "clipplanes" || sprites_3d) return;
if (has_texture)
texture_format = this.getMaterial(id, "textype");
result = "/* ****** "+type+" object "+id+" fragment shader ****** */\n"+
"#ifdef GL_ES\n"+
"  precision highp float;\n"+
"#endif\n"+
"  varying vec4 vCol; // carries alpha\n"+
"  varying vec4 vPosition;\n";
if (has_texture || type === "text")
result = result + "  varying vec2 vTexcoord;\n"+
" uniform sampler2D uSampler;\n";
if (is_lit && !fixed_quads)
result = result + "  varying vec3 vNormal;\n";
for (i = 0; i < nclipplanes; i++)
result = result + "  uniform vec4 vClipplane"+i+";\n";
if (is_lit) {
nlights = this.countLights();
if (nlights)
result = result + "  uniform mat4 mvMatrix;\n";
else
is_lit = false;
}
if (is_lit) {
result = result + "    uniform vec3 emission;\n"+
"   uniform float shininess;\n";
for (i=0; i < nlights; i++) {
result = result + "    uniform vec3 ambient" + i + ";\n"+
"   uniform vec3 specular" + i +"; // light*material\n"+
"   uniform vec3 diffuse" + i + ";\n"+
"   uniform vec3 lightDir" + i + ";\n"+
"   uniform bool viewpoint" + i + ";\n"+
"   uniform bool finite" + i + ";\n";
}
}
result = result + "  void main(void) {\n";
for (i=0; i < nclipplanes;i++)
result = result + "    if (dot(vPosition, vClipplane"+i+") < 0.0) discard;\n";
if (is_lit) {
result = result + "    vec3 eye = normalize(-vPosition.xyz);\n"+
"   vec3 lightdir;\n"+
"   vec4 colDiff;\n"+
"   vec3 halfVec;\n"+
"   vec4 lighteffect = vec4(emission, 0.);\n"+
"   vec3 col;\n"+
"   float nDotL;\n";
if (fixed_quads) {
result = result +   "    vec3 n = vec3(0., 0., 1.);\n";
}
else {
result = result +   "    vec3 n = normalize(vNormal);\n"+
"   n = -faceforward(n, n, eye);\n";
}
for (i=0; i < nlights; i++) {
result = result + "   colDiff = vec4(vCol.rgb * diffuse" + i + ", vCol.a);\n"+
"   lightdir = lightDir" + i + ";\n"+
"   if (!viewpoint" + i +")\n"+
"     lightdir = (mvMatrix * vec4(lightdir, 1.)).xyz;\n"+
"   if (!finite" + i + ") {\n"+
"     halfVec = normalize(lightdir + eye);\n"+
"   } else {\n"+
"     lightdir = normalize(lightdir - vPosition.xyz);\n"+
"     halfVec = normalize(lightdir + eye);\n"+
"   }\n"+
"    col = ambient" + i + ";\n"+
"   nDotL = dot(n, lightdir);\n"+
"   col = col + max(nDotL, 0.) * colDiff.rgb;\n"+
"   col = col + pow(max(dot(halfVec, n), 0.), shininess) * specular" + i + ";\n"+
"   lighteffect = lighteffect + vec4(col, colDiff.a);\n";
}
} else {
result = result +   "   vec4 colDiff = vCol;\n"+
"    vec4 lighteffect = colDiff;\n";
}
if ((has_texture && texture_format === "rgba") || type === "text")
result = result +   "    vec4 textureColor = lighteffect*texture2D(uSampler, vTexcoord);\n";
if (has_texture) {
result = result + {
rgb:            "   vec4 textureColor = lighteffect*vec4(texture2D(uSampler, vTexcoord).rgb, 1.);\n",
alpha:          "   vec4 textureColor = texture2D(uSampler, vTexcoord);\n"+
"   float luminance = dot(vec3(1.,1.,1.), textureColor.rgb)/3.;\n"+
"   textureColor =  vec4(lighteffect.rgb, lighteffect.a*luminance);\n",
luminance:      "   vec4 textureColor = vec4(lighteffect.rgb*dot(texture2D(uSampler, vTexcoord).rgb, vec3(1.,1.,1.))/3., lighteffect.a);\n",
"luminance.alpha":"    vec4 textureColor = texture2D(uSampler, vTexcoord);\n"+
"   float luminance = dot(vec3(1.,1.,1.),textureColor.rgb)/3.;\n"+
"   textureColor = vec4(lighteffect.rgb*luminance, lighteffect.a*textureColor.a);\n"
}[texture_format]+
"   gl_FragColor = textureColor;\n";
} else if (type === "text") {
result = result +   "    if (textureColor.a < 0.1)\n"+
"     discard;\n"+
"   else\n"+
"     gl_FragColor = textureColor;\n";
} else
result = result +   "   gl_FragColor = lighteffect;\n";
result = result + "  }\n";
return result;
};
this.getShader = function(shaderType, code) {
var gl = this.gl, shader;
shader = gl.createShader(shaderType);
gl.shaderSource(shader, code);
gl.compileShader(shader);
if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS) && !gl.isContextLost())
alert(gl.getShaderInfoLog(shader));
return shader;
};
this.handleLoadedTexture = function(texture, textureCanvas) { 
var gl = this.gl || this.initGL();
gl.pixelStorei(gl.UNPACK_FLIP_Y_WEBGL, true);
gl.bindTexture(gl.TEXTURE_2D, texture);
gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, textureCanvas);
gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.LINEAR);
gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR_MIPMAP_NEAREST);
gl.generateMipmap(gl.TEXTURE_2D);
gl.bindTexture(gl.TEXTURE_2D, null);
};
this.loadImageToTexture = function(uri, texture) {
var canvas = this.textureCanvas,
ctx = canvas.getContext("2d"),
image = new Image(),
self = this;
image.onload = function() {
var w = image.width,
h = image.height,
canvasX = self.getPowerOfTwo(w),
canvasY = self.getPowerOfTwo(h),
gl = self.gl || self.initGL(),
maxTexSize = gl.getParameter(gl.MAX_TEXTURE_SIZE);
if (maxTexSize > 4096) maxTexSize = 4096;
while (canvasX > 1 && canvasY > 1 && (canvasX > maxTexSize || canvasY > maxTexSize)) {
canvasX /= 2;
canvasY /= 2;
}
canvas.width = canvasX;
canvas.height = canvasY;
ctx.imageSmoothingEnabled = true;
ctx.drawImage(image, 0, 0, canvasX, canvasY);
self.handleLoadedTexture(texture, canvas);
self.drawScene();
};
image.src = uri;
};
this.drawTextToCanvas = function(text, cex, family, font) {
var canvasX, canvasY,
textY,
scaling = 20,
textColour = "white",
backgroundColour = "rgba(0,0,0,0)",
canvas = this.textureCanvas,
ctx = canvas.getContext("2d"),
i, textHeights = [], widths = [], offset = 0, offsets = [],
fontStrings = [],
getFontString = function(i) {
textHeights[i] = scaling*cex[i];
var fontString = textHeights[i] + "px",
family0 = family[i],
font0 = font[i];
if (family0 === "sans")
family0 = "sans-serif";
else if (family0 === "mono")
family0 = "monospace";
fontString = fontString + " " + family0;
if (font0 === 2 || font0 === 4)
fontString = "bold " + fontString;
if (font0 === 3 || font0 === 4)
fontString = "italic " + fontString;
return fontString;
};
cex = this.repeatToLen(cex, text.length);
family = this.repeatToLen(family, text.length);
font = this.repeatToLen(font, text.length);
canvasX = 1;
for (i = 0; i < text.length; i++)  {
ctx.font = fontStrings[i] = getFontString(i);
widths[i] = ctx.measureText(text[i]).width;
offset = offsets[i] = offset + 2*textHeights[i];
canvasX = (widths[i] > canvasX) ? widths[i] : canvasX;
}
canvasX = this.getPowerOfTwo(canvasX);
canvasY = this.getPowerOfTwo(offset);
canvas.width = canvasX;
canvas.height = canvasY;
ctx.fillStyle = backgroundColour;
ctx.fillRect(0, 0, ctx.canvas.width, ctx.canvas.height);
ctx.textBaseline = "alphabetic";
for(i = 0; i < text.length; i++) {
textY = offsets[i];
ctx.font = fontStrings[i];
ctx.fillStyle = textColour;
ctx.textAlign = "left";
ctx.fillText(text[i], 0,  textY);
}
return {canvasX:canvasX, canvasY:canvasY,
widths:widths, textHeights:textHeights,
offsets:offsets};
};
this.setViewport = function(id) {
var gl = this.gl || this.initGL(),
vp = this.getObj(id).par3d.viewport,
x = vp.x*this.canvas.width,
y = vp.y*this.canvas.height,
width = vp.width*this.canvas.width,
height = vp.height*this.canvas.height;
this.vp = {x:x, y:y, width:width, height:height};
gl.viewport(x, y, width, height);
gl.scissor(x, y, width, height);
gl.enable(gl.SCISSOR_TEST);
};
this.setprMatrix = function(id) {
var subscene = this.getObj(id),
embedding = subscene.embeddings.projection;
if (embedding === "replace")
this.prMatrix.makeIdentity();
else
this.setprMatrix(subscene.parent);
if (embedding === "inherit")
return;
// This is based on the Frustum::enclose code from geom.cpp
var bbox = subscene.par3d.bbox,
scale = subscene.par3d.scale,
ranges = [(bbox[1]-bbox[0])*scale[0]/2,
(bbox[3]-bbox[2])*scale[1]/2,
(bbox[5]-bbox[4])*scale[2]/2],
radius = Math.sqrt(this.sumsq(ranges))*1.1; // A bit bigger to handle labels
if (radius <= 0) radius = 1;
var observer = subscene.par3d.observer,
distance = observer[2],
FOV = subscene.par3d.FOV, ortho = FOV === 0,
t = ortho ? 1 : Math.tan(FOV*Math.PI/360),
near = distance - radius,
far = distance + radius,
hlen = t*near,
aspect = this.vp.width/this.vp.height,
z = subscene.par3d.zoom;
if (ortho) {
if (aspect > 1)
this.prMatrix.ortho(-hlen*aspect*z, hlen*aspect*z,
-hlen*z, hlen*z, near, far);
else
this.prMatrix.ortho(-hlen*z, hlen*z,
-hlen*z/aspect, hlen*z/aspect,
near, far);
} else {
if (aspect > 1)
this.prMatrix.frustum(-hlen*aspect*z, hlen*aspect*z,
-hlen*z, hlen*z, near, far);
else
this.prMatrix.frustum(-hlen*z, hlen*z,
-hlen*z/aspect, hlen*z/aspect,
near, far);
}
};
this.setmvMatrix = function(id) {
var observer = this.getObj(id).par3d.observer;
this.mvMatrix.makeIdentity();
this.setmodelMatrix(id);
this.mvMatrix.translate(-observer[0], -observer[1], -observer[2]);
};
this.setmodelMatrix = function(id) {
var subscene = this.getObj(id),
embedding = subscene.embeddings.model;
if (embedding !== "inherit") {
var scale = subscene.par3d.scale,
bbox = subscene.par3d.bbox,
center = [(bbox[0]+bbox[1])/2,
(bbox[2]+bbox[3])/2,
(bbox[4]+bbox[5])/2];
this.mvMatrix.translate(-center[0], -center[1], -center[2]);
this.mvMatrix.scale(scale[0], scale[1], scale[2]);
this.mvMatrix.multRight( subscene.par3d.userMatrix );
}
if (embedding !== "replace")
this.setmodelMatrix(subscene.parent);
};
this.setnormMatrix = function(subsceneid) {
var self = this,
recurse = function(id) {
var sub = self.getObj(id),
embedding = sub.embeddings.model;
if (embedding !== "inherit") {
var scale = sub.par3d.scale;
self.normMatrix.scale(1/scale[0], 1/scale[1], 1/scale[2]);
self.normMatrix.multRight(sub.par3d.userMatrix);
}
if (embedding !== "replace")
recurse(sub.parent);
};
self.normMatrix.makeIdentity();
recurse(subsceneid);
};
this.setprmvMatrix = function() {
this.prmvMatrix = new CanvasMatrix4( this.mvMatrix );
this.prmvMatrix.multRight( this.prMatrix );
};
this.countClipplanes = function() {
return this.countObjs("clipplanes");
};
this.countLights = function() {
return this.countObjs("light");
};
this.countObjs = function(type) {
var self = this,
bound = 0;
Object.keys(this.scene.objects).forEach(
function(key) {
if (self.getObj(parseInt(key, 10)).type === type)
bound = bound + 1;
});
return bound;
};
this.initSubscene = function(id) {
var sub = this.getObj(id),
i, obj;
if (sub.type !== "subscene")
return;
sub.par3d.userMatrix = this.toCanvasMatrix4(sub.par3d.userMatrix);
sub.par3d.listeners = [].concat(sub.par3d.listeners);
sub.backgroundId = undefined;
sub.subscenes = [];
sub.clipplanes = [];
sub.transparent = [];
sub.opaque = [];
sub.lights = [];
for (i=0; i < sub.objects.length; i++) {
obj = this.getObj(sub.objects[i]);
if (typeof obj === "undefined") {
sub.objects.splice(i, 1);
i--;
} else if (obj.type === "background")
sub.backgroundId = obj.id;
else
sub[this.whichList(obj.id)].push(obj.id);
}
};
this.copyObj = function(id, reuse) {
var obj = this.getObj(id),
prev = document.getElementById(reuse);
if (prev !== null) {
prev = prev.rglinstance;
var
prevobj = prev.getObj(id),
fields = ["flags", "type",
"colors", "vertices", "centers",
"normals", "offsets",
"texts", "cex", "family", "font", "adj",
"material",
"radii",
"texcoords",
"userMatrix", "ids",
"dim",
"par3d", "userMatrix",
"viewpoint", "finite"],
i;
for (i = 0; i < fields.length; i++) {
if (typeof prevobj[fields[i]] !== "undefined")
obj[fields[i]] = prevobj[fields[i]];
}
} else
console.warn("copyObj failed");
};
this.planeUpdateTriangles = function(id, bbox) {
var perms = [[0,0,1], [1,2,2], [2,1,0]],
x, xrow, elem, A, d, nhits, i, j, k, u, v, w, intersect, which, v0, v2, vx, reverse,
face1 = [], face2 = [], normals = [],
obj = this.getObj(id),
nPlanes = obj.normals.length;
obj.bbox = bbox;
obj.vertices = [];
obj.initialized = false;
for (elem = 0; elem < nPlanes; elem++) {
//    Vertex Av = normal.getRecycled(elem);
x = [];
A = obj.normals[elem];
d = obj.offsets[elem][0];
nhits = 0;
for (i=0; i<3; i++)
for (j=0; j<2; j++)
for (k=0; k<2; k++) {
u = perms[0][i];
v = perms[1][i];
w = perms[2][i];
if (A[w] !== 0.0) {
intersect = -(d + A[u]*bbox[j+2*u] + A[v]*bbox[k+2*v])/A[w];
if (bbox[2*w] < intersect && intersect < bbox[1+2*w]) {
xrow = [];
xrow[u] = bbox[j+2*u];
xrow[v] = bbox[k+2*v];
xrow[w] = intersect;
x.push(xrow);
face1[nhits] = j + 2*u;
face2[nhits] = k + 2*v;
nhits++;
}
}
}
if (nhits > 3) {
/* Re-order the intersections so the triangles work */
for (i=0; i<nhits-2; i++) {
which = 0; /* initialize to suppress warning */
for (j=i+1; j<nhits; j++) {
if (face1[i] == face1[j] || face1[i] == face2[j] ||
face2[i] == face1[j] || face2[i] == face2[j] ) {
which = j;
break;
}
}
if (which > i+1) {
this.swap(x, i+1, which);
this.swap(face1, i+1, which);
this.swap(face2, i+1, which);
}
}
}
if (nhits >= 3) {
/* Put in order so that the normal points out the FRONT of the faces */
v0 = [x[0][0] - x[1][0] , x[0][1] - x[1][1], x[0][2] - x[1][2]];
v2 = [x[2][0] - x[1][0] , x[2][1] - x[1][1], x[2][2] - x[1][2]];
/* cross-product */
vx = this.xprod(v0, v2);
reverse = this.dotprod(vx, A) > 0;
for (i=0; i<nhits-2; i++) {
obj.vertices.push(x[0]);
normals.push(A);
for (j=1; j<3; j++) {
obj.vertices.push(x[i + (reverse ? 3-j : j)]);
normals.push(A);
}
}
}
}
obj.pnormals = normals;
};
this.initObj = function(id) {
var obj = this.getObj(id),
flags = obj.flags,
type = obj.type,
is_indexed = flags & this.f_is_indexed,
is_lit = flags & this.f_is_lit,
has_texture = flags & this.f_has_texture,
fixed_quads = flags & this.f_fixed_quads,
depth_sort = flags & this.f_depth_sort,
sprites_3d = flags & this.f_sprites_3d,
sprite_3d = flags & this.f_sprite_3d,
gl = this.gl || this.initGL(),
texinfo, drawtype, nclipplanes, f, frowsize, nrows,
i,j,v, mat, uri, matobj;
if (typeof id !== "number") {
this.alertOnce("initObj id is "+typeof id);
}
obj.initialized = true;
if (type === "bboxdeco" || type === "subscene")
return;
if (type === "light") {
obj.ambient = new Float32Array(obj.colors[0].slice(0,3));
obj.diffuse = new Float32Array(obj.colors[1].slice(0,3));
obj.specular = new Float32Array(obj.colors[2].slice(0,3));
obj.lightDir = new Float32Array(obj.vertices[0]);
return;
}
if (type === "clipplanes") {
obj.vClipplane = this.flatten(this.cbind(obj.normals, obj.offsets));
return;
}
if (type == "background" && typeof obj.ids !== "undefined") {
obj.quad = this.flatten([].concat(obj.ids));
return;
}
if (typeof obj.vertices === "undefined")
obj.vertices = [];
v = obj.vertices;
obj.vertexCount = v.length;
if (!obj.vertexCount) return;
if (!sprites_3d) {
if (gl.isContextLost()) return;
obj.prog = gl.createProgram();
gl.attachShader(obj.prog, this.getShader( gl.VERTEX_SHADER,
this.getVertexShader(id) ));
gl.attachShader(obj.prog, this.getShader( gl.FRAGMENT_SHADER,
this.getFragmentShader(id) ));
//  Force aPos to location 0, aCol to location 1
gl.bindAttribLocation(obj.prog, 0, "aPos");
gl.bindAttribLocation(obj.prog, 1, "aCol");
gl.linkProgram(obj.prog);
var linked = gl.getProgramParameter(obj.prog, gl.LINK_STATUS);
if (!linked) {
// An error occurred while linking
var lastError = gl.getProgramInfoLog(obj.prog);
console.warn("Error in program linking:" + lastError);
gl.deleteProgram(obj.prog);
return;
}
}
if (type === "text") {
texinfo = this.drawTextToCanvas(obj.texts,
this.flatten(obj.cex),
this.flatten(obj.family),
this.flatten(obj.family));
}
if (fixed_quads && !sprites_3d) {
obj.ofsLoc = gl.getAttribLocation(obj.prog, "aOfs");
}
if (sprite_3d) {
obj.origLoc = gl.getUniformLocation(obj.prog, "uOrig");
obj.sizeLoc = gl.getUniformLocation(obj.prog, "uSize");
obj.usermatLoc = gl.getUniformLocation(obj.prog, "usermat");
}
if (has_texture || type == "text") {
obj.texture = gl.createTexture();
obj.texLoc = gl.getAttribLocation(obj.prog, "aTexcoord");
obj.sampler = gl.getUniformLocation(obj.prog, "uSampler");
}
if (has_texture) {
mat = obj.material;
if (typeof mat.uri !== "undefined")
uri = mat.uri;
else if (typeof mat.uriElementId === "undefined") {
matobj = this.getObj(mat.uriId);
if (typeof matobj !== "undefined") {
uri = matobj.material.uri;
} else {
uri = "";
}
} else
uri = document.getElementById(mat.uriElementId).rglinstance.getObj(mat.uriId).material.uri;
this.loadImageToTexture(uri, obj.texture);
}
if (type === "text") {
this.handleLoadedTexture(obj.texture, this.textureCanvas);
}
var stride = 3, nc, cofs, nofs, radofs, oofs, tofs, vnew, v1;
nc = obj.colorCount = obj.colors.length;
if (nc > 1) {
cofs = stride;
stride = stride + 4;
v = this.cbind(v, obj.colors);
} else {
cofs = -1;
obj.onecolor = this.flatten(obj.colors);
}
if (typeof obj.normals !== "undefined") {
nofs = stride;
stride = stride + 3;
v = this.cbind(v, typeof obj.pnormals !== "undefined" ? obj.pnormals : obj.normals);
} else
nofs = -1;
if (typeof obj.radii !== "undefined") {
radofs = stride;
stride = stride + 1;
if (obj.radii.length === v.length) {
v = this.cbind(v, obj.radii);
} else if (obj.radii.length === 1) {
v = v.map(function(row, i, arr) { return row.concat(obj.radii[0]);});
}
} else
radofs = -1;
if (type == "sprites" && !sprites_3d) {
tofs = stride;
stride += 2;
oofs = stride;
stride += 2;
vnew = new Array(4*v.length);
var size = obj.radii, s = size[0]/2;
for (i=0; i < v.length; i++) {
if (size.length > 1)
s = size[i]/2;
vnew[4*i]  = v[i].concat([0,0,-s,-s]);
vnew[4*i+1]= v[i].concat([1,0, s,-s]);
vnew[4*i+2]= v[i].concat([1,1, s, s]);
vnew[4*i+3]= v[i].concat([0,1,-s, s]);
}
v = vnew;
obj.vertexCount = v.length;
} else if (type === "text") {
tofs = stride;
stride += 2;
oofs = stride;
stride += 2;
vnew = new Array(4*v.length);
for (i=0; i < v.length; i++) {
vnew[4*i]  = v[i].concat([0,-0.5]).concat(obj.adj[0]);
vnew[4*i+1]= v[i].concat([1,-0.5]).concat(obj.adj[0]);
vnew[4*i+2]= v[i].concat([1, 1.5]).concat(obj.adj[0]);
vnew[4*i+3]= v[i].concat([0, 1.5]).concat(obj.adj[0]);
for (j=0; j < 4; j++) {
v1 = vnew[4*i+j];
v1[tofs+2] = 2*(v1[tofs]-v1[tofs+2])*texinfo.widths[i];
v1[tofs+3] = 2*(v1[tofs+1]-v1[tofs+3])*texinfo.textHeights[i];
v1[tofs] *= texinfo.widths[i]/texinfo.canvasX;
v1[tofs+1] = 1.0-(texinfo.offsets[i] -
v1[tofs+1]*texinfo.textHeights[i])/texinfo.canvasY;
vnew[4*i+j] = v1;
}
}
v = vnew;
obj.vertexCount = v.length;
} else if (typeof obj.texcoords !== "undefined") {
tofs = stride;
stride += 2;
oofs = -1;
v = this.cbind(v, obj.texcoords);
} else {
tofs = -1;
oofs = -1;
}
if (stride !== v[0].length) {
this.alertOnce("problem in stride calculation");
}
obj.vOffsets = {vofs:0, cofs:cofs, nofs:nofs, radofs:radofs, oofs:oofs, tofs:tofs, stride:stride};
obj.values = new Float32Array(this.flatten(v));
if (sprites_3d) {
obj.userMatrix = new CanvasMatrix4(obj.userMatrix);
obj.objects = this.flatten([].concat(obj.ids));
is_lit = false;
}
if (is_lit && !fixed_quads) {
obj.normLoc = gl.getAttribLocation(obj.prog, "aNorm");
}
nclipplanes = this.countClipplanes();
if (nclipplanes && !sprites_3d) {
obj.clipLoc = [];
for (i=0; i < nclipplanes; i++)
obj.clipLoc[i] = gl.getUniformLocation(obj.prog,"vClipplane" + i);
}
if (is_lit) {
obj.emissionLoc = gl.getUniformLocation(obj.prog, "emission");
obj.emission = new Float32Array(this.stringToRgb(this.getMaterial(id, "emission")));
obj.shininessLoc = gl.getUniformLocation(obj.prog, "shininess");
obj.shininess = this.getMaterial(id, "shininess");
obj.nlights = this.countLights();
obj.ambientLoc = [];
obj.ambient = new Float32Array(this.stringToRgb(this.getMaterial(id, "ambient")));
obj.specularLoc = [];
obj.specular = new Float32Array(this.stringToRgb(this.getMaterial(id, "specular")));
obj.diffuseLoc = [];
obj.lightDirLoc = [];
obj.viewpointLoc = [];
obj.finiteLoc = [];
for (i=0; i < obj.nlights; i++) {
obj.ambientLoc[i] = gl.getUniformLocation(obj.prog, "ambient" + i);
obj.specularLoc[i] = gl.getUniformLocation(obj.prog, "specular" + i);
obj.diffuseLoc[i] = gl.getUniformLocation(obj.prog, "diffuse" + i);
obj.lightDirLoc[i] = gl.getUniformLocation(obj.prog, "lightDir" + i);
obj.viewpointLoc[i] = gl.getUniformLocation(obj.prog, "viewpoint" + i);
obj.finiteLoc[i] = gl.getUniformLocation(obj.prog, "finite" + i);
}
}
if (is_indexed) {
if ((type === "quads" || type === "text" ||
type === "sprites") && !sprites_3d) {
nrows = Math.floor(obj.vertexCount/4);
f = Array(6*nrows);
for (i=0; i < nrows; i++) {
f[6*i] = 4*i;
f[6*i+1] = 4*i + 1;
f[6*i+2] = 4*i + 2;
f[6*i+3] = 4*i;
f[6*i+4] = 4*i + 2;
f[6*i+5] = 4*i + 3;
}
frowsize = 6;
} else if (type === "triangles") {
nrows = Math.floor(obj.vertexCount/3);
f = Array(3*nrows);
for (i=0; i < f.length; i++) {
f[i] = i;
}
frowsize = 3;
} else if (type === "spheres") {
nrows = obj.vertexCount;
f = Array(nrows);
for (i=0; i < f.length; i++) {
f[i] = i;
}
frowsize = 1;
} else if (type === "surface") {
var dim = obj.dim[0],
nx = dim[0],
nz = dim[1];
f = [];
for (j=0; j<nx-1; j++) {
for (i=0; i<nz-1; i++) {
f.push(j + nx*i,
j + nx*(i+1),
j + 1 + nx*(i+1),
j + nx*i,
j + 1 + nx*(i+1),
j + 1 + nx*i);
}
}
frowsize = 6;
}
obj.f = new Uint16Array(f);
if (depth_sort) {
drawtype = "DYNAMIC_DRAW";
} else {
drawtype = "STATIC_DRAW";
}
}
if (type !== "spheres" && !sprites_3d) {
obj.buf = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, obj.buf);
gl.bufferData(gl.ARRAY_BUFFER, obj.values, gl.STATIC_DRAW); //
}
if (is_indexed && type !== "spheres" && !sprites_3d) {
obj.ibuf = gl.createBuffer();
gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, obj.ibuf);
gl.bufferData(gl.ELEMENT_ARRAY_BUFFER, obj.f, gl[drawtype]);
}
if (!sprites_3d) {
obj.mvMatLoc = gl.getUniformLocation(obj.prog, "mvMatrix");
obj.prMatLoc = gl.getUniformLocation(obj.prog, "prMatrix");
}
if (type === "text") {
obj.textScaleLoc = gl.getUniformLocation(obj.prog, "textScale");
}
if (is_lit && !sprites_3d) {
obj.normMatLoc = gl.getUniformLocation(obj.prog, "normMatrix");
}
};
this.setDepthTest = function(id) {
var gl = this.gl || this.initGL(),
tests = {never: gl.NEVER,
less:  gl.LESS,
equal: gl.EQUAL,
lequal:gl.LEQUAL,
greater: gl.GREATER,
notequal: gl.NOTEQUAL,
gequal: gl.GEQUAL,
always: gl.ALWAYS},
test = tests[this.getMaterial(id, "depth_test")];
gl.depthFunc(test);
};
this.mode4type = {points : "POINTS",
linestrip : "LINE_STRIP",
abclines : "LINES",
lines : "LINES",
sprites : "TRIANGLES",
planes : "TRIANGLES",
text : "TRIANGLES",
quads : "TRIANGLES",
surface : "TRIANGLES",
triangles : "TRIANGLES"};
this.drawObj = function(id, subsceneid) {
var obj = this.getObj(id),
subscene = this.getObj(subsceneid),
flags = obj.flags,
type = obj.type,
is_indexed = flags & this.f_is_indexed,
is_lit = flags & this.f_is_lit,
has_texture = flags & this.f_has_texture,
fixed_quads = flags & this.f_fixed_quads,
depth_sort = flags & this.f_depth_sort,
sprites_3d = flags & this.f_sprites_3d,
sprite_3d = flags & this.f_sprite_3d,
is_lines = flags & this.f_is_lines,
gl = this.gl || this.initGL(),
sphereMV, baseofs, ofs, sscale, i, count, light,
faces;
if (typeof id !== "number") {
this.alertOnce("drawObj id is "+typeof id);
}
if (type === "planes") {
if (obj.bbox !== subscene.par3d.bbox || !obj.initialized) {
this.planeUpdateTriangles(id, subscene.par3d.bbox);
}
}
if (!obj.initialized)
this.initObj(id);
if (type === "clipplanes") {
count = obj.offsets.length;
var IMVClip = [];
for (i=0; i < count; i++) {
IMVClip[i] = this.multMV(this.invMatrix, obj.vClipplane.slice(4*i, 4*(i+1)));
}
obj.IMVClip = IMVClip;
return;
}
if (type === "light" || type === "bboxdeco" || !obj.vertexCount)
return;
this.setDepthTest(id);
if (sprites_3d) {
var norigs = obj.vertices.length,
savenorm = new CanvasMatrix4(this.normMatrix);
this.origs = obj.vertices;
this.usermat = new Float32Array(obj.userMatrix.getAsArray());
this.radii = obj.radii;
this.normMatrix = subscene.spriteNormmat;
for (this.iOrig=0; this.iOrig < norigs; this.iOrig++) {
for (i=0; i < obj.objects.length; i++) {
this.drawObj(obj.objects[i], subsceneid);
}
}
this.normMatrix = savenorm;
return;
} else {
gl.useProgram(obj.prog);
}
if (sprite_3d) {
gl.uniform3fv(obj.origLoc, new Float32Array(this.origs[this.iOrig]));
if (this.radii.length > 1) {
gl.uniform1f(obj.sizeLoc, this.radii[this.iOrig][0]);
} else {
gl.uniform1f(obj.sizeLoc, this.radii[0][0]);
}
gl.uniformMatrix4fv(obj.usermatLoc, false, this.usermat);
}
if (type === "spheres") {
gl.bindBuffer(gl.ARRAY_BUFFER, this.sphere.buf);
} else {
gl.bindBuffer(gl.ARRAY_BUFFER, obj.buf);
}
if (is_indexed && type !== "spheres") {
gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, obj.ibuf);
} else if (type === "spheres") {
gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, this.sphere.ibuf);
}
gl.uniformMatrix4fv( obj.prMatLoc, false, new Float32Array(this.prMatrix.getAsArray()) );
gl.uniformMatrix4fv( obj.mvMatLoc, false, new Float32Array(this.mvMatrix.getAsArray()) );
var clipcheck = 0,
clipplaneids = subscene.clipplanes,
clip, j;
for (i=0; i < clipplaneids.length; i++) {
clip = this.getObj(clipplaneids[i]);
for (j=0; j < clip.offsets.length; j++) {
gl.uniform4fv(obj.clipLoc[clipcheck + j], clip.IMVClip[j]);
}
clipcheck += clip.offsets.length;
}
if (typeof obj.clipLoc !== "undefined")
for (i=clipcheck; i < obj.clipLoc.length; i++)
gl.uniform4f(obj.clipLoc[i], 0,0,0,0);
if (is_lit) {
gl.uniformMatrix4fv( obj.normMatLoc, false, new Float32Array(this.normMatrix.getAsArray()) );
gl.uniform3fv( obj.emissionLoc, obj.emission);
gl.uniform1f( obj.shininessLoc, obj.shininess);
for (i=0; i < subscene.lights.length; i++) {
light = this.getObj(subscene.lights[i]);
gl.uniform3fv( obj.ambientLoc[i], this.componentProduct(light.ambient, obj.ambient));
gl.uniform3fv( obj.specularLoc[i], this.componentProduct(light.specular, obj.specular));
gl.uniform3fv( obj.diffuseLoc[i], light.diffuse);
gl.uniform3fv( obj.lightDirLoc[i], light.lightDir);
gl.uniform1i( obj.viewpointLoc[i], light.viewpoint);
gl.uniform1i( obj.finiteLoc[i], light.finite);
}
for (i=subscene.lights.length; i < obj.nlights; i++) {
gl.uniform3f( obj.ambientLoc[i], 0,0,0);
gl.uniform3f( obj.specularLoc[i], 0,0,0);
gl.uniform3f( obj.diffuseLoc[i], 0,0,0);
}
}
if (type === "text") {
gl.uniform2f( obj.textScaleLoc, 0.75/this.vp.width, 0.75/this.vp.height);
}
gl.enableVertexAttribArray( this.posLoc );
var nc = obj.colorCount;
count = obj.vertexCount;
if (depth_sort) {
var nfaces = obj.centers.length,
frowsize, z, w;
if (sprites_3d) frowsize = 1;
else if (type === "triangles") frowsize = 3;
else frowsize = 6;
var depths = new Float32Array(nfaces);
faces = new Array(nfaces);
for(i=0; i<nfaces; i++) {
z = this.prmvMatrix.m13*obj.centers[3*i] +
this.prmvMatrix.m23*obj.centers[3*i+1] +
this.prmvMatrix.m33*obj.centers[3*i+2] +
this.prmvMatrix.m43;
w = this.prmvMatrix.m14*obj.centers[3*i] +
this.prmvMatrix.m24*obj.centers[3*i+1] +
this.prmvMatrix.m34*obj.centers[3*i+2] +
this.prmvMatrix.m44;
depths[i] = z/w;
faces[i] = i;
}
var depthsort = function(i,j) { return depths[j] - depths[i]; };
faces.sort(depthsort);
if (type !== "spheres") {
var f = new Uint16Array(obj.f.length);
for (i=0; i<nfaces; i++) {
for (j=0; j<frowsize; j++) {
f[frowsize*i + j] = obj.f[frowsize*faces[i] + j];
}
}
gl.bufferData(gl.ELEMENT_ARRAY_BUFFER, f, gl.DYNAMIC_DRAW);
}
}
if (type === "spheres") {
subscene = this.getObj(subsceneid);
var scale = subscene.par3d.scale,
scount = count;
gl.vertexAttribPointer(this.posLoc,  3, gl.FLOAT, false, 4*this.sphere.vOffsets.stride,  0);
gl.enableVertexAttribArray(obj.normLoc );
gl.vertexAttribPointer(obj.normLoc,  3, gl.FLOAT, false, 4*this.sphere.vOffsets.stride,  0);
gl.disableVertexAttribArray( this.colLoc );
var sphereNorm = new CanvasMatrix4();
sphereNorm.scale(scale[0], scale[1], scale[2]);
sphereNorm.multRight(this.normMatrix);
gl.uniformMatrix4fv( obj.normMatLoc, false, new Float32Array(sphereNorm.getAsArray()) );
if (nc == 1) {
gl.vertexAttrib4fv( this.colLoc, new Float32Array(obj.onecolor));
}
if (has_texture) {
gl.enableVertexAttribArray( obj.texLoc );
gl.vertexAttribPointer(obj.texLoc, 2, gl.FLOAT, false, 4*this.sphere.vOffsets.stride, 4*this.sphere.vOffsets.tofs);
gl.activeTexture(gl.TEXTURE0);
gl.bindTexture(gl.TEXTURE_2D, obj.texture);
gl.uniform1i( obj.sampler, 0);
}
for (i = 0; i < scount; i++) {
sphereMV = new CanvasMatrix4();
if (depth_sort) {
baseofs = faces[i]*obj.vOffsets.stride;
} else {
baseofs = i*obj.vOffsets.stride;
}
ofs = baseofs + obj.vOffsets.radofs;
sscale = obj.values[ofs];
sphereMV.scale(sscale/scale[0], sscale/scale[1], sscale/scale[2]);
sphereMV.translate(obj.values[baseofs],
obj.values[baseofs+1],
obj.values[baseofs+2]);
sphereMV.multRight(this.mvMatrix);
gl.uniformMatrix4fv( obj.mvMatLoc, false, new Float32Array(sphereMV.getAsArray()) );
if (nc > 1) {
ofs = baseofs + obj.vOffsets.cofs;
gl.vertexAttrib4f( this.colLoc, obj.values[ofs],
obj.values[ofs+1],
obj.values[ofs+2],
obj.values[ofs+3] );
}
gl.drawElements(gl.TRIANGLES, this.sphere.sphereCount, gl.UNSIGNED_SHORT, 0);
}
return;
} else {
if (obj.colorCount === 1) {
gl.disableVertexAttribArray( this.colLoc );
gl.vertexAttrib4fv( this.colLoc, new Float32Array(obj.onecolor));
} else {
gl.enableVertexAttribArray( this.colLoc );
gl.vertexAttribPointer(this.colLoc, 4, gl.FLOAT, false, 4*obj.vOffsets.stride, 4*obj.vOffsets.cofs);
}
}
if (is_lit && obj.vOffsets.nofs > 0) {
gl.enableVertexAttribArray( obj.normLoc );
gl.vertexAttribPointer(obj.normLoc, 3, gl.FLOAT, false, 4*obj.vOffsets.stride, 4*obj.vOffsets.nofs);
}
if (has_texture || type === "text") {
gl.enableVertexAttribArray( obj.texLoc );
gl.vertexAttribPointer(obj.texLoc, 2, gl.FLOAT, false, 4*obj.vOffsets.stride, 4*obj.vOffsets.tofs);
gl.activeTexture(gl.TEXTURE0);
gl.bindTexture(gl.TEXTURE_2D, obj.texture);
gl.uniform1i( obj.sampler, 0);
}
if (fixed_quads) {
gl.enableVertexAttribArray( obj.ofsLoc );
gl.vertexAttribPointer(obj.ofsLoc, 2, gl.FLOAT, false, 4*obj.vOffsets.stride, 4*obj.vOffsets.oofs);
}
var mode = this.mode4type[type];
if (type === "sprites" || type === "text" || type === "quads") {
count = count * 6/4;
} else if (type === "surface") {
count = obj.f.length;
}
if (is_lines) {
gl.lineWidth( this.getMaterial(id, "lwd") );
}
gl.vertexAttribPointer(this.posLoc,  3, gl.FLOAT, false, 4*obj.vOffsets.stride,  4*obj.vOffsets.vofs);
if (is_indexed) {
gl.drawElements(gl[mode], count, gl.UNSIGNED_SHORT, 0);
} else {
gl.drawArrays(gl[mode], 0, count);
}
};
this.drawBackground = function(id, subsceneid) {
var gl = this.gl || this.initGL(),
obj = this.getObj(id),
bg, i;
if (!obj.initialized)
this.initObj(id);
if (obj.colors.length) {
bg = obj.colors[0];
gl.clearColor(bg[0], bg[1], bg[2], bg[3]);
gl.depthMask(true);
gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
}
if (typeof obj.quad !== "undefined") {
this.prMatrix.makeIdentity();
this.mvMatrix.makeIdentity();
gl.disable(gl.BLEND);
gl.disable(gl.DEPTH_TEST);
gl.depthMask(false);
for (i=0; i < obj.quad.length; i++)
this.drawObj(obj.quad[i], subsceneid);
}
};
this.drawSubscene = function(subsceneid) {
var gl = this.gl || this.initGL(),
obj = this.getObj(subsceneid),
objects = this.scene.objects,
subids = obj.objects,
subscene_has_faces = false,
subscene_needs_sorting = false,
flags, i;
if (obj.par3d.skipRedraw)
return;
for (i=0; i < subids.length; i++) {
flags = objects[subids[i]].flags;
if (typeof flags !== "undefined") {
subscene_has_faces |= (flags & this.f_is_lit)
& !(flags & this.f_fixed_quads);
subscene_needs_sorting |= (flags & this.f_depth_sort);
}
}
this.setViewport(subsceneid);
if (typeof obj.backgroundId !== "undefined")
this.drawBackground(obj.backgroundId, subsceneid);
if (subids.length) {
this.setprMatrix(subsceneid);
this.setmvMatrix(subsceneid);
if (subscene_has_faces) {
this.setnormMatrix(subsceneid);
if ((obj.flags & this.f_sprites_3d) &&
typeof obj.spriteNormmat === "undefined") {
obj.spriteNormmat = new CanvasMatrix4(this.normMatrix);
}
}
if (subscene_needs_sorting)
this.setprmvMatrix();
gl.enable(gl.DEPTH_TEST);
gl.depthMask(true);
gl.disable(gl.BLEND);
var clipids = obj.clipplanes;
if (typeof clipids === "undefined") {
console.warn("bad clipids");
}
if (clipids.length > 0) {
this.invMatrix = new CanvasMatrix4(this.mvMatrix);
this.invMatrix.invert();
for (i = 0; i < clipids.length; i++)
this.drawObj(clipids[i], subsceneid);
}
subids = obj.opaque;
if (subids.length > 0) {
for (i = 0; i < subids.length; i++) {
this.drawObj(subids[i], subsceneid);
}
}
subids = obj.transparent;
if (subids.length > 0) {
gl.depthMask(false);
gl.blendFuncSeparate(gl.SRC_ALPHA, gl.ONE_MINUS_SRC_ALPHA,
gl.ONE, gl.ONE);
gl.enable(gl.BLEND);
for (i = 0; i < subids.length; i++) {
this.drawObj(subids[i], subsceneid);
}
}
subids = obj.subscenes;
for (i = 0; i < subids.length; i++) {
this.drawSubscene(subids[i]);
}
}
};
this.relMouseCoords = function(event) {
var totalOffsetX = 0,
totalOffsetY = 0,
currentElement = this.canvas;
do {
totalOffsetX += currentElement.offsetLeft;
totalOffsetY += currentElement.offsetTop;
currentElement = currentElement.offsetParent;
}
while(currentElement);
var canvasX = event.pageX - totalOffsetX,
canvasY = event.pageY - totalOffsetY;
return {x:canvasX, y:canvasY};
};
this.setMouseHandlers = function() {
var self = this, activeSubscene, handler,
handlers = {}, drag = 0;
handlers.rotBase = 0;
this.screenToVector = function(x, y) {
var viewport = this.getObj(activeSubscene).par3d.viewport,
width = viewport.width*this.canvas.width,
height = viewport.height*this.canvas.height,
radius = Math.max(width, height)/2.0,
cx = width/2.0,
cy = height/2.0,
px = (x-cx)/radius,
py = (y-cy)/radius,
plen = Math.sqrt(px*px+py*py);
if (plen > 1.e-6) {
px = px/plen;
py = py/plen;
}
var angle = (Math.SQRT2 - plen)/Math.SQRT2*Math.PI/2,
z = Math.sin(angle),
zlen = Math.sqrt(1.0 - z*z);
px = px * zlen;
py = py * zlen;
return [px, py, z];
};
handlers.trackballdown = function(x,y) {
var activeSub = this.getObj(activeSubscene),
activeModel = this.getObj(this.useid(activeSub.id, "model")),
i, l = activeModel.par3d.listeners;
handlers.rotBase = this.screenToVector(x, y);
this.saveMat = [];
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.saveMat = new CanvasMatrix4(activeSub.par3d.userMatrix);
}
};
handlers.trackballmove = function(x,y) {
var rotCurrent = this.screenToVector(x,y),
rotBase = handlers.rotBase,
dot = rotBase[0]*rotCurrent[0] +
rotBase[1]*rotCurrent[1] +
rotBase[2]*rotCurrent[2],
angle = Math.acos( dot/this.vlen(rotBase)/this.vlen(rotCurrent) )*180.0/Math.PI,
axis = this.xprod(rotBase, rotCurrent),
objects = this.scene.objects,
activeSub = this.getObj(activeSubscene),
activeModel = this.getObj(this.useid(activeSub.id, "model")),
l = activeModel.par3d.listeners,
i;
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.par3d.userMatrix.load(objects[l[i]].saveMat);
activeSub.par3d.userMatrix.rotate(angle, axis[0], axis[1], axis[2]);
}
this.drawScene();
};
handlers.trackballend = 0;
handlers.axisdown = function(x,y) {
handlers.rotBase = this.screenToVector(x, this.canvas.height/2);
var activeSub = this.getObj(activeSubscene),
activeModel = this.getObj(this.useid(activeSub.id, "model")),
i, l = activeModel.par3d.listeners;
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.saveMat = new CanvasMatrix4(activeSub.par3d.userMatrix);
}
};
handlers.axismove = function(x,y) {
var rotCurrent = this.screenToVector(x, this.canvas.height/2),
rotBase = handlers.rotBase,
angle = (rotCurrent[0] - rotBase[0])*180/Math.PI,
rotMat = new CanvasMatrix4();
rotMat.rotate(angle, handlers.axis[0], handlers.axis[1], handlers.axis[2]);
var activeSub = this.getObj(activeSubscene),
activeModel = this.getObj(this.useid(activeSub.id, "model")),
i, l = activeModel.par3d.listeners;
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.par3d.userMatrix.load(activeSub.saveMat);
activeSub.par3d.userMatrix.multLeft(rotMat);
}
this.drawScene();
};
handlers.axisend = 0;
handlers.y0zoom = 0;
handlers.zoom0 = 0;
handlers.zoomdown = function(x, y) {
var activeSub = this.getObj(activeSubscene),
activeProjection = this.getObj(this.useid(activeSub.id, "projection")),
i, l = activeProjection.par3d.listeners;
handlers.y0zoom = y;
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.zoom0 = Math.log(activeSub.par3d.zoom);
}
};
handlers.zoommove = function(x, y) {
var activeSub = this.getObj(activeSubscene),
activeProjection = this.getObj(this.useid(activeSub.id, "projection")),
i, l = activeProjection.par3d.listeners;
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.par3d.zoom = Math.exp(activeSub.zoom0 + (y-handlers.y0zoom)/this.canvas.height);
}
this.drawScene();
};
handlers.zoomend = 0;
handlers.y0fov = 0;
handlers.fovdown = function(x, y) {
handlers.y0fov = y;
var activeSub = this.getObj(activeSubscene),
activeProjection = this.getObj(this.useid(activeSub.id, "projection")),
i, l = activeProjection.par3d.listeners;
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.fov0 = activeSub.par3d.FOV;
}
};
handlers.fovmove = function(x, y) {
var activeSub = this.getObj(activeSubscene),
activeProjection = this.getObj(this.useid(activeSub.id, "projection")),
i, l = activeProjection.par3d.listeners;
for (i = 0; i < l.length; i++) {
activeSub = this.getObj(l[i]);
activeSub.par3d.FOV = Math.max(1, Math.min(179, activeSub.fov0 +
180*(y-handlers.y0fov)/this.canvas.height));
}
this.drawScene();
};
handlers.fovend = 0;
this.canvas.onmousedown = function ( ev ){
if (!ev.which) // Use w3c defns in preference to MS
switch (ev.button) {
case 0: ev.which = 1; break;
case 1:
case 4: ev.which = 2; break;
case 2: ev.which = 3;
}
drag = ["left", "middle", "right"][ev.which-1];
var coords = self.relMouseCoords(ev);
coords.y = self.canvas.height-coords.y;
activeSubscene = self.whichSubscene(coords);
var sub = self.getObj(activeSubscene), f;
handler = sub.par3d.mouseMode[drag];
switch (handler) {
case "xAxis":
handler = "axis";
handlers.axis = [1.0, 0.0, 0.0];
break;
case "yAxis":
handler = "axis";
handlers.axis = [0.0, 1.0, 0.0];
break;
case "zAxis":
handler = "axis";
handlers.axis = [0.0, 0.0, 1.0];
break;
}
f = handlers[handler + "down"];
if (f) {
coords = self.translateCoords(activeSubscene, coords);
f.call(self, coords.x, coords.y);
ev.preventDefault();
}
};
this.canvas.onmouseup = function ( ev ){
if ( drag === 0 ) return;
var f = handlers[handler + "up"];
if (f)
f();
drag = 0;
};
this.canvas.onmouseout = this.canvas.onmouseup;
this.canvas.onmousemove = function ( ev ) {
if ( drag === 0 ) return;
var f = handlers[handler + "move"];
if (f) {
var coords = self.relMouseCoords(ev);
coords.y = self.canvas.height - coords.y;
coords = self.translateCoords(activeSubscene, coords);
f.call(self, coords.x, coords.y);
}
};
handlers.wheelHandler = function(ev) {
var del = 1.02, i;
if (ev.shiftKey) del = 1.002;
var ds = ((ev.detail || ev.wheelDelta) > 0) ? del : (1 / del);
if (typeof activeSubscene === "undefined")
activeSubscene = self.scene.rootSubscene;
var activeSub = self.getObj(activeSubscene),
activeProjection = self.getObj(self.useid(activeSub.id, "projection")),
l = activeProjection.par3d.listeners;
for (i = 0; i < l.length; i++) {
activeSub = self.getObj(l[i]);
activeSub.par3d.zoom *= ds;
}
self.drawScene();
ev.preventDefault();
};
this.canvas.addEventListener("DOMMouseScroll", handlers.wheelHandler, false);
this.canvas.addEventListener("mousewheel", handlers.wheelHandler, false);
};
this.useid = function(subsceneid, type) {
var sub = this.getObj(subsceneid);
if (sub.embeddings[type] === "inherit")
return(this.useid(sub.parent, type));
else
return subsceneid;
};
this.inViewport = function(coords, subsceneid) {
var viewport = this.getObj(subsceneid).par3d.viewport,
x0 = coords.x - viewport.x*this.canvas.width,
y0 = coords.y - viewport.y*this.canvas.height;
return 0 <= x0 && x0 <= viewport.width*this.canvas.width &&
0 <= y0 && y0 <= viewport.height*this.canvas.height;
};
this.whichSubscene = function(coords) {
var self = this,
recurse = function(subsceneid) {
var subscenes = self.getChildSubscenes(subsceneid), i, id;
for (i=0; i < subscenes.length; i++) {
id = recurse(subscenes[i]);
if (typeof(id) !== "undefined")
return(id);
}
if (self.inViewport(coords, subsceneid))
return(subsceneid);
else
return undefined;
},
rootid = this.scene.rootSubscene,
result = recurse(rootid);
if (typeof(result) === "undefined")
result = rootid;
return result;
};
this.translateCoords = function(subsceneid, coords) {
var viewport = this.getObj(subsceneid).par3d.viewport;
return {x: coords.x - viewport.x*this.canvas.width,
y: coords.y - viewport.y*this.canvas.height};
};
this.initSphere = function() {
var verts = this.scene.sphereVerts, 
reuse = verts.reuse, result;
if (typeof reuse !== "undefined") {
var prev = document.getElementById(reuse).rglinstance.sphere;
result = {values: prev.values, vOffsets: prev.vOffsets, it: prev.it};
} else 
result = {values: new Float32Array(this.flatten(this.cbind(this.transpose(verts.vb),
this.transpose(verts.texcoords)))),
it: new Uint16Array(this.flatten(this.transpose(verts.it))),
vOffsets: {vofs:0, cofs:-1, nofs:-1, radofs:-1, oofs:-1, 
tofs:3, stride:5}};
result.sphereCount = result.it.length;
this.sphere = result;
};
this.initSphereGL = function() {
var gl = this.gl || this.initGL(), sphere = this.sphere;
if (gl.isContextLost()) return;
sphere.buf = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, sphere.buf);
gl.bufferData(gl.ARRAY_BUFFER, sphere.values, gl.STATIC_DRAW);
sphere.ibuf = gl.createBuffer();
gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, sphere.ibuf);
gl.bufferData(gl.ELEMENT_ARRAY_BUFFER, sphere.it, gl.STATIC_DRAW);
return;
};
this.initialize = function(el, x) {
this.textureCanvas = document.createElement("canvas");
this.textureCanvas.style.display = "block";
this.scene = x;
this.normMatrix = new CanvasMatrix4();
this.saveMat = {};
this.distance = null;
this.posLoc = 0;
this.colLoc = 1;
if (el) {
el.rglinstance = this;
this.el = el;
this.webGLoptions = el.rglinstance.scene.webGLoptions;
this.initCanvas();
}
};
this.restartCanvas = function() {
var newcanvas = document.createElement("canvas");
newcanvas.width = this.el.width;
newcanvas.height = this.el.height;
newcanvas.addEventListener("webglcontextrestored",
this.onContextRestored, false);
newcanvas.addEventListener("webglcontextlost",
this.onContextLost, false);            
while (this.el.firstChild) {
this.el.removeChild(this.el.firstChild);
}
this.el.appendChild(newcanvas);
this.canvas = newcanvas;
this.gl = null;      	
}
this.initCanvas = function() {
this.restartCanvas();
var objs = this.scene.objects,
self = this;
Object.keys(objs).forEach(function(key){
var id = parseInt(key, 10),
obj = self.getObj(id);
if (typeof obj.reuse !== "undefined")
self.copyObj(id, obj.reuse);
});
Object.keys(objs).forEach(function(key){
self.initSubscene(parseInt(key, 10));
});
this.setMouseHandlers();      
this.initSphere();
this.onContextRestored = function(event) {
self.initGL();
self.drawScene();
console.log("restored context for "+self.scene.rootSubscene);
}
this.onContextLost = function(event) {
if (!self.drawing)
self.restartCanvas();
event.preventDefault();
}
this.initGL0();
lazyLoadScene = function() {
if (self.isInBrowserViewport()) {
if (!self.gl) {
self.initGL();
}
self.drawScene();
}
}
window.addEventListener("DOMContentLoaded", lazyLoadScene, false);
window.addEventListener("load", lazyLoadScene, false);
window.addEventListener("resize", lazyLoadScene, false);
window.addEventListener("scroll", lazyLoadScene, false);
};
/* this is only used by writeWebGL; rglwidget has
no debug element and does the drawing in rglwidget.js */
this.start = function() {
if (typeof this.prefix !== "undefined") {
this.debugelement = document.getElementById(this.prefix + "debug");
this.debug("");
}
this.drag = 0;
this.drawScene();
};
this.debug = function(msg, img) {
if (typeof this.debugelement !== "undefined" && this.debugelement !== null) {
this.debugelement.innerHTML = msg;
if (typeof img !== "undefined") {
this.debugelement.insertBefore(img, this.debugelement.firstChild);
}
} else if (msg !== "")
alert(msg);
};
this.getSnapshot = function() {
var img;
if (typeof this.scene.snapshot !== "undefined") {
img = document.createElement("img");
img.src = this.scene.snapshot;
img.alt = "Snapshot";
}
return img;
};
this.initGL0 = function() {
if (!window.WebGLRenderingContext){
alert("Your browser does not support WebGL. See http://get.webgl.org");
return;
}
};
this.isInBrowserViewport = function() {
var rect = this.canvas.getBoundingClientRect(),
windHeight = (window.innerHeight || document.documentElement.clientHeight),
windWidth = (window.innerWidth || document.documentElement.clientWidth);
return (
rect.top >= -windHeight &&
rect.left >= -windWidth &&
rect.bottom <= 2*windHeight &&
rect.right <= 2*windWidth);
}
this.initGL = function() {
var self = this;
if (this.gl) {
if (!this.drawing && this.gl.isContextLost())
this.restartCanvas();
else
return this.gl;
}
// if (!this.isInBrowserViewport()) return; Return what??? At this point we know this.gl is null.
this.canvas.addEventListener("webglcontextrestored",
this.onContextRestored, false);
this.canvas.addEventListener("webglcontextlost",
this.onContextLost, false);      
this.gl = this.canvas.getContext("webgl", this.webGLoptions) ||
this.canvas.getContext("experimental-webgl", this.webGLoptions);
var save = this.startDrawing();
this.initSphereGL(); 
Object.keys(this.scene.objects).forEach(function(key){
self.initObj(parseInt(key, 10));
});
this.stopDrawing(save);
return this.gl;
};
this.resize = function(el) {
this.canvas.width = el.width;
this.canvas.height = el.height;
};
this.drawScene = function() {
var gl = this.gl || this.initGL(),
save = this.startDrawing();
gl.enable(gl.DEPTH_TEST);
gl.depthFunc(gl.LEQUAL);
gl.clearDepth(1.0);
gl.clearColor(1,1,1,1);
gl.depthMask(true); // Must be true before clearing depth buffer
gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
this.drawSubscene(this.scene.rootSubscene);
this.stopDrawing(save);
};
this.subsetSetter = function(el, control) {
if (typeof control.subscenes === "undefined" ||
control.subscenes === null)
control.subscenes = this.scene.rootSubscene;
var value = Math.round(control.value),
subscenes = [].concat(control.subscenes),
i, j, entries, subsceneid,
ismissing = function(x) {
return control.fullset.indexOf(x) < 0;
},
tointeger = function(x) {
return parseInt(x, 10);
};
for (i=0; i < subscenes.length; i++) {
subsceneid = subscenes[i];
if (typeof this.getObj(subsceneid) === "undefined")
this.alertOnce("typeof object is undefined");
entries = this.getObj(subsceneid).objects;
entries = entries.filter(ismissing);
if (control.accumulate) {
for (j=0; j<=value; j++)
entries = entries.concat(control.subsets[j]);
} else {
entries = entries.concat(control.subsets[value]);
}
entries = entries.map(tointeger);
this.setSubsceneEntries(this.unique(entries), subsceneid);
}
};
this.propertySetter = function(el, control)  {
var value = control.value,
values = [].concat(control.values),
svals = [].concat(control.param),
direct = values[0] === null,
entries = [].concat(control.entries),
ncol = entries.length,
nrow = values.length/ncol,
properties = this.repeatToLen(control.properties, ncol),
objids = this.repeatToLen(control.objids, ncol),
property = properties[0], objid = objids[0],
obj = this.getObj(objid),
propvals, i, v1, v2, p, entry, gl, needsBinding,
newprop, newid,
getPropvals = function() {
if (property === "userMatrix")
return obj.userMatrix.getAsArray();
else
return obj[property];
};
if (direct && typeof value === "undefined")
return;
if (control.interp) {
values = values.slice(0, ncol).concat(values).
concat(values.slice(ncol*(nrow-1), ncol*nrow));
svals = [-Infinity].concat(svals).concat(Infinity);
for (i = 1; i < svals.length; i++) {
if (value <= svals[i]) {
if (svals[i] === Infinity)
p = 1;
else
p = (svals[i] - value)/(svals[i] - svals[i-1]);
break;
}
}
} else if (!direct) {
value = Math.round(value);
}
propvals = getPropvals();
for (j=0; j<entries.length; j++) {
entry = entries[j];
newprop = properties[j];
newid = objids[j];
if (newprop != property || newid != objid) {
property = newprop;
objid = newid;
obj = this.getObj(objid);
propvals = getPropvals();
}
if (control.interp) {
v1 = values[ncol*(i-1) + j];
v2 = values[ncol*i + j];
this.setElement(propvals, entry, p*v1 + (1-p)*v2);
} else if (!direct) {
this.setElement(propvals, entry, values[ncol*value + j]);
} else {
this.setElement(propvals, entry, value[j]);
}
}
needsBinding = [];
for (j=0; j < entries.length; j++) {
if (properties[j] === "values" &&
needsBinding.indexOf(objids[j]) === -1) {
needsBinding.push(objids[j]);
}
}
for (j=0; j < needsBinding.length; j++) {
gl = this.gl || this.initGL();
obj = this.getObj(needsBinding[j]);
gl.bindBuffer(gl.ARRAY_BUFFER, obj.buf);
gl.bufferData(gl.ARRAY_BUFFER, obj.values, gl.STATIC_DRAW);
}
};
this.vertexSetter = function(el, control)  {
var svals = [].concat(control.param),
j, k, p, propvals, stride, ofs, obj,
attrib,
ofss    = {x:"vofs", y:"vofs", z:"vofs",
red:"cofs", green:"cofs", blue:"cofs",
alpha:"cofs", radii:"radofs",
nx:"nofs", ny:"nofs", nz:"nofs",
ox:"oofs", oy:"oofs", oz:"oofs",
ts:"tofs", tt:"tofs"},
pos     = {x:0, y:1, z:2,
red:0, green:1, blue:2,
alpha:3,radii:0,
nx:0, ny:1, nz:2,
ox:0, oy:1, oz:2,
ts:0, tt:1},
values = control.values,
direct = values === null,
ncol,
interp = control.interp,
vertices = [].concat(control.vertices),
attributes = [].concat(control.attributes),
value = control.value;
ncol = Math.max(vertices.length, attributes.length);
if (!ncol)
return;
vertices = this.repeatToLen(vertices, ncol);
attributes = this.repeatToLen(attributes, ncol);
if (direct)
interp = false;
/* JSON doesn't pass Infinity */
svals[0] = -Infinity;
svals[svals.length - 1] = Infinity;
for (j = 1; j < svals.length; j++) {
if (value <= svals[j]) {
if (interp) {
if (svals[j] === Infinity)
p = 1;
else
p = (svals[j] - value)/(svals[j] - svals[j-1]);
} else {
if (svals[j] - value > value - svals[j-1])
j = j - 1;
}
break;
}
}
obj = this.getObj(control.objid);
propvals = obj.values;
for (k=0; k<ncol; k++) {
attrib = attributes[k];
vertex = vertices[k];
ofs = obj.vOffsets[ofss[attrib]];
if (ofs < 0)
this.alertOnce("Attribute '"+attrib+"' not found in object "+control.objid);
else {
stride = obj.vOffsets.stride;
ofs = vertex*stride + ofs + pos[attrib];
if (direct) {
propvals[ofs] = value;
} else if (interp) {
propvals[ofs] = p*values[j-1][k] + (1-p)*values[j][k];
} else {
propvals[ofs] = values[j][k];
}
}
}
if (typeof obj.buf !== "undefined") {
var gl = this.gl || this.initGL();
gl.bindBuffer(gl.ARRAY_BUFFER, obj.buf);
gl.bufferData(gl.ARRAY_BUFFER, propvals, gl.STATIC_DRAW);
}
};
this.ageSetter = function(el, control) {
var objids = [].concat(control.objids),
nobjs = objids.length,
time = control.value,
births = [].concat(control.births),
ages = [].concat(control.ages),
steps = births.length,
j = Array(steps),
p = Array(steps),
i, k, age, j0, propvals, stride, ofs, objid, obj,
attrib, dim,
attribs = ["colors", "alpha", "radii", "vertices",
"normals", "origins", "texcoords",
"x", "y", "z",
"red", "green", "blue"],
ofss    = ["cofs", "cofs", "radofs", "vofs",
"nofs", "oofs", "tofs",
"vofs", "vofs", "vofs",
"cofs", "cofs", "cofs"],
dims    = [3,1,1,3,
3,2,2,
1,1,1,
1,1,1],
pos     = [0,3,0,0,
0,0,0,
0,1,2,
0,1,2];
/* Infinity doesn't make it through JSON */
ages[0] = -Infinity;
ages[ages.length-1] = Infinity;
for (i = 0; i < steps; i++) {
if (births[i] !== null) {  // NA in R becomes null
age = time - births[i];
for (j0 = 1; age > ages[j0]; j0++);
if (ages[j0] == Infinity)
p[i] = 1;
else if (ages[j0] > ages[j0-1])
p[i] = (ages[j0] - age)/(ages[j0] - ages[j0-1]);
else
p[i] = 0;
j[i] = j0;
}
}
for (l = 0; l < nobjs; l++) {
objid = objids[l];
obj = this.getObj(objid);
propvals = obj.values;
stride = obj.vOffsets.stride;
for (k = 0; k < attribs.length; k++) {
attrib = control[attribs[k]];
if (typeof attrib !== "undefined") {
ofs = obj.vOffsets[ofss[k]];
if (ofs >= 0) {
dim = dims[k];
ofs = ofs + pos[k];
for (i = 0; i < steps; i++) {
if (births[i] !== null) {
for (d=0; d < dim; d++) {
propvals[i*stride + ofs + d] = p[i]*attrib[dim*(j[i]-1) + d] + (1-p[i])*attrib[dim*j[i] + d];
}
}
}
} else
this.alertOnce("\'"+attribs[k]+"\' property not found in object "+objid);
}
}
obj.values = propvals;
if (typeof obj.buf !== "undefined") {
gl = this.gl || this.initGL();
gl.bindBuffer(gl.ARRAY_BUFFER, obj.buf);
gl.bufferData(gl.ARRAY_BUFFER, obj.values, gl.STATIC_DRAW);
}
}
};
this.oldBridge = function(el, control) {
var attrname, global = window[control.prefix + "rgl"];
if (typeof global !== "undefined")
for (attrname in global)
this[attrname] = global[attrname];
window[control.prefix + "rgl"] = this;
};
this.Player = function(el, control) {
var
self = this,
components = [].concat(control.components),
Tick = function() { /* "this" will be a timer */
var i,
nominal = this.value,
slider = this.Slider,
labels = this.outputLabels,
output = this.Output,
step;
if (typeof slider !== "undefined" && nominal != slider.value)
slider.value = nominal;
if (typeof output !== "undefined") {
step = Math.round((nominal - output.sliderMin)/output.sliderStep);
if (labels !== null) {
output.innerHTML = labels[step];
} else {
step = step*output.sliderStep + output.sliderMin;
output.innerHTML = step.toPrecision(output.outputPrecision);
}
}
for (i=0; i < this.actions.length; i++) {
this.actions[i].value = nominal;
}
self.applyControls(el, this.actions, false);
self.drawScene();
},
OnSliderInput = function() { /* "this" will be the slider */
this.rgltimer.value = Number(this.value);
this.rgltimer.Tick();
},
addSlider = function(min, max, step, value) {
var slider = document.createElement("input");
slider.type = "range";
slider.min = min;
slider.max = max;
slider.step = step;
slider.value = value;
slider.oninput = OnSliderInput;
slider.sliderActions = control.actions;
slider.sliderScene = this;
slider.className = "rgl-slider";
slider.id = el.id + "-slider";
el.rgltimer.Slider = slider;
slider.rgltimer = el.rgltimer;
el.appendChild(slider);
},
addLabel = function(labels, min, step, precision) {
var output = document.createElement("output");
output.sliderMin = min;
output.sliderStep = step;
output.outputPrecision = precision;
output.className = "rgl-label";
output.id = el.id + "-label";
el.rgltimer.Output = output;
el.rgltimer.outputLabels = labels;
el.appendChild(output);
},
addButton = function(label) {
var button = document.createElement("input"),
onclicks = {Reverse: function() { this.rgltimer.reverse();},
Play: function() { this.rgltimer.play();
this.value = this.rgltimer.enabled ? "Pause" : "Play"; },
Slower: function() { this.rgltimer.slower(); },
Faster: function() { this.rgltimer.faster(); },
Reset: function() { this.rgltimer.reset(); }};
button.rgltimer = el.rgltimer;
button.type = "button";
button.value = label;
if (label === "Play")
button.rgltimer.PlayButton = button;
button.onclick = onclicks[label];
button.className = "rgl-button";
button.id = el.id + "-" + label;
el.appendChild(button);
};
if (typeof control.reinit !== "undefined" && control.reinit !== null) {
control.actions.reinit = control.reinit;
}
el.rgltimer = new rgltimerClass(Tick, control.start, control.interval, control.stop, control.value, control.rate, control.loop, control.actions);
for (var i=0; i < components.length; i++) {
switch(components[i]) {
case "Slider": addSlider(control.start, control.stop,
control.step, control.value);
break;
case "Label": addLabel(control.labels, control.start,
control.step, control.precision);
break;
default:
addButton(components[i]);
}
}
el.rgltimer.Tick();
};
this.applyControls = function(el, x, draw) {
var self = this, reinit = x.reinit, i, control, type;
for (i = 0; i < x.length; i++) {
control = x[i];
type = control.type;
self[type](el, control);
}
if (typeof reinit !== "undefined" && reinit !== null) {
reinit = [].concat(reinit);
for (i = 0; i < reinit.length; i++)
self.getObj(reinit[i]).initialized = false;
}
if (typeof draw === "undefined" || draw)
self.drawScene();
};
this.sceneChangeHandler = function(message) {
var self = document.getElementById(message.elementId).rglinstance,
objs = message.objects, mat = message.material,
root = message.rootSubscene,
initSubs = message.initSubscenes,
redraw = message.redrawScene,
skipRedraw = message.skipRedraw,
deletes, subs, allsubs = [], i,j;
if (typeof message.delete !== "undefined") {
deletes = [].concat(message.delete);
if (typeof message.delfromSubscenes !== "undefined")
subs = [].concat(message.delfromSubscenes);
else
subs = [];
for (i = 0; i < deletes.length; i++) {
for (j = 0; j < subs.length; j++) {
self.delFromSubscene(deletes[i], subs[j]);
}
delete self.scene.objects[deletes[i]];
}
}
if (typeof objs !== "undefined") {
Object.keys(objs).forEach(function(key){
key = parseInt(key, 10);
self.scene.objects[key] = objs[key];
self.initObj(key);
var obj = self.getObj(key),
subs = [].concat(obj.inSubscenes), k;
allsubs = allsubs.concat(subs);
for (k = 0; k < subs.length; k++)
self.addToSubscene(key, subs[k]);
});
}
if (typeof mat !== "undefined") {
self.scene.material = mat;
}
if (typeof root !== "undefined") {
self.scene.rootSubscene = root;
}
if (typeof initSubs !== "undefined")
allsubs = allsubs.concat(initSubs);
allsubs = self.unique(allsubs);
for (i = 0; i < allsubs.length; i++) {
self.initSubscene(allsubs[i]);
}
if (typeof skipRedraw !== "undefined") {
root = self.getObj(self.scene.rootSubscene);
root.par3d.skipRedraw = skipRedraw;
}
if (redraw)
self.drawScene();
};
}).call(rglwidgetClass.prototype);
rgltimerClass = function(Tick, startTime, interval, stopTime, value, rate, loop, actions) {
this.enabled = false;
this.timerId = 0;
this.startTime = startTime;         /* nominal start time in seconds */
this.value = value;                 /* current nominal time */
this.interval = interval;           /* seconds between updates */
this.stopTime = stopTime;           /* nominal stop time */
this.rate = rate;                   /* nominal units per second */
this.loop = loop;                   /* "none", "cycle", or "oscillate" */
this.realStart = undefined;         /* real world start time */
this.multiplier = 1;                /* multiplier for fast-forward
or reverse */
this.actions = actions;
this.Tick = Tick;
};
(function() {
this.play = function() {
if (this.enabled) {
this.enabled = false;
window.clearInterval(this.timerId);
this.timerId = 0;
return;
}
var tick = function(self) {
var now = new Date();
self.value = self.multiplier*self.rate*(now - self.realStart)/1000 + self.startTime;
if (self.value > self.stopTime || self.value < self.startTime) {
if (!self.loop) {
self.reset();
} else {
var cycle = self.stopTime - self.startTime,
newval = (self.value - self.startTime) % cycle + self.startTime;
if (newval < self.startTime) {
newval += cycle;
}
self.realStart += (self.value - newval)*1000/self.multiplier/self.rate;
self.value = newval;
}
}
if (typeof self.Tick !== "undefined") {
self.Tick(self.value);
}
};
this.realStart = new Date() - 1000*(this.value - this.startTime)/this.rate/this.multiplier;
this.timerId = window.setInterval(tick, 1000*this.interval, this);
this.enabled = true;
};
this.reset = function() {
this.value = this.startTime;
this.newmultiplier(1);
if (typeof this.Tick !== "undefined") {
this.Tick(this.value);
}
if (this.enabled)
this.play();  /* really pause... */
if (typeof this.PlayButton !== "undefined")
this.PlayButton.value = "Play";
};
this.faster = function() {
this.newmultiplier(Math.SQRT2*this.multiplier);
};
this.slower = function() {
this.newmultiplier(this.multiplier/Math.SQRT2);
};
this.reverse = function() {
this.newmultiplier(-this.multiplier);
};
this.newmultiplier = function(newmult) {
if (newmult != this.multiplier) {
this.realStart += 1000*(this.value - this.startTime)/this.rate*(1/this.multiplier - 1/newmult);
this.multiplier = newmult;
}
};
}).call(rgltimerClass.prototype);</script>
<div id="unnamed_chunk_1div" class="rglWebGL"></div>
<script type="text/javascript">
var unnamed_chunk_1div = document.getElementById("unnamed_chunk_1div"),
unnamed_chunk_1rgl = new rglwidgetClass();
unnamed_chunk_1div.width = 505;
unnamed_chunk_1div.height = 505;
unnamed_chunk_1rgl.initialize(unnamed_chunk_1div,
{"material":{"color":"#000000","alpha":1,"lit":true,"ambient":"#000000","specular":"#FFFFFF","emission":"#000000","shininess":50,"smooth":true,"front":"filled","back":"filled","size":3,"lwd":1,"fog":false,"point_antialias":false,"line_antialias":false,"texture":null,"textype":"rgb","texmipmap":false,"texminfilter":"linear","texmagfilter":"linear","texenvmap":false,"depth_mask":true,"depth_test":"less"},"rootSubscene":1,"objects":{"7":{"id":7,"type":"spheres","material":{},"vertices":[[-7.315,6.695,-1.77],[-6.027,7.312,-1.841],[-5.382,7.427,-0.46],[-5.995,8.462,0.314],[-5.556,6.146,0.348],[-4.401,5.324,0.15],[-5.551,6.643,1.782],[-4.218,6.743,2.298],[-6.208,8.014,1.662],[-7.648,7.933,1.97],[-8.712,7.912,1.13],[-9.888,7.834,1.654],[-9.59,7.798,3.02],[-10.46,7.712,4.139],[-11.688,7.651,4.148],[-9.753,7.702,5.335],[-8.379,7.766,5.447],[-7.886,7.743,6.686],[-7.552,7.846,4.399],[-8.219,7.858,3.222],[-7.682,5.633,-0.58],[-8.781,4.764,-1.176],[-8.131,6.477,0.607],[-4.547,3.725,0.024],[-3.56,3.247,-0.969],[-5.982,3.403,-0.146],[-4.085,3.214,1.481],[-2.921,3.758,2.116],[-3.153,3.99,3.608],[-4.335,4.762,3.836],[-3.371,2.678,4.35],[-2.108,2.216,4.838],[-4.219,3.101,5.534],[-3.41,3.582,6.614],[-5.077,4.213,4.939],[-6.38,3.685,4.492],[-6.838,3.449,3.238],[-8.033,2.974,3.118],[-8.431,2.876,4.455],[-9.613,2.437,5.061],[-10.664,1.994,4.372],[-9.67,2.473,6.404],[-8.629,2.914,7.113],[-7.465,3.352,6.643],[-7.431,3.306,5.296],[-1.73,0.653,4.766],[-0.258,0.529,4.868],[-2.443,0.056,3.615],[-2.381,0.072,6.119],[-1.825,0.408,7.394],[-2.85,0.248,8.515],[-4.051,0.968,8.23],[-3.277,-1.203,8.68],[-2.416,-1.826,9.638],[-4.663,-1.079,9.288],[-4.602,-0.979,10.716],[-5.193,0.207,8.659],[-6.083,-0.096,7.523],[-5.795,-0.208,6.202],[-6.767,-0.491,5.4],[-7.848,-0.584,6.282],[-9.214,-0.874,6.021],[-9.75,-1.11,4.94],[-9.969,-0.87,7.187],[-9.476,-0.618,8.452],[-10.359,-0.661,9.449],[-8.192,-0.344,8.707],[-7.437,-0.343,7.585],[-2.226,-3.424,9.644],[-1.184,-3.763,10.64],[-2.082,-3.879,8.243],[-3.644,-3.946,10.201],[-3.902,-3.981,11.607],[-5.362,-4.315,11.905],[-6.253,-3.514,11.125],[-5.692,-5.754,11.542],[-5.444,-6.583,12.681],[-7.189,-5.696,11.302],[-7.922,-5.822,12.526],[-7.368,-4.311,10.682],[-7.399,-4.399,9.203],[-8.636,-4.53,8.581],[-9.663,-4.569,9.256],[-8.671,-4.616,7.223],[-7.543,-4.574,6.502],[-7.613,-4.659,5.173],[-6.269,-4.439,7.136],[-6.243,-4.356,8.48],[-5.014,-8.122,12.488],[-4.878,-8.737,13.827],[-3.883,-8.172,11.535],[-6.306,-8.759,11.77],[-7.583,-8.72,12.41],[-8.721,-8.936,11.414],[-8.674,-7.984,10.35],[-8.621,-10.294,10.74],[-9.337,-11.248,11.528],[-9.373,-10.076,9.439],[-10.778,-10.298,9.605],[-9.076,-8.61,9.119],[-8.017,-8.497,8.097],[-6.71,-8.164,8.239],[-5.982,-8.128,7.174],[-6.906,-8.479,6.185],[-6.727,-8.62,4.783],[-5.702,-8.458,4.125],[-7.909,-8.988,4.152],[-9.117,-9.197,4.787],[-10.136,-9.564,4.01],[-9.294,-9.066,6.107],[-8.155,-8.708,6.743],[-8.543,-12.353,12.39],[-8.92,-12.189,13.812],[-7.117,-12.312,11.995],[-9.174,-13.737,11.857],[-9.946,-14.574,12.726],[-11.149,-15.176,12.002],[-11.929,-14.162,11.365],[-10.72,-16.126,10.895],[-10.669,-17.451,11.434],[-11.877,-16.05,9.916],[-12.909,-16.985,10.248],[-12.355,-14.611,10.07],[-11.795,-13.766,9.006],[-10.793,-12.857,9.062],[-10.493,-12.235,7.974],[-11.404,-12.793,7.072],[-11.64,-12.58,5.713],[-10.962,-11.699,4.993],[-12.611,-13.298,5.129],[-13.316,-14.176,5.837],[-13.182,-14.46,7.13],[-12.199,-13.726,7.692],[-10.087,-18.67,10.558],[-9.777,-19.791,11.473],[-9.037,-18.136,9.662],[-11.352,-19.09,9.656],[-12.499,-19.703,10.252],[-13.676,-19.752,9.278],[-13.948,-18.459,8.721],[-13.379,-20.652,8.085],[-13.833,-21.976,8.382],[-14.266,-20.065,7.006],[-15.613,-20.54,7.114],[-14.171,-18.574,7.305],[-13.071,-17.959,6.539],[-11.753,-17.855,6.843],[-10.986,-17.277,5.979],[-11.896,-16.951,4.968],[-11.75,-16.311,3.734],[-10.58,-15.863,3.28],[-12.855,-16.152,2.984],[-14.036,-16.596,3.419],[-14.287,-17.215,4.568],[-13.165,-17.362,5.302],[-12.833,-23.231,8.244],[-13.461,-24.399,8.901],[-11.48,-22.793,8.654],[-12.816,-23.496,6.655],[-13.922,-24.139,6.016],[-14.117,-23.64,4.585],[-14.194,-22.209,4.539],[-12.94,-24.018,3.693],[-13.236,-25.259,3.047],[-12.951,-22.915,2.655],[-13.912,-23.169,1.624],[-13.338,-21.709,3.497],[-12.14,-21.06,4.06],[-11.521,-21.268,5.248],[-10.469,-20.567,5.507],[-10.357,-19.785,4.353],[-9.393,-18.798,4.012],[-8.431,-18.409,4.672],[-9.644,-18.254,2.759],[-10.69,-18.61,1.931],[-10.759,-17.973,0.762],[-11.601,-19.536,2.244],[-11.377,-20.082,3.462],[-12.058,-26.306,2.716],[-12.67,-27.633,2.482],[-11,-26.152,3.739],[-11.488,-25.758,1.313],[-12.383,-25.431,0.245],[-11.879,-24.243,-0.57],[-11.563,-23.129,0.264],[-10.585,-24.568,-1.292],[-10.899,-25.154,-2.558],[-9.989,-23.192,-1.529],[-10.483,-22.609,-2.74],[-10.452,-22.408,-0.3],[-9.352,-22.272,0.673],[-9.127,-22.939,1.834],[-8.062,-22.636,2.497],[-7.497,-21.644,1.687],[-6.332,-20.877,1.8],[-5.478,-20.996,2.816],[-6.076,-19.99,0.821],[-6.914,-19.863,-0.21],[-8.042,-20.537,-0.416],[-8.276,-21.418,0.577],[-9.92,-26.253,-3.211],[-10.544,-26.747,-4.458],[-9.527,-27.21,-2.153],[-8.626,-25.379,-3.606],[-8.564,-24.711,-4.868],[-7.376,-23.754,-4.944],[-7.346,-22.863,-3.832],[-6.055,-24.496,-4.881],[-5.684,-24.885,-6.206],[-5.095,-23.42,-4.403],[-4.56,-22.672,-5.501],[-5.979,-22.546,-3.508],[-5.696,-22.814,-2.077],[-4.804,-21.974,-1.419],[-4.285,-21.036,-2.021],[-4.528,-22.22,-0.11],[-5.1,-23.246,0.533],[-4.805,-23.457,1.816],[-6.02,-24.114,-0.137],[-6.288,-23.864,-1.434],[-5.01,-26.323,-6.475],[-4.644,-26.402,-7.907],[-5.88,-27.361,-5.877],[-3.654,-26.242,-5.611],[-2.641,-25.289,-5.942],[-1.491,-25.315,-4.936],[-1.815,-24.583,-3.756],[-1.194,-26.728,-4.462],[-0.214,-27.304,-5.33],[-0.556,-26.505,-3.1],[0.864,-26.358,-3.206],[-1.217,-25.215,-2.612],[-2.228,-25.507,-1.579],[-3.512,-25.921,-1.718],[-4.195,-26.124,-0.642],[-3.262,-25.809,0.352],[-3.397,-25.831,1.766],[-4.382,-26.138,2.434],[-2.221,-25.443,2.396],[-1.056,-25.079,1.751],[-0.031,-24.737,2.532],[-0.921,-25.056,0.421],[-2.055,-25.43,-0.215],[0.136,-28.873,-5.24],[1.047,-29.21,-6.357],[-1.13,-29.621,-5.069],[0.969,-28.971,-3.864],[1.379,-30.241,-3.348],[2.732,-30.152,-2.644],[3.79,-29.916,-3.573],[2.784,-28.98,-1.677],[2.318,-29.418,-0.398],[4.273,-28.698,-1.579],[4.894,-29.51,-0.576],[4.776,-29.054,-2.977],[4.976,-27.836,-3.786],[4.157,-27.253,-4.696],[4.575,-26.174,-5.269],[5.829,-26.006,-4.673],[6.829,-25.04,-4.825],[6.725,-24.008,-5.664],[7.941,-25.176,-4.081],[8.066,-26.202,-3.236],[7.184,-27.172,-3.014],[6.08,-27.013,-3.77],[1.361,-28.473,0.49],[0.752,-29.302,1.554],[0.497,-27.698,-0.428],[2.405,-27.457,1.178],[3.37,-27.937,2.118],[4.63,-27.074,2.125],[5.158,-26.91,0.808],[4.34,-25.668,2.624],[4.553,-25.639,4.039],[5.425,-24.839,1.96],[6.608,-24.786,2.766],[5.677,-25.579,0.652],[5.041,-24.891,-0.487],[3.827,-25.087,-1.056],[3.531,-24.372,-2.091],[4.687,-23.597,-2.236],[5.058,-22.607,-3.153],[4.27,-22.205,-4.15],[6.273,-22.047,-3.003],[7.077,-22.436,-2.011],[6.828,-23.362,-1.092],[5.608,-23.907,-1.262],[3.448,-25.006,5.024],[3.619,-25.612,6.363],[2.133,-25.07,4.347],[3.897,-23.46,5.108],[5.236,-23.102,5.473],[5.753,-21.938,4.628],[5.817,-22.296,3.242],[4.824,-20.729,4.708],[5.322,-19.834,5.706],[4.998,-20.077,3.352],[6.136,-19.208,3.327],[5.194,-21.281,2.443],[3.905,-21.752,1.905],[2.923,-22.467,2.507],[1.882,-22.762,1.802],[2.203,-22.179,0.572],[1.53,-22.115,-0.651],[0.33,-22.658,-0.853],[2.139,-21.465,-1.658],[3.34,-20.912,-1.474],[4.062,-20.91,-0.362],[3.433,-21.565,0.629],[4.322,-18.841,6.487],[5.137,-17.854,7.23],[3.322,-19.662,7.205],[3.574,-18.073,5.284],[4.262,-17.08,4.518],[3.599,-16.854,3.159],[3.421,-18.086,2.459],[2.203,-16.268,3.304],[2.299,-14.841,3.282],[1.515,-16.72,2.029],[1.735,-15.795,0.958],[2.173,-18.069,1.746],[1.295,-19.173,2.177],[1.278,-19.867,3.342],[0.374,-20.779,3.482],[-0.306,-20.696,2.263],[-1.419,-21.441,1.786],[-2.039,-22.337,2.356],[-1.791,-21.04,0.509],[-1.172,-20.047,-0.225],[-1.669,-19.811,-1.439],[-0.126,-19.343,0.216],[0.254,-19.715,1.459],[1.015,-13.93,3.626],[1.468,-12.529,3.772],[0.266,-14.581,4.724],[0.132,-14.037,2.282],[0.587,-13.436,1.067],[-0.246,-13.883,-0.134],[-0.335,-15.31,-0.208],[-1.684,-13.399,-0.034],[-1.783,-12.111,-0.648],[-2.421,-14.405,-0.897],[-2.339,-14.066,-2.286],[-1.67,-15.697,-0.59],[-2.341,-16.442,0.504],[-3.255,-17.428,0.159],[-3.509,-17.701,-1.011],[-3.867,-18.086,1.211],[-3.65,-17.851,2.558],[-4.252,-18.498,3.412],[-2.683,-16.81,2.826],[-2.07,-16.15,1.814],[-2.895,-11.057,-0.149],[-2.703,-9.794,-0.895],[-2.894,-11.049,1.331],[-4.269,-11.733,-0.648],[-4.45,-12.069,-2.026],[-5.498,-13.163,-2.213],[-5.228,-14.295,-1.394],[-6.88,-12.698,-1.793],[-7.514,-12.086,-2.92],[-7.599,-14.005,-1.487],[-8.265,-14.518,-2.646],[-6.466,-14.932,-1.039],[-6.529,-15.171,0.417],[-7.4,-16.149,0.878],[-8.097,-16.78,0.084],[-7.46,-16.38,2.218],[-6.699,-15.681,3.07],[-6.781,-15.933,4.376],[-5.802,-14.672,2.597],[-5.75,-14.45,1.273],[-8.981,-11.436,-2.783],[-9.796,-11.886,-3.933],[-8.823,-9.99,-2.51],[-9.555,-12.14,-1.453],[-10.713,-12.976,-1.516],[-11.474,-12.983,-0.19],[-10.731,-13.661,0.83],[-11.712,-11.567,0.327],[-13.02,-11.153,-0.075],[-11.709,-11.741,1.835],[-13.014,-12.076,2.321],[-10.73,-12.892,2.043],[-9.367,-12.413,2.361],[-8.507,-11.667,1.621],[-7.357,-11.391,2.138],[-7.44,-12.026,3.38],[-6.487,-12.098,4.431],[-5.361,-11.606,4.475],[-6.968,-12.835,5.507],[-8.211,-13.432,5.569],[-8.496,-14.09,6.694],[-9.112,-13.37,4.584],[-8.667,-12.655,3.525],[-13.405,-9.59,-0.116],[-13.15,-9.086,-1.484],[-12.772,-8.927,1.046],[-14.999,-9.616,0.124],[-15.768,-10.794,-0.15],[-16.648,-11.178,1.038],[-15.896,-11.877,2.029],[-17.214,-9.949,1.736],[-18.505,-9.674,1.185],[-17.396,-10.412,3.172],[-18.696,-10.977,3.376],[-16.3,-11.462,3.343],[-15.156,-10.916,4.097],[-14.133,-10.132,3.676],[-13.243,-9.792,4.549],[-13.724,-10.426,5.701],[-13.256,-10.488,7.019],[-12.14,-9.887,7.43],[-13.977,-11.203,7.899],[-15.091,-11.823,7.512],[-15.625,-11.833,6.296],[-14.887,-11.11,5.431],[-19.177,-8.223,1.371],[-19.779,-8.16,2.721],[-20.007,-7.94,0.179],[-17.9,-7.244,1.341],[-17.731,-6.236,2.34],[-17.656,-6.839,3.744],[-16.654,-7.86,3.822],[-17.277,-5.789,4.787],[-18.477,-5.3,5.392],[-16.507,-6.591,5.817],[-17.387,-7.212,6.761],[-15.797,-7.627,4.95],[-14.471,-7.151,4.504],[-13.944,-7.126,3.256],[-12.745,-6.668,3.121],[-12.414,-6.34,4.439],[-11.217,-5.785,4.966],[-10.194,-5.467,4.363],[-11.297,-5.613,6.342],[-12.391,-5.933,7.121],[-12.275,-5.693,8.427],[-13.521,-6.457,6.634],[-13.466,-6.634,5.294],[-18.871,-3.742,5.288],[-20.341,-3.627,5.418],[-18.187,-3.169,4.108],[-18.199,-3.121,6.612],[-18.792,-3.333,7.896],[-17.781,-3.128,9.023],[-16.605,-3.916,8.816],[-17.306,-1.682,9.092],[-18.127,-0.98,10.029],[-15.912,-1.81,9.675],[-15.943,-1.851,11.106],[-15.431,-3.132,9.088],[-14.648,-2.907,7.857],[-13.375,-2.374,7.994],[-12.934,-2.109,9.111],[-12.642,-2.157,6.868],[-13.136,-2.45,5.658],[-12.392,-2.224,4.576],[-14.449,-3,5.512],[-15.166,-3.212,6.632],[-18.497,0.569,9.79],[-19.733,0.871,10.547],[-18.436,0.841,8.337],[-17.272,1.335,10.499],[-16.952,1.077,11.868],[-15.461,1.268,12.142],[-14.661,0.516,11.226],[-15.039,2.716,11.951],[-15.173,3.4,13.2],[-13.563,2.592,11.625],[-12.767,2.525,12.813],[-13.505,1.283,10.841],[-13.503,1.542,9.383],[-12.287,1.808,8.776],[-11.233,1.833,9.408],[-12.325,2.044,7.415],[-13.455,2.038,6.616],[-13.371,2.261,5.41],[-14.679,1.753,7.33],[-14.668,1.519,8.664],[-15.436,4.988,13.237],[-15.899,5.35,14.595],[-16.253,5.349,12.057],[-13.957,5.593,13.03],[-12.831,4.997,13.682],[-11.566,5.103,12.831],[-11.781,4.611,11.511],[-11.136,6.546,12.648],[-10.373,7.014,13.766],[-10.288,6.464,11.387],[-8.922,6.166,11.696],[-10.941,5.33,10.595],[-11.726,5.867,9.463],[-11.031,6.256,8.325],[-9.808,6.143,8.282],[-11.739,6.758,7.276],[-13.071,6.875,7.339],[-13.733,7.372,6.294],[-13.792,6.476,8.508],[-13.084,5.98,9.541],["NaN","NaN","NaN"]],"colors":[[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.7529412,0.7960784,1],[1,0.7529412,0.7960784,1],[1,0.7529412,0.7960784,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,1,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0.6470588,0,1],[1,0,0,1],[1,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[1,0,0,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[1,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,1,1],[0,0,0,1],[0,0,0,1],[1,0.7529412,0.7960784,1]],"radii":[[0.612233]],"centers":[[-7.315,6.695,-1.77],[-6.027,7.312,-1.841],[-5.382,7.427,-0.46],[-5.995,8.462,0.314],[-5.556,6.146,0.348],[-4.401,5.324,0.15],[-5.551,6.643,1.782],[-4.218,6.743,2.298],[-6.208,8.014,1.662],[-7.648,7.933,1.97],[-8.712,7.912,1.13],[-9.888,7.834,1.654],[-9.59,7.798,3.02],[-10.46,7.712,4.139],[-11.688,7.651,4.148],[-9.753,7.702,5.335],[-8.379,7.766,5.447],[-7.886,7.743,6.686],[-7.552,7.846,4.399],[-8.219,7.858,3.222],[-7.682,5.633,-0.58],[-8.781,4.764,-1.176],[-8.131,6.477,0.607],[-4.547,3.725,0.024],[-3.56,3.247,-0.969],[-5.982,3.403,-0.146],[-4.085,3.214,1.481],[-2.921,3.758,2.116],[-3.153,3.99,3.608],[-4.335,4.762,3.836],[-3.371,2.678,4.35],[-2.108,2.216,4.838],[-4.219,3.101,5.534],[-3.41,3.582,6.614],[-5.077,4.213,4.939],[-6.38,3.685,4.492],[-6.838,3.449,3.238],[-8.033,2.974,3.118],[-8.431,2.876,4.455],[-9.613,2.437,5.061],[-10.664,1.994,4.372],[-9.67,2.473,6.404],[-8.629,2.914,7.113],[-7.465,3.352,6.643],[-7.431,3.306,5.296],[-1.73,0.653,4.766],[-0.258,0.529,4.868],[-2.443,0.056,3.615],[-2.381,0.072,6.119],[-1.825,0.408,7.394],[-2.85,0.248,8.515],[-4.051,0.968,8.23],[-3.277,-1.203,8.68],[-2.416,-1.826,9.638],[-4.663,-1.079,9.288],[-4.602,-0.979,10.716],[-5.193,0.207,8.659],[-6.083,-0.096,7.523],[-5.795,-0.208,6.202],[-6.767,-0.491,5.4],[-7.848,-0.584,6.282],[-9.214,-0.874,6.021],[-9.75,-1.11,4.94],[-9.969,-0.87,7.187],[-9.476,-0.618,8.452],[-10.359,-0.661,9.449],[-8.192,-0.344,8.707],[-7.437,-0.343,7.585],[-2.226,-3.424,9.644],[-1.184,-3.763,10.64],[-2.082,-3.879,8.243],[-3.644,-3.946,10.201],[-3.902,-3.981,11.607],[-5.362,-4.315,11.905],[-6.253,-3.514,11.125],[-5.692,-5.754,11.542],[-5.444,-6.583,12.681],[-7.189,-5.696,11.302],[-7.922,-5.822,12.526],[-7.368,-4.311,10.682],[-7.399,-4.399,9.203],[-8.636,-4.53,8.581],[-9.663,-4.569,9.256],[-8.671,-4.616,7.223],[-7.543,-4.574,6.502],[-7.613,-4.659,5.173],[-6.269,-4.439,7.136],[-6.243,-4.356,8.48],[-5.014,-8.122,12.488],[-4.878,-8.737,13.827],[-3.883,-8.172,11.535],[-6.306,-8.759,11.77],[-7.583,-8.72,12.41],[-8.721,-8.936,11.414],[-8.674,-7.984,10.35],[-8.621,-10.294,10.74],[-9.337,-11.248,11.528],[-9.373,-10.076,9.439],[-10.778,-10.298,9.605],[-9.076,-8.61,9.119],[-8.017,-8.497,8.097],[-6.71,-8.164,8.239],[-5.982,-8.128,7.174],[-6.906,-8.479,6.185],[-6.727,-8.62,4.783],[-5.702,-8.458,4.125],[-7.909,-8.988,4.152],[-9.117,-9.197,4.787],[-10.136,-9.564,4.01],[-9.294,-9.066,6.107],[-8.155,-8.708,6.743],[-8.543,-12.353,12.39],[-8.92,-12.189,13.812],[-7.117,-12.312,11.995],[-9.174,-13.737,11.857],[-9.946,-14.574,12.726],[-11.149,-15.176,12.002],[-11.929,-14.162,11.365],[-10.72,-16.126,10.895],[-10.669,-17.451,11.434],[-11.877,-16.05,9.916],[-12.909,-16.985,10.248],[-12.355,-14.611,10.07],[-11.795,-13.766,9.006],[-10.793,-12.857,9.062],[-10.493,-12.235,7.974],[-11.404,-12.793,7.072],[-11.64,-12.58,5.713],[-10.962,-11.699,4.993],[-12.611,-13.298,5.129],[-13.316,-14.176,5.837],[-13.182,-14.46,7.13],[-12.199,-13.726,7.692],[-10.087,-18.67,10.558],[-9.777,-19.791,11.473],[-9.037,-18.136,9.662],[-11.352,-19.09,9.656],[-12.499,-19.703,10.252],[-13.676,-19.752,9.278],[-13.948,-18.459,8.721],[-13.379,-20.652,8.085],[-13.833,-21.976,8.382],[-14.266,-20.065,7.006],[-15.613,-20.54,7.114],[-14.171,-18.574,7.305],[-13.071,-17.959,6.539],[-11.753,-17.855,6.843],[-10.986,-17.277,5.979],[-11.896,-16.951,4.968],[-11.75,-16.311,3.734],[-10.58,-15.863,3.28],[-12.855,-16.152,2.984],[-14.036,-16.596,3.419],[-14.287,-17.215,4.568],[-13.165,-17.362,5.302],[-12.833,-23.231,8.244],[-13.461,-24.399,8.901],[-11.48,-22.793,8.654],[-12.816,-23.496,6.655],[-13.922,-24.139,6.016],[-14.117,-23.64,4.585],[-14.194,-22.209,4.539],[-12.94,-24.018,3.693],[-13.236,-25.259,3.047],[-12.951,-22.915,2.655],[-13.912,-23.169,1.624],[-13.338,-21.709,3.497],[-12.14,-21.06,4.06],[-11.521,-21.268,5.248],[-10.469,-20.567,5.507],[-10.357,-19.785,4.353],[-9.393,-18.798,4.012],[-8.431,-18.409,4.672],[-9.644,-18.254,2.759],[-10.69,-18.61,1.931],[-10.759,-17.973,0.762],[-11.601,-19.536,2.244],[-11.377,-20.082,3.462],[-12.058,-26.306,2.716],[-12.67,-27.633,2.482],[-11,-26.152,3.739],[-11.488,-25.758,1.313],[-12.383,-25.431,0.245],[-11.879,-24.243,-0.57],[-11.563,-23.129,0.264],[-10.585,-24.568,-1.292],[-10.899,-25.154,-2.558],[-9.989,-23.192,-1.529],[-10.483,-22.609,-2.74],[-10.452,-22.408,-0.3],[-9.352,-22.272,0.673],[-9.127,-22.939,1.834],[-8.062,-22.636,2.497],[-7.497,-21.644,1.687],[-6.332,-20.877,1.8],[-5.478,-20.996,2.816],[-6.076,-19.99,0.821],[-6.914,-19.863,-0.21],[-8.042,-20.537,-0.416],[-8.276,-21.418,0.577],[-9.92,-26.253,-3.211],[-10.544,-26.747,-4.458],[-9.527,-27.21,-2.153],[-8.626,-25.379,-3.606],[-8.564,-24.711,-4.868],[-7.376,-23.754,-4.944],[-7.346,-22.863,-3.832],[-6.055,-24.496,-4.881],[-5.684,-24.885,-6.206],[-5.095,-23.42,-4.403],[-4.56,-22.672,-5.501],[-5.979,-22.546,-3.508],[-5.696,-22.814,-2.077],[-4.804,-21.974,-1.419],[-4.285,-21.036,-2.021],[-4.528,-22.22,-0.11],[-5.1,-23.246,0.533],[-4.805,-23.457,1.816],[-6.02,-24.114,-0.137],[-6.288,-23.864,-1.434],[-5.01,-26.323,-6.475],[-4.644,-26.402,-7.907],[-5.88,-27.361,-5.877],[-3.654,-26.242,-5.611],[-2.641,-25.289,-5.942],[-1.491,-25.315,-4.936],[-1.815,-24.583,-3.756],[-1.194,-26.728,-4.462],[-0.214,-27.304,-5.33],[-0.556,-26.505,-3.1],[0.864,-26.358,-3.206],[-1.217,-25.215,-2.612],[-2.228,-25.507,-1.579],[-3.512,-25.921,-1.718],[-4.195,-26.124,-0.642],[-3.262,-25.809,0.352],[-3.397,-25.831,1.766],[-4.382,-26.138,2.434],[-2.221,-25.443,2.396],[-1.056,-25.079,1.751],[-0.031,-24.737,2.532],[-0.921,-25.056,0.421],[-2.055,-25.43,-0.215],[0.136,-28.873,-5.24],[1.047,-29.21,-6.357],[-1.13,-29.621,-5.069],[0.969,-28.971,-3.864],[1.379,-30.241,-3.348],[2.732,-30.152,-2.644],[3.79,-29.916,-3.573],[2.784,-28.98,-1.677],[2.318,-29.418,-0.398],[4.273,-28.698,-1.579],[4.894,-29.51,-0.576],[4.776,-29.054,-2.977],[4.976,-27.836,-3.786],[4.157,-27.253,-4.696],[4.575,-26.174,-5.269],[5.829,-26.006,-4.673],[6.829,-25.04,-4.825],[6.725,-24.008,-5.664],[7.941,-25.176,-4.081],[8.066,-26.202,-3.236],[7.184,-27.172,-3.014],[6.08,-27.013,-3.77],[1.361,-28.473,0.49],[0.752,-29.302,1.554],[0.497,-27.698,-0.428],[2.405,-27.457,1.178],[3.37,-27.937,2.118],[4.63,-27.074,2.125],[5.158,-26.91,0.808],[4.34,-25.668,2.624],[4.553,-25.639,4.039],[5.425,-24.839,1.96],[6.608,-24.786,2.766],[5.677,-25.579,0.652],[5.041,-24.891,-0.487],[3.827,-25.087,-1.056],[3.531,-24.372,-2.091],[4.687,-23.597,-2.236],[5.058,-22.607,-3.153],[4.27,-22.205,-4.15],[6.273,-22.047,-3.003],[7.077,-22.436,-2.011],[6.828,-23.362,-1.092],[5.608,-23.907,-1.262],[3.448,-25.006,5.024],[3.619,-25.612,6.363],[2.133,-25.07,4.347],[3.897,-23.46,5.108],[5.236,-23.102,5.473],[5.753,-21.938,4.628],[5.817,-22.296,3.242],[4.824,-20.729,4.708],[5.322,-19.834,5.706],[4.998,-20.077,3.352],[6.136,-19.208,3.327],[5.194,-21.281,2.443],[3.905,-21.752,1.905],[2.923,-22.467,2.507],[1.882,-22.762,1.802],[2.203,-22.179,0.572],[1.53,-22.115,-0.651],[0.33,-22.658,-0.853],[2.139,-21.465,-1.658],[3.34,-20.912,-1.474],[4.062,-20.91,-0.362],[3.433,-21.565,0.629],[4.322,-18.841,6.487],[5.137,-17.854,7.23],[3.322,-19.662,7.205],[3.574,-18.073,5.284],[4.262,-17.08,4.518],[3.599,-16.854,3.159],[3.421,-18.086,2.459],[2.203,-16.268,3.304],[2.299,-14.841,3.282],[1.515,-16.72,2.029],[1.735,-15.795,0.958],[2.173,-18.069,1.746],[1.295,-19.173,2.177],[1.278,-19.867,3.342],[0.374,-20.779,3.482],[-0.306,-20.696,2.263],[-1.419,-21.441,1.786],[-2.039,-22.337,2.356],[-1.791,-21.04,0.509],[-1.172,-20.047,-0.225],[-1.669,-19.811,-1.439],[-0.126,-19.343,0.216],[0.254,-19.715,1.459],[1.015,-13.93,3.626],[1.468,-12.529,3.772],[0.266,-14.581,4.724],[0.132,-14.037,2.282],[0.587,-13.436,1.067],[-0.246,-13.883,-0.134],[-0.335,-15.31,-0.208],[-1.684,-13.399,-0.034],[-1.783,-12.111,-0.648],[-2.421,-14.405,-0.897],[-2.339,-14.066,-2.286],[-1.67,-15.697,-0.59],[-2.341,-16.442,0.504],[-3.255,-17.428,0.159],[-3.509,-17.701,-1.011],[-3.867,-18.086,1.211],[-3.65,-17.851,2.558],[-4.252,-18.498,3.412],[-2.683,-16.81,2.826],[-2.07,-16.15,1.814],[-2.895,-11.057,-0.149],[-2.703,-9.794,-0.895],[-2.894,-11.049,1.331],[-4.269,-11.733,-0.648],[-4.45,-12.069,-2.026],[-5.498,-13.163,-2.213],[-5.228,-14.295,-1.394],[-6.88,-12.698,-1.793],[-7.514,-12.086,-2.92],[-7.599,-14.005,-1.487],[-8.265,-14.518,-2.646],[-6.466,-14.932,-1.039],[-6.529,-15.171,0.417],[-7.4,-16.149,0.878],[-8.097,-16.78,0.084],[-7.46,-16.38,2.218],[-6.699,-15.681,3.07],[-6.781,-15.933,4.376],[-5.802,-14.672,2.597],[-5.75,-14.45,1.273],[-8.981,-11.436,-2.783],[-9.796,-11.886,-3.933],[-8.823,-9.99,-2.51],[-9.555,-12.14,-1.453],[-10.713,-12.976,-1.516],[-11.474,-12.983,-0.19],[-10.731,-13.661,0.83],[-11.712,-11.567,0.327],[-13.02,-11.153,-0.075],[-11.709,-11.741,1.835],[-13.014,-12.076,2.321],[-10.73,-12.892,2.043],[-9.367,-12.413,2.361],[-8.507,-11.667,1.621],[-7.357,-11.391,2.138],[-7.44,-12.026,3.38],[-6.487,-12.098,4.431],[-5.361,-11.606,4.475],[-6.968,-12.835,5.507],[-8.211,-13.432,5.569],[-8.496,-14.09,6.694],[-9.112,-13.37,4.584],[-8.667,-12.655,3.525],[-13.405,-9.59,-0.116],[-13.15,-9.086,-1.484],[-12.772,-8.927,1.046],[-14.999,-9.616,0.124],[-15.768,-10.794,-0.15],[-16.648,-11.178,1.038],[-15.896,-11.877,2.029],[-17.214,-9.949,1.736],[-18.505,-9.674,1.185],[-17.396,-10.412,3.172],[-18.696,-10.977,3.376],[-16.3,-11.462,3.343],[-15.156,-10.916,4.097],[-14.133,-10.132,3.676],[-13.243,-9.792,4.549],[-13.724,-10.426,5.701],[-13.256,-10.488,7.019],[-12.14,-9.887,7.43],[-13.977,-11.203,7.899],[-15.091,-11.823,7.512],[-15.625,-11.833,6.296],[-14.887,-11.11,5.431],[-19.177,-8.223,1.371],[-19.779,-8.16,2.721],[-20.007,-7.94,0.179],[-17.9,-7.244,1.341],[-17.731,-6.236,2.34],[-17.656,-6.839,3.744],[-16.654,-7.86,3.822],[-17.277,-5.789,4.787],[-18.477,-5.3,5.392],[-16.507,-6.591,5.817],[-17.387,-7.212,6.761],[-15.797,-7.627,4.95],[-14.471,-7.151,4.504],[-13.944,-7.126,3.256],[-12.745,-6.668,3.121],[-12.414,-6.34,4.439],[-11.217,-5.785,4.966],[-10.194,-5.467,4.363],[-11.297,-5.613,6.342],[-12.391,-5.933,7.121],[-12.275,-5.693,8.427],[-13.521,-6.457,6.634],[-13.466,-6.634,5.294],[-18.871,-3.742,5.288],[-20.341,-3.627,5.418],[-18.187,-3.169,4.108],[-18.199,-3.121,6.612],[-18.792,-3.333,7.896],[-17.781,-3.128,9.023],[-16.605,-3.916,8.816],[-17.306,-1.682,9.092],[-18.127,-0.98,10.029],[-15.912,-1.81,9.675],[-15.943,-1.851,11.106],[-15.431,-3.132,9.088],[-14.648,-2.907,7.857],[-13.375,-2.374,7.994],[-12.934,-2.109,9.111],[-12.642,-2.157,6.868],[-13.136,-2.45,5.658],[-12.392,-2.224,4.576],[-14.449,-3,5.512],[-15.166,-3.212,6.632],[-18.497,0.569,9.79],[-19.733,0.871,10.547],[-18.436,0.841,8.337],[-17.272,1.335,10.499],[-16.952,1.077,11.868],[-15.461,1.268,12.142],[-14.661,0.516,11.226],[-15.039,2.716,11.951],[-15.173,3.4,13.2],[-13.563,2.592,11.625],[-12.767,2.525,12.813],[-13.505,1.283,10.841],[-13.503,1.542,9.383],[-12.287,1.808,8.776],[-11.233,1.833,9.408],[-12.325,2.044,7.415],[-13.455,2.038,6.616],[-13.371,2.261,5.41],[-14.679,1.753,7.33],[-14.668,1.519,8.664],[-15.436,4.988,13.237],[-15.899,5.35,14.595],[-16.253,5.349,12.057],[-13.957,5.593,13.03],[-12.831,4.997,13.682],[-11.566,5.103,12.831],[-11.781,4.611,11.511],[-11.136,6.546,12.648],[-10.373,7.014,13.766],[-10.288,6.464,11.387],[-8.922,6.166,11.696],[-10.941,5.33,10.595],[-11.726,5.867,9.463],[-11.031,6.256,8.325],[-9.808,6.143,8.282],[-11.739,6.758,7.276],[-13.071,6.875,7.339],[-13.733,7.372,6.294],[-13.792,6.476,8.508],[-13.084,5.98,9.541],["NaN","NaN","NaN"]],"ignoreExtent":false,"flags":3},"8":{"id":8,"type":"text","material":{"lit":false},"vertices":[[-6.1375,-37.83762,-12.32369]],"colors":[[0,0,0,1]],"texts":[[""]],"cex":[[1]],"adj":[[0.5,0.5]],"centers":[[-6.1375,-37.83762,-12.32369]],"family":[["sans"]],"font":[[1]],"ignoreExtent":true,"flags":40},"9":{"id":9,"type":"text","material":{"lit":false},"vertices":[[-25.91673,-10.8895,-12.32369]],"colors":[[0,0,0,1]],"texts":[[""]],"cex":[[1]],"adj":[[0.5,0.5]],"centers":[[-25.91673,-10.8895,-12.32369]],"family":[["sans"]],"font":[[1]],"ignoreExtent":true,"flags":40},"10":{"id":10,"type":"text","material":{"lit":false},"vertices":[[-25.91673,-37.83762,3.344]],"colors":[[0,0,0,1]],"texts":[[""]],"cex":[[1]],"adj":[[0.5,0.5]],"centers":[[-25.91673,-37.83762,3.344]],"family":[["sans"]],"font":[[1]],"ignoreExtent":true,"flags":40},"5":{"id":5,"type":"light","vertices":[[0,0,1]],"colors":[[1,1,1,1],[1,1,1,1],[1,1,1,1]],"viewpoint":true,"finite":false},"4":{"id":4,"type":"background","material":{"fog":true},"colors":[[0.2980392,0.2980392,0.2980392,1]],"centers":[[0,0,0]],"sphere":false,"fogtype":"none","flags":0},"6":{"id":6,"type":"background","material":{"lit":false,"back":"lines"},"colors":[[1,1,1,1]],"centers":[[0,0,0]],"sphere":false,"fogtype":"none","flags":0},"1":{"id":1,"type":"subscene","par3d":{"antialias":8,"FOV":30,"ignoreExtent":false,"listeners":1,"mouseMode":{"left":"trackball","right":"zoom","middle":"fov","wheel":"pull"},"observer":[0,0,106.5257],"modelMatrix":[[1.07761,0,0,6.613828],[0,0.2705166,1.278355,-1.329028],[0,-0.7432381,0.4652832,-116.1751],[0,0,0,1]],"projMatrix":[[3.732051,0,0,0],[0,3.732051,0,0],[0,0,-3.863703,-384.0129],[0,0,-1,0]],"skipRedraw":false,"userMatrix":[[1,0,0,0],[0,0.3420201,0.9396926,0],[0,-0.9396926,0.3420201,0],[0,0,0,1]],"scale":[1.07761,0.7909375,1.360397],"viewport":{"x":0,"y":0,"width":1,"height":1},"zoom":1,"bbox":[-20.90914,8.63414,-31.01506,9.23606,-8.35704,15.04504],"windowRect":[100,100,604,604],"family":"sans","font":1,"cex":1,"useFreeType":true,"fontname":"/home/cosi/R/x86_64-pc-linux-gnu-library/3.3/rgl/fonts/FreeSans.ttf","maxClipPlanes":8},"embeddings":{"viewport":"replace","projection":"replace","model":"replace"},"objects":[6,7,8,9,10,5],"subscenes":[],"flags":1067}},"snapshot":"data:image/png;base64,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","width":505,"height":505,"sphereVerts":{"vb":[[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0.07465783,0.1464466,0.2126075,0.2705981,0.3181896,0.3535534,0.3753303,0.3826834,0.3753303,0.3535534,0.3181896,0.2705981,0.2126075,0.1464466,0.07465783,0,0,0.1379497,0.2705981,0.3928475,0.5,0.5879378,0.6532815,0.6935199,0.7071068,0.6935199,0.6532815,0.5879378,0.5,0.3928475,0.2705981,0.1379497,0,0,0.18024,0.3535534,0.51328,0.6532815,0.7681778,0.8535534,0.9061274,0.9238795,0.9061274,0.8535534,0.7681778,0.6532815,0.51328,0.3535534,0.18024,0,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,0.9807853,0.9238795,0.8314696,0.7071068,0.5555702,0.3826834,0.1950903,0,0,0.18024,0.3535534,0.51328,0.6532815,0.7681778,0.8535534,0.9061274,0.9238795,0.9061274,0.8535534,0.7681778,0.6532815,0.51328,0.3535534,0.18024,0,0,0.1379497,0.2705981,0.3928475,0.5,0.5879378,0.6532815,0.6935199,0.7071068,0.6935199,0.6532815,0.5879378,0.5,0.3928475,0.2705981,0.1379497,0,0,0.07465783,0.1464466,0.2126075,0.2705981,0.3181896,0.3535534,0.3753303,0.3826834,0.3753303,0.3535534,0.3181896,0.2705981,0.2126075,0.1464466,0.07465783,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,-0,-0.07465783,-0.1464466,-0.2126075,-0.2705981,-0.3181896,-0.3535534,-0.3753303,-0.3826834,-0.3753303,-0.3535534,-0.3181896,-0.2705981,-0.2126075,-0.1464466,-0.07465783,-0,-0,-0.1379497,-0.2705981,-0.3928475,-0.5,-0.5879378,-0.6532815,-0.6935199,-0.7071068,-0.6935199,-0.6532815,-0.5879378,-0.5,-0.3928475,-0.2705981,-0.1379497,-0,-0,-0.18024,-0.3535534,-0.51328,-0.6532815,-0.7681778,-0.8535534,-0.9061274,-0.9238795,-0.9061274,-0.8535534,-0.7681778,-0.6532815,-0.51328,-0.3535534,-0.18024,-0,-0,-0.1950903,-0.3826834,-0.5555702,-0.7071068,-0.8314696,-0.9238795,-0.9807853,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,-0,-0,-0.18024,-0.3535534,-0.51328,-0.6532815,-0.7681778,-0.8535534,-0.9061274,-0.9238795,-0.9061274,-0.8535534,-0.7681778,-0.6532815,-0.51328,-0.3535534,-0.18024,-0,-0,-0.1379497,-0.2705981,-0.3928475,-0.5,-0.5879378,-0.6532815,-0.6935199,-0.7071068,-0.6935199,-0.6532815,-0.5879378,-0.5,-0.3928475,-0.2705981,-0.1379497,-0,-0,-0.07465783,-0.1464466,-0.2126075,-0.2705981,-0.3181896,-0.3535534,-0.3753303,-0.3826834,-0.3753303,-0.3535534,-0.3181896,-0.2705981,-0.2126075,-0.1464466,-0.07465783,-0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],[-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1],[0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,0.9807853,0.9238795,0.8314696,0.7071068,0.5555702,0.3826834,0.1950903,0,0,0.18024,0.3535534,0.51328,0.6532815,0.7681778,0.8535534,0.9061274,0.9238795,0.9061274,0.8535534,0.7681778,0.6532815,0.51328,0.3535534,0.18024,0,0,0.1379497,0.2705981,0.3928475,0.5,0.5879378,0.6532815,0.6935199,0.7071068,0.6935199,0.6532815,0.5879378,0.5,0.3928475,0.2705981,0.1379497,0,0,0.07465783,0.1464466,0.2126075,0.2705981,0.3181896,0.3535534,0.3753303,0.3826834,0.3753303,0.3535534,0.3181896,0.2705981,0.2126075,0.1464466,0.07465783,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,-0,-0.07465783,-0.1464466,-0.2126075,-0.2705981,-0.3181896,-0.3535534,-0.3753303,-0.3826834,-0.3753303,-0.3535534,-0.3181896,-0.2705981,-0.2126075,-0.1464466,-0.07465783,-0,-0,-0.1379497,-0.2705981,-0.3928475,-0.5,-0.5879378,-0.6532815,-0.6935199,-0.7071068,-0.6935199,-0.6532815,-0.5879378,-0.5,-0.3928475,-0.2705981,-0.1379497,-0,-0,-0.18024,-0.3535534,-0.51328,-0.6532815,-0.7681778,-0.8535534,-0.9061274,-0.9238795,-0.9061274,-0.8535534,-0.7681778,-0.6532815,-0.51328,-0.3535534,-0.18024,-0,-0,-0.1950903,-0.3826834,-0.5555702,-0.7071068,-0.8314696,-0.9238795,-0.9807853,-1,-0.9807853,-0.9238795,-0.8314696,-0.7071068,-0.5555702,-0.3826834,-0.1950903,-0,-0,-0.18024,-0.3535534,-0.51328,-0.6532815,-0.7681778,-0.8535534,-0.9061274,-0.9238795,-0.9061274,-0.8535534,-0.7681778,-0.6532815,-0.51328,-0.3535534,-0.18024,-0,-0,-0.1379497,-0.2705981,-0.3928475,-0.5,-0.5879378,-0.6532815,-0.6935199,-0.7071068,-0.6935199,-0.6532815,-0.5879378,-0.5,-0.3928475,-0.2705981,-0.1379497,-0,-0,-0.07465783,-0.1464466,-0.2126075,-0.2705981,-0.3181896,-0.3535534,-0.3753303,-0.3826834,-0.3753303,-0.3535534,-0.3181896,-0.2705981,-0.2126075,-0.1464466,-0.07465783,-0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0.07465783,0.1464466,0.2126075,0.2705981,0.3181896,0.3535534,0.3753303,0.3826834,0.3753303,0.3535534,0.3181896,0.2705981,0.2126075,0.1464466,0.07465783,0,0,0.1379497,0.2705981,0.3928475,0.5,0.5879378,0.6532815,0.6935199,0.7071068,0.6935199,0.6532815,0.5879378,0.5,0.3928475,0.2705981,0.1379497,0,0,0.18024,0.3535534,0.51328,0.6532815,0.7681778,0.8535534,0.9061274,0.9238795,0.9061274,0.8535534,0.7681778,0.6532815,0.51328,0.3535534,0.18024,0,0,0.1950903,0.3826834,0.5555702,0.7071068,0.8314696,0.9238795,0.9807853,1,0.9807853,0.9238795,0.8314696,0.7071068,0.5555702,0.3826834,0.1950903,0]],"it":[[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,119,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,136,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,153,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,170,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,187,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,204,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,221,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,238,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,255,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270,0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,119,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,136,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,153,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,170,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,187,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,204,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,221,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,238,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,255,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270],[17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,119,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,136,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,153,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,170,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,187,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,204,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,221,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,238,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,255,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270,272,273,274,275,276,277,278,279,280,281,282,283,284,285,286,287,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,135,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,152,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,169,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,186,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,203,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,220,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,237,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,254,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270,271,273,274,275,276,277,278,279,280,281,282,283,284,285,286,287,288],[18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,135,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,152,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,169,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,186,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,203,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,220,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,237,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,254,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270,271,273,274,275,276,277,278,279,280,281,282,283,284,285,286,287,288,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,135,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,152,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,169,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,186,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,203,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,220,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,237,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,254,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270,271]],"primitivetype":"triangle","material":null,"normals":null,"texcoords":[[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.0625,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.125,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.1875,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.25,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.3125,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.4375,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.5625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.625,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.6875,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.75,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.8125,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.875,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,0.9375,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],[0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1,0,0.0625,0.125,0.1875,0.25,0.3125,0.375,0.4375,0.5,0.5625,0.625,0.6875,0.75,0.8125,0.875,0.9375,1]]}});
unnamed_chunk_1rgl.prefix = "unnamed_chunk_1";
</script>
<p id="unnamed_chunk_1debug">
You must enable Javascript to view this page properly.</p>
<script>unnamed_chunk_1rgl.start();</script>

--- .class #id 

## Slide 2



