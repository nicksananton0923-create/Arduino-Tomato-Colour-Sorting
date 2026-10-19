 Arduino-Based Smart Conveyor Belt for Tomato Colour Detection and Sorting

An educational Arduino project exploring a conveyor-belt concept that measures tomato surface colour and commands a servo-operated sorting gate. The intended categories are green, partially ripe, and red.

> **Project status:** The repository contains proposed hardware documentation and educational starter code. The physical system, wiring, classification accuracy, and sorting performance have not been confirmed by this README. The colour thresholds are starting values, not validated ripeness standards.
 🎯 Project Objective

Explore how an embedded controller can combine a presence sensor, colour measurements, conveyor control, and a sorting mechanism to demonstrate a basic automation workflow.

The intended workflow is:

1. Start the conveyor using the operator control.
2. Detect an object at the sensing position.
3. Pause the conveyor and obtain colour readings.
4. Classify the reading using configurable colour-ratio rules.
5. Move the servo to a category-specific position.
6. Return to a ready state for the next object.

The actual mechanism and control sequence must be verified against the physical design. The current sketch pauses the conveyor during measurement and uses an IR sensor-clear condition before resuming.

 ✨ Intended Features

- TCS34725 colour measurements over I²C.
- IR-based object-presence detection.
- Five-sample averaging for colour readings.
- Configurable colour-ratio thresholds.
- Conveyor motor control through a motor driver.
- Servo-operated sorting-gate concept.
- Start and software Stop buttons.
- Serial Monitor output for readings and classification.

These are code-level design features, not proof of successful hardware operation or accurate classification.

 🧰 Proposed Hardware

| Component | Purpose |
|---|---|
| Arduino Uno R3 | Main controller |
| TCS34725 colour sensor breakout | Red, green, blue, and clear-channel readings |
| Digital IR presence sensor | Object detection |
| DC geared motor and conveyor assembly | Object transport |
| Motor driver, proposed as L298N | Motor control |
| SG90 micro servo | Lightweight sorting-gate demonstration |
| Start and Stop push buttons | Operator inputs |
| Red and green LEDs with resistors | Status indication |
| Suitable regulated supplies and wiring | Power and connections |

These are proposed candidate components. Confirm the exact parts, electrical ratings, and wiring before building the system.

 🔌 Pin Connections in the Current Sketch

| Function | Arduino Uno pin |
|---|---|
| IR sensor output | D2 |
| Start button to GND | D3 |
| Stop button to GND | D4 |
| Motor driver ENA / PWM | D5 |
| Motor driver IN1 | D7 |
| Motor driver IN2 | D8 |
| Servo signal | D9 |
| Green LED through resistor | D10 |
| Red LED through resistor | D11 |
| TCS34725 SDA | A4 |
| TCS34725 SCL | A5 |

The sketch assumes the IR sensor output is **LOW when an object is detected** and uses `INPUT_PULLUP` for the buttons. Verify these assumptions against the actual modules.

 💻 Source Code and Libraries

The current Arduino sketch is stored in [`Code`](<Code>).

Libraries referenced by the sketch:

- Adafruit TCS34725
- Adafruit BusIO dependency
- `Servo` and `Wire`, provided with the appropriate Arduino board package

Install compatible libraries and select the correct board and port in the Arduino IDE before compiling.

 🎨 Colour Classification and Calibration

The sketch calculates normalized red, green, and blue ratios and compares them with configurable starting values.

Current example settings:

- `GREEN_G_RATIO_MIN = 0.38`
- `GREEN_OVER_RED_MIN = 1.15`
- `RED_R_RATIO_MIN = 0.40`
- `RED_OVER_GREEN_MIN = 1.20`

These values are **not validated for all tomato varieties, sensor distances, or lighting conditions**. Colour measurements describe reflected light, not internal sugar content or biological ripeness.

Follow the existing [colour sensor calibration guide](<Colour sensor calibration guide>) to standardize the sensor distance and illumination, collect labelled samples, tune thresholds, and validate them on separate samples.

 📚 Existing Project Documentation

- [Bill of materials spreadsheet](<Bill_of_materials.xlsx>)
- [Components, functions, and connection notes](<Components, functions and connection notes>)
- [Control logic](<Control Logic>)
- [Proposed wiring and connection diagram](<Proposed wiring and connection diagram>)
- [System block diagram](<System block diagram>)
- [Testing and results record](<Testing and results record>)
- [Operation notes](<How to work>)
- [Questions and answers](<Question and Answers>)
- [Conveyor connection image](<Conveyer  connection.jpg>)
- [Logic image](<logics.jpg>)

All links point to existing paths; no files need to be renamed for this README revision.

 🧪 Testing and Verification

Before claiming successful sorting, document and verify:

1. Sensor detection polarity and repeatability.
2. Colour readings under fixed, controlled illumination.
3. Calibration data and the resulting classification thresholds.
4. Motor-driver compatibility with the motor's supply and stall current.
5. Servo angles and the actual gate geometry.
6. Behaviour when the sensor reading is invalid.
7. Repeated object detection and conveyor restart behaviour.
8. The results of tests on separate samples not used for calibration.

**Known code-review item:** the conveyor stops at detection and later waits for the IR sensor to clear before restarting. If an object remains in front of the sensor while the conveyor is stopped, the sketch may not resume automatically. This should be reviewed before claiming continuous operation.

 ⚠️ Safety Notes

- A software Stop button is not a safety-rated emergency stop.
- Provide a suitable physical means of disconnecting motor power.
- Never power a motor or servo directly from an Arduino GPIO pin.
- Use an appropriate motor driver and regulated supply.
- Keep motor current out of breadboards and low-current signal wiring.
- Check voltage compatibility and common-ground requirements before connecting modules.
- Test mechanical motion with lightweight dummy objects before operating the conveyor with produce.

 📈 Future Improvements

- Review and validate the sensor-clear and restart state logic.
- Add explicit sensor fault handling and a recoverable fault state.
- Store classification and test data with sample identifiers.
- Evaluate accuracy using a confusion matrix and separate validation samples.
- Document real build photographs and measured results only after obtaining them.
- Improve mechanical tracking if the sensing station and sorting gate are separated.

 📄 Project Status

**Educational starter code and documentation are available. Physical verification, classification accuracy, and sorting performance remain unconfirmed.**
