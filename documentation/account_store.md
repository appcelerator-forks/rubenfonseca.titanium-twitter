# AccountStore

## Reference

### - grantPermission({...})

You must call grantPermission on the AccountStore object before you'll be able to call any
other method on the object. The grantPermission asks the user for permission to use the
on-disc account storage.

It accepts the following params:

- *granted*: a callback called if the user grants permission to your application
- *denied*: a callback called if the user denies permission to your application


        var accountStore = Twitter.createAccountStore();
        accountStore.grantPermission({
          granted: function(e) {
            alert('Permission granted!');
          },
          denied: function(e) {
            alert('Permission denied!');
          }
        });

### - accounts()

Returns the stored list of accounts. Each object of the returned list is an [Account](account.html) object.

    accountStore.grantPermission({
      granted: function(e) {
        var accounts = accountStore.accounts();
        alert("Number of accounts: " + accounts.length);
      }
    });

### - accountWithIdentifier(identifier)

Returns an Account with the identifier passed as a parameter. Returns `null` if there isn't any.

    accountStore.grantPermission({
      granted: function(e) {
        var account = accountStore.accountWithIdentifier('123123123-12312-3123-12312-31231');
        Ti.API.log("Account is " + account);
      }
    });

### - saveAccount(account, {...})

Saves an [Account](account.html) into the AccountStore persistent storage. The first argument
should be the filled Account object. The second argument is a dictionary with the following keys:

- *success*: a callback fired if the save suceeds
- *failure*: a callback fired if the save fails. It contains an error message on the event `error` key
  (see example)

      var account = ...;
      accountStore.save(account, {
        success: function(e) {
          alert('Saved :D');
        }, 
        failure: function(e) {
          alert('Failed. Reason: ' + e.error);
        }
      });
