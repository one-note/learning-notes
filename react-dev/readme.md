# React JS Notes
React Hooks:
•	useState
•	useEffect
•	useContext
•	useMemo
•	useCallback
•	useRef
•	useReducer / Redux

## useState
```javascript
export const StateExample1 = ()=>{
  // not using state. 
  // so even though count increase with each click, no re-rendering will happen.
    let count = 0;
    const countHandler = ()=>{
        count = count +1;
        console.log(count); // increment of count wont be visible.
    }
    return <>
      <h1>State Example 1</h1>
      <button onClick={countHandler}>Increase Count</button>{count}
      <hr />
    </>
}
 
export const StateExample2 = ()=>{
    // array destructuring
    let [count,setCount] = useState(10); // initialize count with 10

    const countHandler = ()=>{
       setCount((prevState)=>{ // setCount as a higher order function
        return prevState + 1;
       });
    }
    return <>
      <h1>State Example 2</h1>
      <button onClick={countHandler}>Increase Count</button>{count}
      <hr />
    </>
}

const StateExample3 = () => {
  let [person, setPerson] = useState({ name: "John", age: 20 });
  const increaseAge = () => {
    setPerson((prevPerson) => {
      return { ...prevPerson, age: prevPerson.age + 1 };
    });
  };
  return (
    <>
      <h1>State Example 3: Objects</h1>
      <div>{person.age}</div>
      <button onClick={increaseAge}>Increase Age</button>
      <hr />
    </>
  );
};
export default StateExample3;

 
const StateExample4 = () => {
  let [items, setItem] = useState(["a", "b"]);
  const addItem = () => {
    const item = "k" + ":" + Math.random();
    setItem((prevItems) => {
      return [...prevItems, item];
    });
  };
  return <>
     <span>StateExample 4</span>
      <ul>
        {items.map((item, index) => {
          return <li key={index}>{item}</li>;
        })}
      </ul>
      <button onClick={addItem}>Add Item</button>
      <hr />
    </>
};
export default StateExample4;
```
Notes:
 
useEffect


export const UseEffectExample = () => {
  let [count, setCount] = useState(0);
  let [age, setAge] = useState(10);

  const increaseCount = () => {
    setCount((prevCount) => {
      return prevCount + 1;
    });
  };

  const increaseAge = () => {
    setAge((prevAge) => {
      return prevAge + 1;
    });
  };

  useEffect(()=>{
    console.log('always exists on any state change');
  });

  useEffect(()=>{
    console.log('runs only once. not aware about any state');
  },[]);

  useEffect(()=>{
    console.log('exists when count state change');
  },[count]);

  return (
    <>
      <h1>Use Effect Example</h1>
      {count} <button onClick={increaseCount}>Increase Count</button>
      {age} <button onClick={increaseAge}>Increase Age</button>
      <hr />
    </>
  );
};

Notes:
 
useContext / createContext

Defining context:

import { createContext } from "react";

export const AppContext = createContext();


Initialize Context
import { AppContext } from "./ContextDef";
import { Header } from "./Header";

export const Page = ()=>{

    let person= {name: 'John Doe', age: 10};

    return <>
      <AppContext.Provider value={person}>
        <Header age={person.age}/>
      </AppContext.Provider>  
    </>
}

Consuming Context
import { useContext } from "react";
import { AppContext } from "./ContextDef";

export const Header=(props)=>{
    const person = useContext(AppContext);
    return <>
     Welcome {person.name} & your age: {props.age}
    </>
}

Notes:
What is prop drilling in react.
 
useMemo

export const MemoExample = ()=>{

    const [count, setCount] = useState(0);

    const sqrFunction = ()=>{
        console.log('on each render it will be called');
        return Math.pow(count,3)+":::";
    }
    const sqrValue = sqrFunction() + Math.random(); // invocation

    const memoSqrValue1 = useMemo(()=>{
        console.log('memo sqr value. runs on any state change');
        return sqrFunction() + Math.random();
    })

    const memoSqrValue2 = useMemo(()=>{
        console.log('memo sqr value. runs once dont aware about any state');
        return sqrFunction() + Math.random();
    },[])

    const memoSqrValue3 = useMemo(()=>{
        console.log('memo sqr value. runs when count state change');
        return sqrFunction() + Math.random();
    },[count])

    const increaseCount = ()=>{
        setCount((prevCount)=>{
            return prevCount + 1;
        })
    }

    return <>
    <h1>Memo Example</h1>
    Square Value: {sqrValue} <br />
    Memo Value1: {memoSqrValue1} <br />
    Memo Value2: {memoSqrValue2} <br />
    Memo Value3: {memoSqrValue3} <br />
    Count value: {count} <br />
    <button onClick={increaseCount}>Increase Count</button>
    <hr />
    </>
}

Notes:
 
useCallback

import { memo, useEffect } from "react";
import { useState } from "react"

export const CallbackExample = ()=>{

    let [itemCount,setItemCount] = useState(1);
    let [price,setPrice] = useState(100);

    const increasePrice = ()=>{
        setPrice((prevPrice)=>{
            return prevPrice + 1;
        })
    }

    const increaseItemCount = ()=>{
        setItemCount((prevCount)=>{return prevCount + 1});
    }
    return <>
    <h1>Callback Example</h1>
    <h1>{price}</h1>
    <button onClick={increasePrice}>Item Price Increment</button>
    <Item count={itemCount} increment={increaseItemCount}/>
    <hr />
    </>
}

const Item=({count, increment})=>{
    return <>
     {console.log('item')}
     <h1>Item: {count}</h1>
     <button onClick={increment}>Item Increment</button>
    </>
}
 
import React, { memo, useEffect } from "react";
import { useState } from "react"

export const CallbackExample1 = ()=>{

    let [itemCount,setItemCount] = useState(1);
    let [price,setPrice] = useState(100);

    const increasePrice = ()=>{
        setPrice((prevPrice)=>{
            return prevPrice + 1;
        })
    }

    const increaseItemCount = ()=>{
        setItemCount((prevCount)=>{return prevCount + 1});
    }

    return <>
    <h1>Callback Example 1</h1>
    <h1>{price}</h1>
    <button onClick={increasePrice}>Item Price Increment</button>
    <ItemMemo count={itemCount} increment={increaseItemCount}/>
    <hr />
    </>
}

const Item=({count, increment})=>{
    return <>
     {console.log('item')}
     <h1>Item: {count}</h1>
     <button onClick={increment}>Item Increment</button>
    </>
}

const ItemMemo = React.memo(Item);
 
import React, { memo, useEffect } from "react";
import { useCallback } from "react";
import { useState } from "react"

export const CallbackExample2 = ()=>{

    let [itemCount,setItemCount] = useState(1);
    let [price,setPrice] = useState(100);

    const increasePrice = ()=>{
        setPrice((prevPrice)=>{
            return prevPrice + 1;
        })
    }

    const increaseItemCount = ()=>{
        setItemCount((prevCount)=>{return prevCount + 1});
    }

    const increaseItemCountCallback = useCallback(()=>{
        setItemCount((prevCount)=>{return prevCount + 1});
    },[itemCount]);

    return <>
    <h1>Callback Example 2</h1>
    <h1>{price}</h1>
    <button onClick={increasePrice}>Item Price Increment</button>
    <ItemMemo count={itemCount} increment={increaseItemCountCallback}/>
    <hr />
    </>
}

const Item=({count, increment})=>{
    return <>
     {console.log('item')}
     <h1>Item: {count}</h1>
     <button onClick={increment}>Item Increment</button>
    </>
}

const ItemMemo = React.memo(Item);

Notes:
 
useRef
import { useRef } from "react"

export const RefExample = ()=>{

    let inputRef =useRef();
    const handleOnChange = ()=>{
        console.log(inputRef.current.value);
    }

    return <>
      <input onChange={handleOnChange} type="text" ref= {inputRef} />
    </>
}
 
useReducer
 
React Form

