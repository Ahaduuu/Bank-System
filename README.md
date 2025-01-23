class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance
        self.transaction_history = []
        
    def deposit(self, amount):
        """Deposit money into the account"""
        if amount <= 0:
            print("Deposit amount must be positive.")
        else:
            self.balance += amount
            self.transaction_history.append(f"Deposited: ${amount}")
            print(f"${amount} deposited. New balance: ${self.balance}")
    
    def withdraw(self, amount):
        """Withdraw money from the account"""
        if amount <= 0:
            print("Withdrawal amount must be positive.")
        elif amount > self.balance:
            print("Insufficient funds.")
        else:
            self.balance -= amount
            self.transaction_history.append(f"Withdrew: ${amount}")
            print(f"${amount} withdrawn. New balance: ${self.balance}")
    
    def check_balance(self):
        """Check the current balance of the account"""
        print(f"Account balance: ${self.balance}")
    
    def transfer(self, amount, target_account):
        """Transfer money to another account"""
        if self.balance >= amount:
            self.withdraw(amount)
            target_account.deposit(amount)
            self.transaction_history.append(f"Transferred: ${amount} to {target_account.owner}")
        else:
            print("Insufficient funds for transfer.")
    
    def show_transaction_history(self):
        """Show the list of transactions for the account"""
        print(f"Transaction history for {self.owner}:")
        for transaction in self.transaction_history:
            print(transaction)
        
# Example Usage:
def main():
    # Create two accounts
    account1 = BankAccount("Alice", 1000)
    account2 = BankAccount("Bob", 500)
    
    # Display initial balances
    account1.check_balance()
    account2.check_balance()
    
    # Deposit money
    account1.deposit(200)
    account2.deposit(300)
    
    # Withdraw money
    account1.withdraw(150)
    account2.withdraw(100)
    
    # Transfer money between accounts
    account1.transfer(250, account2)
    
    # Display balances after transactions
    account1.check_balance()
    account2.check_balance()
    
    # Display transaction history
    account1.show_transaction_history()
    account2.show_transaction_history()

if __name__ == "__main__":
    main()

