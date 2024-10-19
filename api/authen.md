# Authen

- [Home](https://github.com/rhman-ibrahim)
- [Overview](#overview)
- [Models](#models)
- [View Sets](#view-sets)
- [Helper Functions](#helper-functions)

## Overview

`Authen` is a [Python](https://www.python.org/) API developed with [Django](https://www.djangoproject.com/) and Django REST Framework ([DRF](https://www.django-rest-framework.org/)), designed for user authentication. It includes a custom authentication model [Account](#account) for handling user credentials and a [Profile](#profile) model to manage user information.

`Authen` uses JSON Web Tokens ([JWT](https://jwt.io/introduction)) to provide a stateless authentication to reduce server loading as all of necessary information is contained within the token instead of storing session data on the server.

## Models

### Stamp

`Stamp` is an abstract model it does not create a separate table in the database. It serves as a blueprint for other models to inherit fields and methods. It provides a unique serial, time information about instance creation and last update.

|Field|Description|
|--|--|
|id|An auto field, the primary key of the database table|
|identifier|An uneditable char field stores a random unique identifier by [generate_uuid](#generate_uuid)|
|created|A date time field stores the time of creation|
|updated|A date time field stores the time of last update|

|Method|Description|
|--|--|
|time_to_text|A static method that uses [timeago](https://pypi.org/project/timeago/) to format Django date time fields|
|created_text|An instance method that utilizes `time_to_text` to format `created`|
|updated_text|An instance method that utilizes `time_to_text` to format `updated`|

### Account

`Account` is the primary model of the `Authen` application, it inherits each of `AbstractBaseUser` to create a custom user model, `PermissionsMixin` to utilize permission and group functionalities and `Stamp`.

|Field|Description|
|--|--|
|username|A char field that stores the username|
|secret|A char field that stores a secret key by [generate_uuid](#generate_uuid), it could be used instead of username/password|
|groups|A many to many relation field between `Account` model and `Group` model|
|user_permissions|A many to many relation field between `Account` model and `Permission` model|
|is_active|A boolean field that stores the state of being active|
|is_superuser|A boolean field that stores the state of being a system super user|
|is_admin|A boolean field that stores the state of being an admin|
|is_staff|A boolean field that stores the state of being a staff|

|Method|Description|
|--|--|
|get_role|An instance method that returns the account's role: `superuser`, `admin`, `staff` or `user`|
|renew_secret|An instance method that updates the account's secret by [generate_uuid](#generate_uuid)|
|log|An instance method creates a log entry for an action made by the account|

### Profile

`Profile` is a complementary model in the `Authen`'s authentication management, it is connected to the `Account` model on creation by a `post_save` signal, it stores the user's secondary data and all of its fields are optional.

|Field|Description|
|--|--|
|account|A one to one relation field that connects each account instance to a profile instance|
|gender|A char field with choices that stores the user's gender: `Female`, `Male` or `Withheld`|
|firstname|A char field that stores the firstname|
|lastname|A char field that stores the lastname|
|email|An e-mail field that stores the e-mail address|
|phone|A char field that stores a phone number|
|about|A text field that stores an about paragraph|

|Method|Description|
|--|--|
|get_info|An instance method that returns a dictionary of `username`, `firstname`, `lastname` and `gender`|
|get_contact|An instance method that returns a dictionary of `username`, `email` and `phone`|
|get_about|An instance method that returns a dictionary of `username` and `about`|
|clear_info|An instance mothod that clears `firstname`, `lastname` and sets `gender` to `Withheld`|
|clear_contact|An instance mothod that clears `email` and `phone`|
|clear_about|An instance mothod that clears `about`|
|clear|An instance mothod that clears the profile instance data|

## View Sets

### BaseViewSet

|Method|Type|Description|Parameter|On Success|On Failure|
|--|--|--|--|--|--|
|authenticate_jwt|static|Authenticates the request by validating the access token|request|A tuple of Account model instance and access token string|--|
|extract_cookies|static|Extracts the cookies from request headers|request headers|returns cookies as key/value dictionary|returns an empty dictionary {}|
|extract_form_errors|static|Extracts form field and non field errors|BaseModelForm instance|A list of all form errors as strings|--|
|get_user_id|static|Decodes the access token|access_token|Account instance id|`None`|
|get_profile|static|Returns the profile instance after caching it|request|Profile model instance|--|
|set_cookie|static|Creates a cookie with pre defined attributes|response, key, value, expires|`None`|`None`|
|authen|static|Used a decorator, it validates the incoming request and attaches related variables to the request object.|role, permission, group|Passes the request to the decorated view-set method|Raises an exception|

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

Using `uuid4` from [`UUID`](https://docs.python.org/3/library/uuid.html) this function creates in a form of a string a random series of numbers and letters, separated by hyphens. It's often used to create a "one-of-a-kind" ID that won't be repeated, even if it's generated millions of times.

Example output: *c9b1d53e-65f3-4f07-bd89-13a2c9fdde65*.
