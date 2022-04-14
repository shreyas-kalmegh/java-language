# Exception Wrapping



### What is Exception Wrapping?

Exception wrapping is wrapping is when you catch an exception, wrap it in a different exception and throw that exception. Here is an example:

```
    try{
        dao.readPerson();
    } catch (SQLException sqlException) {
        throw new MyException("error text", sqlException);
    }
```

The first reason is, that declared exceptions aggregate towards the top of the call stack. If you do not wrap exceptions, but instead pass them on by declaring your methods to throw them, you may end up with top level methods that declare many different exceptions. Declaring all these exceptions in each method back up the call stack becomes tedious.

The second reason is that you may not want your top level components to know anything about the bottom level components, nor the exceptions they throw. For instance, the purpose of DAO interfaces and implementations is to abstract the details of data access away from the rest of the application. Now, if your DAO methods throw SQLException's then the code using the DAO's will have to catch them. What if you change to an implementation that reads the data from a web service instead of from a database? Then you DAO methods will have to throw both RemoteException and SQLException. And, if you have a DAO that reads data from a file, you will need to throw IOException too. That is three different exceptions, each bound to their own DAO implementation.

To avoid this your DAO interface methods can throw DaoException. In each implementation of the DAO interface (database, file, web service) you will catch the specific exceptions (SQLException, IOException, RemoteException), wrap it in a DaoException, and throw the DaoException.
