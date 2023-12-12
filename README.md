# Decorator
Lab Assignment 10

CIMB is a digital bank that offers GSave and UpSave savings accounts.   As with a typical Savings Account, it contains accountNumber, accountName, and a balance for that account.

The typical savings account offers an interest rate of 1%.
The benefits of the typical savings account is the same with the "Standard Savings Account" as compared to other banks.

The GSave account offers an interest rate of 2.5%.
Benefits include the "Standard Savings Account" plus access to "GCash transfer".

The UpSave account offers the highest interest rate of 4.0%.
Benefits include the "Standard Savings Account" plus "with Insurance".


Develop a decorator pattern approach that will implement the given UML diagram:



The content of your Cimb.java should ONLY contain the following codes with the exception of inserting your own package name :




public class Cimb {

	public static void main(String[] args) {
		
		SavingsAccount account = new SavingsAccount();
		
		account.setAccountNumber(1234);
		account.setAccountName("Juan Dela Cruz");
		account.setBalance(10000.0);
		
		System.out.println(account.showInfo());
		System.out.println("Account type: " + account.showAccountType());
		System.out.println("Interest rate: " + account.getInterestRate());
		System.out.println("New balance: " + account.computeBalanceWithInterest());
		System.out.println("Benefits: " + account.showBenefits());
		
		System.out.println("----------------------");
		
		GSave gSave = new GSave(account);
		System.out.println(gSave.showInfo());
		System.out.println("Account type: " + gSave.showAccountType());
		System.out.println("Interest rate: " + gSave.getInterestRate());
		System.out.println("New balance: " + gSave.computeBalanceWithInterest());
		System.out.println("Benefits: " + gSave.showBenefits());
		
		System.out.println("----------------------");
		
		UpSave upSave = new UpSave(account);
		System.out.println(upSave.showInfo());
		System.out.println("Account type: " + upSave.showAccountType());
		System.out.println("Interest rate: " + upSave.getInterestRate());
		System.out.println("New balance: " + upSave.computeBalanceWithInterest());
		System.out.println("Benefits: " + upSave.showBenefits());
	}
}









You should display the following output:



Description of the following methods

showAccountType() - Either returns "Savings Account", "GSave" or "UpSave"
getInterestRate() - Either returns 1% for Savings Account; 2.5% for GSave; 4.0% UpSave
getBalance() - Returns the balance of the account set.
showBenefits() - Either returns "Standard Savings Account" for Savings Account;
		    benefits offered by savings account + "GSave Transfer";
                            benefits offered by savings account + "With Insurance";
computeBalanceWithInterest() - returns new balance by computing the balance plus the interest depending on the interest rate.
showInfo() - Returns details of account number, account name, and balance.

BankAcountDecorator must be an interface.

Follow instructions.  You are not allowed to insert other methods except what is stated in the diagram (setters and getters are allowed).


In your solution you must provide the following in your Github link account:
  Problem statement (description of the problem. Just copy what is stated here).
  UML Class Diagram
  Uploaded java codes for the solution.










                +------------------+
                |    Component     |
                +------------------+
                |    operation()   |
                +------------------+
                        /\
                        |
                        |
            +----------------------+
            |      ConcreteComponent |
            +----------------------+
            |   operation()         |
            +----------------------+
                        /\
                        |
                        |
            +----------------------+
            |     Decorator         |
            +----------------------+
            |   -component: Component|
            +----------------------+
            |   operation()         |
            +----------------------+
                        /\
                        |
                        |
            +----------------------+
            |  ConcreteDecorator    |
            +----------------------+
            |   operation()         |
            |   addedBehavior()     |
            +----------------------+










// Step 1: Component interface
interface Component {
    String operation();
}

// Step 2: ConcreteComponent
class ConcreteComponent implements Component {
    @Override
    public String operation() {
        return "ConcreteComponent operation";
    }
}

// Step 3: Decorator
abstract class Decorator implements Component {
    private Component component;

    public Decorator(Component component) {
        this.component = component;
    }

    @Override
    public String operation() {
        return component.operation();
    }
}

// Step 4: ConcreteDecorator
class ConcreteDecorator extends Decorator {
    public ConcreteDecorator(Component component) {
        super(component);
    }

    @Override
    public String operation() {
        return "ConcreteDecorator operation, " + super.operation();
    }

    public String addedBehavior() {
        return "Additional behavior";
    }
}

// Example usage
public class DecoratorPatternExample {
    public static void main(String[] args) {
        // Creating a ConcreteComponent
        Component component = new ConcreteComponent();
        System.out.println("Result of ConcreteComponent: " + component.operation());

        // Wrapping ConcreteComponent with ConcreteDecorator
        Decorator decoratedComponent = new ConcreteDecorator(component);
        System.out.println("Result of Decorated Component: " + decoratedComponent.operation());
        System.out.println("Result of Added Behavior: " + ((ConcreteDecorator) decoratedComponent).addedBehavior());
    }
}





In this Java implementation:

Component is an interface that declares the operation method.
ConcreteComponent is a concrete class that implements the Component interface.
Decorator is an abstract class that also implements the Component interface and holds a reference to a Component object.
ConcreteDecorator is a concrete class that extends Decorator and adds new functionality to the base component.
The example usage in the main method demonstrates how to use these classes to create a decorated component with additional behavior.
