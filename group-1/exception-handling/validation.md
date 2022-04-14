# Validation



When receiving input that needs to be validated before it can be used, validate all input before using any of it. You should not change any state in the application or attached systems until all input data has been validated. That way you avoid leaving the application in a half valid state.

For instance, in a DAO method that inserts a user and an address into two different tables in a database, do like this:

```
  check if user already exists
  validate user
  validate address

  insert user
  insert address
```

Do not do like this:

```
  check if user already exists
  validate user
  insert user

  validate address
  insert address
```

### Throw Exception or return false

When validating input data you do not always have to throw an exception if the input is invalid. How to handle invalid data or state sensibly often depends on the condition:

```
Can the code detecting the error, interact sensibly with the
user, to correct the error?
```

If the error is caused by input from a user, and that user is able to correct the input and retry, then interacting is often preferrable to throwing an exception. In addition you might want to detect all possible errors in the input before showing them to the user. That way the user can correct all the errors before next retry, instead of repeated iterations of correcting, retrying, correcting, retrying et
