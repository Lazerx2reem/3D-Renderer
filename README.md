# 3D-Renderer

First of all, we want to put at least something on screen. For that we will use an application with our rendered image and two sliders to adjust its rotation.

<img width="401" alt="Screenshot 2024-09-12 at 4 41 37 PM" src="https://github.com/user-attachments/assets/0ebb994d-18d1-4a7d-bc05-e66316c2029c">

DemoViewer.java makes the base GUI

Vertex is a structure to store our three coordinates (X, Y and Z), and triangle binds together three vertices and stores its color.

<img width="525" alt="Screenshot 2024-09-12 at 4 42 55 PM" src="https://github.com/user-attachments/assets/d2e900c0-6cd4-4152-b4a4-1219ca8aba63">

We assume that X coordinate means movement in left-right direction, Y means movement up-down on screen, and Z will be depth (so Z axis is perpendicular to your screen). Positive Z will mean "towards the observer".

After we add the Traingles we get:

<img width="403" alt="Screenshot 2024-09-12 at 4 45 55 PM" src="https://github.com/user-attachments/assets/2fd3b1fb-2bb2-4213-9353-07fa185fb110">

To add rotations we will use the concept of matrices.

<img width="638" alt="Screenshot 2024-09-12 at 4 56 20 PM" src="https://github.com/user-attachments/assets/883dea5c-781d-43db-bf7c-c33248dbc31b">

We create utility class Matrix3 that will handle matrix-matrix and vector-matrix multiplication.

The horizontal slider would control "heading" - in our case, rotation in XZ direction (left-right), and vertical slider will control "pitch" - rotation in YZ direction (up-down). We create our rotation matrix and add it to the code.

https://github.com/user-attachments/assets/393c79a9-c25b-4aee-8260-ede69a7c8c0c

We now work on the Y axis rotation 

<img width="508" alt="Screenshot 2024-09-12 at 5 02 57 PM" src="https://github.com/user-attachments/assets/52efd133-c787-4c13-a7d2-e9ab2a66935d">

The result looks like this:

https://github.com/user-attachments/assets/2bc62c70-2750-4e29-83f8-cd1c010dfcc2

We now use a simple method called rasterization. We build an intermediate array during rasterization that will store depth of last seen element at any given pixel. This concept is called z-buffer. The resultant is:

https://github.com/user-attachments/assets/96a76710-cdc4-4402-8ea6-f87db58a3458

We now work on perception based shadows. In computer graphics, we can achieve similar effect by using so-called "shading" - altering the color of the surface based on its angle and distance to lights. Now we calculate cosine between triangle normal and light direction. For simplicity, we will assume that our light is positioned directly behind the camera at some infinite distance so our light source direction will be  [ 0, 0, 1]

<img width="287" alt="Screenshot 2024-09-12 at 5 24 00 PM" src="https://github.com/user-attachments/assets/b0743329-f430-4da4-921d-e498f569f8c7">

Now that we have our shade coefficient, we can apply it to triangle color. First we make a simple version of it:

<img width="481" alt="Screenshot 2024-09-12 at 5 25 02 PM" src="https://github.com/user-attachments/assets/96da4014-884c-4676-a532-6cca2bc53242">

While it will give us some shading effect, it will have much quicker falloff than we need. That happens because Java uses sRGB color space, which is already scaled to match our logarithmic color perception. So we need to convert each color from scaled to linear format, apply shade, and then convert back to scaled format.

<img width="535" alt="Screenshot 2024-09-12 at 5 25 52 PM" src="https://github.com/user-attachments/assets/d2659e6e-ffa6-436a-9727-14eab196dd92">

The final result of the tetrahedron looks like this:

https://github.com/user-attachments/assets/ce629781-1652-4ef6-90a6-ad9b2b5fd5ca

We can also quickly create a sphere approximation from this tetrahedron. It can be done by repeatedly subdividing each triangle into four smaller ones and "inflating":

<img width="773" alt="Screenshot 2024-09-12 at 5 28 03 PM" src="https://github.com/user-attachments/assets/4cefe7ed-2695-4b37-9fce-11ee5c18d9a5">

The real final result looks like this:


https://github.com/user-attachments/assets/4b7c7ab9-2c63-42d7-beba-1f1462560f92




