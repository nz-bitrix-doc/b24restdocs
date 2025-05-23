# Knowledge Base Embedding Locations

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it soon.

{% endnote %}

In the Bitrix24 interface, there are locations for users to embed Knowledge Bases.

![Knowledge Base Embedding Locations](_images/application_embedding.png)

Let's explore how to work with this from the REST perspective. Note that these are not pure embedding locations, which are discussed [here](../../../widgets/index.md). This is specifically about working with Knowledge Bases from the interface perspective.

First, you need to decide on the menu you want to embed into and obtain its code. You can do this by opening the menu binding selection ("Select Knowledge Base") in the interface and checking the address of the opened frame. There will be a parameter, for example, `menuId=crm_switcher:deal`. This is the so-called menu code, and you can work with it.

#|
|| **Method** | **Description** ||
|| [landing.site.bindingToGroup](./landing-site-binding-to-group.md) | Binds to a Social Network group ||
|| [landing.site.bindingToMenu](./landing-site-binding-to-menu.md) | Embeds into the menu ||
|| [landing.site.getGroupBindings](./landing-site-get-group-bindings.md) | Retrieves group bindings ||
|| [landing.site.getMenuBindings](./landing-site-get-menu-bindings.md) | Retrieves a list of menu bindings ||
|| [landing.site.unbindingFromGroup](./landing-site-unbinding-from-group.md) | Removes binding from a Social Network group ||
|| [landing.site.unbindingFromMenu](./landing-site-unbinding-from-menu.md) | Removes from the menu ||
|#