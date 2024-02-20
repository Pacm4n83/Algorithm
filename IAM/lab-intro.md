# Lab 6: Client app for the GitHub API

This task shows how easy you can use one of the well-known OAuth2/OIDC provider like GitHub, Google or Facebook with Spring Security.

Spring Security provides the class _CommonOAuth2Provider_ containing predefined configurations for setting up one of these providers in your client application.

* Google
* GitHub
* Facebook
* Okta 

These predefined configurations already include the base configuration settings for the different providers, so you just have to configure your application-specific parts.

For details please see the corresponding section in the [spring security reference documentation](https://docs.spring.io/spring-security/site/docs/current/reference/htmlsingle/#oauth2login-common-oauth2-provider)

This task implements a simple client to display notifications for the GitHub user who will authorize this client to use his/her GitHub credentials.

The relevant OAuth2 configuration part is quite simple and is located in
_application.yml_ file:

```
spring:
  security:
    oauth2:
      client:
        registration:
          github:
            client-id: <client_id>
            client-secret: <client_secret>
            scope:
              - read:user
              - notifications
            redirect-uri: '{baseUrl}/login/oauth2/code/{registrationId}'
```

As you can see there are placeholders or _client_id_ and _client_secret_.
To get these credentials you need a GitHub account, after logging into your account:

1. Go to your personal settings 
2. Then select _Developer Settings_, select _OAuth Apps_ and click on _New OAuth App_
3. Use _Notification-Client_ as application name
4. Use _http://localhost:9090/login/oauth2/code/github_ as redirect uri
5. Use _http://localhost:9090_ as homepage url
6. Click on _Register application'
7. Now you should see the generated values for _Client ID_ and _Client Secret_
8. Copy these values over the placeholders in _application.yml_ file

Now start the main class _com.example.github.GitHubClientApplication_ and 
browse to [localhost:9090](http://localhost:9090). 

After you log in into GitHub you should see the user attributes, and you should be able to get the notifications by clicking on the button at the top of the screen.


![](https://i.imgur.com/hAyAZGu.png)

![](https://i.imgur.com/MrTz0X1.png)

![](https://i.imgur.com/CTBArOn.png)


## Bonus: Implementing Two-Factor Authentication (2FA):

1. Enhance security by implementing Two-Factor Authentication (2FA) in Keycloak. Use open-source tools/libraries (e.g., FreeOTP) for 2FA setup.
2. Test the 2FA implementation with a sample user.

