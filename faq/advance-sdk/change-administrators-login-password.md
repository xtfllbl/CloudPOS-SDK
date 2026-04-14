# Change Administrator's Login Password

### Required Permissions

* Applications must declare the specified permissions in their manifest to use this AIDL interface.

| Permission                            | Function              |
| ------------------------------------- | --------------------- |
| android.permission.ADMIN\_PWD\_MODIFY | modify admin password |
| android.permission.ADMIN\_PWD         | get admin password    |
| android.permission.ADMIN\_PWD\_RESET  | reset admin password  |

### API Overview

#### Modify Admin Password

{% code overflow="wrap" %}
```java
boolean forceModifyAdminPwd(String newPwd);
```
{% endcode %}

This function allows the modification of the admin password. Provide the new password ('newPwd') as arguments.

| Parameters |                     |
| ---------- | ------------------- |
| newPwd     | new admin password. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### Check Admin Password

```java
boolean isAdminPwd(String pwd);
```

Returns 'true' if the provided password ('pwd') matches the current admin password.

| Parameters |                 |
| ---------- | --------------- |
| pwd        | admin password. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### Check whether Admin Logged in

```java
boolean isAdminLoggedIn();
```

Returns 'true' if the administrator logged in.

| Returns |                                                                                       |
| ------- | ------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if logged in. false if not.</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).
