# SQL_TASK-4
SQL queries using SUM, COUNT, AVG, GROUP BY
SELECT SUM(AmountPaid) AS TotalRevenue FROM payments;
SELECT COUNT(BookingID) AS TotalBookings FROM bookings;
SELECT AVG(TotalAmount) AS AvgBookingAmount FROM bookings;
SELECT MAX(TotalAmount) AS MaxBookingAmount FROM bookings;
SELECT g.GuestID,
       g.Name,
       ROUND(SUM(p.AmountPaid), 2) AS TotalPaid
FROM guests g
JOIN bookings b ON g.GuestID = b.GuestID
JOIN payments p ON b.BookingID = p.BookingID
GROUP BY g.GuestID, g.Name
ORDER BY TotalPaid DESC;
SELECT RoomID, COUNT(*) AS NumBookings
FROM bookings
GROUP BY RoomID
ORDER BY NumBookings DESC;
SELECT RoomType, ROUND(AVG(PricePerNight),2) AS AvgPrice
FROM rooms
GROUP BY RoomType;
SELECT BookingID, SUM(ServiceCost) AS TotalServiceCost
FROM services_used
GROUP BY BookingID;
-- Rooms with more than 1 booking
SELECT RoomID, COUNT(*) AS NumBookings
FROM bookings
GROUP BY RoomID
HAVING COUNT(*) > 1;

-- Guests who spent more than 10000
SELECT b.GuestID, g.Name, SUM(p.AmountPaid) AS TotalSpent
FROM payments p
JOIN bookings b ON p.BookingID = b.BookingID
JOIN guests g ON b.GuestID = g.GuestID
GROUP BY b.GuestID, g.Name
HAVING SUM(p.AmountPaid) > 10000;




