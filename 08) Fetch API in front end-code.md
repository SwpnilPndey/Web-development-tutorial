1. Fetch API is used to fetch data from an API endpoint 

2. Fetch API returns a promise. Hence, there are two ways to use fetch API : 

    - fetch.then.then
    - await fetch 

3. Fetch.then method is declared : 

fetch("API endpoint path")
    .then((response) => response.json())
    .then((data) => {
    // now data is available as object or array of objects, in whatever format it was 
    // stored 
    }


4. await fetch is used as :

const variableJSON = await fetch("API endpoint path");
const variableObj = await variableJSON.json();
// Obviously inside an async function

