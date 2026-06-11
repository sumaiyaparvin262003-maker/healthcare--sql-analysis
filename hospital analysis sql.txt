
--Step_1: create hospital data table

create table hospital_data
(
Hospital_Name varchar(100),
Location_ varchar (100),
Department varchar (100),
Doctors_Count int,
Patients_Count int,
Admission_Date date,
Discharge_Date  date,
Medical_Expenses numeric(10,2)
);

-- Data Validation : Display all records to verify successful data import

select * from hospital_data;

 -- 1. Total Number of Patients
--Write an SQL query to find the total number of patients across all hospitals.

select sum(patients_count) as total_no_of_patients from hospital_data;


-- 2. Average Number of Doctors per Hospital
-- Retrieve the average count of doctors available in each hospital.

select hospital_name, avg(doctors_count) as avg_no_of_dr from hospital_data group by hospital_name ;

-- 3. Hospital with the Maximum Medical Expenses
-- Identify the hospital that recorded the highest medical expenses.

select hospital_name, medical_expenses from hospital_data order by medical_expenses desc limit 3 ;

-- 4. Top 3 Departments with the Highest Number of Patients
-- Find the top 3 hospital departments that have the highest number of patients.

select department, patients_count from hospital_data order by patients_count desc limit 3 ;

-- 5. Daily Average Medical Expenses
-- Calculate the average medical expenses per day for each hospital.

select hospital_name, avg(medical_expenses) as avg_daily_expenses from hospital_data group by hospital_name;


-- 6. Total Patients Treated Per City
-- Count the total number of patients treated in each city.

select location_, sum(patients_count) as total_patient_count from hospital_data group by location_;


-- 7. Identify the Department with the Lowest Number of Patients
-- Find the department with the least number of patients.

select department, patients_count from hospital_data order by patients_count asc limit 3 ;

-- 8. Longest Hospital Stay
-- Find the patient with the longest stay by calculating the difference between Discharge Date and Admission Date.

select hospital_name, admission_date, discharge_date, (discharge_date - admission_date) as stay  from hospital_data order by stay desc limit 10;  


-- 9. Average Length of Stay Per Department
-- Calculate the average number of days patients spend in each department.

select department, avg (discharge_date - admission_date) as length_stay_per_dept from hospital_data group by department;

-- 10. Monthly Medical Expenses Report
-- Group the data by month and calculate the total medical expenses for each month.

select date_trunc('month', admission_date) as month_, sum (medical_expenses) as total__expenses from hospital_data
group by date_trunc('month', admission_date) order by month_;
