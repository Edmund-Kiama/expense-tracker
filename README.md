# Vue Expense Tracker Application

This is a Vue.js application designed for tracking transactions, including income and expenses. The application allows users to input and delete transactions, and it calculates and displays the balance, total income, and total expenses dynamically. The data is stored in the browser's localStorage, ensuring persistence across page reloads.

## Features

### Core Functionality

- **Track Transactions**: Users can add transactions (income or expenses) through a form.
- **Display Balance**: Automatically calculates and displays the current balance by summing the income and expenses.
- **View Income and Expenses**: Separate sections show the total income and total expenses.
- **Delete Transactions**: Users can delete individual transactions from the list.
- **Data Persistence**: All transactions are saved to `localStorage` for persistence across sessions.

### Highlights

- Reactive data updates using Vue’s `ref` and `computed` properties.
- Dynamic rendering of income, expenses, and balance using Vue components.
- Local storage integration for saving transactions across sessions.
- Modular and reusable components for easy maintainability.

## Application Structure

The application is organized into multiple Vue components, each responsible for specific functionality.

### Components

1. **`Header.vue`**  
   Displays the application header, providing an overview and title for the app.
   
2. **`Balance.vue`**  
   Shows the current balance calculated from the income and expenses.

3. **`IncomeExpenses.vue`**  
   Displays the total income and expenses. It receives computed values for income and expenses as props.
   
4. **`TransactionList.vue`**  
   Renders the list of transactions. Each transaction can be deleted via an event handler.
   
5. **`AddTransaction.vue`**  
   Provides an interface for users to input new transactions. It emits an event with the submitted data.

## Core Logic

### Data Binding and Computation

- **Transactions**: Transactions are stored in a reactive `ref` array, where each transaction includes an `id`, `text`, and `amount`.
- **Balance Calculation**: The balance is computed dynamically by summing up the amount values from all transactions.
- **Income Calculation**: Income is filtered and computed from the transactions with positive amounts.
- **Expenses Calculation**: Expenses are computed similarly, with a filter for negative amounts.

### Adding and Deleting Transactions

- **Add Transaction**: The handleTransactionSubmitted method adds a new transaction to the list. Each transaction has a unique id generated using generateUniqueId().
- **Generate Unique ID**: The generateUniqueId function ensures that each transaction has a unique identifier.
- **Delete Transaction**: The handleTransactionDeleted method removes a transaction by filtering out the one with the matching id.

### Local Storage Integration
The transactions are saved to localStorage, ensuring that the data persists even after the user refreshes the page or closes the browser.

- **Saving Transactions**: The saveTransactionsToLocalStorage method converts the transactions array into a JSON string and saves it to localStorage.
- **Loading Transactions**: On page load, the transactions are retrieved from localStorage if available.

## How to Use

### Prerequisites

1. Ensure that you have Node.js and npm installed on your system.
2. Install Vue CLI globally.

### Installation
1. Clone this repository
2. Navigate to the project folder of the cloned repo.

### Running the application

1. Start the development server by running `npm run dev`
2. Once the server is running, open your browser and go to the link provided

## Technologies Used

1. **Vue.js**: Framework for building the user interface.
2. **JavaScript**: Language for implementing the application logic.
3. **CSS**: Styling for the user interface.
4. **localStorage**: For persistent data storage in the browser.

## License

This project is licensed under the MIT License.
