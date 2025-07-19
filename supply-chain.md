---
title: The Dronery Supply Chain
---

<img src="resources/logo.png" align="center" width="80%">

The following is a work in progress.

# The Dronery Supply Chain

Recently I argued in Lawfare that [small drone development is too
important to leave to private
industry](https://www.lawfaremedia.org/article/a-return-to-in-house-weapons-development).
In that piece I consider a "Dronery", a government or non-profit owned
facility deadicated to the design and manufacturing of small,
autonomous drones.

Simply put, defense contractors are the wrong tool for autonomous
drone development as the tendency for [rent
seeking](https://en.wikipedia.org/wiki/Rent-seeking) will add one or
two orders of magnitude to the price of systems where perhaps the
biggest quality is quantity.

This is particularly true when adding autonomy as the costs for
autonomous operations is almost entirely in software.  Software has
huge [non-recurring
engineering](https://en.wikipedia.org/wiki/Non-recurring_engineering)
costs (NRE) but costs $0 for each additional copy.  So even just a
single penny charged for software that a contractor was already paid
to design is rent seeking.

This is an attempt to understand the supply chain needs, challenges,
and approaches faced by a dronery intending on producing anywhere from
10,000 to 1,000,000 small drones a year.

## The Dronery's Conceptual Designs

For this analysis we will assume four conceptual designs: the small
quadcopter, the large quadcopter, the small fixed-wing and the large
fixed-wing.  The small versions can carry a 500g warhead (roughly
equivalent to a hand-grenade) while the large versions can carry
either a 4kg warhead (sufficient for an anti-tank round) or an
advanced sensor package.

The quadcopters are assumed to be manufactured with carbon fiber sheet
stock cut by CNC machines while the fixed-wing airframes are assumed
to be constructed of expanded polypropylene (EPP) foam.

All designs share a common control platform and software stack.  For
this analysis the control platform will be assumed to be a successor
to the Kestrel design: a 40mm x 55mm board that runs the low level
autopilot, general power supply, and which provides two four-lane MIPI
CSI camera connectors, two USB3 (5Gbps) connections, an SD Card
interface and general purpose I/O to an embedded host computer
compatible with the [Raspberry Pi CM5 compute
module](https://www.raspberrypi.com/products/compute-module-5/).

Experience suggests that this should be sufficient for well-structured
autonomous operations, such as performing automatic target
identification and tracking, communication and coordination,
terrain-matching, and optical flow image processing.

The conceptual design will also include a high-density connector for a
separate radio module, as there are significant tradeoffs in
cost/performance/bandwidth/jamming resistance between various options.

## Supply Chain: Control Board

### Embedded Processors

### Power Management

### Proprioception

## Supply Chain: Host Computer

### COTS

### Custom Module

## Supply Chain: Radio Communication

## Supply Chain: Cameras

## Supply Chain: Advanced Camerasó

## Supply Chain: Advanaced Sensors

## Supply Chain: Carbon Fiber

## Supply Chain: EPP Foam

## Supply Chain: Batteries

## Supply Chain: Motors

## Supply Chain: Motor Speed Controllers
