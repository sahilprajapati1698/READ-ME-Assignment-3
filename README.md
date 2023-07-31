Sahil Prajapati 

CSC 7200

Student ID - @01410508


QUESTION 1 ANSWER

1.	SOURCE CODE


class Employee {
    private String name;
    private String department;
    private double payRate;

    public Employee(String name, String department, double payRate) {
        this.name = name;
        this.department = department;
        this.payRate = payRate;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

    public void setPayRate(double payRate) {
        this.payRate = payRate;
    }

    public String getNameAndDepartment() {
        return name + " - " + department;
    }

    public double weeklyPay(int hoursWorked) {
        if (hoursWorked < 40) {
            return hoursWorked * payRate;
        } else {
            return 40 * payRate;
        }
    }
}


class UnionEmployee extends Employee {
    private double dues;

    public UnionEmployee(String name, String department, double payRate, double dues) {
        super(name, department, payRate);
        this.dues = dues;
    }

    public void setDues(double dues) {
        this.dues = dues;
    }

    @Override
    public double weeklyPay(int hoursWorked) {
        double basePay = super.weeklyPay(hoursWorked);
        double overtimePay = Math.max(hoursWorked - 40, 0)* (hourly_pay * 1.5);
        return basePay + overtimePay - dues;
    }
}



class CommissionEmployee extends Employee {
    private double commissionRate;
    private double salesAmount;

    public CommissionEmployee(String name, String department, double payRate, double commissionRate) {
        super(name, department, payRate);
        this.commissionRate = commissionRate;
        this.salesAmount = 0;
    }

    public void setCommissionRate(double commissionRate) {
        this.commissionRate = commissionRate;
    }

    public void setSalesAmount(double salesAmount) {
        this.salesAmount = salesAmount;
    }

    @Override
    public double weeklyPay(int hoursWorked) {
        double basePay = super.weeklyPay(hoursWorked);
        return basePay + (commissionRate * salesAmount);
    }
}


public class TestEmployees {
    public static void display(Employee employee, int hoursWorked) {
        System.out.println("Employee Info: " + employee.getNameAndDepartment());
        System.out.printf("Weekly Pay: $%.2f%n", employee.weeklyPay(hoursWorked));
        System.out.println();
    }

    public static void main(String[] args) {
        // Creating instances of UnionEmployee and CommissionEmployee
        UnionEmployee unionEmployee = new UnionEmployee("John Doe", "HR", 25.0, 20.0);
        CommissionEmployee commissionEmployee = new CommissionEmployee("Jane Smith", "Sales", 20.0, 0.1);

        // Testing for different hours worked
        int hoursWorkedLessThan40 = 30;
        int hoursWorked40 = 40;
        int hoursWorkedGreaterThan40 = 50;

        System.out.println("Testing Union Employee:");
        display(unionEmployee, hoursWorkedLessThan40);
        display(unionEmployee, hoursWorked40);
        display(unionEmployee, hoursWorkedGreaterThan40);

        System.out.println("Testing Commission Employee:");
        display(commissionEmployee, hoursWorkedLessThan40);
        display(commissionEmployee, hoursWorked40);
        display(commissionEmployee, hoursWorkedGreaterThan40);
    }
}

