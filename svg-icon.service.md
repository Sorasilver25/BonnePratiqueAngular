
# 📦 Angular SVG Icon Service

Un service Angular minimaliste pour centraliser l'enregistrement des icônes SVG personnalisées avec `MatIconRegistry`.

---

## 📁 Arborescence recommandée

```
src/
├── app/
│   └── core/
│       └── services/
│           └── svg-icon.service.ts
├── assets/
│   └── icons/
│       ├── calendar.svg
│       ├── user.svg
│       ├── edit.svg
│       ├── trash.svg
│       ├── image.svg
│       └── board.svg
```

---

## 💡 Service Angular

```ts
import { Injectable } from '@angular/core';
import { MatIconRegistry } from '@angular/material/icon';
import { DomSanitizer } from '@angular/platform-browser';

@Injectable({ providedIn: 'root' })
export class SvgIconService {
  private icons = [
    'calendar',
    'user',
    'edit',
    'trash',
    'image',
    'board'
    // ➕ Ajoute ici d'autres noms de fichiers SVG sans extension
  ];

  constructor(
    private iconRegistry: MatIconRegistry,
    private sanitizer: DomSanitizer
  ) {
    this.registerIcons();
  }

  private registerIcons(): void {
    this.icons.forEach(icon =>
      this.iconRegistry.addSvgIcon(
        icon,
        this.sanitizer.bypassSecurityTrustResourceUrl(`assets/icons/${icon}.svg`)
      )
    );
  }
}
```

---

## 🧪 Exemple d'utilisation HTML

```html
<mat-icon svgIcon="calendar"></mat-icon>
<mat-icon svgIcon="user"></mat-icon>
<mat-icon svgIcon="edit"></mat-icon>
```

---

## ✅ Prérequis

Assure-toi que ton module Angular importe bien `MatIconModule` depuis `@angular/material/icon`.

```ts
import { MatIconModule } from '@angular/material/icon';

@NgModule({
  imports: [
    MatIconModule,
    // ...
  ]
})
export class AppModule { }
```

---

## 📝 Astuce bonus

Pour une solution plus dynamique, tu peux charger les noms d’icônes via un fichier JSON (`assets/icons/icons.json`) et utiliser `HttpClient` dans le service pour enregistrer les icônes.

