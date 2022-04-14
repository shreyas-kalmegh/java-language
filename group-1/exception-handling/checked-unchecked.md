# Checked, Unchecked



In Java there are basically two types of exceptions: Checked exceptions and unchecked exceptions. C# only has unchecked exceptions. The differences between checked and unchecked exceptions are:

1. Checked exceptions must be explicitly caught or propagated as described in [Basic try-catch-finally Exception Handling](https://jenkov.com/tutorials/java-exception-handling/basic-try-catch-finally.html). Unchecked exceptions do not have this requirement. They don't have to be caught or declared thrown.\
   \

2. Checked exceptions in Java extend the java.lang.Exception class. Unchecked exceptions extend the java.lang.RuntimeException.

### Example

#### Checked

```
    public String readDataFromUrl(String url)
    throws BadUrlException{
        if(isUrlBad(url)){
            throw new BadUrlException("Bad URL: " + url);
        }

        String data = null;
        //read lots of data over HTTP and return
        //it as a String instance.

        return data;
    }
    
    public void storeDataFromUrl(String url)
    throws BadUrlException{
        String data = readDataFromUrl(url);
    }
```

#### Unchecked

```

    public String readDataFromUrl(String url) {
        if(isUrlBad(url)){
            throw new BadUrlException("Bad URL: " + url);
        }

        String data = null;
        //read lots of data over HTTP and
        //return it as a String instance.

        return data;
    }
    
    public void storeDataFromUrl(String url){
        String data = readDataFromUrl(url);
    }

```
