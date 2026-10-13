# OpenCart Option Text Truncation Fix

Prevents long product option values from being shortened to 20 characters in OpenCart 3.

OpenCart's standard cart, checkout confirmation and order-email controllers deliberately shorten long option values using code similar to:

```php
'value' => (utf8_strlen($value) > 20 ? utf8_substr($value, 0, 20) . '..' : $value)
```

That can make important option information ambiguous or unreadable — for example product sizes, adapter combinations, personalised values or other long variants.

This OCMOD keeps the complete option value instead.

Developed by [Rigu](https://rigu.co.uk), an independent UK camera accessories retailer, after encountering the issue with products that use longer option descriptions.

## What it fixes

The modification removes the 20-character truncation from:

- Shopping cart
- Standard OpenCart checkout confirmation
- Customer and admin order emails
- Journal 3 checkout, when Journal 3 is installed

The Journal operation is optional and safely skipped on stores that do not use Journal 3.

## Example

Instead of:

```text
Lens 77mm / Filter 82..
```

the customer sees:

```text
Lens 77mm / Filter 82mm
```

## Compatibility

- OpenCart 3.x
- Tested on OpenCart 3.0.5.1
- Journal 3 support included as an optional modification
- No core files are overwritten

Stores using heavily modified checkout or mail controllers may require adaptation.

## Installation

1. Go to the **Releases** section of this repository.
2. Download the latest `rigu_full_option_values.ocmod.zip`.
3. In OpenCart admin, go to **Extensions → Installer**.
4. Upload the `.ocmod.zip` file.
5. Go to **Extensions → Modifications**.
6. Click **Refresh**.
7. Test a product with an option value longer than 20 characters in the cart, checkout and an order email.

## Uninstallation

1. Remove the modification through **Extensions → Installer**.
2. Go to **Extensions → Modifications**.
3. Click **Refresh**.

## How it works

The modification replaces OpenCart's 20-character option-value shortening logic with the unmodified option value:

```php
'value' => $value
```

This changes display only. It does not alter the stored product option value.

## Licence

MIT. See [LICENSE](LICENSE).

## About Rigu

[Rigu](https://rigu.co.uk) is an independent UK retailer specialising in camera straps, creative photographic filters and light-painting equipment.

This fix was originally created for the Rigu OpenCart store and is shared in case it is useful to other OpenCart users.
