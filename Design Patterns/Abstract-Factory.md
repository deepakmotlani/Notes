### Abstract Factory
This pattern is 1 level above the factory pattern it actually returns the factory of object.

Lets suppose we have 2 type of objects Bank & Loan. For these we have BankFactory & LoanFactory interfaces. These BankFactory & LoanFactory are implemented by HDFCBank, SBIBank etc. & HomeLoan, Personal Loan etc. respectively.

These 2 factories i.e. BankFactory & LoanFactory extends AbstractFactory class as below

```
abstract class AbstractFactory{  
  public abstract Bank getBank(String bank);  
  public abstract Loan getLoan(String loan);  
}

class BankFactory extends AbstractFactory{  
   public Bank getBank(String bank){  
      if(bank == null){  
         return null;  
      }  
      if(bank.equalsIgnoreCase("HDFC")){  
         return new HDFC();  
      } else if(bank.equalsIgnoreCase("ICICI")){  
         return new ICICI();  
      } else if(bank.equalsIgnoreCase("SBI")){  
         return new SBI();  
      }  
      return null;  
   }  
  public Loan getLoan(String loan) {  
      return null;  
   }  
}

class LoanFactory extends AbstractFactory{  
     public Bank getBank(String bank){  
        return null;  
     }  

     public Loan getLoan(String loan){  
      if(loan == null){  
         return null;  
      }  
      if(loan.equalsIgnoreCase("Home")){  
         return new HomeLoan();  
      } else if(loan.equalsIgnoreCase("Business")){  
         return new BussinessLoan();  
      } else if(loan.equalsIgnoreCase("Education")){  
         return new EducationLoan();  
      }  
      return null;  
   }       
}  

class FactoryCreator {  
     public static AbstractFactory getFactory(String choice){  
      if(choice.equalsIgnoreCase("Bank")){  
         return new BankFactory();  
      } else if(choice.equalsIgnoreCase("Loan")){  
         return new LoanFactory();  
      }  
      return null;  
   }  
}
```

Now you need to 1st get the factory & from that factory you will get the objects.
