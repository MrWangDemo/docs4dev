## 8. Embedding the Config Server

The Config Server runs best as a standalone application. However, if need be, you can embed it in another application. To do so, use the  `@EnableConfigServer`  annotation. An optional property named  `spring.cloud.config.server.bootstrap`  can be useful in this case is. It is a flag to indicate whether the server should configure itself from its own remote repository. By default, the flag is off, because it can delay startup. However, when embedded in another application, it makes sense to initialize the same way as any other application. When setting  `spring.cloud.config.server.bootstrap`  to  `true`  you must also use a [composite environment repository configuration](multi__spring_cloud_config_server.html#composite-environment-repositories). For example

```java
spring:
application:
name: configserver
profiles:
active: composite
cloud:
config:
server:
composite:
- type: native
search-locations: ${HOME}/Desktop/config
bootstrap: true
```

> If you use the bootstrap flag, the config server needs to have its name and repository URI configured in  `bootstrap.yml` .

To change the location of the server endpoints, you can (optionally) set  `spring.cloud.config.server.prefix`  (for example,  `/config` ), to serve the resources under a prefix. The prefix should start but not end with a  `/` . It is applied to the  `@RequestMappings`  in the Config Server (that is, underneath the Spring Boot  `server.servletPath`  and  `server.contextPath`  prefixes).

If you want to read the configuration for an application directly from the backend repository (instead of from the config server), you basically wat an embedded config server with no endpoints. You can switch off the endpoints entirely by not using the  `@EnableConfigServer`  annotation (set  `spring.cloud.config.server.bootstrap=true` ).
