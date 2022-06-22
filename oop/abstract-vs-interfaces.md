# Abstract vs Interfaces

If you need to separate an interface from its implementation, use an interface.&#x20;

If you also need to provide a base class or default implementation of the interface, add an abstract class (or normal class) that implements the interface

![The blue class knows only the interface. The abstract class implements the interface, and the subclass inherits from the abstract class.](<../.gitbook/assets/image (2).png>)



First the interface:

```
public interface URLProcessor {

    public void process(URL url) throws IOException;
}
```

Second, the abstract base class:

```
public abstract class URLProcessorBase implements URLProcessor {

    public void process(URL url) throws IOException {
        URLConnection urlConnection = url.openConnection();
        InputStream input = urlConnection.getInputStream();

        try{
            processURLData(input);
        } finally {
            input.close();
        }
    }

    protected abstract void processURLData(InputStream input)
        throws IOException;

}
```

Third, the subclass of the abstract base class:

```
public class URLProcessorImpl extends URLProcessorBase {

    @Override
    protected void processURLData(InputStream input) throws IOException {
        int data = input.read();
        while(data != -1){
            System.out.println((char) data);
            data = input.read();
        }
    }
}
```

Fourth, how to use the interface `URLProcessor` as variable type, even though it is the subclass `UrlProcessorImpl` that is instantiated.

```
URLProcessor urlProcessor = new URLProcessorImpl();

urlProcessor.process(new URL("http://jenkov.com"));
```
