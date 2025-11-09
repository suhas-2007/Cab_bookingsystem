# FLOWCHART.md

## Ride Booking System - Main Flowchart

---

    ### User Booking Journey

    +-------------------------------------------------------------+
    | Start (Welcome Screen) |
    +----------------------------+--------------------------------+
    |
    v
    +-------------------------------+
    | "Self" or "Other" Booking? |
    +-------------------------------+
    /
    v v
    +-------------------+ +------------------------------+
    | Enter Name | | Enter User Name |
    | (if "self") | | Enter Name for Booking |
    +-------------------+ +------------------------------+
    |
    v
    +--------------------------+
    | Enter Mobile Number |
    +--------------------------+
    |
    v
    +-------------------------------+
    | Enter User Gender |
    +-------------------------------+
    |
    v
    +---------------------------------------+
    | "Today" or "Other Day" Ride? |
    +---------------------------------------+
    /
    v v
    +----------------------+ +------------------------+
    | Set Current Date | | Enter Date: DD MM YYYY |
    +----------------------+ +------------------------+
    |
    v
    +----------------------------------+
    | Enter Start & Destination Points |
    +----------------------------------+
    |
    v
    +-----------------------------------------------+
    | Enter Journey Start Time (HH MM, 24h clock) |
    +-----------------------------------------------+
    |
    v
    +--------------------------------------+
    | Select Vehicle: Car / Bike / Auto |
    +--------------------------------------+
    | | |
    +----+ +--+--+ +----+
    | | | |
    v v v v
    Car Option Bike Auto
    (Sedan/SUV) (Scooty/Motorbike)
    | | |
    +---------------------+
    |
    v
    +------------------------------------------------+
    | Filter and Show Eligible Drivers (by gender, |
    | type, subtype, date) |
    +----------------+-------------------------------+
    |
    v
    +-------------------------------+
    | Show Max 4 Drivers to Choose |
    +-------------------------------+
    |
    v
    +------------------------------+
    | Confirm Booking Date? (y/n) |
    +------------------------------+
    | |
    (n) (y)
    | |
    End v
    +----------------------+
    | Select Driver (#) |
    +----------------------+
    |
    v
    +------------------------------+
    | Calculate Fare (Show Estimate)|
    +------------------------------+
    |
    v
    +------------------------------------------------+
    | User Pre-allocation Options: |
    | - Cancel & feedback |
    | - Continue ride |
    | - Request decrease/increase fare |
    | - Confirm with current fare |
    +------------------------------------------------+
    |
    v
    +------------------------------+
    | Simulate Driver Allocation |
    +------------------------------+
    |
    v
    +----------------------+
    | Generate & Show OTP |
    +----------------------+
    |
    v
    +--------------------------+
    | Show Final Booking Info |
    +--------------------------+
    |
    v
    +-------------------------------+
    | Show Arrival Time Calculation |
    +-------------------------------+
    |
    v
    +------------------------------------------+
    | (Optional) Show Journey Updates (ETA, |
    | speed) |
    +------------------------------------------+
    |
    v
    +-------------------------+
    | Prompt for Ride Rating |
    +-------------------------+
    |
    v
    +---------------------+
    | Prompt for Feedback |
    +---------------------+
    |
    v
    +------------------+
    | Print Summary |
    +------------------+
    |
    v
    +--------+
    | END |
    +--------+

text

---

### Modular Internal Flows

#### 1. Booking Pre-Allocation Decision

    [Estimate Shown]
    |
    v
    +----------------------------+
    | Option A: Cancel & FB |---[End + Save FB]
    | Option B: Continue |---[Repeat options]
    | Option C: Decrease fare |---[Apply 10% off + Repeat]
    | Option D: Increase fare |---[Apply 10% up + Repeat]
    | Option E: Confirm & Proceed|---[Continue]
    +----------------------------+

text

#### 2. Driver Filtering

    [Vehicle type/subtype]
    |
    v
    [Check driver gender]
    |
    v
    [Check available day]
    |
    v
    [List eligible drivers]

text

---

### Notation

- Rectangles = action/step
- Diamonds (written as decision text) = conditional step
- Parallel paths shown by multi-branching
- Loops show user-driven option revisits

---
