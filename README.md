# 3D-Renderer

First of all, we want to put at least something on screen. For that we will use an application with our rendered image and two sliders to adjust its rotation.

DemoViewer.java makes the base GUI

Vertex is a structure to store our three coordinates (X, Y and Z), and triangle binds together three vertices and stores its color.

We assume that X coordinate means movement in left-right direction, Y means movement up-down on screen, and Z will be depth (so Z axis is perpendicular to your screen). Positive Z will mean "towards the observer".

To add rotations we will matrices.

We create utility class Matrix3 that will handle matrix-matrix and vector-matrix multiplication.

The horizontal slider would control "heading" - in our case, rotation in XZ direction (left-right), and vertical slider will control "pitch" - rotation in YZ direction (up-down). We create our rotation matrix and add it to the code.

We now work on the Y axis rotation 

We now use a simple method called rasterization

We build an intermediate array during rasterization that will store depth of last seen element at any given pixel. This concept is called z-buffer.

We now work on perception based shadows. In computer graphics, we can achieve similar effect by using so-called "shading" - altering the color of the surface based on its angle and distance to lights.
