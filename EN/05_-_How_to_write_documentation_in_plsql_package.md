Writing documentation for a PL/SQL package involves providing clear, concise, and well-structured information about the package, its functions, and procedures. This helps other developers understand the purpose of the package, how it works, and how to use it effectively. Here's a step-by-step guide on how to write documentation for a PL/SQL package:

Provide an overview:
Start by providing a brief overview of the package. Explain its purpose, features, and any dependencies or prerequisites.

```
/*
  Package Name: EMPLOYEE_MGMT
  Author: Your Name
  Creation Date: 30-Mar-2023
  Description: This package manages employee data, including CRUD operations and calculations for employee statistics.
  Dependencies: HR schema
*/
```
Document each function and procedure:
For each function and procedure in the package, provide a detailed description of its purpose, input parameters, return values, and any exceptions it may raise.

```
/*
  Function: GET_EMPLOYEE
  Description: Retrieves employee data based on the employee_id.
  Parameters:
    - p_employee_id: The ID of the employee to be fetched. (IN, NUMBER)
  Returns:
    - Employee record as a user-defined object (EMPLOYEE_REC).
  Exceptions:
    - EMPLOYEE_NOT_FOUND: Raised if the employee_id does not exist in the database.
*/
```
Include inline comments:
Use inline comments to explain complex logic, loops, or conditions within your functions and procedures. This will help developers understand the code's purpose and functionality.

```
PROCEDURE update_employee_salary (p_employee_id NUMBER, p_new_salary NUMBER) IS
BEGIN
  -- Validate the input parameters
  IF p_employee_id IS NULL OR p_new_salary IS NULL THEN
    RAISE INVALID_INPUT;
  END IF;

  -- Update the salary of the specified employee
  UPDATE employees
  SET salary = p_new_salary
  WHERE employee_id = p_employee_id;

  -- Check if the update was successful
  IF SQL%ROWCOUNT = 0 THEN
    RAISE EMPLOYEE_NOT_FOUND;
  END IF;

  COMMIT;
EXCEPTION
  WHEN INVALID_INPUT THEN
    RAISE_APPLICATION_ERROR(-20001, 'Invalid input parameters');
  WHEN EMPLOYEE_NOT_FOUND THEN
    RAISE_APPLICATION_ERROR(-20002, 'Employee not found');
END update_employee_salary;
```
Provide usage examples:
Include examples demonstrating how to use the package functions and procedures. This can be especially helpful for complex operations or when specific input data is required.

```
/*
  Usage Example:

  -- Declare a variable to store the employee record
  DECLARE
    l_employee_rec EMPLOYEE_MGMT.EMPLOYEE_REC;
  BEGIN
    -- Fetch the employee data
    l_employee_rec := EMPLOYEE_MGMT.GET_EMPLOYEE(100);

    -- Display the employee data
    DBMS_OUTPUT.PUT_LINE('Employee ID: ' || l_employee_rec.employee_id);
    DBMS_OUTPUT.PUT_LINE('First Name: ' || l_employee_rec.first_name);
    DBMS_OUTPUT.PUT_LINE('Last Name: ' || l_employee_rec.last_name);
  END;
/
*/
```
By following these guidelines, you can create well-documented PL/SQL packages that are easy for other developers to understand and use.