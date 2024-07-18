
# Transaction Management System

A Swift project to manage financial transactions, including adding, filtering, deleting, and calculating totals for transactions.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Tech Stack](#tech-stack)
- [License](#license)

## Features

- **Add Transactions**: Add new transactions with details like name, category, price, and date.
- **Add Categories**: Add unique categories to the system.
- **Filter Transactions**: Filter transactions by category.
- **Calculate Totals**: Calculate the total amount of transactions for a specific category.
- **Delete Transactions**: Delete transactions by their name.

## Installation

1. **Clone the repository**
   ```sh
   git clone https://github.com/Nafachri/Assignment1_NaufalAlFachri.playground.git
   ```

2. **Open the project**
   Open the cloned repository in Xcode.

## Usage

Here is an example of how to use the `Transaction` struct and `TransactionManager` class:

```swift
import Cocoa

// MARK: struct/class transaction
struct Transaction {
  var name: String
  var category: String
  var price: Double
  var date: Date = .now
}
  
// MARK: Dictionary
var distractionary: [String: Transaction] = [
  "Income": Transaction(name: "Uang Jajan", category: "Income", price: 50000.0)
]

for (key, transaction) in distractionary {
  print("Key: \(key), Transaction: \(transaction)")
}

// MARK: Class of Transaction Manager
class TransactionManager {
  var listOfTransaction: [Transaction] = []
  var listOfCategory: Set<String> = []
  
  // MARK: Adding Transaction Function
  func addTransaction(transaction: Transaction){
    listOfTransaction.append(transaction)
  }
  
  // MARK: Adding Category
  func addCategory(category: String){
    listOfCategory.insert(category)
  }
  
  // MARK: Filter Transaction
  func filterTransaction(type: String) -> [Transaction] {
    listOfTransaction.filter { $0.category == type }
  }
  
  // MARK: Calculate Total Transaction
  func calculateTotalTransaction(type: String) -> Double {
    filterTransaction(type: type).reduce(into: 0) { before, newValue in
      before += newValue.price
    }
  }
  
  // MARK: Delete Transaction By Name
  func deleteTransactionByName(name: String) {
    for (index, transaction) in listOfTransaction.enumerated() {
      if name == transaction.name {
        listOfTransaction.remove(at: index)
        break
      }
    }
  }
}

// Example usage
var transactionManager = TransactionManager()
transactionManager.addTransaction(transaction: Transaction(name: "Buy Petrol", category: "Expenses", price: 20_000))
transactionManager.addTransaction(transaction: Transaction(name: "Buy Martabak", category: "Expenses", price: 18_000))
transactionManager.addTransaction(transaction: Transaction(name: "Sell Monitor", category: "Income", price: 2_000_000))

print("list of transactions: ", transactionManager.listOfTransaction)
print("filter function: ", transactionManager.filterTransaction(type: "Income"))
transactionManager.deleteTransactionByName(name: "Buy Petrol")
print("calculate total transactions: ", transactionManager.calculateTotalTransaction(type: "Expenses"))
print("list of final transactions: ", transactionManager.listOfTransaction)
```

## Tech Stack

- **Language**: Swift
- **IDE**: Xcode
- **Framework**: Cocoa (for macOS development)

## License

This project is licensed under the WTFPL License - see the [WTFPL](https://en.wikipedia.org/wiki/WTFPL) file for details.
