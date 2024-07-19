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

OrderTable Should look as follows:

```
const OrderTable = () => {
  return (
    <>
      <p>test, Hi from OrderTable!</p>
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
        <tbody></tbody>
      </table>
    </>
  );
};

export default OrderTable;

```



