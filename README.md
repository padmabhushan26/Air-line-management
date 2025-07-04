# Air-line-managementclass Flight:
    def __init__(self, flight_number, origin, destination, seats):
        self.flight_number = flight_number
        self.origin = origin
        self.destination = destination
        self.seats = seats  # total seats
        self.booked_passengers = []

    def book_seat(self, passenger_name):
        if len(self.booked_passengers) < self.seats:
            self.booked_passengers.append(passenger_name)
            print(f"Seat booked for {passenger_name} on flight {self.flight_number}")
        else:
            print("No available seats!")

    def cancel_booking(self, passenger_name):
        if passenger_name in self.booked_passengers:
            self.booked_passengers.remove(passenger_name)
            print(f"Booking cancelled for {passenger_name}")
        else:
            print(f"No booking found for {passenger_name}")

    def show_passengers(self):
        if not self.booked_passengers:
            print("No passengers booked yet.")
        else:
            print("Passenger List:")
            for p in self.booked_passengers:
                print(f"- {p}")

    def flight_info(self):
        print(f"\nFlight {self.flight_number}: {self.origin} -> {self.destination}")
        print(f"Total seats: {self.seats} | Available: {self.seats - len(self.booked_passengers)}")


class AirlineSystem:
    def __init__(self):
        self.flights = {}

    def add_flight(self, flight_number, origin, destination, seats):
        if flight_number in self.flights:
            print("Flight already exists!")
        else:
            self.flights[flight_number] = Flight(flight_number, origin, destination, seats)
            print(f"Flight {flight_number} added.")

    def view_flights(self):
        if not self.flights:
            print("No flights available.")
        else:
            for flight in self.flights.values():
                flight.flight_info()

    def book_seat(self, flight_number, passenger_name):
        if flight_number in self.flights:
            self.flights[flight_number].book_seat(passenger_name)
        else:
            print("Flight not found.")

    def cancel_booking(self, flight_number, passenger_name):
        if flight_number in self.flights:
            self.flights[flight_number].cancel_booking(passenger_name)
        else:
            print("Flight not found.")

    def show_passengers(self, flight_number):
        if flight_number in self.flights:
            self.flights[flight_number].show_passengers()
        else:
            print("Flight not found.")


# Example interaction (CLI-like)
if __name__ == "__main__":
    system = AirlineSystem()

    while True:
        print("\n--- Airline Management Menu ---")
        print("1. Add Flight")
        print("2. View Flights")
        print("3. Book Seat")
        print("4. Cancel Booking")
        print("5. Show Passenger List")
        print("6. Exit")
        
        choice = input("Choose an option: ")

        if choice == '1':
            fn = input("Flight number: ")
            origin = input("Origin: ")
            dest = input("Destination: ")
            seats = int(input("Number of seats: "))
            system.add_flight(fn, origin, dest, seats)

        elif choice == '2':
            system.view_flights()

        elif choice == '3':
            fn = input("Flight number: ")
            name = input("Passenger name: ")
            system.book_seat(fn, name)

        elif choice == '4':
            fn = input("Flight number: ")
            name = input("Passenger name: ")
            system.cancel_booking(fn, name)

        elif choice == '5':
            fn = input("Flight number: ")
            system.show_passengers(fn)

        elif choice == '6':
            print("Exiting system. Goodbye!")
            break

        else:
            print("Invalid choice. Please try again.")
