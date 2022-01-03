# React Localstorage

Consider a dummy login screen(which has no authentication), we can login as long as we have a valid email and the password is at least seven characters long.

Problem:
We can send a HTTP request to backend server, consider that no such server exists.

When we login using the credentials, if we refresh the page we'll lose login status. If we had a server, once we login, we send request to backend and get some log-in data, like some token that identifies the user as authenticated. But we should make sure the user authenticated status is there once we reload the page.
If we use state to make the login status of user, when we reload the page, the entire application restarts and all the varibales from last execution are lost. Since we lose all the data, we can insted store them somewhere where it stays on reload. We should also make sure that when the application starts, we check if the data exists. If it does exist, we log the user in automatically so the user doesnt have to re-enter the details.
We can use useEffect here.

In loginhandler we store the data collected in browser storage. The browser has many storages, we can use cookies or local storage here because it's easier to work with.
Local storage is a storage mechanism built into the browser which is totally independent of react. "localStorage" is a global object which is available in the browser. It is used with setItem, we can then give the item an identifier of our choice, should be a string. It should have a second argument which should be a string. We can add the storage in a function, because it is the function that executes only when the user clicks a button, this is rare and hence we can use this as a use case.
Consider scenario 1 where the app restarts because the user left the page and comes back or because we reload the page. Then in localStorage we can check if we have the key and value pair. When the app restarts, the app component runs again and therefore we can reach the localStorage at the top of component function using "localStorage.getItem" and search for our key, which will return the items stored in there. 
If we don't useEffect in this process, we could create an infinite loop. When we reload the page, we dont have to enter the details again. Once we click logout, the localStorage data is cleared.
