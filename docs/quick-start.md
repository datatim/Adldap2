## Quick Start & and Testing an LDAP connection

If you need to test something with access to an LDAP server, the generous folks at [Georgia Tech](http://drupal.gatech.edu/handbook/public-ldap-server) have you covered.

Use the following configuration:

```php
$config = [
  'account_suffix'        => '@gatech.edu',
  'domain_controllers'    => ['whitepages.gatech.edu'],
  'base_dn'               => 'dc=whitepages,dc=gatech,dc=edu',
  'admin_username'        => '',
  'admin_password'        => '',
];

// Create a new connection provider.
$provider = new \Adldap\Connections\Provider($config);

$ad = new \Adldap\Adldap();

// Add the provider to Adldap.
$ad->addProvider('default', $provider);

// Try connecting to the provider.
// If the connection is successful, the connected provider is returned.
$provider = $ad->connect('default');

// Create a new search.
$search = $provider->search();

// Call query methods upon the search itself.
$results = $search->where('...')->get();

// Or create a new query object.
$query = $search->newQuery();

$results = $search->where('...')->get();
```

However while useful for basic testing, the queryable data only includes user data, so if you're looking for testing with any other information
or functionality such as modification, you'll have to use your own server.