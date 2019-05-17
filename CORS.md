## CORS - Cross Origin Resource Sharing

CORS allows a webpage to request additional resources into browser from other domains e.g. fonts, CSS or static 
	images from CDNs.

CORS defines a way in which browser & server can interact to determine whether or not it is safe to allow cross-origin
	requests.
Ex - Suppose I visit a webpage www.example.com on my browser, now this web-page tries to make a cross-origin
		request to www.userservice.com to fetch user data

1. Browser sends a OPTIONS request to www.userservice.com containing the domain that originally served the page.
	
```
Origin: www.example.com		
```
2. Server at to www.userservice.com may respond to browser with:
```
Access-Control-Allow-Origin: www.example.com //indicating that it allows CORS with www.example.com
```
```
Access-Control-Allow-Origin: * //indicating that it allows CORS with all domains
```
or an Error Page, indicating it doesn't allow cross-origin requests.

## Pre flight example
When performing certain types of cross-domain Ajax requests, modern browsers that support CORS will insert an 
extra "preflight" request to determine whether they have permission to perform the action.

	```
		OPTIONS /
		Host: userservice.com
		Origin: www.example.com
	```
	If userservice.com is willing to accept the action, it may respond with the following headers:
	```
		Access-Control-Allow-Origin: www.example.com
		Access-Control-Allow-Methods: PUT, DELETE
	```

## The headers that relate to CORS are
**Request headers**
* Origin
* Access-Control-Request-Method
* Access-Control-Request-Headers

**Response headers**
* Access-Control-Allow-Origin
* Access-Control-Allow-Credentials
* Access-Control-Expose-Headers
* Access-Control-Max-Age
* Access-Control-Allow-Methods
* Access-Control-Allow-Headers

## Spring MVC & CORS
Spring MVC provides **@CrossOrigin** annotation at method & global level. By default @CrossOrigin allows all origins, all headers & HTTP methods specified in @RequestMapping & maxAge of 30mins. You can override default CORS configuration by providing values to annotation attributes -
* origins - list of all allowed origins, its values is placed in Access-Control-Allow-Origin header of both pre-flight response & actual response.
	'*' - means all origins are allowed
	If undefined, all origins are allowed
* allowedHeaders - List of request headers that can be used during the actual request. Value is used in preflight’s response header Access-Control-Allow-Headers.
	'*' – means that all headers requested by the client are allowed.
	If undefined, all requested headers are allowed.
* methods - List of supported HTTP request methods. If undefined, methods defined by RequestMapping annotation are used.
* allowCredentials - It determine whether browser should include any cookies associated with the request.
	– false – cookies should not included.
	– "" (empty string) – means undefined.
	– true – pre-flight response will include the header Access-Control-Allow-Credentials with value set to true.
	– If undefined, credentials are allowed.

**This is how @CrossOrigin can be used at class level, method level or at both the levels.**
```
@Controller
@CrossOrigin(origins = "*", allowedHeaders = "*")
public class HomeController
{
    @CrossOrigin(origins = "http://example.com")
    @GetMapping(path="/")
    public String homeInit(Model model) {
        return "home";
    }
}
```

To do CORS configuration at appplication level in Spring Boot
```
@Configuration
public class CorsConfiguration
{
    @Bean
    public WebMvcConfigurer corsConfigurer()
    {
        return new WebMvcConfigurerAdapter() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**").allowedMethods("GET", "POST");
            }
        };
    }
}
```
