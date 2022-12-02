# Revision for Servlets and JSP
## Session management
Sessions will be created automatically when a client sends a request to the server

 - Session ID can be accessed through `Devloper Tools > Application > Cookies > SessionId`

Session Management

 - Sessions can be accessed in servlets through:

 ```java
 // to get the current session
HttpSession session = req.getSession();

// to invalidate the current session
session.invalidate();
req.getSession().invalidate();

// to set session attributes which can be accessed through the session
session.setAttribute("attributeName", attributeObject);
 ```

 - Having session attributes enable features like access restriction, login, and persistent data through the session until invalidated

Servlets

 - Servlets can be used to perform functions based on the incoming requests
 - `@WebServlet("/PATH")` annotation on top of the `doGet` methods dictate which servlet is used to handle the request mapping instead of XML
 - Generally have one front controller that manages all the requests and sends out to other servlets or JSP to handle
 - Can overwrite different request methods like `doGet`. `doPost`, `doPut` and `doDelete` to perform different tasks, one request mapping can perform different functions depending on whether it is _GET_ or _POST_
 - Parameters from forms can also help to implement conditional logic on what task should be performed

 ```java
 if(request.getParameter("paramName").equals("actionName")) {
    // perform action
 }
 ```

 - Request attributes can be used to transfer information from one servlet to another, things like objects, arrays, string, boolean, etc can be sent around
 - To forward the request and response to another servlet or JSP:
```java
RequestDispatcher dispatcher = request.getRequestDispatcher("PATH-TO-SERVLET-OR-JSP");
dispatcher.forward(request, response);
// OR
dispatcher.include(request, response);
```

Filters
 - Another topic to check up
 - Able to access requests before it reach the servlets
 - Used quite often for data pre-processing