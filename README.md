CREATE TABLE Employees (
    emp_id INT AUTO_INCREMENT PRIMARY KEY,
    emp_name VARCHAR(100),
    salary DECIMAL(10, 2),
    department VARCHAR(50)
);
DELIMITER $$

CREATE PROCEDURE IncreaseSalary(
    IN p_emp_id INT,
    IN p_percentage DECIMAL(5,2)
)
BEGIN
    UPDATE Employees
    SET salary = salary + (salary * p_percentage / 100)
    WHERE emp_id = p_emp_id;
END $$

DELIMITER ;
CALL IncreaseSalary(1, 10);
DELIMITER $$

CREATE FUNCTION GetAnnualSalary(p_emp_id INT)
RETURNS DECIMAL(12,2)
DETERMINISTIC
BEGIN
    DECLARE monthly_salary DECIMAL(10,2);

    SELECT salary INTO monthly_salary
    FROM Employees
    WHERE emp_id = p_emp_id;

    RETURN monthly_salary * 12;
END $$

DELIMITER ;
SELECT emp_name, GetAnnualSalary(emp_id) AS annual_salary
FROM Employees;
CREATE PROCEDURE IncreaseSalary(IN p_emp_id INT, IN p_percentage DECIMAL(5,2))
CREATE FUNCTION GetAnnualSalary(p_emp_id INT) RETURNS DECIMAL(12,2)
