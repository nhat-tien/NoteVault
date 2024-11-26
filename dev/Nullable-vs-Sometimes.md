---
date: 2023-09-01
tags:
  - php
  - laravel
---

>[!info] summary
The takeaway from this article is that if the field you are validating has to exist, but can be null, use **nullable**. If the field you are validating may or may not be present in the request, and you need to validate it when it is, use **sometimes**.

Often times you have [validation in your requests](https://rappasoft.com/blog/laravel-validation-101-controllers-form-requests-rules) using one or more of the wide variety of rules that come built in with Laravel.

The more fields you are validating, the more chance you don't actually need all of them to process what you're doing.

There are quite a few validation rules to reach from to exclude validation, but when I have data that is not required, I usually reach for one of these:

## Nullable

Using the _nullable_ rule, you are telling Laravel that the field under validation may be **null** but if it is _not null_, to validate it against the rest of rules in the array for that key.

This is useful when paired with the **[TrimStrings](https://github.com/laravel/framework/blob/7.x/src/Illuminate/Foundation/Http/Middleware/TrimStrings.php)** and **[ConvertEmptyStringsToNull](https://github.com/laravel/framework/blob/7.x/src/Illuminate/Foundation/Http/Middleware/ConvertEmptyStringsToNull.php)** middleware, as any field sent through the request will be trimmed, and if that string is empty, will be converted to null. So you can safely send through empty strings and expect null to validate on the other end.

For example:

```php
request()->validate([
	'first_name' => ['required', 'string'],
	'middle_initial' => ['nullable', 'string', 'max:1'],
	'last_name' => ['required', 'string'],
]);
```

In this example, assume 3 text inputs on the UI, for first_name, middle_initial, and last_name. Also assume no HTML5 or Javascript validation is being applied on the frontend.

If the user were to leave first_name or last_name blank, they would ge a validation error. However, if they were to leave middle_initial blank, the ConvertEmptyStringsToNull middleware would take it and convert it to null, and the nullable validation rule would be applied which would skip the rest of the rules.

However, if the user enters anything in the field, it will be validated against the rest of the rules.

## Sometimes
### [Validating When Present](https://laravel.com/docs/10.x/validation#validating-when-present)

In some situations, you may wish to run validation checks against a field **only** if that field is present in the data being validated. To quickly accomplish this, add the `sometimes` rule to your rule list:

```php
$v = Validator::make($data, [    
	'email' => 'sometimes|required|email',
]);
```

In the example above, the `email` field will only be validated if it is present in the `$data` array.

---

The _sometimes_ rule is slightly different but instead of validating if the field is null, it validates if the field is _present_ in the current request at all.

A good example is when you have a form that is maybe interacting with javascript, or run by a javascript framework. You may be enabling/disabling fields on that form based on the user's interaction.

The sometimes validation rule comes into play here, as any disabled field will not be present in the request.

For example:

```php
request()->validate([
	'first_name' => ['required', 'string'],
	'last_name' => ['required', 'string'], 
	'phone_number' => ['sometimes', 'required', 'digits:10'],
]);
```

In this example, if there's a part of the form that disables the phone_number input, then the _digits_ validation rule will not be applied. However, if the field is not disabled, and the form sends through anything else, even and empty string that gets converted to null, than the validation rule will get fired against the rest of the rules.

# Ref
- [article](https://rappasoft.com/blog/nullable-vs-sometimes)
