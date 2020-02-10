# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

## Basic Build Instructions

1. Make a build directory: `mkdir build && cd build`
2. Compile: `cmake .. && make`
3. Run it: `./pid`. 

## Reflection

### PID controller implementation

The PID controller consists of Proportional(P), Integration(I) and Differential(D) controllers.

* the P control in this application steers against the Cross-track error(CTE),
* the D control steers against overshoots and oscillations imported by P control,
* the I control helps steering to the inner circle of the curve when turning.

### PID coefficients optimization

The PID parameters are chosen manually by several attempts, the details are shown in table below.

|     Kp     |     Ki     |     Kd    |   Result  |   
|:--------------:|:--------------:|:-------------:|:----------:|
|    1.0      |     0.0     |   0.0    |   Overshoot |
|    0.5      |     0.0     |   0.0    |   Overshoot |
|  **0.25**   |     0.0     |   0.0    |   Overshoot |
|    0.125     |     0.0     |   0.0    |   Lack of steering |
| | | | |
|    0.25      |     0.0     |   5.0    |   Overshoot |
|    0.25      |     0.0     |   10.0    |   Oscillation |
|    0.25      |     0.0     | **15.0**   |   Oscillation |
|    0.25      |     0.0     |   20.0    |   Undershoot |
| | | | |
|    0.25      |     0.001    |   15.0    |   Overshoot  |
|    0.25      |  **0.0005**  |   15.0    |   Final params |

### Final result

Here's the result with final PID coefficients.

<video id="video" controls="" preload="none">
    <source id="mp4" src="./video/output_project_video.mp4" type="video/mp4">
</video>