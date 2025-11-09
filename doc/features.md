# Table of Contents

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

# Project Overview

### Purpose

The Ride Booking System is a C++ project designed to showcase practical application of Object-Oriented Programming (OOP) principles, including encapsulation, inheritance, abstraction, composition, templates, and runtime interaction through a command-line interface. It allows users to book rides for various vehicle types and manage bookings and driver interactions with realistic workflow.

---

## Key Features (with Code Snippets)

### 1. Multi-Type Vehicle Support

*Users can book Cars (Sedan/SUV), Bikes (Scooty/Motorbike), or Autos.*

     cpp
    Vehicle* v1 = new Car("KA01SED1001", "Sedan");
    Vehicle* v2 = new Bike("KA01SCT3001", "Scooty");
    Vehicle* v3 = new Auto("KA03AUTO101");

text

### 2. Driver Profile Management
    cpp
    Driver* d = new Driver("Sneha", 102, v1, "female", "9001100111", {4.9, 4.8}, allDaysOfMonth());
    std::cout << d->getName() << ", Vehicle: "; d->getVehicle()->displayDetails();

text
- Filter drivers by type, subtype, gender, and date:

      cpp
      for (auto d : drivers) {
      if (d->getVehicle()->getType() == "Car" &&
      d->getGender() == "female" &&
      d->isAvailableOnDay(rideDate.day))
      eligibleDrivers.push_back(d);
      }

text

### 3. Flexible Booking Workflow

     cpp
    std::string selfOrOther;
    std::cout << "Are you booking for yourself or someone else? (self/other): ";
    getline(std::cin, selfOrOther);
    Date rideDate;
    std::cout << "Enter ride date (day month year): ";
    std::cin >> rideDate.day >> rideDate.month >> rideDate.year;

text

### 4. Detailed Driver Selection

    cpp
    std::cout << "\nAvailable drivers for "; rideDate.print(); std::cout << ":\n";
    for (int i = 0; i < nDisplay; ++i)
    std::cout << i+1 << ". Name: " << eligibleDrivers[i]->getName()
    << ", Rating: " << eligibleDrivers[i]->averageRating() << ...

text

### 5. Smart Fare Calculation & Options

    cpp
    double fare = calculateFare(typeString, subtypeChoice, duration);
    if (preOpt == "C" || preOpt == "c") fare *= 0.9;
    if (preOpt == "D" || preOpt == "d") fare *= 1.1;
    if (preOpt == "A" || preOpt == "a") {
    std::cout << "Please provide feedback for this cancellation: ";
    getline(std::cin, cancelFeedback);
    }

text

### 6. Simulated Allocation and Journey

    cpp
    startTimer(allocationWait);
    int otp = generateOTP();
    std::cout << "OTP for Booking Confirmation: " << otp << std::endl;
    printArrivalTime(startHr, startMin, duration);

text

### 7. Live Ride Updates

    cpp
    if (needUpdates == "y" || needUpdates == "Y") giveOneUpdate(duration);

text

### 8. Rating and Feedback Collection

    cpp
    double rating;
    std::cout << "\nPlease rate your ride (1-5): ";
    std::cin >> rating; bk.setRating(rating);
    getline(std::cin, feedback);
    std::cout << "Your feedback: " << feedback << std::endl;

text

### 9. Booking History

    cpp
    BookingContainer<Booking> bookingList;
    bookingList.addBooking(bk);

text

### 10. Clean Resource Management

    cpp
    cleanup(vehicles, drivers);

text

---

## OOP Concepts Implementation (with Code Snippets)

### 1. Encapsulation

**Definition:** Encapsulation means hiding internal data and exposing only necessary methods to interact with the class.

    cpp
    class Booking {
    private:
    int bookingID; // Hidden: cannot access directly from outside
    double fare;
    Driver* driver;
    public:
    int getBookingID() const { return bookingID; } // Controlled access
    double getFare() const { return fare; }
    Driver* getDriver() const { return driver; }
    // All ride details safely handled through public methods only
    };

text

---

### 2. Inheritance

**Definition:** Inheritance means creating new classes (derived) from an existing base, sharing and extending functionality.

    cpp
    class Vehicle {
    public:
    virtual void displayDetails() const = 0;
    // Base members and methods
    };

    class Car : public Vehicle {
    public:
    void displayDetails() const override {
    std::cout << "Car Details...\n";
    }
    // Extra Car-specific members/methods
    };

text
*Here, `Car` inherits from `Vehicle` and overrides `displayDetails()`.*

---

### 3. Polymorphism

**Definition:** Polymorphism allows you to use a base class pointer/reference to access objects of derived types and call their overridden methods.

    cpp
    Vehicle* v1 = new Car("KA01SED1001", "Sedan");
    Vehicle* v2 = new Bike("KA01SCT3001", "Scooty");

    // Polymorphic call: resolved at runtime
    v1->displayDetails(); // Calls Car's version
    v2->displayDetails(); // Calls Bike's version

text

---

### 4. Abstraction

**Definition:** Abstraction exposes only the essential features of the class and hides the complex implementation details.

    cpp
    class Driver {
    private:
    std::vector<double> ratings;
    public:
    double averageRating() const {
    return ratings.empty() ? 0.0 :
    std::accumulate(ratings.begin(), ratings.end(), 0.0) / ratings.size();
    }
    // The user only calls averageRating(), not knowing how ratings are actually calculated or stored.
    };

text
*User interacts only via public methods, not with rating vector internals.*

---

### 5. Composition

**Definition:** Composition links classes together so one class "has-a" instance/pointer of another class.

    cpp
    class Driver {
    private:
    Vehicle* assignedVehicle; // Composition: Driver "has-a" Vehicle
    public:
    Vehicle* getVehicle() const { return assignedVehicle; }
    };

    class Booking {
    private:
    Driver* driver; // Booking "has-a" Driver
    public:
    Driver* getDriver() const { return driver; }
    };

text

---

### 6. Templates/Generics

**Definition:** C++ templates allow you to write classes/functions that work with any data type.

    cpp
    template<class T>
    class BookingContainer {
    private:
    std::vector<T> bookings;
    public:
    void addBooking(const T& booking) { bookings.push_back(booking); }
    void displayAll() const { for(const auto& b : bookings) b.printBooking(); }
    };

    // Usage example:
    BookingContainer<Booking> bookingList;
    bookingList.addBooking(bk); // bk is a Booking object

text

---

## Sample Utility Struct

// Simple Date struct for ride scheduling

    cpp
    struct Date {
    int day;
    int month;
    int year;
    void print() const {
    std::cout << day << "/" << month << "/" << year;
    }
    };

text

---

# Features Implementation

(See previous sections for code-backed examples like driver filtering, booking flows, fare logic, resource management, and feedback.)

---

# Architecture & Design

Refer to [Class Relationships](#class-relationships) and the snippets above for example inheritance, polymorphism, and composition patterns.
