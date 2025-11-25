## Spring Security Overview

Spring Security is a powerful and customizable authentication and access-control framework for Java applications. In this project, Spring Security is integrated to provide both authentication and authorization features, ensuring that users can access only the resources they're permitted to.

### Features Implemented
- **User Authentication**: Users can register and log in to their accounts securely.
- **Role-Based Access Control**: Different user roles are assigned to manage permissions effectively.
- **JWT Authentication**: Utilizes JSON Web Tokens for stateless security, enhancing performance and scalability.
- **Exception Handling**: Custom error responses for unauthorized access and token-related issues.

### Implementation Steps
1. **Add Spring Security Dependency**: Ensure that your `pom.xml` includes the Spring Security starter.
2. **Web Security Configuration**: Create a configuration class to extend `WebSecurityConfigurerAdapter` and override necessary methods to customize the security settings.
3. **Authentication Manager**: Set up an authentication manager bean to handle user credentials validation.
4. **Configure HTTP Security**: Use the `http` object to customize the security configurations, such as form login and access rules.
5. **Exception Handling**: Implement custom error handling for unauthorized access attempts to provide meaningful feedback.

### Example Configuration Snippet
Here's a basic example of a security configuration class:

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/api/public/**").permitAll()
                .anyRequest().authenticated()
                .and()
            .formLogin();
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()
            .withUser("user").password("{noop}password").roles("USER");
    }
}

