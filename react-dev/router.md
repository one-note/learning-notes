# BrowserRouter

# Simple Routing
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

## Defining Components

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
## Registering Components With Routes and Route

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

    let {bookId} = useParams(); // retrieved the bookId
    return <>
      {bookId}
    </>
}

const NewBook = ()=>{
    return <>
    <h1>New Book</h1>
    </>
}
export {BookList, Book, NewBook}
```

## Add Routes, Route, Link

```jsx
import { Link, Route, Routes } from "react-router-dom"
import { Book, BookList, NewBook } from "./Pages"

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
            <li><Link to="books/new">New Book</Link></li>
        </ul>
      <Routes>
        <Route path="/books" element={<BookList/>}/>
        <Route path="/books/:bookId" element={<Book/>}/>
        <Route path="/books/new" element={<NewBook/>}/>
      </Routes>
    </>

}
```

# Nested Route

## Define Components

```jsx
import { Link, useParams } from "react-router-dom"


const BookList = ()=>{

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

    let {bookId} = useParams(); // retrieved the bookId
    return <>
      {bookId}
    </>
}

const NewBook = ()=>{
    return <>
    <h1>New Book</h1>
    </>
}
export {BookList, Book, NewBook}
```

## Add Routes, Route, Nested Route and Link

```jsx
import { Link, Route, Routes } from "react-router-dom";
import { Book, BookList, NewBook } from "./Pages";

export const Example3 = () => {
  let content = `nested routes`;

  let styles = {
    color: "red",
    fontSize: "30px",
    style: "bold",
  };
  return (
    <>
      <p style={styles}>{content}</p>
      <ul>
        <li>
          <Link to="shops/books">Book List</Link>
        </li>
        <li>
          <Link to="shops/books/new">New Book</Link>
        </li>
      </ul>
      <Routes>
        <Route path="shops">
          <Route path="books" element={<BookList />} />
          <Route path="books/:bookId" element={<Book />} />
          <Route path="books/new" element={<NewBook />} />
        </Route>
      </Routes>
    </>
  );
};

```

# React Routlet

A place holder in parent compoent to display components mapped by child routes.

## Define Components
```jsx
import { Outlet } from "react-router-dom"


const Home=()=>{
    return <>
    <h1>Home</h1>
    </>
}

const About = ()=>{
    return <>
    <h1>About</h1>
    <Outlet/>
    </>
}

const Settings = ()=>{
    return <>
    <h1>Settings</h1>
    </>
}

export {Home, About, Settings}
```

Outlet is defined inside About Component. It means About component will have nested route or child route.

## Define Routes, Route, Link

```jsx
import { Link, Route, Router, Routes } from "react-router-dom";
import { About, Home, Settings } from "./Pages";

export const Example4 = () => {
  let styles = { fontSize: "20px", color: "red" };
  let content = `Routlet Example`;
  return (
    <>
      <h1 style={styles}>{content}</h1>

      <ul>
        <li>
          <Link to="home">Home</Link>
        </li>
        <li>
          <Link to="about">About</Link>
        </li>
        <li>
          <Link to="about/settings">About | Settings</Link>
        </li>
      </ul>

      <Routes>
        <Route path="home" element={<Home />} />
        <Route path="about" element={<About />}>
          <Route path="settings" element={<Settings />} />
        </Route>
      </Routes>
    </>
  );
};

```

# Routlet Context

## Define Component

- outlet context will be defined in parent component
- when child component rendered as nested route, child component can consume it from `useRouteletContext()`

```jsx
import { Outlet, useOutletContext } from "react-router-dom"


const Home=()=>{
    return <>
    <h1>Home</h1>
    </>
}

const About = ()=>{

    let person={
        name: 'John Doe',
        city: 'Paris',
        age: 30
    }
    return <>
    <h1>About</h1>
  
    <Outlet context={person}/>
    </>
}

const Settings = ()=>{

    let {name, age} = useOutletContext();
    return <>
    <h1>Settings</h1>
    {name} | {age}
    </>
}

export {Home, About, Settings}
```

## Add Rputes, Route, Link

```jsx
import { Link, Route, Routes } from "react-router-dom";
import { About, Home, Settings } from "./Pages";

export const Example5 = () => {
  let styles = { fontSize: "20px", color: "red" };
  let content = `Routlet Context Example`;
  return (
    <>
      <h1 style={styles}>{content}</h1>

      <ul>
        <li>
          <Link to="home">Home</Link>
        </li>
        <li>
          <Link to="about">About</Link>
        </li>
        <li>
          <Link to="about/settings">About | Settings</Link>
        </li>
      </ul>

      <Routes>
        <Route path="home" element={<Home />} />
        <Route path="about" element={<About />}>
          <Route path="settings" element={<Settings />} />
        </Route>
      </Routes>
    </>
  );
};

```
# Multiple Routes

## Define Multiple Routes
```jsx
import { Route, Routes } from "react-router-dom";
import { About, Contact, Home, Nav } from "./Pages";

export const Example6 = () => {
  let content = `multiple routes`;
  let styles = { fontSize: "20px", color: "red" };

  return (
    <>
      <h1 style={styles}>{content}</h1>

      <Nav />
      <Routes>
        <Route path="home" element={<Home />} />
        <Route path="about" element={<About />} />
      </Routes>
      <Routes>
        <Route path="contact" element={<Contact />} />
      </Routes>
    </>
  );
};

```

## Define Components

```jsx
import { Link } from "react-router-dom"


const Home=()=>{
    return <>
    <h1>Home</h1>
    </>
}

const About=()=>{
    return <>
    <h1>About</h1>
    </>
}

const Contact=()=>{
    return <>
    <h1>Contact</h1>
    </>
}

const Nav=()=>{

    return <>
    <ul>
        <li><Link to="home">Home</Link></li>
        <li><Link to="about">About</Link></li>
        <li><Link to="contact">Contact</Link></li>
    </ul>
    </>
}
export {Home, About, Contact, Nav}
```

# Component as Routes

## Register Component as Routes
```jsx
import { Route, Routes } from "react-router-dom";
import { AuthorRoutes, Home, Nav } from "./Pages";

export const Example7 = () => {
  let content = `component as routes`;
  let styles = { fontSize: "20px", color: "red" };

  return (
    <>
      <h1 style={styles}>{content}</h1>
      <Nav />
      <Routes>
        <Route path="home" element={<Home />} />
        {/* <Route path="author" element={<Author/>}>
            <Route path="books" element={<Books/>}/>
        </Route> */}
        <Route path="author/*" element={<AuthorRoutes />} />
        {/** AuthorRoutes is a component but defined with Route */}
      </Routes>
    </>
  );
};

```

## Define Componenr as Routes

```jsx
import { Link, Outlet, Route, Routes } from "react-router-dom";

const Home = () => {
  return (
    <>
      <h1>Home</h1>
    </>
  );
};

const Author = () => {
  return (
    <>
      <h1>Author</h1>
      <Outlet />
    </>
  );
};

const AuthorRoutes = () => {
  return (
    <>
      <Routes>
        <Route path="/" element={<Author />}>
          <Route path="books" element={<Books />} />
        </Route>
      </Routes>
    </>
  );
};

const Books = () => {
  return (
    <>
      <h1>Books</h1>
    </>
  );
};

const Nav = () => {
  return (
    <>
      <ul>
        <li>
          <Link to="home">Home</Link>
        </li>
        <li>
          <Link to="author">Author</Link>
        </li>
        <li>
          <Link to="author/books">Author/Books</Link>
        </li>
      </ul>
    </>
  );
};

export { Home, Author, AuthorRoutes, Books, Nav };

```

# Navigate

## Navigate Component

```jsx
import { useState } from "react"
import { Link, Navigate, Route, Routes } from "react-router-dom"


const Home=()=>{
    return <>
      <h1>Home</h1>
    </>
}

const Home2=()=>{
   
    let [count,setCount] = useState(1);

    const increaseCount=()=>{
        setCount((prevState)=>{return prevState + 1});
    }

    return <>
    <h2>Home 2</h2>
    {  // navigating conditionally
     count===3 && <p><Navigate to="../home"/></p>
    }

    <button onClick={increaseCount}>Navigate</button>
    </>
}

const Nav = ()=>{
    return <>
    <ul>
        <li><Link to="home">Home</Link></li>
        <li><Link to="home2">Home 2</Link></li>
    </ul>
    </>
}

const PageRoutes=()=>{
    return <>
    <Routes>
        <Route path="home" element={<Home/>}/>
        <Route path="home2" element={<Home2/>}/>
    </Routes>
    </>
}

export {PageRoutes, Nav}
```

## Define Routes

import { Route, Routes } from "react-router-dom";
import { Nav, PageRoutes } from "./Pages";

export const Example8 = () => {
  let content = `navigation | Link | <Navigate/> | useNavigate()`;
  let styles = { fontSize: "20px", color: "red" };

  return (
    <>
      <h1 style={styles}>{content}</h1>

      <Nav />
      <Routes>
        <Route path="/*" element={<PageRoutes />} />
      </Routes>
    </>
  );
};

