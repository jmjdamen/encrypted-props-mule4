# encrypted-props-mule4
Simple Mule 4 app using encrypted properties

## How to use

On the runtime where the application gets deployed the secure key for decryption needs to be passed in.

### Anypoint Studio 
Set VM Arguments in Run Configuration: -Dsecure.key=abcd1234abcd1234
Application url: http://localhost:8090

### Customer-Hosted (standalone runtime)
Start the Mule runtime with: -M-Dsecure.key=abcd1234abcd1234
Application url: http://localhost:8090

### CloudHub
Set property with

key                         value
secure.key     				abcd1234abcd1234

Application url: CloudHub application URL

*Both properties secure.key and secure::sensitive.value are 'flagged' as secure properties in the file mule-artifact.json
In CloudHub this will have as a result that the property values will be hidden when they are overridden via the Runtime Manager properties tab.*

## How it works

The file secured-properties.yaml contains a property that has an encrypted value, property name sensitive.value.
It was encryped using an algorithm (see XML for details) and the secure key.

When testing the application the application prints the contents of the properties file (encrypted value) + the decrypted value.
If the secure key is not present, the app will not deploy, it will act as an ignition key.

When you want to override property from Anypoint Runtime Manager, the override needs to happen like this:

key                         value
secure::sensitive.value     your new desired value in plain text

*Please note that it matters if secure::key is typed in via the plain text properties view or the table view in Runtime Manager.
When typed in the table view Runtime Manager will escape the colons like this: secure\\:\\:sensitive.value
When you provide this via the text view you need to pass this syntax in yourself.*

More info: https://docs.mulesoft.com/mule-runtime/4.2/secure-configuration-properties
