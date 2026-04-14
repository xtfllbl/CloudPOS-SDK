# Update Role Passwords API

### Required Permissions

* Include the following permissions in your application's manifest:
  * 'android.permission.USER\_PWD': permission for isUserPwd.
  * 'android.permission.USER\_PWD\_MODIFY': permission for forceModifyUserPwd, enableUserLogin.

### API Functions

#### verifyUserPwd

{% code overflow="wrap" lineNumbers="true" %}
```java
boolean verifyUserPwd(String pwd);
```
{% endcode %}

Checks if the provided string ('pwd') is the current user password.

| Parameters |                                            |
| ---------- | ------------------------------------------ |
| pwd        | the user role password. It can not be null |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### forceModifyUserPwd

{% code overflow="wrap" %}
```java
boolean forceModifyUserPwd(String newPwd);
```
{% endcode %}

Modifies the user role password to the new password ('newPwd').

| Parameters |                                                |
| ---------- | ---------------------------------------------- |
| newPwd     | the new user role password. It can not be null |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

setUserLoginMode

{% code overflow="wrap" %}
```java
boolean setUserLoginMode(boolean eneable);
```
{% endcode %}

Enables or disables user role login based on the boolean value ('enable').

| Parameters |                                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------------ |
| eneable    | for the user login setting, a boolean value is used: true enables user login, while false disables it. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

isUserLoginMode

{% code overflow="wrap" %}
```java
boolean isUserLoginMode();
```
{% endcode %}

Check whether enable user role login mode.

| Returns |                                                                                        |
| ------- | -------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if enable. false if disable.</p> |

###

isUserLoggedIn

{% code overflow="wrap" %}
```java
boolean isUserLoggedIn(boolean eneable);
```
{% endcode %}

Check whether the user logged in.

| Returns |                                                                                       |
| ------- | ------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if logged in. false if not.</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).
