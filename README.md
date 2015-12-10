# php-consul-http-client

## Allows for [Consul](https://www.consul.io/) Service Lookup over HTTP

This module requests all `passing` consul services with the desired name, and
optional version tag, and returns the URL of a randomly selected copy of the service.

Example:

```
<?php

// Passing `null` as the first argument lets the module create it's own http client
$serviceLookup = new CascadeEnergy\ServiceDiscovery\Consul\ConsulHttp(null,"<ip-of-consul-server>:8500");

// `service-version` is optional
$serviceUrl = $serviceLookup->getServiceAddress(<service-name>, <service-version>);

if ($serviceUrl == null) {
  //If no healthy instances of the desired service are found, the url returned is `null`
  //this can be handled in any convenient manner such as:
  throw new Exception('Service not found!');
} else {
  //The service was found!
  $client = new <insert-your-favorite-http-client-here>();

  $request = $client->put("$url/<route>",null,<body>);

  // keep interacting with the service, ask for urls of new services, etc...
}
```
