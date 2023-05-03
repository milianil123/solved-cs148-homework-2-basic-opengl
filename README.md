Download Link: https://assignmentchef.com/product/solved-cs148-homework-2-basic-opengl
<br>
Introduction to Computer Graphics and Imaging

In Lecture 3, we discussed the homogeneous coordinate system appearing often in computer graphics. In the first part of this assignment, we will see how homogeneous coordinates simplify the process of computing camera transformations.

First, a quick warm-up:

<strong>Problem 1 </strong>(10 points)<strong>. </strong>(a) Give two different homogeneous expressions for the point (x, y, z) = (3, −2, 7). (b) Convert (5, −10, 15; −5) to standard coordinates. (c) Explain what the homogeneous point (1, 2, 3; 0) represents. (d) Give a homogeneous transformation matrix translating (4, −2, 5) to the origin.

Now, let’s continue with the task at hand: finding a matrix converting points in <strong>R</strong><sup>3 </sup>(really projective space <strong>P</strong><sup>3</sup>, meaning they are represented with four numbers as we saw in Problem 1) to so-called normalized device coordinates. Our first job is to take the camera from an arbitrary location and orientation in space to a convenient canonical position and orientation.

<strong>Problem 2 </strong>(20 points)<strong>. </strong>Suppose that the camera is located at eye position ~e = (e<sub>x</sub>, e<sub>y</sub>, e<sub>z</sub>). Furthermore, assume the camera has gaze direction ~g = (g<sub>x</sub>, g<sub>y</sub>, g<sub>z</sub>) and up vector <sup>~</sup>t = (t<sub>x</sub>, t<sub>y</sub>, t<sub>z</sub>); assume . Find an expression for the matrix M<sub>cam </sub>translating~e to the origin and rotating so that ~g

points down the −z axis and~t points up the +y axis; your expression can contain intermediate variables, matrix inverses, cross products, variables you labeled earlier, or anything else convenient.

<strong>Comprehensive hint: </strong>This is a tricky problem, so let’s break it down. First, remember that points in <strong>R</strong><sup>3 </sup>are become sets of four numbers (x, y, z; 1) in projective space <strong>P</strong><sup>3 </sup>and that directions can be expressed as (x, y, z; 0). A reasonable set of steps to get to the solution is to do the following:

<ol>

 <li>Write a vector representing the product M<sub>cam </sub>(e<sub>x</sub>, e<sub>y</sub>, e<sub>z</sub>; 1); note that your answer isn’t unique since it could be multiplied by a constant (that is, the points (x, y, z; w) and (ax, ay, az; aw) are the same in projective space), but this degree of freedom actually can be ignored for this problem.</li>

 <li>Write a vector representing the product M<sub>cam </sub> (t<sub>x</sub>, t<sub>y</sub>, t<sub>z</sub>; 0).</li>

 <li>Write a vector representing the product M<sub>cam </sub> (g<sub>x</sub>, g<sub>y</sub>, g<sub>z</sub>; 0).</li>

 <li>Define ~u =~t ×~ Write a vector representing the product M<sub>cam </sub>· (u<sub>x</sub>, u<sub>y</sub>, u<sub>z</sub>; 0). Drawing a picture may help here – remember the right-hand rule!</li>

 <li>Combining your answers to the last few steps, write a matrix equation of the form M<sub>cam</sub>U = V, for U, V ∈ <strong>R</strong><sup>4</sup><sup>×</sup><sup>4 </sup>constructed from the vectors we’ve computed and defined above.</li>

 <li>Use a matrix inverse to get an expression for M<sub>cam</sub>. You don’t need to simplify here, although it turns out that the simplified expression is fairly nice.</li>

</ol>

Figure 1: For problem 3.

We now can assume that we have applied M<sub>cam</sub>, so our camera is located at the origin (0, 0, 0) and is pointed down the −z axis. Next, we’ll implement a perspective matrix that converts these coordinates to image coordinates. We’re not going to worry about depth computation here; we will discuss an interesting nonlinearity involved in depth computation during Lecture 4.

<strong>Problem 3 </strong>(20 points)<strong>. </strong>Write a 3 × 4 matrix M<sub>persp </sub>that takes a point (x, y, z; w) in canonical camera coordinates above and yields a point (x<sup>0</sup>, y<sup>0</sup>; w<sup>0</sup>) on the image plane [−1, 1] × [−1, 1]. In particular, the square marked in Figure 1 centered on the −z axis at distance d from the origin should be mapped to [−1, 1] × [−1, 1], as should lines from the origin through this square.

<strong>Hint: </strong>First work out the projection formula in inhomogeneous coordinates without using matrices, and then figure out how to homogenize and convert to matrix form.

Finally, we can combine these matrices to get the transformation directly from world coordinates to the image plane.

<strong>Problem 4 </strong>(10 points)<strong>. </strong>Write such a transformation matrix P in terms of M<sub>persp </sub>and M<sub>cam</sub>.

Now that you understand the theory of transformations, we’ll spend the rest of this assignment making use of OpenGL’s built-in capabilities to compose and construct transformations. We have two objectives here: for you to be exposed to basic OpenGL, and for you to get more practice formulating linear transformations.

In this assignment, we will make use of the GLUT (“GL Utility Toolkit”) library to make it easier to write OpenGL code. GLUT is a simple platform-independent way to set up a window and make callbacks for keyboards, mice, timers, and so on. We have provided the GLUT code you need in the starter code, but you should take a look to make sure you understand what it’s giving you. We also have set up a simple camera pointing at the origin, where the left mouse button rotates about the y axis and the right mouse button zooms. You can use the keyboard to switch between displays for each of the problems.

<strong>Problem 5 </strong>(40 points)<strong>. </strong>Fill in problem1, problem2, and problem3 in the skeleton code provided on the course website to reproduce the images shown in Figure 2. We’re not worried about 100% pixel-perfect reproductions of the images, but do try your best to get close. You should produce these images using the glutSolidTeapot and glutSolidCube functions (do not add your own geometry!), combined with OpenGL’s transformation mechanisms, including glPushMatrix, glPopMatrix, glTranslatef, and so

(a) problem1                                                (b) problem2                                                (c) problem3

Figure 2: For problem 5.

<ol>

 <li>You may need to look ahead to Lecture 5 if you begin programming this assignment early. To receive full credit, you should use and compose transformations in a way to get the scene cleanly.</li>

</ol>

Finally, fill in problem4 to render an interesting scene of your choosing. Your scene at the least should:

<ol>

 <li>Make use of OpenGL’s transformation mechanisms in a nontrivial way, with at least one instance ofnested applications of glPushMatrix.</li>

 <li>Render at least one triangle by feeding in its coordinates directly (OpenGL immediate mode is OKhere, even though it’s deprecated)</li>

 <li>Entertain the instructor and/or course assistant</li>

</ol>

The best submissions will be shown in class.