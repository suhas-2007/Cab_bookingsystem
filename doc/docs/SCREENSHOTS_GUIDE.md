text
# SCREENSHOTS_GUIDE.md

## Guide to Capturing and Labeling Screenshots for the Ride Booking System Project

---

### System Requirements

- **OS:** Windows 10/11, Linux, or macOS
- **Processor:** Any modern x86/x64 processor
- **RAM:** 512 MB minimum (2 GB+ recommended)
- **Storage:** 10 MB free for files and screenshots
- **Compiler:** g++ 6.3+ with C++17 support (or compatible compiler on your platform)
- **Terminal:** Supports standard output and (optionally) ANSI colors
- **Screenshot Tool:** Snipping Tool, Spectacle, gnome-screenshot, Shift+Command+4, or similar

---

## Workflow and Screenshot Checklist

Follow this sequence to capture all required screenshots with relevant CLI/text output.

---

### 1. Program Welcome Screen

Shows the initial project banner or greeting.

    std::cout << "Welcome to Ride Booking System!\n";

text

### 2. Input: Booking Type

Covers input for "self" or "other" booking and identifying information.

    std::cout << "Are you booking for yourself or someone else? (self/other): ";

text

### 3. Input: Ride Date and Journey Details

Shows date (today/other), start point, destination, and start time collection.

    std::cout << "Book ride for today or another day? (today/other): ";
    std::cout << "Enter your current location: ";
    std::cout << "Enter your destination location: ";

text

### 4. Vehicle and Driver Selection

Shows vehicle choices and lists eligible drivers.

    std::cout << "Choose Vehicle Type:\n1. Car\n2. Bike\n3. Auto\nChoice: ";
    std::cout << "\nAvailable drivers for "; rideDate.print(); std::cout << ":\n";

text

### 5. Fare Calculation and User Decisions

Displays estimated fare and pre-allocation decisions (continue, cancel, fare adjust, etc.).

    std::cout << "\nEstimated fare for your trip: ₹" << std::fixed << std::setprecision(2) << fare << std::endl;
    std::cout << "\nOptions before allocation: \n"
    << "A. Cancel Ride & give feedback\n"
    << "B. Continue ride (back to options)\n"
    << "C. Request Decrease Fare\n"
    << "D. Increase Fare for faster allocation\n"
    << "E. Continue with current fare\n"
    << "Choose option (A/B/C/D/E): ";

text

### 6. Driver Allocation & OTP

Shows allocation simulation and generated OTP display.

    startTimer(allocationWait);
    int otp = generateOTP();
    std::cout << "OTP for Booking Confirmation: " << otp << std::endl;

text

### 7. Booking Summary

Captures the main printout of all ride, driver, and OTP details.

    bk.printBooking();

text

### 8. Journey Arrival / Ride Updates

Covers calculations or outputs for arrival time and any journey progress updates.

    printArrivalTime(startHr, startMin, duration);
    giveOneUpdate(duration);

text

### 9. Post-Ride Rating and Feedback

Covers the collection/display of ride rating and textual comments after ride completion.

    std::cout << "\nYou have reached your destination. Please rate your ride (1-5): ";
    std::cout << "\nAny feedback for your ride? ";

text

### 10. Final Completion/Goodbye

Shows the closing summary of the session.

    std::cout << "\nThank you for your rating and feedback!\n";
    bk.printBooking();
    std::cout << "Your feedback: " << feedback << std::endl;

text

---

## Screenshot Capture and File Organization

- Save screenshots as:  
  `01_welcome_screen.png`  
  `02_input_booking_type.png`  
  `03_input_ride_date.png`  
  ... up to `10_final_goodbye.png`
- Place all screenshots in a `screenshots/` folder.
- When embedding in documentation, use:
![Welcome](screenshots/01

text

---

## Practical Tips

- Maximize terminal, use a readable font.
- Take screenshots after each relevant system or user prompt.
- Crop excess borders and only show the terminal.
- Use one color scheme/theme throughout for consistency.

---

## Expected Output (OOP Concept-Wise)

This section gives sample output divided according to the main OOP concepts demonstrated.

---

### 1. Encapsulation

All information is only displayed using public methods.

    Welcome to Ride Booking System!
    Are you booking for yourself or someone else? (self/other): self
    Enter your name: Amit
    Enter your mobile number: 9000112233
    Enter your gender (male/female): male

text

### 2. Inheritance

Different vehicle types/subtypes derived from Vehicle base class.

    Choose Vehicle Type:

    Car

    Bike

    Auto
    Choice: 1
    Choose car type:

    Sedan

    SUV
    Choice: 1

    Available drivers for 9/11/2025:

    Name: Ajay, Gender: male, Mobile: 8899001100, Avg. Rating: 4.3, Vehicle: Car (Sedan), Number: KA01SED1001
    ...
  
text

### 3. Polymorphism

    displayDetails() resolves at runtime for each vehicle/driver.
    Available drivers for 9/11/2025:

    Name: Ajay, Gender: male, Mobile: 8899001100, Avg. Rating: 4.3, Vehicle: Car (Sedan), Number: KA01SED1001

    Name: Manish, Gender: male, Mobile: 9234567812, Avg. Rating: 4.5, Vehicle: Car (Sedan), Number: KA02SED2002
    ...
  
    Driver: Manish, ID: 105, Gender: male, Mobile: 9234567812, Avg. Rating: 4.5
    Vehicle Assigned: Car (Sedan), Number: KA02SED2002

text

### 4. Abstraction

Exposes only needed prompts, prints and summary, logic is hidden.

    Estimated fare for your trip: ₹752.00

    Options before allocation:
    A. Cancel Ride & give feedback
    B. Continue ride (back to options)
    C. Request Decrease Fare
    D. Increase Fare for faster allocation
    E. Continue with current fare
    Choose option (A/B/C/D/E): E

text

### 5. Composition

Booking links to Driver, Driver links to Vehicle. Output shows relationship.

    Booking #1 for Amit
    Booking for: Amit
    User mobile: 9000112233
    Driver mobile: 9234567812
    Date: 9/11/2025
    From: Home To: Airport
    Driver: Manish, ID: 105, Gender: male, Mobile: 9234567812
    Vehicle Assigned: Car (Sedan), Number: KA02SED2002
     ...

text

### 6. Templates/Generics

Generic BookingContainer stores & retrieves bookings.

    Booking successful! Here are the details:
    Booking #1 for Amit
    ...
Booking #2 for Pooja
...

text

---

### Full Sample Output

    Welcome to Ride Booking System!
    Are you booking for yourself or someone else? (self/other): self
    Enter your name: Amit
    Enter your mobile number: 9000112233
    Enter your gender (male/female): male
    Book ride for today or another day? (today/other): today
    Enter your current location: Home
    Enter your destination location: Airport
    Enter your journey start time (hour min): 11 30
    Choose Vehicle Type:

    Car

    Bike

    Auto
    Choice: 1
    Choose car type:

    Sedan

    SUV
    Choice: 1

    Available drivers for 9/11/2025:

    Name: Ajay, Gender: male, Mobile: 8899001100, Avg. Rating: 4.3, Vehicle: Car (Sedan), Number: KA01SED1001

    Name: Manish, Gender: male, Mobile: 9234567812, Avg. Rating: 4.5, Vehicle: Car (Sedan), Number: KA02SED2002

    Name: Gaurav, Gender: male, Mobile: 7888999000, Avg. Rating: 3.9, Vehicle: Car (SUV), Number: KA02SUV2003

    Name: Deepak, Gender: male, Mobile: 8333111222, Avg. Rating: 4.4, Vehicle: Car (Sedan), Number: KA01SED1001
    
    Do you want to confirm booking on this date? (y/n): y

    Choose a driver by number (1-4): 2

    Estimated fare for your trip: ₹752.00
  
    Options before allocation:
    A. Cancel Ride & give feedback
    B. Continue ride (back to options)
    C. Request Decrease Fare
    D. Increase Fare for faster allocation
    E. Continue with current fare
    Choose option (A/B/C/D/E): E

    Allocating a driver, please wait...
    (loading...)

    Booking successful! Here are the details:

    Booking #1 for Amit
    Booking for: Amit
    User mobile: 9000112233
    Driver mobile: 9234567812
    Date: 9/11/2025
    From: Home To: Airport
    Driver: Manish, ID: 105, Gender: male, Mobile: 9234567812, Avg. Rating: 4.5
    Vehicle Assigned: Car (Sedan), Number: KA02SED2002
    Estimated Duration: 50 min
    Total Fare: ₹752.00
    OTP for Booking Confirmation: 1234

    Sharing OTP (1234) with your driver...
    Your estimated arrival time: 12:20

    Would you like a ride update about ETA and speed? (y/n): y
    ETA: 34 min remaining, Current speed: 38 km/hr

    You have reached your destination. Please rate your ride (1-5): 5

    Any feedback for your ride? Excellent service

    Thank you for your rating and feedback!

    Booking #1 for Amit
    Booking for: Amit
    User mobile: 9000112233
    Driver mobile: 9234567812
    Date: 9/11/2025
    From: Home To: Airport
    Driver: Manish, ID: 105, Gender: male, Mobile: 9234567812, Avg. Rating: 4.5
    Vehicle Assigned: Car (Sedan), Number: KA02SED2002
    Estimated Duration: 50 min
    Total Fare: ₹752.00
    OTP for Booking Confirmation: 1234
    Your Rating: 5/5
    Your feedback: Excellent service

text

---

Every screenshot maps to this output and illustrates relevant OOP concepts. This markdown provides a comprehensive guide for your project.
