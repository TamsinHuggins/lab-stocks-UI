﻿# lab-stocks-UI


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


## Clean up App 

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

## Create OrderTable Folder and OrderTable Component

Create components folder in src. Create a new OrderTable folder in components. Create OrderTable.jsx file in the OrderTable folder.

![image](https://github.com/user-attachments/assets/a211687b-937a-41ed-a7c8-749fc47e476d)



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


## CHALLENGE : Render the OrderTable component in App.jsx so that test welcome from OrderTable appears in the browser. This will involve:
- Exporting the OrderTable component as default export
- Importing the OrderTable component into App
- Rendering an instance of OrderTable in App 


## Add dummyData.js to the project
- Create a new folder in src called data.
- Download dummyData.js from course site and place it inside data folder
- We will use this data to simulate some of the functions of the back end before we build the proper REST calls to the backend.


## Rendering data

Pull in the dummy orders and render some of the information so that it appears on screen.


```
import { getDummyOrders } from "../../data/dummyData";

const OrderTable = () => {
  // getDummyOrders function will be replaced by a function that makes a GET request to our backend
  const dummyOrders = getDummyOrders();

  return (
    <>
      <h1>Orders History</h1>
      <h2>Your Recent Order of {dummyOrders[0].ticker} </h2>
      <p>
        Price: {dummyOrders[0].price}, Quantity: {dummyOrders[0].quantity}
      </p>
    </>
  );
};

export default OrderTable;

```



## Add to OrderTable the table that will hold information about all the customer's stock orders

### Copy the basic HTML for a table with the appropreate headers into the OrderTable component

This is all basic HTML, the challenge comes from interpreting a very nested structure 

- table wraps around the entire table
   - thead wraps around a table header
      - tr wraps around a table row
         - th holds a single value in the table header

   - tbody wraps around the table body
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
![image](https://github.com/user-attachments/assets/0989533c-275a-47de-9304-f5d62bf27456)


## Challenge: Add one order to the table as a row.

Your table App should look something like this:

![image](https://github.com/user-attachments/assets/03fc3eb1-fe5a-44ba-9f08-69966553cabc)


## Understanding Nested Components

Remember that components in React are reusable and customizable.

We can make a React component called OrderTableRow, and render it into OrderTable as many times as desired, e.g.:

```
        <tbody>
          <OrderTableRow order={firstOrder} />
          <OrderTableRow order={secondOrder} />
        </tbody>

```


### Create an OrderTableRow component 

Create OrderTableRow.jsx in components. 

OrderTableRow will recieve a single order object through props and put the data into the right boxes/fields.

```
const OrderTableRow = (props) => {
  return (
    <tr>
      <td>{props.order.created}</td>
      <td>{props.order.statusCode}</td>
      <td>{props.order.type}</td>
      <td>{props.order.ticker}</td>
      <td>{props.order.quantity}</td>
      <td>{props.order.price}</td>
    </tr>
  );
};
export default OrderTableRow;

```
### Render orderTableRow into the table body

```

import { getDummyOrders } from "../../data/dummyData";
import OrderTableRow from "./OrderTableRow";

const OrderTable = () => {
  // getDummyOrders function will be replaced by a function that makes a GET request to our backend
  const dummyOrders = getDummyOrders();
  const firstOrder = dummyOrders[0];

  return (
    <>
      <h1>Orders History</h1>
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
          <OrderTableRow order={firstOrder} />
        </tbody>
      </table>
    </>
  );
};

export default OrderTable;



```


## Using Map

We have saved ourselves from having to write loads of HTML, by creating a reusable table row component that will recieve an order and give back a row for that order.


```
        <tbody>
          <OrderTableRow order={firstOrder} />
          <OrderTableRow order={secondOrder} />
          <OrderTableRow order={thirdOrder} />
        </tbody>

```

The example code above would create 3 table rows for 3 orders.

This code could cause us problems in the future, though. It's rendering data that is going to **change** over time.
We need logic that says "for every order, add a row to the table"


```
import { getDummyOrders } from "../../data/dummyData";
import OrderTableRow from "./OrderTableRow";

const OrderTable = () => {
  // getDummyOrders function will be replaced by a function that makes a GET request to our backend
  const dummyOrders = getDummyOrders();

  return (
    <>
      <h1>Orders History</h1>
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
          {dummyOrders.map((order, index) => (
            <OrderTableRow key={index} order={order} />
          ))}
        </tbody>
      </table>
    </>
  );
};

export default OrderTable;

```

## A Buy component!

### Challenge: Create a component called PlaceOrder that will eventually have the functionality to buy or sell a stoek.

Create a new file called PlaceOrder.jsx for the a new PlaceOrder component.

![image](https://github.com/user-attachments/assets/268e29d1-3d7e-496d-b980-8f06dbaf0adb)


Have PurchaseStock return something basic like \<p\> hello from PurchaseStock\</p\>
Build up something that looks like the following image. The button does not need to work yet!







