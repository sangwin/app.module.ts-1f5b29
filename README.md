markdown

````

# Dynamic Component Bootstrapping in Angular

## Overview

This project demonstrates how to **dynamically bootstrap an Angular component** at runtime using `DoBootstrap` and `ApplicationRef`.

Instead of using the standard `bootstrap` array in `@NgModule`, the application selects a component based on an API response or a previously saved selection in `localStorage`.

## Features

- **Dynamic Bootstrapping:** Loads a component at runtime.
- **API Integration:** Supports retrieving the component selector from an API.
- **Local Storage:** Remembers the previously selected component.
- **Multiple Components:** Supports bootstrapping different components from a predefined list.
- **Custom Initialization:** Uses Angular's `DoBootstrap` lifecycle hook.

## Implementation

The example uses two components:

- `AppComponent` — selector: `app-root`
- `SecondaryComponent` — selector: `app-secondary`

The `AppModule` implements `DoBootstrap` to control which component is initialized.

```typescript
export class AppModule implements DoBootstrap {
  ngDoBootstrap(app: ApplicationRef): void {
    fetch('API URL').then((name: string) => {
      const selectedComponent = localStorage.getItem('selected_component');

      bootstrapSelectedComponent(
        app,
        selectedComponent ? selectedComponent : name
      );
    });
  }
}
```

## How It Works

1. **Application Initialization:** Angular initializes the module without a predefined bootstrap component.
2. **Component Selection:** The application retrieves a component selector from an API or uses the value stored in `localStorage`.
3. **Component Mapping:** A predefined mapping associates component selectors with Angular component classes.
4. **DOM Creation:** An element matching the selected component's selector is added to the DOM.
5. **Bootstrapping:** `ApplicationRef.bootstrap()` initializes the selected component.

## Example Flow

```text
Application Starts
       |
       v
   ngDoBootstrap()
       |
       v
   Fetch Component Name
       |
       v
 Check localStorage
       |
       v
 Select Component
       |
       v
 Create DOM Element
       |
       v
 Bootstrap Component
```

## Use Cases

- Applications that load different entry components based on configuration.
- Multi-brand or white-label applications.
- Runtime component selection based on user preferences.
- Applications that require server-driven startup configuration.

## Important Notes

- The component selector must exist in the predefined component mapping.
- The selected component must be included in the Angular module's declarations.
- Validate API responses and stored values before bootstrapping.
- The example uses a mock `fetch()` function. Replace it with a real API call for production use.
- `entryComponents` is unnecessary in modern Angular versions; it was relevant to older Angular versions.
- This example follows the NgModule-based Angular architecture. Modern standalone applications can use a different bootstrapping approach.

## Reference

- [Angular DoBootstrap API](https://angular.dev/api/core/DoBootstrap)
- [Angular ApplicationRef API](https://angular.dev/api/core/ApplicationRef)

## Author

**Sangwin Gawande**

Website: [https://sangw.in](https://sangw.in)

---

Cheers!!
````
