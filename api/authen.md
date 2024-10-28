# Authen

- [Home](https://github.com/rhman-ibrahim)
- [Overview](#overview)
- [Models](#models)
- [View Sets](#view-sets)
- [Helper Functions](#helper-functions)

## Overview

***Authen*** is a [Python](https://www.python.org/) API developed with [Django](https://www.djangoproject.com/) and Django REST Framework ([DRF](https://www.django-rest-framework.org/)), designed for user authentication. It includes a custom authentication model [Account](#account) for handling user credentials and a [Profile](#profile) model to manage user information.

***Authen*** uses JSON Web Tokens ([JWT](https://jwt.io/introduction)) by [Simple JWT](https://pypi.org/project/djangorestframework-simplejwt/) to provide a stateless authentication to reduce server loading as all of necessary information is contained within the token instead of storing session data on the server.

## Models

### Stamp

***Stamp*** is an abstract model it does not create a separate table in the database. It serves as a blueprint for other models to inherit fields and methods. It provides a unique serial, time information about instance creation and last update.

|Attribute|Type|Description|
|--|--|--|
|id|Property|An auto field, the primary key of the database table|
|identifier|Property|An uneditable char field stores a random unique identifier by [generate_uuid](#generate_uuid)|
|created|Property|A date time field stores the time of creation|
|updated|Property|A date time field stores the time of last update|
|time_to_text|Method|A static method that uses [timeago](https://pypi.org/project/timeago/) to format Django date time fields|
|created_text|Method|An instance method that utilizes *time_to_text* to format *created*|
|updated_text|Method|An instance method that utilizes *time_to_text* to format *updated*|

### Account

***Account*** is the primary model of the *Authen* application, it inherits each of *AbstractBaseUser* to create a custom user model, *PermissionsMixin* to utilize permission and group functionalities and *Stamp*.

|Attribute|Type|Description|
|--|--|--|
|username|Property|A char field that stores the username|
|secret|Property|A char field that stores a secret key by [generate_uuid](#generate_uuid), it could be used instead of username/password|
|groups|Property|A many to many relation field between *Account* model and *Group* model|
|user_permissions|Property|A many to many relation field between *Account* model and *Permission* model|
|is_active|Property|A boolean field that stores the state of being active|
|is_superuser|Property|A boolean field that stores the state of being a system super user|
|is_admin|Property|A boolean field that stores the state of being an admin|
|is_staff|Property|A boolean field that stores the state of being a staff|
|get_role|Method|An instance method that returns the account's role: *superuser*, *admin*, *staff* or *user*|
|renew_secret|Method|An instance method that updates the account's secret by [generate_uuid](#generate_uuid)|
|log|Method|An instance method creates a log entry for an action made by the account|

### Profile

***Profile*** is a complementary model to *Authen*'s authentication, it is connected to the *Account* model on creation by a *post_save* signal, it stores the user's secondary data and all of its fields are optional.

|Attribute|Type|Description|
|--|--|--|
|account|Property|A one to one relation field that connects each account instance to a profile instance|
|gender|Property|A char field with choices that stores the user's gender: *Female*, *Male* or *Withheld*|
|firstname|Property|A char field that stores the firstname|
|lastname|Property|A char field that stores the lastname|
|email|Property|An e-mail field that stores the e-mail address|
|phone|Property|A char field that stores a phone number|
|about|Property|A text field that stores an about paragraph|
|get_info|Method|An instance method that returns a dictionary of *username*, *firstname*, *lastname* and *gender*|
|get_contact|Method|An instance method that returns a dictionary of *username*, *email* and *phone*|
|get_about|Method|An instance method that returns a dictionary of *username* and *about*|
|clear_info|Method|An instance mothod that clears *firstname*, *lastname* and sets *gender* to *Withheld*|
|clear_contact|Method|An instance mothod that clears *email* and *phone*|
|clear_about|Method|An instance mothod that clears *about*|
|clear|Method|An instance mothod that clears the profile instance data|

## View Sets

### BaseViewSet

**BaseViewSet** provides common functionalities that are used in different areas of this application *authen* or others where *authen* is installed. The main player of *BaseViewSet* is ***authen*** as this method is used as a decorator to authenticate the access.

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|authen|static|Validates the access with this [workflow](#the-authen-method-workflow)|role, permission, group|Passes the request to the decorated method|Read the [exceptions](#the-authen-method-exceptions) table|
|extract_form_errors|static|Extracts form field and non field errors|BaseModelForm instance|A list of all form errors as strings|Returns HTTP_500_INTERNAL_SERVER_ERROR|
|set_cookie|static|Creates a cookie with pre defined attributes|response, key, value, expires|Retruns None|Returns None|

### The **authen** method Workflow

1. Default:
    1. **Extracting the Token from the Request**: The **authenticate** method from **JWTAuthentication** first looks for the token in the request's Authorization header, the header should follow the format: `Authorization: Bearer <token>` and if the header does not have the expected format or if it is missing, the method returns None, which means the authentication is unsuccessful.
    2. **Validating the Token**: If a token is found, the method validates it using the Simple JWT backend. This validation process involves checking that the token is well-formed, has not expired, and is signed with a valid secret key.
    3. **Decoding the Token**: Once the token is validated, it is decoded to extract the payload.
    The payload contains information about the user, such as the user ID and other claims.
    4. **Fetching the User**: Using the user ID from the token's payload, the method retrieves the corresponding user from the database. If the user is not found, or if the token is not valid, the authentication will fail.
    5. **Returning the User and Token**: If everything is correct, the method returns a tuple containing the user object and the validated token and this allows accessing both the authenticated user and the token in your views.
    6. **Assigning the user and token**: Finally the **authen** method assigns `request.account` and `request.token` to the actual *account* instance and token returned respectively.
2. Role:
    1. If the role parameter was provided with an actual role argument, authen will compare the account's actual role rank to it.
    2. If it is equal to it or hight, authen will set `request.role_check_passed` (`False` by default) to `True` and pass the request; else it will return a `HTTP_401_UNAUTHORIZED` with a message: '*Unauthorized access, lack of authority.*'.
3. Permission:
    1. If the permission parameter was provided with an actual permission: `<app_label>.<permission_codename>`, authen will use `has_perm` to check if the user has this permission.
    2. If `has_perm` return `True` authen will set `request.permission_check_passed` (`False` by default) to `True` and pass the request; else it will return a `HTTP_401_UNAUTHORIZED` with a message: '*Unauthorized access, lack of permission.*'.
4. Group:
    1. If the group parameter was provided with an actual group's name, authen will check if the user is a member of this group.
    2. If `True` authen will set `request.group_check_passed` (`False` by default) to `True` and pass the request; else it will return a `HTTP_401_UNAUTHORIZED` with a message: '*Unauthorized access, lack of membership.*'.
5. Finally *authen* handles different exceptions as it wraps different view-set methods of this application or other Schema applications, read the [exceptions](#the-authen-method-exceptions) table.

### The **authen** method Exceptions

|Exception Raised|Return|Message|
|--|--|--|
|InvalidToken|HTTP_401_UNAUTHORIZED|Invalid token provided|
|AuthenticationFailed|HTTP_401_UNAUTHORIZED|Authentication failed, please check your credentials|
|TokenError|HTTP_422_UNPROCESSABLE_ENTITY|There was an error with your token. Please try again|
|TokenBackendError|HTTP_500_INTERNAL_SERVER_ERROR|Internal server error with token processing|
|ObjectDoesNotExist|HTTP_404_NOT_FOUND|The <model_name> instance can not be found|
|Exception|HTTP_500_INTERNAL_SERVER_ERROR|An unexpected error occurred, please try again later|

### SignViewSet

**SignViewSet** manages the all of sign operations through `authen/` URL, signing-up: registering a new user by creating an account, signing-in: verifying the account credentials by issuing JWT tokens (refresh and access tokens), refreshing the accessing token and signing-out: blacklisting the refresh token.

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|authenticate_pair|static|Uses `AuthenticationForm` with the request data to validates the account credentials|`username`, `password`|Calls `issue_jwt_tokens`|HTTP_401_UNAUTHORIZED|
|authenticate_secret|static|Uses the secret string to find its account|`secret`|Renews the account's secret then calls `issue_jwt_tokens`|HTTP_401_UNAUTHORIZED|
|issue_jwt_tokens|static|Creates a refresh token and an access token for the account as cookies|Account instance|HTTP_204_NO_CONTENT|Read the [exceptions](#the-authen-method-exceptions) table|
|refresh_access_token|PUT|Retrives the `refreshToken` instance and uses it to create a new `access_token` as a cookie|Account instance|HTTP_204_NO_CONTENT|Read the [exceptions](#the-authen-method-exceptions) table|
|sign_up|POST|Uses the SignUpForm with request data to create a new account|`username`, `password1`, `password2`|HTTP_201_CREATED|HTTP_400_BAD_REQUEST|
|sign_in|PATCH|Calls `authenticate_pair` or `authenticate_secret` according to the request data structure|request data|--|--|
|sign_out|DELETE|Clears the cache, deletes the cookies and blacklists the refresh token|request|HTTP_204_NO_CONTENT|Read the [exceptions](#the-authen-method-exceptions) table|

### AccountViewSet

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|get|GET|--|--|--|--|
|put|PUT|--|--|--|--|
|post|POST|--|--|--|--|
|patch|PATCH|--|--|--|--|
|delete|DELETE|--|--|--|--|

### ProfileViewSet

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|get|GET|--|--|--|--|
|put|PUT|--|--|--|--|
|post|POST|--|--|--|--|
|patch|PATCH|--|--|--|--|
|delete|DELETE|--|--|--|--|

## Helper Functions

### generate_uuid

Using ***uuid4*** from [UUID](https://docs.python.org/3/library/uuid.html) this function creates in a form of a string a random series of numbers and letters, separated by hyphens. It's often used to create a "one-of-a-kind" ID that won't be repeated, even if it's generated millions of times.

Example output: *c9b1d53e-65f3-4f07-bd89-13a2c9fdde65*.
