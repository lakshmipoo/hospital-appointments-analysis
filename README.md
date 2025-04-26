# hospital-appointments-analysis
Power BI project analyzing hospital appointment no-shows using Excel, SQL, and Power BI.
# Hospital Appointments - No-Show Analysis (Power BI Project)

This project analyzes hospital appointment data to identify factors affecting patient no-shows using Excel, SQL, and Power BI.

## Tools Used:
- Microsoft Excel
- MySQL
- Power BI

## Key Insights:
- No-show rate by gender
- No-show rate by weekday
- Impact of scholarship on no-shows
- Appointment patterns by neighborhood

## Project Files:
- `Hospital_Appointments_Dashboard.pbix` - Power BI interactive dashboard

---
 1. Database and Table Creation
    CREATE DATABASE HospitalAppointments;
USE HospitalAppointments;

CREATE TABLE Appointments2 (
    PatientId BIGINT,
    AppointmentID BIGINT,
    Gender VARCHAR(1),
    ScheduledDay DATE,
    AppointmentDay DATE,
    Age INT,
    Neighbourhood VARCHAR(100),
    Scholarship TINYINT,
    Hipertension TINYINT,
    Diabetes TINYINT,
    VisitShow VARCHAR(3),
    WaitingTime INT,
    DayOfWeek VARCHAR(15)
);
2. Loading Data into SQL
LOAD DATA LOCAL INFILE 'path_to_csv/appointments_cleaned.csv'
INTO TABLE Appointments2
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
3. Basic Exploratory Queries
 SELECT COUNT(*) AS TotalAppointments FROM Appointments2;
 SELECT COUNT(*) AS TotalNoShows FROM Appointments2 WHERE VisitShow = 'No';
 SELECT ROUND(
    (SUM(CASE WHEN VisitShow = 'No' THEN 1 ELSE 0 END) / COUNT(*)) * 100, 2
) AS NoShowRatePercentage FROM Appointments2;
SELECT Gender,
       COUNT(*) AS TotalAppointments,
       SUM(CASE WHEN VisitShow = 'No' THEN 1 ELSE 0 END) AS TotalNoShows,
       ROUND(SUM(CASE WHEN VisitShow = 'No' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS NoShowRate
FROM Appointments2
GROUP BY Gender;

 --Built as part of my data analyst portfolio journey.
