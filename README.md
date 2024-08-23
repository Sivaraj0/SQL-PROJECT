# SQL-PROJECT
# Airlines Database Management
CREATE TABLE Airports (
    Airportcode INT PRIMARY KEY,
    AirportName VARCHAR(50),
    City VARCHAR(50),
    Country VARCHAR(50)
);

CREATE TABLE Flights (
    FlightID INT PRIMARY KEY,
    FlightNumber VARCHAR(10),
    DepartureAirportCode int ,
    ArrivalAirportCode int ,
    DepartureTime DATETIME,
    ArrivalTime DATETIME,
    Price DECIMAL(10, 2),
    FOREIGN KEY (DepartureAirportCode) REFERENCES Airports(AirportCode),
    FOREIGN KEY (ArrivalAirportCode) REFERENCES Airports(AirportCode)
);
select * from flights;

CREATE TABLE Passengers (
    PassengerID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100),
    PhoneNumber VARCHAR(20)
);

CREATE TABLE Tickets (
    TicketID INT PRIMARY KEY,
    PassengerID INT,
    FlightID INT,
    SeatNumber VARCHAR(10),
    FOREIGN KEY (PassengerID) REFERENCES Passengers(PassengerID),
    FOREIGN KEY (FlightID) REFERENCES Flights(FlightID)
);

select * from airports;

-- Insert some sample data
INSERT INTO Airports (AirportCode, AirportName, City, Country)
VALUES
    (1, 'John F. Kennedy International Airport', 'New York', 'USA'),
    (2, 'Los Angeles International Airport', 'Los Angeles', 'USA'),
    (3, 'Heathrow Airport', 'London', 'UK'),
    (4, 'Charles de Gaulle Airport', 'Paris', 'France'),
    (5, 'Chennai International Airport', 'Chennai', 'India'),
     (6, 'Dubai International Airport', 'Dubai', 'United Arab Emirates'),
    (7, 'Frankfurt Airport', 'Frankfurt', 'Germany'),
    (8, 'Changi Airport', 'Singapore', 'Singapore'),
    (9, 'Incheon International Airport', 'Seoul', 'South Korea'),
    (10, 'Sydney Kingsford Smith Airport', 'Sydney', 'Australia');
    

INSERT INTO Flights (FlightID,FlightNumber, DepartureAirportCode, ArrivalAirportCode, DepartureTime, ArrivalTime, Price)
VALUES
    (1, 'AA123', 1 , 2 , '2024-06-05 08:00:00', '2024-06-05 11:00:00', 250.00),
    (2, 'BA456', 2 , 3 , '2024-06-06 10:00:00', '2024-06-06 12:00:00', 150.00),
	 (3, 'DL789', 3 , 8 , '2024-06-07 09:30:00', '2024-06-07 14:30:00', 400.00),
    (4, 'AF101', 4 , 7 , '2024-06-08 07:45:00', '2024-06-08 11:15:00', 350.00),
    (5, 'UA112', 5 , 6 , '2024-06-09 13:00:00', '2024-06-09 18:00:00', 500.00),
    (6, 'EK223', 6 , 5 , '2024-06-10 06:00:00', '2024-06-10 09:00:00', 450.00),
    (7, 'SQ334', 7 , 4 , '2024-06-11 14:00:00', '2024-06-11 17:00:00', 420.00),
    (8, 'LH445', 8 , 3 , '2024-06-12 15:30:00', '2024-06-12 20:30:00', 380.00),
    (9, 'CX556', 9 , 2 , '2024-06-13 11:00:00', '2024-06-13 13:00:00', 300.00),
    (10, 'QF667', 10 , 1 , '2024-06-14 16:00:00', '2024-06-14 19:00:00', 290.00);
    select * from Passengers;
INSERT INTO Passengers (PassengerID , FirstName, LastName, Email, PhoneNumber)
VALUES
    (1,'John', 'Doe', 'john.doe@example.com', '123-456-7890'),
    (2,'Jane', 'Smith', 'jane.smith@example.com', '987-654-3210'),
	(3,'Michael', 'Johnson', 'michael.johnson@example.com', '555-123-4567'),
    (4,'Emily', 'Davis', 'emily.davis@example.com', '555-987-6543'),
    (5,'William', 'Brown', 'william.brown@example.com', '555-456-7890'),
    (6,'Olivia', 'Wilson', 'olivia.wilson@example.com', '555-321-9876'),
    (7,'James', 'Miller', 'james.miller@example.com', '555-654-1234'),
    (8,'Sophia', 'Taylor', 'sophia.taylor@example.com', '555-789-0123'),
    (9,'Benjamin', 'Anderson', 'benjamin.anderson@example.com', '555-234-5678'),
    (10,'Ava', 'Thomas', 'ava.thomas@example.com', '555-876-5432');

INSERT INTO Tickets (TicketID , PassengerID, FlightID, SeatNumber)
VALUES
    (1,1, 1, 'A1'),
    (2,2, 2, 'B2'),
	(3,3, 3, 'C3'),
	(4,4, 4, 'D4'),
	(5,5, 5, 'E5'),
	(6,6, 6, 'F6'), 
	(7,7, 7, 'G7'),
	(8,8, 8, 'H8'),
	(9,9, 9, 'I9'),
	(10, 10,10,'J10');
    select * from Airports;
    select * from Flights;
	select * from Passengers;
    select * from Tickets;
    DELIMITER //
CREATE PROCEDURE GetFlightInfo(IN flight_num VARCHAR(10))
BEGIN
    SELECT 
        Flights.FlightNumber,
        DepartureAirport.AirportName AS DepartureAirport,
        ArrivalAirport.AirportName AS ArrivalAirport,
        Flights.DepartureTime,
        Flights.ArrivalTime,
        Flights.Price
    FROM 
        Flights
    JOIN 
        Airports AS DepartureAirport ON Flights.DepartureAirportCode = DepartureAirport.AirportCode
    JOIN 
        Airports AS ArrivalAirport ON Flights.ArrivalAirportCode = ArrivalAirport.AirportCode
    WHERE 
        Flights.FlightNumber = flight_num;
END //
DELIMITER ;

-- Call the procedure
CALL GetFlightInfo('AA123');
select * from Tickets;
SELECT COUNT(*) AS TotalFlights
FROM Flights;
SELECT * FROM Flights
WHERE DepartureAirportCode = 9 AND ArrivalAirportCode = 2;
