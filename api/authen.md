# Authen

- [Home](https://github.com/rhman-ibrahim)
- [Overview](#overview)
- [Models](#models)
- [View Sets](#view-sets)
- [Helper Functions](#helper-functions)

## Overview

***Authen*** is a [Python](https://www.python.org/) API developed with [Django](https://www.djangoproject.com/) and Django REST Framework ([DRF](https://www.django-rest-framework.org/)), designed for user authentication. It includes a custom authentication model [Account](#account) for handling user credentials and a [Profile](#profile) model to manage user information.

***Authen*** uses JSON Web Tokens ([JWT](https://jwt.io/introduction)) to provide a stateless authentication to reduce server loading as all of necessary information is contained within the token instead of storing session data on the server.

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

**BaseViewSet** provides common functionalities that are used in different areas of this application *authen* or others where *authen* is installed.
The main player of *BaseViewSet* is ***authen*** as this method is used as a decorator by all other methods that needs to be protected.

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|authen|static|Validates requests and adds authentication related data to it|role, permission, group|Passes the request to the decorated method|Read the [exceptions](#the-authen-method-exceptions) table|
|extract_form_errors|static|Extracts form field and non field errors|BaseModelForm instance|A list of all form errors as strings|Returns HTTP_500_INTERNAL_SERVER_ERROR|
|set_cookie|static|Creates a cookie with pre defined attributes|response, key, value, expires|Retruns None|Returns None|

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

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|get|Get|--|--|--|--|
|post|POST|--|--|--|--|
|patch|PATCH|--|--|--|--|
|put|PUT|--|--|--|--|
|delete|DELETE|--|--|--|--|

### AccountViewSet

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|get|Get|--|--|--|--|
|post|POST|--|--|--|--|
|patch|PATCH|--|--|--|--|
|put|PUT|--|--|--|--|
|delete|DELETE|--|--|--|--|

### ProfileViewSet

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|get|Get|--|--|--|--|
|post|POST|--|--|--|--|
|patch|PATCH|--|--|--|--|
|put|PUT|--|--|--|--|
|delete|DELETE|--|--|--|--|

## Helper Functions

### generate_uuid

Using ***uuid4*** from [UUID](https://docs.python.org/3/library/uuid.html) this function creates in a form of a string a random series of numbers and letters, separated by hyphens. It's often used to create a "one-of-a-kind" ID that won't be repeated, even if it's generated millions of times.

Example output: *c9b1d53e-65f3-4f07-bd89-13a2c9fdde65*.
