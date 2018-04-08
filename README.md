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
import { MatDialogModule } from '@angular/material';
import { MatCheckboxModule } from '@angular/material';

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
    MatInputModule,
    BrowserAnimationsModule;
    MatDialogModule,
    MatCheckboxModule,
    
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
Also, update the menu.component.ts file as follows to move the details of the plats into a constant
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
### Exercice Fin module

Task 1

In this task you will be adding a new platdetail component to your Angular application and include the component into the menu component's template so that the details of a specific plat are displayed there:

- Use Angular CLI to create a new component named platdetail,
- Replace the card showing the selected plat in menu component's template with the platdetail component, and
- Update the template of the platdetail component with the following code:

```javascript
<div class="container"
    fxLayout="row"
    fxLayout.sm="column"
    fxLayout.xs="column"
    fxLayoutAlign.gt-mat="space-around center"
    fxLayoutGap="10px" 
    fxLayoutGap.xs="0">

  <div fxFlex="40" *ngIf="plat" >
    <p>Afficher le detail ici</p>
 </div>

  <div fxFlex="20" *ngIf="plat">
      <p>Afficher les commentaires ici</p>
 </div>

</div>
 ```
 Task 2

In this task you will be adding a card component to the platdetail template to display the details of the plat given above:

Add a new constant to the platdetail.component.ts file named PLAT as follows, and initialize it to the JavaScript object given below that contains the details of the plat and comments about the plat:
```javascript
const PLAT = {
  name: 'Uthappizza',
  image: '/assets/images/uthappizza.png',
  category: 'mains',
  label: 'Hot',
  price: '4.99',
  description: 'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
  comments: [
    {
      rating: 5,
      comment: "Imagine all the eatables, living in conFusion!",
      author: "John Lemon",
      date: "2012-10-16T17:57:28.556094Z"
    },
    {
      rating: 4,
      comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
      author: "Paul McVites",
      date: "2014-09-05T17:57:28.556094Z"
    },
    {
      rating: 3,
      comment: "Eat it, just eat it!",
      author: "Michael Jaikishan",
      date: "2015-02-13T17:57:28.556094Z"
    },
    {
      rating: 4,
      comment: "Ultimate, Reaching for the stars!",
      author: "Ringo Starry",
      date: "2013-12-02T17:57:28.556094Z"
    },
    {
      rating: 2,
      comment: "It's your birthday, we're gonna party!",
      author: "25 Cent",
      date: "2011-12-02T17:57:28.556094Z"
    }
  ]
};
```
Now introduce a new variable in the platdetail.component.ts file in the platdetail class called plat
and set it equal to the PLAT constant above:
```javascript
plat = PLAT;
```
The Angular material card component should be used to display the details of the plat as shown above. Please remember to use the Angular "uppercase" pipe on the name displayed in the card title. Also apply the *ngIf="plat" structural directive to both the <mat-card>.

Task 3

In this task you will use the comments that are included in the plat object above to display a list of the comments.

This task involves the following steps:

Use the Angular material list to display the list of comments as shown below. Also apply the *ngIf="plat" structural directive to both the <md-list> that displays the list of comments .
Display the date of the comment by processing it through the Angular built-in date pipe.

### Data binding

Refactoring the Code :

First, create a new class named Comment in a file named comment.ts in the shared folder and include the following in it:

```javascript
export class Comment {
    rating: number;
    comment: string;
    author: string;
    date: string;
}
```
Then update the plat class to allow a plat to have an array of comments as follows:

```javascript
import { Comment } from './comment';

export class Plat {
    name: string;
    image: string;
    category: string;
    label: string;
    price: string;
    description: string;
    comments: Comment[];
}
```
Then create a new file named plats.ts in the shared folder to now export the JavaScript object array of plats:


```javascript
import { Plat } from './plat';

export const PLATS: Plat[] = [
    {
        name: 'Uthappizza',
        image: '/assets/images/uthappizza.png',
        category: 'mains',
        label: 'Hot',
        price: '4.99',
        description: 'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables, living in conFusion!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    },
    {
        name: 'Zucchipakoda',
        image: '/assets/images/zucchipakoda.png',
        category: 'appetizer',
        label: '',
        price: '1.99',
        description: 'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables, living in conFusion!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    },
    {
        name: 'Vadonut',
        image: '/assets/images/vadonut.png',
        category: 'appetizer',
        label: 'New',
        price: '1.99',
        description: 'A quintessential ConFusion experience, is it a vada or is it a donut?',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables, living in conFusion!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    },
    {
        name: 'ElaiCheese Cake',
        image: '/assets/images/elaicheesecake.png',
        category: 'dessert',
        label: '',
        price: '2.99',
        description: 'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables, living in conFusion!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    }
];
```
Updating the Menu Component:

Open menu.component.ts file and update its content, first by deleting the plats constant and then make the following changes:

```javascript
import { Component, OnInit } from '@angular/core';
import { Plat } from '../shared/plat';
import { PLATS } from '../shared/plats';

. . .

export class MenuComponent implements OnInit {

  plats = PLATS;

  selectedPlat: Plat;

. . .

  onSelect(plat: Plat) {
    this.selectedPlat = plat;
  }

}
```
Then update the menu.component.html file as follows:

```javascript
. . .

      <md-grid-tile *ngFor="let plat of plats" (click) = "onSelect(plat)">
        . . .
        
  <app-detail-plat [plat] = "selectedPlat"></app-detail-plat>
        
. . .
```
Open detail-plat.component.ts and update its contents as follows :
```javascript
import { Component, OnInit, Input } from '@angular/core';
import { Plat } from '../shared/plat';

. . .

export class DetailPlatComponent implements OnInit {

  @Input()
  plat: Plat;

. . .
```
Adding a Service 

Create a folder named services in the src/app folder.
```javascript
ng generate service services/plat
```
Open plat.service.ts and update its contents and add the service to the app.module.ts:
```javascript
import { Injectable } from '@angular/core';
import { Plat } from '../shared/plat';
import { PLATS } from '../shared/plats';

@Injectable()
export class PlatService {

  constructor() { }

  getPlats(): Plat[] {
    return PLATS;
  }
}
```
Using the Service
Now update menu.component.ts file to make use of the service as follows:

```javascript
constructor(private platService: PlatService) { }
  
  ngOnInit() {
    this.plats = this.platService.getPlats();
  }
```
