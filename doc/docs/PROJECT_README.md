# Ride Booking System

**An OOP-based C++ project for booking rides, managing drivers, and simulating the allocation process—demonstrating encapsulation, inheritance, abstraction, polymorphism, templates, and real-world workflow.**

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [OOP Concepts Implementation](#oop-concepts-implementation)
3. [Architecture & Design](#architecture--design)
4. [File-by-File Documentation](#file-by-file-documentation)
5. [Features Implementation](#features-implementation)
6. [Class Relationships](#class-relationships)
7. [Function Reference](#function-reference)
8. [UI/UX Features](#uiux-features)
9. [Execution Flow](#execution-flow)
10. [Technical Specifications](#technical-specifications)

---

## Project Overview

### Purpose

The Ride Booking System is an educational C++ project designed to solidify Object-Oriented Programming fundamentals via a practical car/bike/auto booking and simulation engine.

---

### Key Capabilities

- Book Cars (Sedan/SUV), Bikes (Scooty/Motorbike), or Autos
- Profile and manage drivers (gender, ratings, mobile, assigned vehicle, on-duty days)
- Schedule rides for today or any specific day
- Book for self or others, with detailed input
- Filter/choose drivers by type, gender, and date
- Realistic fare estimation and options
- Cancellation feedback, journey and arrival simulation, rider updates
- Ratings and text-feedback collection after each completed booking
- BookingContainer<T> template for extensible storage and simplified management
- Modern, interactive CLI user experience

---

## OOP Concepts Implementation (with Code Snippets)

### 1. Encapsulation

    class Booking {
    private:
    int bookingID; // Hidden: cannot access directly from outside
    double fare;
    Driver* driver;
    public:
    int getBookingID() const { return bookingID; } // Controlled access
    double getFare() const { return fare; }
    Driver* getDriver() const { return driver; }
    };

text

### 2. Inheritance

    class Vehicle {
    public:
    virtual void displayDetails() const = 0;
    };

    class Car : public Vehicle {
    public:
    void displayDetails() const override {
    std::cout << "Car Details...\n";
    }
    };

text

### 3. Polymorphism

    Vehicle* v1 = new Car("KA01SED1001", "Sedan");
    Vehicle* v2 = new Bike("KA01SCT3001", "Scooty");

    v1->displayDetails(); // Car::displayDetails()
    v2->displayDetails(); // Bike::displayDetails()

text

### 4. Abstraction

    class Driver {
    private:
    std::vector<double> ratings;
    public:
    double averageRating() const {
    return ratings.empty() ? 0.0 :
    std::accumulate(ratings.begin(), ratings.end(), 0.0) / ratings.size();
    }
    };

text

### 5. Composition

    class Driver {
    private:
    Vehicle* assignedVehicle; // Composition: Driver "has-a" Vehicle
    public:
    Vehicle* getVehicle() const { return assignedVehicle; }
    };

text

### 6. Templates / Generics

    template<class T>
    class BookingContainer {
    private:
    std::vector<T> bookings;
    public:
    void addBooking(const T& booking) { bookings.push_back(booking); }
    void displayAll() const { for(const auto& b : bookings) b.printBooking(); }
    };

text

---

## Features Implementation

### Booking for Self or Others

    std::string selfOrOther;
    std::cout << "Are you booking for yourself or someone else? (self/other): ";
    getline(std::cin, selfOrOther);

    std::string riderName, bookingFor = "";
    if (selfOrOther == "self") {
    std::cout << "Enter your name: ";
    getline(std::cin, riderName);
    bookingFor = riderName;
    } else {
    std::cout << "Enter your name: ";
    getline(std::cin, riderName);
    std::cout << "Enter the name of the person you are booking for: ";
    getline(std::cin, bookingFor);
    }

text

### Entering or Selecting Ride Date

    std::cout << "Book ride for today or another day? (today/other): ";
    std::string dayChoice;
    getline(std::cin, dayChoice);

    Date rideDate;
    if (dayChoice == "today") {
    time_t tnow = time(0);
    tm* now = localtime(&tnow);
    rideDate.day = now->tm_mday;
    rideDate.month = now->tm_mon + 1;
    rideDate.year = now->tm_year + 1900;
    } else {
    std::cout << "Enter ride date (day month year): ";
    std::cin >> rideDate.day >> rideDate.month >> rideDate.year;
    std::cin.ignore();
    }

text

### Displaying Available Drivers

    std::cout << "\nAvailable drivers for ";
    rideDate.print();
    std::cout << ":\n";

    for (int i = 0; i < nDisplay; ++i) {
    std::cout << i + 1 << ". Name: " << eligibleDrivers[i]->getName()
    << ", Gender: " << eligibleDrivers[i]->getGender()
    << ", Mobile: " << eligibleDrivers[i]->getMobile()
    << ", Avg. Rating: " << std::fixed << std::setprecision(1) << eligibleDrivers[i]->averageRating()
    << ", Vehicle: ";
    eligibleDrivers[i]->getVehicle()->displayDetails();
    }

text

### Fare Calculation & Pre-Allocation Options

    double fare = calculateFare(typeString, subtypeChoice, duration);

    fare_options:
    std::cout << "\nOptions before allocation:\n"
    << "A. Cancel Ride & give feedback\n"
    << "B. Continue ride (back to options)\n"
    << "C. Request Decrease Fare\n"
    << "D. Increase Fare for faster allocation\n"
    << "E. Continue with current fare\n"
    << "Choose option (A/B/C/D/E): ";
    std::string preOpt;
    getline(std::cin, preOpt);

    if (preOpt == "A" || preOpt == "a") {
    std::cout << "You chose to cancel. Please provide feedback for this cancellation: ";
    std::string cancelFeedback;
    getline(std::cin, cancelFeedback);
    std::cout << "Thank you! Your feedback is recorded: " << cancelFeedback << "\nBooking cancelled.\n";
    cleanup(vehicles, drivers);
    return 1;
    } else if (preOpt == "B" || preOpt == "b") {
    goto fare_options;
    } else if (preOpt == "C" || preOpt == "c") {
    fare *= 0.9;
    std::cout << "Fare reduced by 10%. New fare: ₹" << std::fixed << std::setprecision(2) << fare << std::endl;
    goto fare_options;
    } else if (preOpt == "D" || preOpt == "d") {
    fare *= 1.1;
    std::cout << "Fare increased by 10%. New fare: ₹" << std::fixed << std::setprecision(2) << fare << "\n";
    goto fare_options;
    } else if (preOpt != "E" && preOpt != "e") {
    std::cout << "Invalid input.\n";
    goto fare_options;
    }

text

### Booking Confirmation and OTP Display

    startTimer(allocationWait);

    int otp = generateOTP();
    Booking bk(bookingCount++, riderName, bookingFor, userMobile,
    selectedDriver, startLoc, destLoc, duration, otp, fare, rideDate);
    bookingList.addBooking(bk);

    std::cout << "Booking successful! Here are the details:";
    bk.printBooking();

    std::cout << "\nSharing OTP (" << otp << ") with your driver..." << std::endl;
    printArrivalTime(startHr, startMin, duration);

text

### Ride Updates During Journey

    std::string needUpdates;
    do {
    std::cout << "\nWould you like a ride update about ETA and speed? (y/n): ";
    getline(std::cin, needUpdates);
    if (needUpdates == "y" || needUpdates == "Y")
    giveOneUpdate(duration);
    } while (needUpdates == "y" || needUpdates == "Y");

text

### Rating and Feedback Collection

    double rating;
    std::cout << "\nYou have reached your destination. Please rate your ride (1-5): ";
    std::cin >> rating;
    std::cin.ignore();
    bk.setRating(rating);

    std::string feedback;
    std::cout << "\nAny feedback for your ride? ";
    getline(std::cin, feedback);

    std::cout << "\nThank you for your rating and feedback!\n";
    bk.printBooking();
    std::cout << "Your feedback: " << feedback << std::endl;

text

---

## Architecture & Design

See [FLOWCHART.md](FLOWCHART.md) for a full text-based flowchart of the main processes.

---

## Getting Started

**Compile:**
      
      g++ -std=c++17 -Wall -Wextra main.cpp RideBookingSystem.cpp -o ridebooking

text
**Run:**


    ./ridebooking

text

---

## Author

**This project is for academic/learning use—customize and extend as desired!**
