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
## Adding Navigation Links

```jsx
import { Link, Route, Routes } from "react-router-dom"
import { About, Contact, Home, PageNotFound } from "./components/ex1/BasicNavigation"


export const Root = ()=>{

    return <>


        <ul>
            <li><Link to="/">Home</Link></li>
            <li><Link to="about">About</Link></li>
            <li><Link to="contact">Contact</Link></li>
            <li><Link to="contact1">Unknown</Link></li>
        </ul>
       
        <Routes>
            <Route path="/" element={<Home/>}/>
            <Route path="about" element={<About/>}/>
            <Route path="contact" element={<Contact/>}/>
            <Route path="*" element={<PageNotFound/>}/>
        </Routes>

    </>

}
```

# Dynamic Routing

/books/:bookId: Here bookId is dynamic.

## Define Components

```jsx
import { Link, useParams } from "react-router-dom"


const BookList = ()=>{

/** dynamic route added to the li element */
    let style={
        paddingLeft: '25px'
    }
    const books = [
        {id:1,name:'book1'},
        {id:2,name:'book2'}
    ]

    return <>
        <ul>
            {books.map((book)=>{
                return <li key={book.id}>{book.name}
                <span style={style}>
                <Link to={`${book.id}`}>View</Link> 
                </span>
                </li>
            })}
        </ul>
    </>
}

const Book=()=>{

    let {bookId} = useParams();
    return <>
      {bookId}
    </>
}
export {BookList, Book}
```

## Add Routes, Route, Link

```jsx
import { Link, Route, Routes } from "react-router-dom"
import { Book, BookList } from "./Pages"

export const Example2 = ()=>{

    let content = `dynamic routing`;

    let styles = {
        color:'red',
        fontSize:'30px',
        style:'bold'
    }
    return <>
      <p style={styles}>{content}</p>
        <ul>
            <li><Link to="books">Book List</Link></li>
        </ul>
      <Routes>
        <Route path="/books" element={<BookList/>}/>
        <Route path="/books/:bookId" element={<Book/>}/>
      </Routes>
    </>

}
```
