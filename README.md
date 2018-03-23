# Fckin wow shit app, all note to me :D VinhDEPTRAI
## Template syntax: fuck
**{{ expression or statement}}** -> interpolation : you can write expression in this
```typescript
    {{ 1 + 1 }}
```
**[]** -> expression context: component instance
```html
    <!--app.component.html-->
    <!--isUnchanged is prop of the AppComponent-->
    
    <span [hidden]="isUnchanged"></span>
```
**#** An expression may also refer to properties of the template's context such as a template input variable (let hero) or a template reference variable (#heroInput).
```html
    <!--app.component.html-->
    <div *ngFor="let hero of heroes">{{hero.name}}</div>
    <input #heroInput> {{heroInput.value}}
```

## Passing data to component with @Input:

**@Input(): propname** : *received data from outside to component*
>example code in below:
```typescript
export class ContactImageDetailComponent {
  @Input() round: Boolean = false;
  @Input() avatarUrl: string = '';

  constructor() {}
}
```
>passing data from another template:
```html
<tp-contact-image-detail
  [avatarUrl]="contact.avatar?.url"
  [round]="contact.avatar?.round"
>
</tp-contact-image-detail>

```


## Component Event with EventEmitter & @Output
```typescript
    //switches.component.ts
    import { 
        Component, 
        OnInit, 
        Input, 
        Output, 
        EventEmitter 
    } from '@angular/core';

    @Component({
        selector: 'tp-switches',
        templateUrl: './switches.component.html',
        styleUrls: ['./switches.component.scss']
    })
    export class SwitchesComponent implements OnInit {
        @Input() checked: Boolean = false;
        @Output('checkedChange') change = new EventEmitter<boolean>();

        constructor() { }

        ngOnInit() {
        }

         emitChangeValue(event) {
            this.change.emit(event.target.checked);
        }
    }
```
```html
<!-- switches.component.html -->
<label class="tp-toggle tp-toggle--round tp-toggle--flat">
  <input type="checkbox"
    class="tp-toggle__checkbox"
    [checked]="checked"
    (change)="emitChangeValue($event)"/>
  <span class="tp-toggle__icon"></span>
</label>
```
