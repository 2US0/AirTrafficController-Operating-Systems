# Air Traffic Control System

This project simulates an Air Traffic Control System using various operating system concepts. The system is composed of multiple entities such as planes (both passenger and cargo), airports, an air traffic controller, passengers, and a cleanup process. Each entity is implemented as a separate POSIX-compliant C program, and the system utilizes inter-process communication (IPC) mechanisms like pipes and message queues to simulate real-world interactions between these entities.

## Overview

The Air Traffic Control System involves multiple processes interacting to simulate the real-time operation of air traffic management. The system handles the departure and arrival of planes at various airports, manages passengers and cargo, and ensures synchronization and proper communication between all components.

## Components

### Plane

Each plane is a single-threaded process with the following features:
- Prompts user for a unique Plane ID and type (passenger or cargo).
- For passenger planes, prompts for the number of occupied seats and gathers information about passengers' luggage and body weight.
- For cargo planes, prompts for the number of cargo items and their average weight.
- Communicates with the air traffic controller and airports for departure and arrival processes.

### Passenger

Each passenger is a child process of a passenger plane process and is single-threaded. It gathers information about the passenger's luggage and body weight and communicates this to the parent plane process using pipes.

### Airport

Each airport is a multi-threaded process that handles the following:
- Prompts user for the airport number and the number of runways.
- Manages the arrival and departure of planes using a best-fit logic for runway assignment.
- Synchronizes multiple arrivals and departures using mutexes and semaphores.

### Air Traffic Controller

The air traffic controller is a single-threaded process that:
- Manages communication between planes and airports using a single message queue.
- Keeps track of plane journeys and logs information to a text file.
- Handles system termination requests from the cleanup process.

### Cleanup

The cleanup process is a single-threaded process that:
- Continuously prompts the user to terminate the Air Traffic Control System.
- Informs the air traffic controller to initiate the system termination process.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/air-traffic-control-system.git
   cd air-traffic-control-system
   ```

2. Compile the programs using the provided `Makefile`:
   ```bash
   make
   ```

## Usage

1. Start the air traffic controller:
   ```bash
   ./airtrafficcontroller.out
   ```

2. Start the airport processes (one for each airport):
   ```bash
   ./airport.out
   ```

3. Start the plane processes (one for each plane):
   ```bash
   ./plane.out
   ```

4. Optionally, start the cleanup process:
   ```bash
   ./cleanup.out
   ```
