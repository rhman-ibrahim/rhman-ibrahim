[![Tools](https://skillicons.dev/icons?i=python,django)](https://skillicons.dev)

---

# sch.stamps

- This is a container package of all general helper functions, mixins and abstract models needed in building [**`Scheme`**](https://github.com/rhman-ibrahim/rhman-ibrahim#scheme) infrastructure.

- *sch.stamps* was first created to add a unique identifier and time methods to all Django models in [**`Scheme`**](https://github.com/rhman-ibrahim/rhman-ibrahim#scheme), that's why its named *Stamps*.

- *sch.stamps* will be continuously updated to encompass all essential general functions, mixins, and models, ensuring that all helpers are located in one place.

---

## Models

1. `Stamp`

    This is an abstract Django model used to define common fields and methods to be included in multiple other models, as an abstract model it does not have a database table instead, all models inherting it will have its fields and methods.

    - `Stamp` adds an id, idientifier, created and updated fields, and created_text and updated_text methods.
    
    - `idientifier` is a unique identifier for each model instance it is created using `get_random_string` from `django.utils.crypto`

    - The added methods represet the time data using [timeago](https://pypi.org/project/timeago/) but shorten.


## Mixins

1. `LanguageSettingMixin`

    A Django mixin that customizes the initialization of requests to handle language settings based on the Accept-Language header.

    - Internationalization: This mixin is useful for internationalizing as it ensures that the language preference of the user (as specified in the Accept-Language header) is respected for each request.
    
    - Flexibility: By defaulting to settings.LANGUAGE_CODE if the header is not present, it provides a fallback mechanism, ensuring that the application always has a valid language code activated.
    
    - Reusability: As a mixin, `LanguageSettingMixin` can be easily included in any viewset where language setting functionality is needed, promoting code reuse and consistency across your application.


## Functions

1. `calculate_sha256`

    - This function is useful for generating a consistent and unique hash value for any given input, which can be used for tasks like data integrity checks, password storage, or digital signatures.

2. `extract_form_errors`

    - This function collects all form errors, including non-field errors and individual field errors, into a single list. It replaces generic 'this field' references with the actual field names, providing more flexibility and ease in displaying form errors.

3. `generate_identifier`

    - This function utilizes Django's `get_random_string` to create a 32-character random string, which can be used as a unique identifier. This ensures that each call to the function produces a different, unpredictable string, useful for generating secure and unique values.