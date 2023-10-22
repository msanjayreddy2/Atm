# Atm
class Account:
    def __init__(self, user_id, pin, balance):
        self.user_id = user_id
        self.pin = pin
        self.balance = balance
        self.transaction_history = []
        

    def deposit(self, amount):
        self.balance += amount
        self.transaction_history.append(f"Deposit: +${amount}")

    def withdraw(self, amount):
        if self.balance >= amount:
            self.balance -= amount
            self.transaction_history.append(f"Withdraw: -${amount}")
        else:
            print("Insufficient funds.")

    def transfer(self, recipient, amount):
        if self.balance >= amount:
            self.balance -= amount
            recipient.balance += amount
            self.transaction_history.append(f"Transfer to {recipient.user_id}: -${amount}")
            recipient.transaction_history.append(f"Transfer from {self.user_id}: +${amount}")
        else:
            print("Insufficient funds.")

    def display_transaction_history(self):
        print(self.transaction_history)
        


Accounts={}
account1 = Account("1234",1010, 1000)
account2 = Account("5678",2345,500)
Accounts["1234"]=account1
Accounts["5678"]=account2
print(Accounts)
while True:
    user_id = input("Enter User ID: ")
    pin = input("Enter PIN: ")
    if user_id in Accounts or pin ==Accounts[user_id].pin:
        while True:
            print("\nATM Menu:")
            print("1. Deposit")
            print("2. Withdraw")
            print("3. Transfer")
            print("4. Transaction History")
            print("5. Quit")
            choice = input("Enter your choice: ")
            if choice == "1":
                amount = float(input("Enter the deposit amount: $"))
                Accounts[user_id].deposit(amount)
            elif choice == "2":
                amount = float(input("Enter the withdrawal amount: $"))
                Accounts[user_id].withdraw(amount)
            elif choice == "3":
                recipient_id = input("Enter the recipient's User ID: ")
                while recipient_id not in Accounts:
                    print(" user_id not found:")
                    recipient_id = input("Enter the recipient's User ID: ")
                    break
                amount = float(input("Enter the transfer amount: $"))
                
                Accounts[user_id].transfer(Accounts[recipient_id], amount)
            elif choice == "4":
                Accounts[user_id].display_transaction_history()
            elif choice == "5":
                print("Thank you for using the ATM. Goodbye!")
                break
            else:
                print("Invalid choice. Please try again.")
    else:
        print("Invalid User ID or PIN. Please try again.")
