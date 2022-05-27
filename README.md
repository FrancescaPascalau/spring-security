# Spring Security

Spring Security is a framework that provides authentication, authorization, and protection against common attacks. With
first class support for both imperative and reactive applications, it is the de-facto standard for securing Spring-based
applications.

## How it works?

1. When an incoming request reaches our system, Spring Security starts by choosing the right **security filter** to
   process that request:
    - Is the request a POST containing username and password elements? => `UsernamePasswordAuthenticationFilter`
      is chosen.
    - Is the request having a header "Authorization : Basic base64encoded(username:password)"? =>
      `BasicAuthenticationFilter` is chosen
2. When a filter had successfully retrieved Authentication information from the request, the AuthenticationManager is
   invoked to authenticate the request. Via its implementation, the `AuthenticationManager` goes through each of the
   provided AuthenticationProvider(s) and try to authenticate the user based on the passed Authentication Object.
3. When the Authentication is successful, and a matching user if found, an Authentication Object containing the user
   is returned and set into the `SecurityContext`.

- **Authentication**: the act of determining "who" a user is.
- **Authorisation**: the act of determining "what" a user is allowed to do.
- Until a user is "authenticated", Spring Security automatically makes that user an "AnonymousUser".
- You can make resources accessible only to authenticated users, i.e. _not accessible to anonymous
  users_.
- Once the user is authenticated they may have one or more roles (e.g. `User`/`Admin`/`Dev`).
- Spring security allows you to make resources accessible only to users with a given role.
  E.g. _you could say that only Admin users are authorised to access the /admin/dashboard resource path._