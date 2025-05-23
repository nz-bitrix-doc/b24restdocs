# Special Pages

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it soon.

{% endnote %}

When creating a page through the wizard, special pages can be specified in the manifest. For example, the cart page. Special markers are provided for such pages, allowing you to reference a specific system page within the body of the page without knowing its full address or even `ID`.

If there is a corresponding page for this marker within the current site, the address will be substituted in place of the marker; otherwise, the marker will be ignored.

Currently existing markers for special pages:

- `#system_mainpage` – main page
- `#system_catalog` – main catalog page
- `#system_personal` – personal section
- `#system_cart` – cart
- `#system_order` – order checkout
- `#system_payment` – payment page (the actual payment processing)
- `#system_compare` – comparison page

## Examples

```html
<a href="#system_cart">Cart</a>
// note that the marker is intentionally placed without a closing hash symbol #
```

#|
|| **Method** | **Description** ||
|| [landing.syspage.deleteForLanding](./landing-syspage-delete-for-landing.md) | Deletes all mentions of the page as a special one ||
|| [landing.syspage.deleteForSite](./landing-syspage-delete-for-site.md) | Deletes all special pages ||
|| [landing.syspage.getSpecialPage](./landing-syspage-get-special-page.md) | Retrieves the address of the special page on the site ||
|| [landing.syspage.get](./landing-syspage-get.md) | Retrieves the list of special pages ||
|| [landing.syspage.set](./landing-syspage-set.md) | Sets a special page for the site ||
|#