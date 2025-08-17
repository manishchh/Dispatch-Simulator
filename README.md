# 🚖 Nüber Dispatch Simulator (Concurrent Programming in Java)

## 📖 Overview
This project implements a **concurrent simulation of a ride-sharing system (Nüber – an Uber clone)**.  
It was developed as part of a university project to evaluate the impact of government regulations on the maximum number of drivers allowed per region in a city.  

The simulator models:
- Passengers requesting rides  
- Drivers being dispatched  
- Regions with configurable concurrency limits  
- A dispatch system that manages bookings and ensures fairness across regions  

The project is designed to **stress-test Java concurrency features** by handling multiple simultaneous bookings while respecting per-region restrictions and driver availability.  

---

## 🎯 Key Features
- **Concurrent Bookings:** Multiple passengers can book rides simultaneously.  
- **Driver Dispatching:** Drivers are allocated on a FIFO (first-in, first-out) basis from a central pool.  
- **Region Limits:** Each region enforces a configurable maximum number of active bookings.  
- **Thread Management:** Each booking is processed in its own thread, simulating real-world asynchronous ride handling.  
- **Booking Lifecycle:** Passengers are picked up, driven to destinations, and drivers are released back into the pool.  
- **Simulation Engine:** Easily configurable to test different numbers of drivers, passengers, and regional booking caps.  
- **Graceful Termination:** The program completes all active bookings and exits cleanly without leaving background threads.  

---

## 🛠️ Concurrency & Multithreading Concepts Demonstrated
This project is a strong demonstration of **Java concurrency best practices**, showcasing:

- **Thread creation and management** via `Runnable` and `Callable`.  
- **Synchronization** to prevent race conditions on shared resources (e.g., driver pool, booking IDs).  
- **Thread-safe collections** to manage bookings and drivers concurrently.  
- **Blocking and waiting strategies** to ensure fairness and avoid deadlocks.  
- **Executor services & futures** for structured concurrency (ensuring results are returned once jobs complete).  
- **Concurrency stress testing** with multiple passengers, drivers, and regions.  

---

## 🧩 Core Components
- **Person (abstract)** – Base class for `Passenger` and `Driver`.  
- **Passenger** – Generates random travel times.  
- **Driver** – Picks up passengers, simulates driving delays, and returns to idle queue.  
- **Booking** – Represents a ride, uniquely identified with a sequential booking ID (thread-safe).  
- **BookingResult** – Stores results (booking ID, passenger, driver, total trip time).  
- **NuberRegion** – Enforces per-region concurrency limits on bookings.  
- **NuberDispatch** – Central dispatcher that manages drivers, assigns them to regions, and coordinates bookings.  
- **Simulation** – Runs configurable experiments to test how regulation changes impact performance.  

---

## ⚙️ How It Works
1. **Simulation Setup:** Define number of drivers, passengers, and per-region booking caps.  
2. **Booking Requests:** Passengers make ride requests concurrently.  
3. **Dispatching:** The system assigns available drivers to passengers in FIFO order.  
4. **Execution:** Each booking runs in a separate thread (pickup + travel time).  
5. **Completion:** Once trips finish, drivers are released back to the idle pool.  
6. **Termination:** The program exits automatically when all jobs are done.  

---

## 📊 Example Simulation Output
```text
Creating Nuber Dispatch
Creating 2 regions
Creating Nuber region for South
Creating Nuber region for North
Done creating 2 regions

1:null:P-Harold: Starting booking, getting driver
2:null:P-Isabella: Starting booking, getting driver
3:D-Kenneth:P-Jerry: Starting, on way to passenger
4:D-Olivia:P-Stephen: At destination, driver is now free

Active bookings: 10, pending: 6
Active bookings: 8, pending: 4
Active bookings: 0, pending: 0

Simulation complete in 4036ms
