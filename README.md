# NgxBottomSheetModal

Simple bottom sheet modal for Angular, using Tailwind CSS.

This library was generated with [Angular CLI](https://github.com/angular/angular-cli) version 17.3.0.

## Features

- Create clear and reusable modal components.
- It creating managing modals painless and clearer.
- Pass data to the modal and and implement any content you want
- Responsive: displayed as bottom sheet on mobile and as modal dialog in desktop

## Demo

Check the [Demo](https://angular-17-starter-project-rdvpgx.stackblitz.io)

## Prerrequisites

- Tailwind CSS. Check [Angular installation](https://tailwindcss.com/docs/guides/angular)

## Installation

```shell
npm install ngx-bottom-sheet-modal
```

## Usage

1. Add the bottom sheet modal wrapper to your app root. Import it into your component definition and add it to the end of the template:

```typescript
import { Component } from '@angular/core';
import { RouterOutlet } from '@angular/router';
import { NgxBottomSheetModalComponent } from 'ngx-bottom-sheet-modal';

@Component({
  selector: 'app-root',
  standalone: true,
  template: `
  <router-outlet></router-outlet>
  <ngx-bottom-sheet-modal></ngx-bottom-sheet-modal>
  `,
  styleUrl: './app.component.scss',
  imports: [RouterOutlet, NgxBottomSheetModalComponent],
})
export class AppComponent {
  }
}
```

### 1. Create a component with the modal content:

```typescript
import { Component, Input } from "@angular/core";

@Component({
  selector: "app-modal-content-component",
  standalone: true,
  imports: [],
  template: `
    <div class="p-4">
      <h1 class="font-bold text-xl">{{ title }}</h1>
      <p>{{ description }}</p>
      <div class="border-b-2 my-2"></div>
      <p>Tap outside to close.</p>
    </div>
  `,
  styles: ``,
})
export class ModalContentComponent {
  @Input() title!: string;
  @Input() description!: string;
}
```

### 3. Modal trigger

Inject the modal service to the component from which you want to open the modal. Now you can call `openBottomSheet` method any time you want to open the bottom sheet modal (passing the component class and optional inputs):

```typescript
import { Component, inject } from '@angular/core';
import { NgxBottomSheetModalService } from 'ngx-bottom-sheet-modal';
import { ModalContentComponent } from '../../../pages/menu-page/modal-content-component/modal-content-component.component';

export DataType = {name: string, description: string};

@Component({
  selector: 'app-menu-item',
  standalone: true,
  templateUrl: './menu-item.component.html',
  styleUrl: './menu-item.component.scss',
  imports: [],
})
export class MenuItemComponent {
  // Services
  private readonly ngxBottomSheetModalService = inject(
    NgxBottomSheetModalService,
  );

  constructor() {}

  showModal(data: DataType) {
    this.ngxBottomSheetModalService.openBottomSheet({
      contentComponent: ModalContentComponent,
      inputs: data,
    });
  }
}
```

As you can see, you can pass any data to the modal component using the `inputs` parameter of the `openBottomSheet` method. The data will be available in the modal component as `@Input` properties.

### 4. Provide animations

Add `provideAnimations()` to your providers in the `app.congif.ts` file:

```typescript
import { provideAnimations } from "@angular/platform-browser/animations";

export const appConfig: ApplicationConfig = {
  providers: [...provideAnimations()],
};
```

### 5. Update Tailswind CSS config

Include the `ngx-bottom-sheet-modal` styles. Add the following to the `content` section in your `tailwind.config.js` file:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,ts}", "./node_modules/ngx-bottom-sheet-modal/**/*.{html,ts,js,mjs}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](https://raw.githubusercontent.com/quedicesebas/ngx-bottom-sheet-modal/main/LICENSE) file for details.
