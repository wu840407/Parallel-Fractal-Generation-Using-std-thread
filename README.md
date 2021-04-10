# Parallel-Fractal-Generation-Using-std-thread

**2.1 Problem Statement**
```
$ cd <your_workplace>
$ wget https://nctu-sslab.github.io/PP-s21/HW2/HW2_part2.zip
$ unzip HW2_part2.zip -d part2
```
Build and run the code in the part2 directory of the code base. (Type make to build, and ./mandelbrot to run it. ./mandelbrot --help displays the usage information.)

This program produces the image file mandelbrot-serial.ppm, which is a visualization of a famous set of complex numbers called the Mandelbrot set. [Most platforms have a .ppm viewer. For example, to view the resulting images, use tiv command (already installed) to display them on the terminal.]

As you can see in the images below, the result is a familiar and beautiful fractal. Each pixel in the image corresponds to a value in the complex plane, and the brightness of each pixel is proportional to the computational cost of determining whether the value is contained in the Mandelbrot set. To get image 2, use the command option --view 2. (See function mandelbrotSerial() defined in mandelbrotSerial.cpp). You can learn more about the definition of the Mandelbrot set(http://en.wikipedia.org/wiki/Mandelbrot_set).


Your job is to parallelize the computation of the images using std::thread. Starter code that spawns one additional thread is provided in the function mandelbrotThread() located in mandelbrotThread.cpp. In this function, the main application thread creates another additional thread using the constructor std::thread (function, args…). It waits for this thread to complete by calling join on the thread object.

Currently the launched thread does not do any computation and returns immediately. You should add code to workerThreadStart function to accomplish this task. You will not need to make use of any other std::thread API calls in this assignment.

**2.2 Requirements**


1. Modify the starter code to parallelize the Mandelbrot generation using two processors. Specifically, compute the top half of the image in thread 0, and the bottom half of the image in thread 1. This type of problem decomposition is referred to as spatial decomposition since different spatial regions of the image are computed by different processors.
2. Extend your code to use 2, 3, 4 threads, partitioning the image generation work accordingly (threads should get blocks of the image). Q1: In your write-up, produce a graph of speedup compared to the reference sequential implementation as a function of the number of threads used FOR VIEW 1. Is speedup linear in the number of threads used? In your writeup hypothesize why this is (or is not) the case? (You may also wish to produce a graph for VIEW 2 to help you come up with a good answer. Hint: take a careful look at the three-thread data-point.)
3. To confirm (or disprove) your hypothesis, measure the amount of time each thread requires to complete its work by inserting timing code at the beginning and end of workerThreadStart(). Q2: How do your measurements explain the speedup graph you previously created?
4. Modify the mapping of work to threads to achieve to improve speedup to at about 3-4x on both views of the Mandelbrot set (if you’re above 3.5x that’s fine, don’t sweat it). You may not use any synchronization between threads in your solution. We are expecting you to come up with a single work decomposition policy that will work well for all thread counts—hard coding a solution specific to each configuration is not allowed! (Hint: There is a very simple static assignment that will achieve this goal, and no communication/synchronization among threads is necessary.). Q3: In your write-up, describe your approach to parallelization and report the final 4-thread speedup obtained.
5. Q4: Now run your improved code with eight threads. Is performance noticeably greater than when running with four threads? Why or why not? (Notice that the workstation server provides 4 cores 4 threads.)
