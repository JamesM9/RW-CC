# Glossary

## Drone

An unmanned aircraft. Typical examples are: quadrotors, hexacopters, model airplanes, fixed wings, VTOLs, model helicopters.

## Quadcopter

An unmanned aerial vehicle with 4 propellers and an electronic stabilization system.

## Multicopter

An unmanned aerial vehicle with an electronic stabilization system and the number of propellers equal to 3 (tricopter), 4 (quadcopter), 6 (hexacopter), 8 (octocopter), or more.

## Flight controller / autopilot

**1\.** A specialized circuit-board designed for controlling a multicopter, a plane or another vehicle. Examples:
Pixhawk, Speedybee, Naze32, ESP32. Each of which runs autopilot firmware.

## Firmware

Software primarily for embedded systems, for example, a flight controller or an ESC. Think of it as an operating system or the "brain" of the drone. There are a few popular autopilot firmwares Examples: PX4, Ardupilot, BetaFlight.
## Motor

An electric motor that rotates propellers of the multicopter. Brushless motors are commonly used. These motors require an ESC.

## ESC / motor controller

An Electronic Speed Controller. A specialized circuit-board that controls the speed of the brushless motor. It is controlled by a flight controller using pulse width modulation (PWM). There are different types of ESCs. Both singular ESCs and All In One ESCs. Singular ESCs control one motor at a time. While all in one ESCs could control 4-8 motors with all motors connecting to a singular board. 

## Battery

A rechargeable power source for the drone. Quadcopters typically use LiPo (lithium-ion polymer) batteries. They are rechargable but have a limited number of cycles before they become unsafe to use. 

## Battery cell

Single element of the battery pack. Typical drone batteries contain several (2 to 6) cells connected in series. Maximum LiPo cell voltage is 4.2 v; battery voltage is a sum of each cell's voltage (if they are connected in series). The number of cells connected in series is marked by the letter *S*, as in *2S* (two cells in series), *3S*, *4S*.

## Remote control / radio control equipment

A radio-operated quadcopter remote control. Operation of the remote control requires connecting a receiver to the flight controller.

droid may also be [controlled from a smartphone](rc.md).

## Telemetry

**1\.** Transmitting the data about the state of a quadcopter or another aircraft over a distance.

**2\.** The data about the aircraft state (height, orientation, global coordinates, etc.).

**3\.** The Droid uses a built in wifi module in its companion computer to allow the user to connect to the aircraft usin a phone or laptop and control the aircraft. [the use of QGroundControl via Wi-Fi](gcs_bridge.md) The droid can also be controlled manually through the transmitter controller.

## Arming

Armed is the state of copter readiness for the flight. When the gasthrottle stick is lifted, or when an external command with the target point is sent, the copter will fly. Usually, a copter starts rotating its propellers when it is switched to the "armed" state, even if the throttle stick is down.

The opposite state is Disarmed and he motors are not spinning. 

## Raspberry Pi

[A popular single-board computer](raspberry.md) that is used on the droid aircraft. 

## MAVLink

A communication protocol for drones, ground stations and other devices over radio channels. This protocol is widely used for telemetry and not for manual control inputs uisng the transmitter.
