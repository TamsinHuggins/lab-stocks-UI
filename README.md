# lab-stocks-UI


## Create a new React app using Vite

- react-stocks-demo is chosen to be the name of the project for this demo.
- Vite is a build tool for the project.
- NPM (Node Package Manager) is a package manager for JavaScript that allows developers to install, share, and manage dependencies for their projects.


```
npm create vite@latest react-stocks-demo

```

### Choose React
![image](https://github.com/user-attachments/assets/52c1a4a0-666f-4e8a-99f0-1303b25e7df4)


### Choose JavaScript
![image](https://github.com/user-attachments/assets/a09f743a-d246-4fd1-a3c5-941b4bc12e84)

There is something called Babel, which is the compiler that turns React (JSX) code into vanilla JavaScript that the browser can interpret.


 ## Run the project with its starter code

 Go into the folder created by Vite

```
cd .\react-stocks-demo\
```

Install dependencies 

```
npm install
```

Run the project

```
npm run dev
```
If you get  " 'vite' is not recognized as an internal or external command,
operable program or batch file. " then you forgot to install - run npm install.

You will be provided with a link to click on to view the code running in the browser


![image](https://github.com/user-attachments/assets/f797cd64-d802-43de-bcd0-9cc1cbb59187)


You should see the starter code running in the browser.


## Clean up App and create OrderTable component

Delete some code from src/App.jsx. Make it so the App returns just a <p> tag, and check that you can see this text appear in the browser.

```
import "./App.css";

function App() {
  return (
    <>
      <p>test, hello from App</p>
    </>
  );
}

export default App;

```

Create components folder in src. Create a new OrderTable.jsx file in components that will hold the OrderTable Component

![image](https://github.com/user-attachments/assets/115bb2fe-c135-49e0-a075-9c99aff4abe7)



Create the OrderTable component in OrderTable.jsx

```
const OrderTable = () => {
    return (
        <>
            <p>test, Hi from OrderTable!</p>
        </>
    )
}



```


## CHALLENGE : Renter the OrderTable component in App.jsx so that test welcome from OrderTable appears in the browser. This will involve:
- Exporting the OrderTable component as default export
- Importing the OrderTable component into App
- Rendering an instance of OrderTable in App 


## Get dummyData from resources
Create a new folder in src called data. 
In data, create a js file called dummyData.
We will use this data to simulate some of the functions of the back end before we build the proper REST calls to the backend.


```
// dummyOrders array:
// resembles what we would get from the backend with a GET request to /stocks
// Starts with 3 pre-loaded previous orders
// is returned by the getDummyOrders function
// is updated by the buyDummyStock function

const dummyOrders = [
  {
    created: new Date(6, 5, 2024),
    statusCode: "FILLED",
    ticker: "AMZN",
    type: "BUY",
    quantity: 10,
    price: 100.0,
  },
  {
    created: new Date(4, 4, 2024),
    statusCode: "FILLED",
    ticker: "TSLA",
    type: "BUY",
    quantity: 5,
    price: 240.0,
  },
  {
    created: new Date(28, 1, 2024),
    statusCode: "FILLED",
    ticker: "AAPL",
    type: "BUY",
    quantity: 2,
    price: 70.0,
  },
];

// getDummyOrders function:
// resembles the functionality of a GET request to /stocks
// returns the dummyOrders array
// Will be replaced by a call to our backend with the following features:
// REQUEST TYPE: GET
// REQUEST URL: */stocks
// DATA SHAPE: array of objects with the correct keys ( created, statusCode, ticker, type, quantity, price)

export const getDummyOrders = () => {
  return dummyOrders;
};

// OVERIVIEW: List of stocks available to buy and their current prices.
// would come from 3rd party.

export const getDummyStocks = () => {
  const dummyStocks = [
    { ticker: "AMZN", price: 200.0 },
    { ticker: "TSLA", price: 250.0 },
    { ticker: "AAPL", price: 100.0 },
  ];

  return dummyStocks;
};

//OVERVIEW:
// buyDummyStock will write a new transaction to the backend.
// It currently recieves newTransID from React State, this parameter will be removed when we connect to back end.
// it calls getDummyStocks to find the current price of the stock being purchased.
//REQUEST URL: /stocks
//REQUEST TYPE: POST
//DATA SHAPE: order object with the correct keys ( created, statusCode, ticker, type, quantity, price)

export const buyDummyStock = (ticker, quantity) => {
  //find the current rpice of the chosen stock
  const dummyStocks = getDummyStocks();
  const stock = dummyStocks.find((stock) => stock.ticker === ticker);

  const newDummyTransaction = {
    created: new Date(),
    statusCode: "PENDING",
    ticker: ticker,
    type: "BUY",
    quantity: quantity,
    price: stock.price,
  };

  dummyOrders.push(newDummyTransaction); // add the new transaction to the dummyOrders array. later we will change this to be a POST request to the backend

  console.log(dummyOrders);
  return newDummyTransaction;
};


```



## Add to OrderTable the table that will hold information about all the customer's stock orders

### Copy the basic HTML for a table with the appropreate headers into the OrderTable component

This is all basic HTML, the challenge comes from interpreting a very nested structure 

- table wraps around the entire table
   - thead wraps around a table header
      - tr wraps around a table row
         - th holds a single value in the table header

   - tbody wreps around the table body
     - tr will wrap around a table row 
        - td will hold a single value in the table body



```
<table>
 <thead>
  <tr>
   <th>Created</th>
   <th> Status </th>
   <th> Type</th>
   <th> Ticker</th>
   <th> Quantity</th>
   <th> Price</th>
 </tr>
</thead>
 <tbody>
 </tbody>
</table>

```


Your browser might look something like this:

![image](https://github.com/user-attachments/assets/d88f014d-ac3c-4c69-8847-f7634ed95d97)





