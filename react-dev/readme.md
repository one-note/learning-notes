# BrowserRouter

## Simple Routing
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";
import { BrowserRouter } from "react-router-dom";
import { Root } from "./v1/Root";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <Root />
    </BrowserRouter>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```

### Defining Components

```jsx


const Home = ()=>{
    return <>
    <h1>Home Page</h1>
    </>
}

const About =()=>{
    return <>
     <h1>About</h1>
    </>
}

const Contact = ()=>{
    return <>
    <h1>Contact</h1>
    </>
}

const PageNotFound = ()=>{
    return <>
        <h1>Page Not Found</h1>
    </>
}

export {Home,About,Contact,PageNotFound}
```
### Registering Components With Routes and Route

```jsx
import { Route, Router, Routes } from "react-router-dom"
import { About, Contact, Home, PageNotFound } from "./components/ex1/BasicNavigation"


export const Root = ()=>{

    return <>
    
        <Routes>
            <Route path="/" element={<Home/>}/>
            <Route path="about" element={<About/>}/>
            <Route path="contact" element={<Contact/>}/>
            <Route path="*" element={<PageNotFound/>}/>
        </Routes>

    </>

}
```
