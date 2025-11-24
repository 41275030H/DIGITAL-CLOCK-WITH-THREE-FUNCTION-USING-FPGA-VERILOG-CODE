# DIGITAL-CLOCK-WITH-THREE-FUNCTION-USING-FPGA-VERILOG-CODE
Digital clock on FPGA using Verilog with three modes: real-time clock, alarm, and stopwatch timer. Implements time counting, mode switching, and 7-segment display control.
# Digital Clock with Three Functions (FPGA – Verilog)

This project is a **digital clock implemented on FPGA** using **Verilog HDL**.  
The design supports **three main functions**:

1. **Real-Time Clock** – displays current time in HH:MM:SS
2. **Alarm Mode** – user can set an alarm time; an output signal/buzzer is triggered when the time matches
3. **Stopwatch / Timer Mode** – start / stop / reset counting for simple timing measurement

---

## Features

- 1 Hz clock divider from the FPGA system clock
- Time counter (seconds, minutes, hours) with proper rollover
- Mode selection using push buttons / switches:
  - Clock mode
  - Alarm mode
  - Stopwatch / timer mode
- Time setting using buttons (increment hours / minutes)
- 7-segment display driver for HH:MM:SS
- Simple alarm output (LED / buzzer signal)

---

## Project Structure

- `clk_divider.v` – generates 1 Hz clock from the FPGA input clock
- `time_counter.v` – main time counter for hours, minutes, seconds
- `alarm_unit.v` – stores alarm time and compares it with current time
- `stopwatch.v` – stopwatch / timer counter with start/stop/reset
- `display_driver.v` – multiplexing and segment control for 7-segment display
- `top.v` – top module connecting all submodules and FPGA pins


---

## How It Works

1. **Clock Divider**  
   The FPGA board clock (e.g. 50 MHz / 100 MHz) is divided down to **1 Hz**.  
   This 1 Hz signal is used as the time base for the seconds counter.

2. **Time Counting**  
   - Seconds count from 0–59  
   - When seconds reach 59 and overflow, minutes increment  
   - When minutes reach 59 and overflow, hours increment  
   - Hours wrap around after 23 → 00

3. **Mode Selection**  
   - Input switches / buttons select between **Clock / Alarm / Stopwatch** mode  
   - In **Alarm** and **Clock** mode, the user can set hours and minutes using buttons  
   - In **Stopwatch** mode, buttons control **start / stop / reset**

4. **Alarm Output**  
   When current time equals alarm time, a dedicated signal goes high  
   (can be connected to LED or buzzer on the board).

5. **Display**  
   The time is shown in **HH:MM:SS** format using multiplexed 7-segment displays.

---

## Usage

1. Open the project in your FPGA tool (e.g. Vivado / Quartus / ISE).
2. Set `top.v` as the top module.
3. Assign pins for:
   - System clock input
   - Push buttons / switches (mode, set, start, stop, reset)
   - 7-segment segments & digit select
   - Alarm output (LED / buzzer)
4. Synthesize, implement, and program the bitstream to the FPGA board.
5. Change modes and set time using buttons to test each function.

---

## Possible Improvements

- Add date (DD/MM/YY) and 24h / 12h mode
- Debouncing for all push buttons
- More advanced alarm (multiple alarms, snooze, etc.)
- LCD / OLED display instead of only 7-segment

---

## Author

范金潤 / Bryan Fandy
宮崎卓 / Taku Miyazaki

`MIT License` or `GNU GPLv3`

---

If you use this project for learning or teaching, feel free to modify the code and adapt it to your own FPGA board.
