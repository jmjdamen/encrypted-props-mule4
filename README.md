# encrypted-props-mule4
Simple Mule 4 app using encrypted properties

How to use:

On the runtime where the application gets deployed the decryption key needs to be passed in.
Start the Mule runtime with: -M-Dsecure.key=abcd1234abcd1234
Or in Anypoint Studio set VM Arguments in Run Configuration: -Dsecure.key=abcd1234abcd1234

In the file secured-properties.yaml is a property that is encrypted named sensitive.value.
It was encryped using an algorithm (see XML for details) and the secure key.

When testing the application via http://localhost:19090 the app prints the contents of the properties file (encrypted value) + the decrypted value.
If the secure key is not present, the app will not deploy, it will act as an ignition key.

When you want to override property from Anypoint Runtime Manager, the override needs to happen like this:
key                         value
secure::sensitive.value     your new value in plain text

