# UML-Class_Diagram - RBS

## 1. 


                   +---------------------+
                   |       Vehicle       |    <<abstract>>
                   +---------------------+
                   | - number: string    |
                   | - type: string      |
                   | - subType: string   |
                   +---------------------+
                   | + Vehicle(num, tp,stp)
                   | + getType()         |
                   | + getSubType()      |
                   | + getNumber()       |
                   | + displayDetails()=0|
                   +----------^----------+    
                      |        |        |
         --------------         -------------   ------------
        |                            |                      |
    +----------------+     +---------------------+   +--------------------+
    |      Car       |     |       Bike          |   |       Auto         |
    +----------------+     +---------------------+   +--------------------+
    | + Car(num,stp) |     | + Bike(num,stp)     |   | + Auto(num)        |
    | + displayDetails() | | + displayDetails()  |   | + displayDetails() |
    +----------------+     +---------------------+   +--------------------+


**OOPS concepts**: Abstraction,Inheritance,Polymorphism,Encapsulation

## 2.
                   +-------------------------------+
                   |           Driver              |
                   +-------------------------------+
                   | - name: string                |
                   | - gender: string              |
                   | - mobile: string              |
                   | - id: int                     |
                   | - assignedVehicle: Vehicle*   |
                   | - ratings: vector<double>     |
                   | - availableDaysOfMonth: vector<int> |
                   +-------------------------------+
                   | + Driver(...)                 |
                   | + display()                   |
                   | + getVehicle()                |
                   | + getGender()                 |
                   | + getName()                   |
                   | + getID()                     |
                   | + getMobile()                 |
                   | + averageRating()             |
                   | + isAvailableOnDay(day:int)   |
                   +-------------------------------+
                   
**OOPS concepts**: Encapsulation,Composition,Abstraction,Data integrity and modularity

## 3.

                   +----------------------------+
                   |         Booking            |
                   +----------------------------+
                   | - bookingID: int           |
                   | - duration: int            |
                   | - otp: int                 |
                   | - riderName: string        |
                   | - startLocation: string    |
                   | - destination: string      |
                   | - userMobile: string       |
                   | - bookeeName: string       |
                   | - driver: Driver*          |
                   | - rating: double           |
                   | - fare: double             |
                   | - rideDate: Date           |
                   +----------------------------+
                   | + Booking(...)             |
                   | + printBooking()           |
                   | + setRating(rate:double)   |
                   | + getDuration()            |
                   +----------------------------+

**OOPS concepts**: Encapsulation,Composition,Abstraction,Extensibility

## 4.

                   +------------------------------+
                   |      BookingContainer<T>     |    <<template>>
                   +------------------------------+
                   | - bookings: vector<T>        |
                   +------------------------------+
                   | + addBooking(const T&)       |
                   | + displayAll()               |
                   +------------------------------+

**OOPS concepts**: Encapsulation,Abstraction,Templates,Modularity                  

## 5.
                   +---------------------+       <<struct>>
                   |        Date         |
                   +---------------------+
                   | - day: int          |
                   | - month: int        |
                   | - year: int         |
                   +---------------------+
                   | + print()           |
                   +---------------------+
                   
**OOPS concepts**: Grouping related data,Utility struct,Simple encapsulation,Common practice               
