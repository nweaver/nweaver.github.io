---
title: Skerry Technologies
---

<img src="resources/logo.png" align="center" width="80%">

## Putting the *Science* in Mad Science

Welcome to Skerry Technologies, my (currently one-man, completely
unfunded, almost might as well consider it a hobby) Research and
Development operation focused on small Unmanned Aerial Systems. 

Although, in all honesty, it more like "mad engineering" rather than
mad science: its all about trying to understand how to extend the
state of the art in small autonomous drones.

## Project Kestrel

<img style="padding: 0px 4px 0px 0px" align="left" src="resources/kestrel-board.jpg" alt="Kestrel Board" width=100>

The Kestrel design is a small, highly integrated autopilot design for
small drones which couples a Raspberry Pi compute module to an
ardupilot-compatable autopilot board that includes two MIPI CSI2
camera interfaces, a GPS, an IMU, power distribution, and a separate
chip for a LoRa datalink.

The major idea is that by coupling a Raspberry Pi compute module into
a small drone it should be possible to build small, vision based
autonomy in a very low-cost package.  The RP4 compute module has *just
enough* compute to do a reasonable amount of vision processing and, by
coupling it to an independent autopilot, offload all the true
real-time processing to a dedicated coprocessor.

### Current Status

<img style="padding: 0px 4px 0px 0px" align="left" src="resources/kestrel-in-frame.jpg" alt="Kestrel In Frame" width=100>

A previous version of this board has already flown under remote
control using Ardupilot as the on-board autopilot and successfully
recorded video in flight showing the cameras and compute module as
fully operational.

The current board is still undergoing partial validation: the power
supply, CM4, cameras, and GPS are all verified as working.  Physical
integration into a small quadcopter chassis was also successfully
performed.

### Hardware ToDo List

- Port Ardupilot to the current board and fly under remote control.
- Port ExpressLRS to the ESP32 datalink chip.
- Implement RemoteID on the ESP32 datalink chip.
- Consider a revised design to fix identified bugs, switch to a more
  advanced IMU chip, support for the CM5 compute module, better
  internal programming paths, and other changes.

### Software ToDo List

- Lots

Overall, the software stack beyond using existing components exists as
a paper design with effectively no coding.  The primary focus would be
on "old-school" machine vision rather than anything "AI based".  This
is both to improve performance (most ML-based image processing is
expensive) and to provide much stronger explainability.

I've previously had a few students experiment with portions of the
pipeline and it is clear that the Raspberry Pi CM4 has sufficient
compute for a few frames-per-second vision processing with a 1080p
camera.

Low altitude operation: Very low altitude (under 50m altitude) is
focused primarily on collision avoidance.  The primary pipeline in
this mode focuses on optical flow, a traditional machine vision
technique to recreate a 3D environment from a moving camera.

Aerial target recognition: Optial flow is also used to drive target
identification and recognition.  For aerial targets (such as
applications like counter-drone or bird abatement), optical flow is
used to isolate items in space.  Only such items are passed to
machine-learning based target recognition.

Attention-based scanning: In higher altitude operations the software
will take advantage of high resolution cameras with digital
pan/tilt/zoom.  Normally the software will use the entire field of
view at low resolution (1080p/30fps), but if any region appears
interesting, it will perform a digital zoom to isolate the area of
interest for applying ML target recognition.

## Project Sparrowhawk

Project Sparrowhawk is in initial planning, looking at developing
clean-sheet software for a low level drone autopilot that takes
advantage of modern, multicore microprocessors and the far more robust
Rust programming language.

The two primary current open-source autopilot stacks are Ardupilot and
Betaflight.  Ardupilot is a large open-source project written in older
(circa 2010) C++, while Betaflight (a fork of Cleanflight) is a
stripped down design targeting quadcapters written in C.  Also,
although highly integrated in some aspects, neither are designed to
integrate communication, FAA-mandated DroneID, or to take advantage of
modern multicore embedded processors.

The overall objectives are:

- Develop a small, low cost referennce hardware design
- Develop a new software stack for the hardware
- Evaluate Rust's applicability for the embedded environment
- Provide a platform for an integrated systems textbook
- Meet BlueUAS framework requirements for government use

### Intended Hardware Archictecture

The intended autopilot architecture will be a single-sided board with
a 30.5x30.5 mounting form factor with JST connectors.  The board will also
have castillated connections allowing it to be integrated into larger
designs as well.

- CPU:  Raspberry Pi RP2350 in the QFN-80 package
- IMU:  TDK 42688
- Compass: Memsic MMC5983MA
- Barometer: 2x Bosch BMP 390, one with a mounting point to connect to a pitot tube
- GPS: UBlox MIA-M10-Q with an external antenna connector
- WiFi:  Espressif ESP32C3 with a separate connection to the GPS
- LoRa: Semtec, either the LR2021 or SX1280 with an external power
  amplifier
- Power: Unreglated LiPo to 5V buck converter
- Power: 5V to 3.3V LDO

The intended design is small enough that it can be constructed as a
4-layer board and assembled in-house on an existing small pick & place
machine.  It should also be able to trivially meet BlueUAS component
criteria allowing it to be used in US government applications.

### Why Rust?

The use of C and older C++ produces code is inherently unsafe: unable
to be effectively analyzed for correctness and likely rife with memory
errors.  At the same time the hard real-time constraints involved in
operating a drone (a 4-8 kHz update loop that polls the IMU, filters
the noise, and updates the operating state of the motors and
actuators) prohibit the use of any language without C or C++'s
garbage-collector free memory semantics or emphasis on zero-overhead
abstractions.

Thus the only languages that can be safely used to engineer the core
of an autopilot are agressively modern C++ (no raw pointers,
collections with checking assertions enabled, etc) or Rust.  Since
either language choice require effectively either a complete rewrite
of an existing codebase or a clean-sheet design the choice of Rust
seems reasonable.

Using Rust will not only gain the inherent safety advantages that are
built into the language from the start (Rust's design philosophy is
similar to C++ in a focus on zero-overhead abstractions but not at the
cost of safety, unlike modern C++ which can only be safe with explicit
programmer discipline), but will also serve as an experiment, allowing
an evaluation of Rust in practice.

### Why multicore?

The Raspberry Pi microcontrollers as well as the ESP32 line from
Espressif have introduced symmetric multicore designs into the
microcontroller space.  These families of microcontrollers not only
offer a significantly lower price point than competing designs from ST
Microsystems but far more flexible I/O structures, allowing one or two
packages to cover most uses.

The new RP2350 in particular is an excellent part.  Full system BOM
cost is less than $3 and it contains a dual core ARM Cortex-M33 at
150MHz with floating point and 30 or 48 highly flexible general
purpose I/O pins.  It also ships with modern code signing and security
features.

The software would probably be written as a "bare metal" application
which does not rely on an embedded real-time OS.  However the use of a
multicore architecture enables segregation: the critical real-time
control loop will run on the second processor while all the other
tasks, including the interrupt handler, run on the first processor.

### Internal Notes

Recently when I've been teaching undergraduate programming I've made
my internal notes for assignments public.  I think this is a good
practice so for this project I am doing it as well.  My internal notes
page is
[here](https://docs.google.com/document/d/1hUa0FrdigLGIdXH2zxKp_NfoEdorLFmMxy68qCo7wcw/).

## Dr Nicholas Weaver

<img align="right" src="resources/headshot.png" alt="Nicholas Weaver">

I obtained his Ph.D. from the University of California
at Berkeley in 2003.  My primary research focus is on digital,
explainable, and commonly adversarial systems.

Within that, however, is a huge range of topics.  Down at the lowest
level i've designed my own custom boards and an FPGA architecture,
while the high level has ranged up to sophisticated network
measurement techniques and economic disruption of nefarious actors.

When it comes to UAS systems my primary focus is on hardware/software
co-design to enable autonomous operation.  I've developed an autopilot
that can mate a Raspberry Pi compute module to an ardupilot-based
autopilot as a proof of concept and I am now working on developing my
own from-scratch autopilot based on co-designed software and hardware.

My CV is [available here](cv.html) and my nontechnical writing is mostly
published at [Lawfare
Media](https://www.lawfaremedia.org/contributors/nweaver)

<br clear="right">