# recetteApp-exercices-instructions

To install angular-cli globally, type the following at the prompt:

```javascript
npm install -g @angular/cli
```

## Generating and Serving an Angular Project using Angular-CLI

```javascript
ng new recetteApp -dir=<The path of your Angular folder>/recetteApp --style=scss
```

Move to the recetteApp folder and type the following at the prompt:

```javascript
npm install
ng serve --open
```
### Adding a Menu Component

First, download the images.zip file provided above and then unzip the file. Move the resulting images folder containing some PNG files to the Angular project's src/assets folder.

```javascript
ng generate component menu
```
Next, open app.component.html file and add the following after the toolbar:

```javascript
<app-menu></app-menu>
```
### Creating the Menu

Next, create a folder named shared under the src/app/shared folder. To this folder, add a file named plat.ts with the following code:
```javascript
export class Plat {
    name: string;
    image: string;
    category: string;
    label: string;
    price: string;
    description: string;
}
```
Update menu.component.ts as follows to add in the data for four menu items:
```javascript
. . .
import { Plat } from '../shared/plat';
. . .

export class MenuComponent implements OnInit {

  plats: Plat[] = [
                         {
                           name:'Uthappizza',
                           image: '/assets/images/uthappizza.png',
                           category: 'mains',
                           label:'Hot',
                           price:'4.99',
                           description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.'                        },
                        {
                           name:'Zucchipakoda',
                           image: '/assets/images/zucchipakoda.png',
                           category: 'appetizer',
                           label:'',
                           price:'1.99',
                           description:'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce'                        },
                        {
                           name:'Vadonut',
                           image: '/assets/images/vadonut.png',
                           category: 'appetizer',
                           label:'New',
                           price:'1.99',
                           description:'A quintessential ConFusion experience, is it a vada or is it a donut?'                        },
                        {
                           name:'ElaiCheese Cake',
                           image: '/assets/images/elaicheesecake.png',
                           category: 'dessert',
                           label:'',
                           price:'2.99',
                           description:'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms'                        }
                        ];
. . .
}
```
To configure your project to use Angular material, type the following at the prompt to install Angular Material, Angular Animations and HammerJS:
```javascript
npm install --save @angular/material @angular/cdk
npm install --save @angular/animations
npm install --save hammerjs
npm install --save @angular/flex-layout@latest
```
Configure to use Material Design Icons
Next, include the following into the <head> of index.html to make use of Material Design icons:
  
```javascript
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet"> 
```
Updating AppModule
Then, you need to import the Angular Animations Module, Angular Material Module, Flex Layout Module and hammerjs into your root module (src/app/app.module.ts) as follows:
```javascript
. . . 
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { FlexLayoutModule }  from '@angular/flex-layout';
import { MatListModule, MatInputModule } from '@angular/material';
import { MatGridListModule } from '@angular/material';
import { MatCardModule } from '@angular/material/card';
import { MatButtonModule } from '@angular/material';
import { MatToolbarModule } from '@angular/material';

. . . 

import 'hammerjs';

@NgModule({
  
  . . . 
  
  imports: [ 
    
    . . .,
    MatGridListModule,
    FlexLayoutModule,
    MatListModule,
    MatCardModule,
    MatButtonModule,
    MatToolbarModule,
    MatInputModule
    
  ], 
    
    . . . 
  
  
}) 

. . . 
```
Open app.component.html and replace its contents with the following code:
```javascript
<mat-toolbar color="primary"> <span>Restaurant des Recettes</span> </mat-toolbar>
```
Next, update the menu.component.html template as follows:

```javascript
<div class="container"
     fxLayout="column"
     fxLayoutGap="10px">

<mat-list fxFlex>
  <mat-list-item *ngFor="let plat of plats">
    <img mat-list-avatar src={{plat.image}} alt={{plat.name}}>
    <h1 mat-line> {{plat.name}} </h1>
    <p mat-line>
      <span> {{plat.description}} </span>
    </p>
  </mat-list-item>
</mat-list>
```
Add the following CSS class to styles.scss file:
```javascript
@import '~@angular/material/prebuilt-themes/deeppurple-amber.css';
.container {
    margin: 20px;
    display:flex;
}

body { 
  padding: 0; 
  margin: 0; 
  font-family: Roboto, sans-serif; 
  
}

```
Updating the Menu Template

Open menu.component.html and update its content as follows:
```javascript
<<div class="container"
     fxLayout="column"
     fxLayoutGap="10px">

  <div fxFlex>
    <div>
      <h3>Menu</h3>
      <hr>
    </div>
  </div>

  <div fxFlex>
    <mat-grid-list cols="2" rowHeight="200px">
      <mat-grid-tile *ngFor="let plat of plats">
        <img height="200px" src={{plat.image}} alt={{plat.name}}>
        <mat-grid-tile-footer>
          <h1 mat-line>{{plat.name | uppercase}}</h1>
        </mat-grid-tile-footer>
      </mat-grid-tile>
    </mat-grid-list>
  </div>

  <div fxFlex *ngIf="selectedPlat">
    <mat-card>
      <mat-card-header>
        <mat-card-title>
          <h3>{{selectedPlat.name | uppercase}}</h3>
        </mat-card-title>
      </mat-card-header>
      <img mat-card-image src={{selectedPlat.image}} alt={{selectedPlat.name}}>
      <mat-card-content>
        <p>{{selectedPlat.description}}
        </p>
      </mat-card-content>
      <mat-card-actions>
        <button mat-button>LIKE</button>
        <button mat-button>SHARE</button>
      </mat-card-actions>
    </mat-card>
  </div>

</div>
```
Also, update the menu.component.ts file as follows to move the details of the dishes into a constant
```javascript
 . . .
 
 const PLATS: Plat[] = [
 . . .
 
 ];
 
 . . .
 
 export class MenuComponent implements OnInit {

  plats = PLATS;

  selectedPlat = PLATS[0];

 . . .
 
 }
 ```

