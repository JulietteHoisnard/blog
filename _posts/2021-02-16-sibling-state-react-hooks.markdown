---
layout: post
title: "Handle sibling state with React useState hook"
subtitle: ""
date: 2021-02-16 15:26:00 +0100
related_image: https://images.unsplash.com/photo-1589458497992-baa225ead18a?ixid=MXwxMjA3fDB8MHxzZWFyY2h8OXx8aG9vayUyMGZpc2hpbmd8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
tags: [coding]
---

1. Parent:

   ```node
   import React from "react";
   import "./styles.css";
   import Child1 from ...
   import Child2 from ...

    export default App = () => {
      const [footprint, setFootprint] = useState(false);
      return (
      <div className="App">
        <Child1 setFootprint={setFootprint} />
        <Child2 footprint={footprint} />
      </div>
    )}
   ```

);

1. Child1:

   ```node
   import React from "react";
   import "./styles.css";

   export default const Child1({setFootprint}) {
     onMouseEnter={() => {
       setFootprint(true)
     }}
     onMouseLeave={() => {
       setFootprint(false)
     }}
   }
   ```

1. Child2:

   ```node
   import React from "react";
   import "./styles.css";

   export default const Child2({footprint}) {
    if (footprint) const message = <div>FOOTPRINT AVAILABLE</div>
    return message
   }
   ```
